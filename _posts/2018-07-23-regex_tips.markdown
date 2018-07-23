---
layout: post
title:      "Regex tips"
date:       2018-07-23 19:23:06 +0000
permalink:  regex_tips
---


Early on when I was learning regex I thought about what differentiates it between traditional contains/does not contain filters on search engines. What I found was that Regex doesnt just allow you to search for content containing words or phrases, but do pattern matching on large sets of data when you aren't just looking for one result but many fitting an itentified pattern. 

For instance we might want to identify how active tense a particular paragraph in a peice of written content is by checking how many words are in active tense. Using a regular control-f find on the below content you could search for the string "ing" to find all the words containing the character string "ing".

```
If to do were as easy as to know what were good to do, chapels had been churches and poor men's cottages princes' palaces. It is a good divine that follows his own instructions: I can easier teach twenty what were good to be done, than be one of the twenty to follow mine own teach**ing**. The brain may devise laws for the blood, but a hot temper leaps o'er a cold decree: such a hare is madness the youth, to skip o'er the meshes of good counsel the cripple. But this reason**ing** is not in the fashion to choose me a husband. O me, the word 'choose!' I may neither choose whom I would nor refuse whom I dislike; so is the will of a liv**ing** daughter curbed by the will of a dead father. Is it not hard, Nerissa, that I cannot choose one nor refuse none?
```

However this does not specifically pull out words ending in "ing", so would find a word such as "ingenious" to be a match.

To find all words ending in "ing" you could use the regex 

`\w*ing\b`

```
If to do were as easy as to know what were good to do, chapels had been churches and poor men's cottages princes' palaces. It is a good divine that follows his own instructions: I can easier teach twenty what were good to be done, than be one of the twenty to follow mine own **teaching**. The brain may devise laws for the blood, but a hot temper leaps o'er a cold decree: such a hare is madness the youth, to skip o'er the meshes of good counsel the cripple. But this **reasoning** is not in the fashion to choose me a husband. O me, the word 'choose!' I may neither choose whom I would nor refuse whom I dislike; so is the will of a **living** daughter curbed by the will of a dead father. Is it not hard, Nerissa, that I cannot choose one nor refuse none?

**bing**

**ring**

```

But we aren't quite there. A word like bing or ring isn't really what we are looking for. We want to filter our results to find words that have other vowels outside of the i in "ing" to find actual results. 

Using rubular i was able to filter out bing and ting using the following modified regex. This requires words to contain a vowel before the ending string "ing" meaning we should only capture words in present perfect progressive tense.
```
\b\w*[aeiou]\w*ing\b
```

```
If to do were as easy as to know what were good to do, chapels had been churches and poor men's cottages princes' palaces. It is a good divine that follows his own instructions: I can easier teach twenty what were good to be done, than be one of the twenty to follow mine own **teaching**. The brain may devise laws for the blood, but a hot temper leaps o'er a cold decree: such a hare is madness the youth, to skip o'er the meshes of good counsel the cripple. But this **reasoning** is not in the fashion to choose me a husband. O me, the word 'choose!' I may neither choose whom I would nor refuse whom I dislike; so is the will of a **living** daughter curbed by the will of a dead father. Is it not hard, Nerissa, that I cannot choose one nor refuse none?

bing

ring
```

I hope this was helpfull.

