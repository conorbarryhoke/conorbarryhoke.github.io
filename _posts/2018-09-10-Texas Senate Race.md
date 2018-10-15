---
layout: post
title: "NLP on the 2018 Texas Senate Race"
featured-img: cruz-beto
categories: [Project, NLP]
---

Campaigns have radically changed. As demonstrated in 2016, viral content and online message can have a powerful influence over the state of the race. Party platforms have less influence now than what is being discussed across the internet. The challenge for modern campaigns is to be able to effectively stay on top and get the message they want to reach voters.

With the midterm election fast approaching, it is essential for campaigns to know where they stand in the race. We know that there are many social media platforms out there and much of their content can be traced back to Reddit. With the speed at which viral content spreads, it is vital to know if your message is working or if your opponent's attack ads are negatively affecting your campaign.

We will take the high profile campaign between Beto O'Rourke (D) and Ted Cruz (R).

_Applied Tools:_

- webscraping
- APIs
- Natural Language Processing (NLP)

### Data

Data was collected using the Reddit API to access posts from the subreddits for each campaign as well as the Texas subreddit. Since I planned on doing this multiple times and potentially for serveral different subreddits, I decided to write a function that was able to do so for any different subreddit title I decided to use.

```python
#Generic function to scrap subreddit by name & how many times you want to repeat (next page of subreddit)
def reddit_scraper(subreddit, times):

    url = "http://www.reddit.com/r/"+ subreddit +".json"
    after = None #each query is limited to 25 post,
    # 'after' grabs the last post and rewrites the url to grab the next 25 posts

    for i in range(times):
        posts = []
        if after == None:
            current_url = url
        else:
            current_url = url + '?after=' + after
        print(current_url)
        res = requests.get(current_url, headers={'User-agent': ''})
        #print(res.status_code)
        if res.status_code != 200:
            print('Status error: ', res.status_code)
            break
        current_dict = res.json()
        current_posts = [p['data'] for p in current_dict['data']['children']]
        posts.extend(current_posts)
        after = current_dict['data']['after']
        time.sleep(4)
        if i > 0:
            current_df = pd.DataFrame(posts)
            prev_posts = pd.read_csv(subreddit + '.csv')
            all_posts = pd.concat([prev_posts,current_df])
            all_posts.to_csv(subreddit + '.csv', index=False)
        else:
            current_df = pd.DataFrame(posts)
            current_df.to_csv(subreddit + '.csv', index=False)
    return all_posts.shape
```

To create the data to use for the project, I combined the post title with the post content to maximize the text content to use in the model. This was necessary since many reddit posts related to both campaigns were just links to other pages and did not contain much discussion inside the post.

Additionally, it became very apparent how many more posts were occuring for the Beto campaign in the Reddit realm than the Cruz campaign. Since Reddit's API is limited to the last 1000 posts, the timeline
were very different depending on how active each subreddit has been over time.

Each of the total posts per campaign were the same in the following chart, but had a very different timeline and frequency in posts over the last few months.

![TimeSeries](https://raw.githubusercontent.com/babyakja/babyakja.github.io/master/assets/img/posts/TimeSeriesChart.png)

### Models

After using TF-IDF to vectorize the text data, I then applied multiple model types for classification in a pipeline and optimized with GridSearch on my training data to predict which subreddit the post came from.
Ultimately, I ended up using Logistic Regression.

Once the model was finished, predictions were made on the test set and produced the following confusion matrix:

|Reddit Page|Predicted: Beto| Predicted: Cruz|
|---|:---:|:---:|
|Beto_for_Senate| 86 | 8 |
|TedCruz| 3 | 91 |

The model was able to correctly conduct binary classification with an accuracy score of **0.94**. This seem like good news but also too good to be true, so I explored what could be causing this high of an accuracy score.

During review of the coefficients, it was clear that the names of each candidate was the overwhelming influence on the model.

![Beto](https://raw.githubusercontent.com/babyakja/babyakja.github.io/master/assets/img/posts/Beto-coeff.png)
![Cruz Coefficients](https://raw.githubusercontent.com/babyakja/babyakja.github.io/master/assets/img/posts/Crus-coeff.png)

### Application
_Predictions on Texas subreddit_

I wanted to understand the state of a third subreddit using what was trained to the model and if I could get the pulse of the Texas reddit. I used the same function I built earlier and isolated any post referencing a candidate or had a 'politics' flag.

![TX](https://raw.githubusercontent.com/babyakja/babyakja.github.io/master/assets/img/posts/TX-subreddit.png)
For the interactive Tableau chart, [vist this page.](https://public.tableau.com/profile/james6137#!/vizhome/Book3-Txsubredditprediction/TXsubreddit?publish=yes)

### Conclusion

Binary predictor can be effective in a first stage classification but can miss subtle things like sarcasm and word proximity. In the case of the subreddit posts from r/texas, posts with the highest probability as pro-Cruz were some of the strongest insults against him.

_Takeaways_

> __Be careful for the Accuracy Paradox__

> __Knowing your data source__

To check out more about the project, visit hte Github repo [here.](https://github.com/babyakja/subreddit_nlp_tx_senate_race)
