---
layout: post
title: "Engaging with Youtube: How to Get Liked"
featured-img: Comments_Dislikes_Likes_views
categories: [Project, NLP]
---
<h2>Introduction</h2>
What makes people find and click on music on YouTube? Does the way a video is posted have anything to do with how popular it gets? In parts 1-3, I try and partly succeed in predicting how big a music-type video will get. For parts 4-6, I end up pivoting to identifying the most engaging video tags, in an effort to optimize engagement per view for a potential advertiser. In the end, I try to answer the age-old question: What the hell is trap music, actually?


<li>Part 1: YouTube</li>
<li>Part 2: The Data</li>
<li>Part 3: Failing To Regress</li>
<li>Part 4: Engagement by Genre</li>
<li>Part 5: Bonus Word Clouds</li>
<li>Part 6: Conclusion</li>

<h2><p> </p></h2>
<h1>Part 1: YouTube</h1>
<h2>Background</h2>
<h3>What's in a video?</h3>
<li>A <strong>title, about 7 words</strong> on average, often following a format like Song - Artist (Official Music Video)</li>

![Title Words ](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/title_text.bmp)


<h2>Part 2: The Data</h2>
<h2>Part 3: Failing To Regress</h2>
<h2>Part 4: Engagement by Genre</h2>
<h2>Part 5: Bonus Word Clouds</h2>
<h2>Part 6: Conclusion</h2>



![test](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/Comments_Dislikes_Likes_views.bmp)

stuff
stuff

<h2>Part 6: Conclusion</h2>

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
<p>While this information is informative, there is always room for improvement in the analysis and presentation of findings. Some examples below: </p>
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
