---
title: "Chapter 8"
author: "Nicolas Restrepo and Stephen Vaisey"
output: 
  html_document: 
    toc: true
    theme: united
    keep_md: true
---



We are going to practice resampling again, but this time armed with the language we learned in chapter 8. We are going to use three different datasets along the way. Don't forget to load the packages you will need.

To make life easier on yourself, be sure to specify a random number seed using `set.seed()` at the beginning of *each* of your code blocks. 

# Polling

## Question 1

Let's start by redoing the polling analysis we did in class. Be sure to use this exact code (including this specific `set.seed()`) to make the dataset.


```r
set.seed(1108)

poll <- tibble(
  vote_gop = rbinom(n = 1000,
                    size = 1,
                    prob = .53))
```

I want you to make a **bootstrap 95% percent confidence interval** for GOP (Republican) vote share based on this poll. I want you to do this two different ways to connect what you learned in chapter 7 and chapter 8.

##### First way

Calculate it using *only* the following functions:

* `rep_sample_n()`
* `group_by()`
* `summarize()`
* `quantile()`

You may also use the `pull()` or `select()` function if you need them.

A few hints: 

1. Make sure you pay attention to the `replace` option in `rep_sample_n()`.
2. When you have the bootstrap distribution, you can get the confidence interval by piping it to `quantile(c(.025, .975))`.

What is the estimated confidence interval?

#### Second way

Now do it using *only* the following functions:

* `specify()`
* `generate()`
* `calculate()`
* `get_ci()`

What is the estimated confidence interval? (HINT: even though you are estimating a proportion, use `stat = "mean"` instead of `stat = "prop"`.)

How similar are the two confidence intervals you calculated? Why aren't they *exactly* the same?

# History of rap

Here, we are going to use a dataset that contains the results of a survey conducted where artists and critics listed their favorite rap tracks. For each track we have information about its release data, and what we are going to do is to examine what is the year of that shows up the most - i.e. we are going to try to find out the year when rap peaked. 

This is not a silly attempt to make a data analysis course more interesting or relatable, this is a real issue in the sociology of culture. We have evidence [that music sales are higher for old music](https://www.theatlantic.com/ideas/archive/2022/01/old-music-killing-new-music/621339/). Nostalgia is the name of the game. A lot of people really believe that old music was better and organizing their music-listening habits around this idea. So understanding where supposed "experts" place the peak of rap is important and interesting. 

The data can be found [here](https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-04-14/polls.csv). Load the data and call the object `rap_poll` and then we'll get started.

First of all, let's just keep the #1 song listed by each critic to make things simple. Use `filter()` to keep only those songs where `rank` is equal to 1. The resulting data frame should have 107 rows.

## Question 2

Make a histogram of the year each of the tracks was released. What is the year of the most commonly named favorite track in this critic poll? How many critics named a track from this year?

## Question 3

Let's assume that these 107 critics are a random sample of a population of critics. If so, it might be useful to construct a 95% confidence interval for the peak of rap. Calculate this interval, using either implementation of the percentile method I asked you to use above. Report the upper and lower bound of this interval to the nearest year.

## Question 4

Let's say that instead of asking 107 critics, we had asked 25 critics. What would the confidence interval (again, rounded to the nearest year) be in that case? (HINT: you will probably need to use the "first way" for calculating a confidence interval you used above.) How does the width of this confidence interval compare to the width of the confidence interval when we use the full sample of 107?


# World Cup penalties

Okay, let's go back to my favorite sport: the soccer World Cup. We will use a dataset of almost 300 penalties shot at the men's World Cup throughout its history. I want you to use bootstrapping to tell me what is the proportion of penalties scored. This might be useful for predicting the proportion of penalties that will be scored in the next World Cup.

The data can be found [here](https://raw.githubusercontent.com/NicolasRestrep/223_course/main/Data/WorldCupShootouts.csv). Load the data and then use `drop_na()` to drop rows where we don't have complete information. The resulting dataset should have 279 rows. The `Goal` column indicates whether the penalty resulted in a goal.

## Question 5

What proportion of the penalties were scored?

## Question 6

Construct the bootstrap distribution of the proportion of penalties scored. Visualize this distribution and use `shade_ci()` to overlay the 95% percentile confidence interval. What are the lower and upper bounds of the interval?

## Question 7

Using your bootstrap distribution, calculate the **standard error** of this estimate.

## Question 8

The chapter teaches you a neat heuristic: that a 95% confidence interval can be calculated by taking the mean and adding 1.96 standard deviations (for the upper limit) and subtracting 1.96 standard deviations (for the lower limit). Using this, and without using the chapter's helper functions, calculate the 95% confidence interval of the proportion of penalty kicks scored at the World Cup.














