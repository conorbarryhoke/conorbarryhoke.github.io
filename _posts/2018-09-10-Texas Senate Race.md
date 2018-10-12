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

Data was collected usping the Reddit API to access posts from the subreddits for each campaign as well as the Texas subreddit.

### Models

After using TF-IDF to vectorize the text data, I then applied multiple model types for classification in a pipeline and optimized with GridSearch. Ultimately, I ended up using Logistic Regression.

The model was able to correctly conduct binary classification with an accuracy score of **0.94**.

During review of the coefficients, it was clear that the names of each candidate was the overwhelming influence on the model

![Beto](https://raw.githubusercontent.com/babyakja/babyakja.github.io/master/assets/img/posts/Beto-coeff.png)
![Cruz Coefficients](https://raw.githubusercontent.com/babyakja/babyakja.github.io/master/assets/img/posts/Crus-coeff.png)

### Application
_Predictions on Texas subreddit_

I wanted to understand the state of a third subreddit using what was trained to the model and if I could get the pulse of the Texas reddit 

![Texas Predictions](https://raw.githubusercontent.com/babyakja/babyakja.github.io/blob/master/assets/img/posts/TX-subreddit.png)

### Conclusion

Binary predictor can be effective in a first stage classification but can miss subtle things like sarcasm and word proximity. In the case of the subreddit posts from r/texas, posts with the highest probability as pro-Cruz were some of the strongest insults.

__Knowing your data source__
- Timeline of reddit posts were different between both campaigns
  - Beto had much more recent posts
  - Cruz posts dated back to his 2016 presidential campaign
