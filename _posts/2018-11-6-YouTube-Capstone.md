---
layout: post
title: "Engaging with Youtube: How to Get Liked"
featured-img: Comments_Dislikes_Likes_views
categories: [Project, YouTube, Engagement]
---

<h2>Introduction</h2>
What makes people find and click on music on YouTube? Does the way a video is posted have anything to do with how popular it gets? In parts 1-3, I try and partly succeed in predicting how big a music-type video will get. For parts 4-6, I end up pivoting to identifying the most engaging video tags, in an effort to optimize engagement per view for a potential advertiser. In the end, I try to answer the age-old question: What the hell is trap music, actually?

For engagement Visualizations, jump to part 5

<li><a href="#part1">Part 1: YouTube</a></li>
<li><a href="#part2">Part 2: The Data</a></li>
<li><a href="#part3">Part 3: Failing To Regress</a></li>
<li><a href="#part4">Part 4: Engagement by Genre</a></li>
<li><a href="#part5">Part 5: Conclusion</a></li>
<li><a href="#part6">Part 6: Bonus Word Clouds</a></li>


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
      <li>Considered a number of features, including:</li>
        <ul>
          <li>Video Aspects - Duaration (missing lyrics)</li>
          <li>Text Features - title, tags, description: word vectors, sentiment, length; title features: featuring artist, letters in word</li>
          <li>Publication Date - weekend, friday, day of year, day of month, year (controls for more time to see a video after release)</li>
          <li>Meta - has caption, high def vs. standard, content rating</li>
        </ul>
      <li>Number to beat: using only likes, dislikes, and comments, we are able to predict views with r2 <strong>.67</strong> </li>
    </ul>
  </p>

<h2>"Results"</h2>
  <p>
    <ul>
      <li>Tried a number of models, PCA, grid search, with random forrest scoring highest at r2 <strong>.48</strong>, .9 MAE on the log (or +/- 1 order of magnitude)</li>
      <li>Analysis of engagement on biggest misses showed that I was missing the 'it' factor</li>
      <li>Model was still 'good enough' to identify a number of new potential hits that weren't showing up in the main charts</li>
    </ul>
  </p>
<h2 class="mb-0">What can we Know? Rules of Thumb</h2>
  <p>By combining feature importance from Gradient Boost and sign of Linear Regression coefficients, its possible to identify the most significant potential view boosters:</p>
  <p>
    <ol>
      <li>Duration - shorter is better</li>
      <li>Year - older videos have higher total views, probably due to a combination of 1. more time to accumulate views 2. Feature of the ETL phase which probably failed to retrieve old videos with lower view counts</li>
      <li>Day of year: release earlier in the year, although recalling the midsummer dip, it is probably safe to say winter videos do better</li>
      <li>Longer descriptions with more positive tone do better</li>
      <li>The number of tags is much more important than their sentiment</li>
      <li>Longer titles do not do well</li>
      <li>Licensed content is more viewed</li>
      <li>Including a caption seems to help visibility</li>
      <li>Use the letter ‘a’ in the title a bunch, but not ‘p’</li>
      <li>Content cool enough to be prohibited in certain regions is more popular</li>
      <li>The Pitbull Effect: Include a featuring artist for an easy 14% bump</li>
    </ol>
  </p>

<h1><a name="part4">Part 4: Engagement by Genre</a></h1>
<h2>The Pivot</h2>
  <p>After failing to satisfactorily predict views, I realized that what I had was a general approach for describing overall engagement. Views are a measure of engagement, as are likes, dislikes, and comments: Something about a video provokes different kinds of reactions from people. We don't need to perfectly predict any one element if we can describe things in a useful way.</p>
  <p>After messing around with some unsupervised classification, I found what should have been obvious in the first place: genres are pre-existing classes that behave differently. Using the tags and continuously adding popular words to new or existing genres, I was able to identify a number of keywords:</p>
  <ul>
    <li><strong>Variant</strong>: acoustic, cover, instrumental, lyric, lyrics </li>
    <li><strong>Blues </strong>: blues, blue, delta, rhythm, lee hooker</li>
    <li><strong>Christian </strong>: christ, christian, faith, worship</li>
    <li><strong>Classical </strong>: bach, beethoven, classical, composer, concerto, debussy, ensemble, orchestra, piano, symphony, sonata</li>
    <li><strong>Country </strong>: country, western, horse, america, american, soldier, road, home, alabama, denver, haggard, coe</li>
    <li><strong>Dubstep </strong>: dub, dubstep, skrillex, bass</li>
    <li><strong>EDM</strong>: aoki, club, edm, house, dance, dj,electr, electronic, electronica, techno,trance, ultra,</li>
    <li><strong>Extended </strong>: live, album, festival</li>
    <li><strong>Folk </strong>: folk, banjo, indie</li>
    <li><strong>Halloween </strong>: creepy, halloween, eerie, horror, wolves</li>
    <li><strong>Hit </strong>: hit, interscope, new, official, single, sony, warner, vevo</li>
    <li><strong>Italian </strong>: singolo, nuovo, ultimo</li>
    <li><strong>Jazz </strong>: jazz, new orleans, rag, ragtime, swing,</li>
    <li><strong>Kpop </strong>: kpop, korea, korean</li>
    <li><strong>Latin </strong>: latin, musica, reggaeton</li>
    <li><strong>Love Songs </strong>: amore, amor, breakup, break-up, love, need </li>
    <li><strong>Other Rock </strong>: grunge, heavy, metal, punk </li>
    <li><strong>Pop </strong>: clean, pop </li>
    <li><strong>Rap </strong>: rap, hip, hop, hiphop, r&b</li>
    <li><strong>Reggae </strong>: reggae, marley</li>
    <li><strong>Remix </strong>: remix</li>
    <li><strong>Romanian </strong>: romania, romanian</li>
    <li><strong>Relax </strong>: ambient, chill, concentration, downtempo, estudiar, dormir, meditate, meditation, relajar, relax, relaxing, relaxation, trabaja, sleep, sleeping, study, zen</li>
    <li><strong>Rock </strong>: rock, roll, rocknroll, </li>
    <li><strong>Trap </strong>: lean, trap</li>
  </ul>
  <p>These keywords do not produce pure classifications, which is actually useful for understanding overlap between genres</p>
  <h3><p> </p></h3>
  ![genre_correlation](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_correlation.bmp)
  <h3><p> </p></h3>
  <p>For example, trap music is
    <ul>
      <li>22% Remixes (mainly of hit songs)</li>
      <li>18% Latin Music</li>
      <li>14% Dubstep</li>
      <li>13% Covers and instrumentals</li>
      <li>7% Rap samples</li>
      <li>6% Festival music</li>
      <li>5% Trying to scare people into listening</li>
      <li>3% EDM</li>
    </ul>
  </p>
  <p>Once the data was classified, I controlled for views to find expected likes, dislikes, comments, and like / dislike ratio on each video. With a standard deviation of this projection, I was then able to convert actual counts into a deviation from expected, which allowed for direct comparison of videos across view counts. Without this, the characteristics of each genre would be dominated by the average views of the videos in it. </p>

<h2>Exploring Engagement Across Genres</h2>
<h3>Interpreting These Charts</h3>
  <p>The numbers shown for engagement are in terms of standard deviation from expected, in order to allow for comparability across metrics. Loosely speaking, it translates to percentage. Its more of a 'more or less' than a substantive metric at this point, so don't get too caught up. </p>
  <p>That being said, for each metric, one 'unit' translates to within a percent of expected:
    <ul>
      <li>Likes: 50%</li>
      <li>Comments: 60%</li>
      <li>Dislikes: 50%</li>
      <li>Like / Dislike Ratio: 50%</li>
    </ul>
  </p>
<h3>Visualizations</h3>
<h4 class="mb-0">Engagement in Most Viewed Videos of Major Genres</h4>
<p>Most Viewed Videos from each of the biggest categories, sized by favorability (likes / dislikes)</p>
<p>Note that the spread is considerably higher on higher view count videos in general</p>
{% include youtube_capstone/eng_highviews.html %}

<h4 class="mb-0">Engagement Stats By Genre</h4>
<p>Move Slider to isolate videos by view count (slight variance in aggregation method from actual)</p>
{% include youtube_capstone/eng_statsgenre.html %}

<h4 class="mb-0">Engagement Stats By Genre, Measures Isolated</h4>
<p>Move Slider to isolate videos by view count</p>
{% include youtube_capstone/eng_statsgenre_iso.html %}

<h4 class="mb-0">Engagement Stats By Genre, Across Views</h4>
<p>Select Genres to Compare engagement across views</p>
{% include youtube_capstone/eng_statsgenre_views.html %}

<h4 class="mb-0">View Range by Genre</h4>
<p>Spread of log of Views</p>
{% include youtube_capstone/eng_viewranges.html %}


![genre_correlation](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_correlation.bmp)




<h1><a name="part5">Part 5: Conclusion</a></h1>

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


<h1><a name="part6">Part 6: Bonus Word Clouds</a></h1>
<h2>Christian Music</h2>
<h3><p> </p></h3>
![christian words](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_clouds/christian_words.bmp)
<h3><p> </p></h3>
<h2>Classical Music</h2>
<h3><p> </p></h3>
![classical words](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_clouds/classical_words.bmp)
<h3><p> </p></h3>
<h2>Dubstep (music?)</h2>
<h3><p> </p></h3>
![Dubstep words](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_clouds/dubstep_words.bmp)
<h3><p> </p></h3>
<h2>EDM</h2>
<h3><p> </p></h3>
![EDM words](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_clouds/edm_words.bmp)
<h3><p> </p></h3>
<h2>Halloween Songs</h2>
<h3><p> </p></h3>
![halloween words](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_clouds/halloween_words.bmp)
<h3><p> </p></h3>
<h2>Latin Music</h2>
<h3><p> </p></h3>
![Latin words](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_clouds/latin_words.bmp)
<h3><p> </p></h3>
<h2>Hit Music</h2>
<h3><p> </p></h3>
![Hit words](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_clouds/hit_words.bmp)
<h3><p> </p></h3>
<h2>Rap Music</h2>
<h3><p> </p></h3>
![Rap words](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_clouds/rap_words.bmp)
<h3><p> </p></h3>
<h2>Relaxation and Study Music</h2>
<h3><p> </p></h3>
![Relax words](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_clouds/relaxation_words.bmp)
<h3><p> </p></h3>
<h2>Trap</h2>
<h3><p> </p></h3>
![Trao words](https://raw.githubusercontent.com/conorbarryhoke/conorbarryhoke.github.io/master/assets/img/posts/capstone_files/assets/genre_clouds/trap_words.bmp)
<h3><p> </p></h3>

<a href="https://github.com/conorbarryhoke/Capstone">Source Code</a>
