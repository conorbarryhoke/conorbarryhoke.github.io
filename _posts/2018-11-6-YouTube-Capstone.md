---
layout: post
title: "Engaging with Youtube: How to Get Liked"
featured-img: Comments_Dislikes_Likes_views
categories: [Project, NLP]
---
show update count: 2
<h2>Introduction</h2>
What makes people find and click on music on YouTube? Does the way a video is posted have anything to do with how popular it gets? In parts 1-3, I try and partly succeed in predicting how big a music-type video will get. For parts 4-6, I end up pivoting to identifying the most engaging video tags, in an effort to optimize engagement per view for a potential advertiser. In the end, I try to answer the age-old question: What the hell is trap music, actually?


<li><a href="#part1">Part 1: YouTube</a></li>
<li><a href="#part2">Part 2: The Data</a></li>
<li><a href="#part3">Part 3: Failing To Regress</a></li>
<li><a href="#part4">Part 4: Engagement by Genre</a></li>
<li><a href="#part5">Part 5: Bonus Word Clouds</a></li>
<li><a href="#part6">Part 6: Conclusion</a></li>

<h2><p> </p></h2>
<h1><a name="part1">Part 1: YouTube</a></h1>

  <h2>What's in a video?</h2>

  <li>A <strong>title, about 7 words</strong> on average, often following a format like Song - Artist (Official Music Video)</li>
  <h3><p> </p></h3>
  ![Title Words ](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/title_text.bmp)
  <h3><p> </p></h3>

  <li><strong>10-15 Tags</strong>, not visible, meant to help the video show up in searches (e.g. rap, Cardi B, concert)
  </li>
  <h3><p> </p></h3>
  ![Tag Words ](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/tag_text.bmp)
  <h3><p> </p></h3>

  <li>A longer <strong>description, around 100 words</strong>, usually providing detailed information about the artist and the uploader
  </li>
  <h3><p> </p></h3>
  ![Description Words ](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/description_text.bmp)
  <h3><p> </p></h3>

  <h2>Getting the Data</h2>
  <ul>
    <li>The YouTube API allows for automatic calls to its query function, which returns a list of relevant videos</li>
    <li>Each individual video can then be queried for summary statistics </li>
    <li>Time-stamped information, such as when views or comments happened, is not available    </li>
    <li>The query 'budget' makes it very inefficient to get specific comments </li>
  </ul>

<h1><a name="part2">Part 2: The Data</a></h1>
<h2>What can we get?</h2>
  <p>Videos present a remarkably strong relationship across orders of magnitude:</p>
  <h3><p> </p></h3>
  ![Description Words ](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/Comments_Dislikes_Likes_views.bmp)
  <h3><p> </p></h3>
  <p>
    <ul>
      <li>By taking the base10 log, we can see a clear trend across orders of magnitude
      </li>
      <li>Actual and log modes:
        <ul>
          <li>Average Views per video: <strong>53 Million (M)</strong> (7.7 on the graph)</li>
          <li>Peak of Views per video: <strong>10 M</strong> (6.96)</li>
          <li>Peak of Likes per video: <strong>25 thousand (k) (M)</strong> (4.4)</li>
          <li>Peak of Comments per video: <strong>1.3 k</strong> (3.13)</li>
          <li>Peak of Dislikes per video: <strong>870</strong> (2.94)</li>
        </ul>
      </li>
      <li>Which means the percentages of engagment per view are very consistent
        <ul>
          <li>Likes / View: <strong>.28% </strong> </li>
          <li>Comments / View: <strong>.01% </strong> </li>
          <li>Dislikes / View: <strong>.01%</strong> </li>
        </ul>
      </li>
    </ul>
  </p>
<h2>What's Up with the Bump?</h2>
  <p>The bump on the lower side of each curve brings up an import note about how the data was collected. When I ran the search, I pulled as many results as YouTube would give for each letter of the alphabet (about videos 350 per). I think this has to do with how YouTube finds relevant videos: it searches for the most videos that match the string, sorted again by year, and cuts off anything below the threshold. Sure enough, if we look at the results over a few years, most of the bump comes from newer videos, which suggested the remainder of the analysis be restricted to the well behaved videos over 10,000 views (As a bonus, this is only applies to about 500 videos out of 8500 unique entries in the data)
  </p>
  <h3><p> </p></h3>
![Bump over time ](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/Bump_perYear.bmp)
<h3><p> </p></h3>
<h2>Duration Trends</h2>
<p>Most videos fall within 2.5-5 minutes</p>
<h3><p> </p></h3>
![test](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/duration_distribution.bmp)
<h3><p> </p></h3>
<p>Because people don't watch very long or short videos</p>
<h3><p> </p></h3>
![test](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/views_by_duration.bmp)
<h3><p> </p></h3>

<h1><a name="part3">Part 3: Failing To Regress</a></h1>
<h2>The Setup</h2>
  <p>
    <ul>
      <li>The original goal was to predict what went into a big hit (100 M + Views), and to predict views in general</li>
      <li>Considered a number of features, including:
        <ul>
          <li>Video Aspects - Duaration (missing lyrics)</li>
          <li>Text Features - title, tags, description: word vectors, sentiment, length; title features: featuring artist, letters in word</li>
          <li>Publication Date - weekend, friday, day of year, day of month, year (controls for more time to see a video after release)</li>
          <li>Meta - has caption, high def vs. standard, content rating</li>
        </ul>
      </li>
      <li>Number to beat: using only likes, dislikes, and comments, able to predict views with r2 <strong>.67</strong></li>
  </p>


<h1><a name="part4">Part 4: Engagement by Genre</a></h1>
<h1><a name="part5">Part 5: Bonus Word Clouds</a></h1>



<h3><p> </p></h3>
![test](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/Comments_Dislikes_Likes_views.bmp)
<h3><p> </p></h3>

stuff
stuff

<h1><a name="part6">Part 6: Conclusion</a></h1>

The following chart plots likes and comments, scaled by average view counts, for the genres studied.

They are colored by the ratio of likes to dislikes (Higher Ratio: More Green)

{% include youtube_capstone/engagement_summary.html %}

<p>Halloween music, rock and roll, and KPop all provoke the highest rates of engagement per view, followed by love songs, trap, and EDM. Any adversting campaign would do well to target any of these areas.  </p>
<p>Some trends to see here:
  <ul>
    <li>Videos with less engagement are more favorably liked - there is some threshold that provokes a reaction, and the bar for likes is lower than dislikes / comments</li>
    <li>The biggest genres are the most normal, clustered within the main band (latin, pop, etc.)</li>
    <li>Rock fans are quite vocal</li>
    <li>Highest engagement genres: rock, kpop, halloween (spooky music), EDM, love songs, Trap</li>
    <li>Classical music provokes comments, but not likes - presumably, they're above such petty interaction</li>
  </ul>
</p>
<p>While this data is informative, there is always room for improvement in the analysis and presentation of findings. Some examples below: </p>
<ul>
  <li>Filter out other holiday or event-specific music</li>
  <li>Incorporate metrics to compare genres across different view counts (e.g. low, medium, high)</li>
  <li>Host a function to examine individual songs and genres (currently available in notebook)</li>
  <li>Adjust ratio-based model to predict and compare views</li>
  <li>Expand tags used to identify existing genres, and isolate new modes of engagement not directly related to genre</li>
  <li>Continue to refine and engineer new features for use in the regression model, such as a variable to identify 'normal' length songs</li>
  <li>Examine characteristics of heavy hitter channels like Vevo, and try to classify them</li>
  <li>Identify tag words with high cross-over to understand how genres are related</li>
</ul>
