---
title: "Chapter 4"
author: "Nicolas Restrepo"
output: 
  html_document: 
    toc: true
    theme: united
    keep_md: true
---



Chapter 4 is fairly comprehensive but let's do a couple more things to get more comfortable with reading in data and transforming it into a tidy format. 

Let's load the collection of packages we usually rely on: 


```r
library(tidyverse)
```

## Question 1 

We have done this a couple of times but I want to reinforce how handy of a trick this is. It turns out you can read in data directly from the internet. 

Go to this [link](https://github.com/NicolasRestrep/223_course/blob/main/Data/nfl_salaries.csv). Yes, I recognize that this is the course repository. Yes, I recognize you also have this data because you cloned into the repository. But this is useful I promise. 

Then, click on a button that says `Raw`. Once you see the the raw data, copy the link. Now, use `read_csv` but pass the link (inside quotation marks) as an argument.


## Question 2 

This dataset is clearly not in a tidy format. Reshape it so that every row tells you the salary associated with a position each year. Your new dataset should have three columns: `year`, `position`, `salary`. 



## Question 3 

Of course, there are many folks in each position and their salaries are vary widely. Let's look at quarterbacks for example. Filter your newly created dataset so that it only contains quarterbacks. Then, make a histogram where salary is in the x-axis. Then use `facet_wrap` to get the histogram for each `year`. 

What patterns do you notice? 

## Question 4 

Let's calculate the average salary for each position, each year. Create a new dataset that contains the average salary for each position each year. To do this, you will need the `group_by` and `summarize` combo. 



> Hint: Beware of a couple of NAs in there 

## Question 5 

Make a linegraph that traces the evolution of each position's average salary across the years. You can use use different strategies to distinguish between positions - color or facets for example. What is important is that you see each position's trajectory clearly and that they are comparable. 

Describe at least two trends that are apparent to you. 

