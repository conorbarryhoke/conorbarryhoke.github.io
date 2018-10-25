---
layout: post
title: What is Kanye Thinking?
featured-img: kanye-ye
mathjax: true
categories: [Project, NLP]
---


Kanye West has been one of the most controversial public figures over the last decade and recently has been scrutinized for his his views on politics and Trump. This has led to many viewing his actions as something to joke about or being dismiss as crazy.

However, on his latest album __ye__, he openly states on the cover _“I hate being Bi-Polar, its awesome”_ and writes about bipolar disorder being his superpower on the track _Yikes_. The reality is bipolar disorder affects 6.86 million U.S. adults annually and is a critical mental health crisis needing to be addressed. Commonly misdiagnosed or treatment being avoided due to the stigma surrounding bipolar disorder, I wanted to explore if it was possible to create tools that can help predict and assist those with bipolar disorder before the onset of the more severe episodes and help them seek primary care.

_Problem Statement_

Using Machine Learning, what can we learn about how Kanye's behavior and mental state has changed over time and can this be used to build models that can help predict bipolar episodes?

## _Bipolar Disorder_

The NIH defines Bipolar Disorder as being characterized by dramatic shifts in mood, energy, and activity levels that affect a person’s ability to carry out day-to-day tasks.
These shifts in mood and energy levels are more severe than the normal ups and downs that are experienced by everyone.

![Bipolar](https://raw.githubusercontent.com/babyakja/babyakja.github.io/master/assets/img/posts/Bipolar-NIH.png)            

# Data

_Obtain the Data_

## __Lyric Data__

_APIs_ - Apiseed __|__ Spotify
_Webscraping_ - Genius Lyric Site
__14__ Albums __|__ __128__ Unique Songs __|__ __62,648__ Total Words Used

| _Albums_|_Singles_|
|---|---|
|  'KIDS SEE GHOSTS'|  'I Love It'|
|  'ye'| 'XTCY' |
|  'The Life Of Pablo'| 'Lift Yourself' |
|  'Yeezus'||
|  'My Beautiful Dark Twisted Fantasy'||
|  '808s & Heartbreak'||
|  'Graduation'||
|  'Late Registration'||
|  'The College Dropout'||

## __Text Cleaning__




# __Models__

###   _Topic Modeling_
1. LDA (Latent Dirichlet allocation)
Statistics Based
_Sequential_
2. NMF (Non-negative Matrix Factorization)
Linear Algebra

![fit, right](assets/Coherence Score.png)

### _Topics:_

1. Public Persona
1. Speak Ye Truth
1. Broke /Women/ Money
1. Life
1. Make Right/ Legacy

![Kanye Discography](https://raw.githubusercontent.com/babyakja/babyakja.github.io/master/assets/img/posts/Kanye-Discography2.png)            

[Interactive Tableau Chart](https://public.tableau.com/profile/james6137#!/vizhome/KanyeWestGraphs/Discography2?publish=yes)


## Highest Probability Song | _Each Topic_

```
0.9954962574881103
['All of the Lights']
['My Beautiful Dark Twisted Fantasy']
Public Persona

0.9988632784766937
['Last Call']
['The College Dropout']
Speak Ye Truth

0.9966221495074559
['The New Workout Plan']
['The College Dropout']
Broke / Women / Money

0.9955740231167477
['Drive Slow']
['Late Registration']
Life

0.9966283076899758
['Touch the Sky']
['Late Registration']
Make Right/ Legacy
```


## _Most Similar to:_ __Love__

```
[('fadin', 0.5092264413833618),
 ('mistake', 0.49861404299736023),
 ('wake', 0.46998417377471924),
 ('ho', 0.4642098546028137),
 ('myself', 0.42317628860473633),
 ('blame', 0.3949402868747711),
 ('fuckin', 0.381166934967041),
 ('walk', 0.38080090284347534),
 ('hate', 0.38067206740379333),
 ('save', 0.37218549847602844)]
 ```

## _Most Similar to:_ __Myself__

```
[('bed', 0.5850050449371338),
 ('killing', 0.5635855793952942),
 ('killed', 0.5398204326629639),
 ('dawg', 0.5226340293884277),
 ('loving', 0.5117295384407043),
 ('wake', 0.5074575543403625),
 ('hood', 0.5013218522071838),
 ('favorite', 0.4675023555755615),
 ('door', 0.4619908332824707),
 ('catch', 0.44258543848991394)]
 ```

 ## __Sequential Topic Model__

 ### _Can we detect changes in word usage for topics_

 1. Group Songs by years
 1. Creates Topics over Time
 1. Tune Parameters
   _Chain Variance_


#   _Takeaways_

   Data:

   > __Song text data can be inconsistent and difficult to align__

   > __Balancing manual text cleaning with scalable operations is extremely helpful__

   Model:

   > __Topic Modeling can assist in finding overarching groups, focus on need (static vs dynamic)__

   > __Word2Vec creates reliable word association grouping and can be useful on a much larger corpus__

   > __t-SNE can be a great visual tool but difficult to fine tune for classification purposes__
