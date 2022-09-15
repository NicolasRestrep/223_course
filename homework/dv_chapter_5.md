---
title: "Chapter 5"
author: "Nicolas Restrepo"
output: 
  html_document: 
    toc: true
    theme: united
    keep_md: true
---



Here, we are going to practice some of the skills emphasized in Chapter 5. At first, it may seem that a lot of the skills are similar to those we learned in Modern Dive. I have two responses to that. First, you are right; repetition is important. That's how we learn things. Second, this chapter presents some incredibly handy tricks that as a Data Analyst you will use all the time. In these exercises, we are going to be using data from the WNCAA tournament. 

As always, let's begin by reading in the data. 


```r
library(tidyverse)
# Read in the data 
wncaa <- read_csv("../Data/wncaa.csv")

# Glimpse the data 
glimpse(wncaa)
```

```
## Rows: 2,092
## Columns: 19
## $ year              <dbl> 1982, 1982, 1982, 1982, 1982, 1982, 1982, 1982, 1982…
## $ school            <chr> "Arizona St.", "Auburn", "Cheyney", "Clemson", "Drak…
## $ seed              <dbl> 4, 7, 2, 5, 4, 6, 5, 8, 7, 7, 4, 8, 2, 1, 1, 2, 3, 6…
## $ conference        <chr> "Western Collegiate", "Southeastern", "Independent",…
## $ conf_w            <dbl> NA, NA, NA, 6, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ conf_l            <dbl> NA, NA, NA, 3, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ conf_percent      <dbl> NA, NA, NA, 66.7, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ conf_place        <chr> "-", "-", "-", "4th", "-", "-", "-", "-", "-", "-", …
## $ reg_w             <dbl> 23, 24, 24, 20, 26, 19, 21, 14, 21, 28, 24, 17, 22, …
## $ reg_l             <dbl> 6, 4, 2, 11, 6, 7, 8, 10, 8, 7, 5, 13, 7, 5, 1, 6, 4…
## $ reg_percent       <dbl> 79.3, 85.7, 92.3, 64.5, 81.3, 73.1, 72.4, 58.3, 72.4…
## $ how_qual          <chr> "at-large", "at-large", "at-large", "at-large", "aut…
## $ x1st_game_at_home <chr> "Y", "N", "Y", "N", "Y", "N", "N", "N", "N", "N", "Y…
## $ tourney_w         <dbl> 1, 0, 4, 0, 2, 0, 0, 0, 0, 0, 2, 0, 2, 1, 5, 3, 1, 1…
## $ tourney_l         <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1…
## $ tourney_finish    <chr> "RSF", "1st", "N2nd", "1st", "RF", "1st", "1st", "1s…
## $ full_w            <dbl> 24, 24, 28, 20, 28, 19, 21, 14, 21, 28, 26, 17, 24, …
## $ full_l            <dbl> 7, 5, 3, 12, 7, 8, 9, 11, 9, 8, 6, 14, 8, 6, 1, 7, 5…
## $ full_percent      <dbl> 77.4, 82.8, 90.3, 62.5, 80.0, 70.4, 70.0, 56.0, 70.0…
```

We have data for all teams that have made it to the WNCAA tournament. We have a wealth of information from `reg_percent`, the percentage of wins in the regular season, to the place they ended in a given tournament (`tourney_finish`).

## Question 1

Let's practice some of the summarizing skills that Healy introduces. We are going to examine the percentage of tournaments that schools have won. 

First, `filter` the dataset for observations where `tourney_finish` equals `Champ`. 



Now, use `group_by` and `summarize` to calculate the percentage of tournaments each team has. 

> Hint: look at the first code chunk of the chapter. 



Plot a bar plot that shows these percentages by school. 

What trends do you see? Who are the two teams that have won the most?

## Question 2 

Let's now look at how the top teams have been seeded as they enter into the tournament. Let's begin by creating a dataset that includes just the "top teams". How are we going to do this? Well, let's take the teams that show up in your bar plot above. We are going to work with the dataset that only includes teams that have ever won the tournament. I'll show you how to do it. 

The dataset I created for the plot above is called `champs`. Let's get the names of the champions: 


```r
champ_names <- unique(champs$school)
```

Now, we filter our original name so that only these schools are included. 


```r
winners <- wncaa %>% 
  filter(school %in% champ_names)
```

Now, make a plot that shows boxplots for the distribution of `seeds` for each school. Make sure you use `coord_flip()` so that the school names are legible. 

But here we probably want to organize the boxplots so that they convey information more clearly. Use the `reorder()` trick that the book introduces to show the distributions in a more legible order. 

Describe the results? Any surprises? 

Try to make the same plot using `geom_violin()` instead of boxplots. 

Which one do you think is more informative? 

## Question 3 

Try making the plot above but using `geom_point`. Why does it not work very well? 

## Question 4 

Okay, now let's try the `summarize_if` verb. Let's take the `winners` dataset, group by school, and take the `mean()` and `sd()` of the columns **if** they are numeric. 

Let's explore the average win percentage of these schools across the seasons. In your new dataset, this column should be called `reg_percent_mean`. Make a dot plot, where this column is in the y-axis and school is the x-axis. Again, use our tricks, `coord_flip` and `reorder` to make the plot legible.



Describe the results. 

Now, let's try to take into account the standard deviation. Use the `geom_pointrange` to show the intervals of one standard deviation below and above the mean (just like in the chapter).

What is the school with the most narrow interval? 

Can you make the same plot using `geom_linerange` ? 

## Question 5 

It would be interesting to explore how your performance in the regular season is related to full performance, after the tournament is done. Let's take our `winners` dataframe and plot these two variables in a scatterplot where `reg_percent` is in the x-axis and `full_percent` is in the y-axis. 

Add `geom_abline()` to your call. Without arguments, this just plots a 45 degree line. You can think about this line as performance in regular season perfectly predicting the full performance. Now, this is almost impossible, as most teams will take losses in the tournament. This is why we expect most points to be below this line. The points are above this line represent teams whose overall performance improved after the tournament - they did better than we would have expected given the regular season. 

What patterns do you see? 

## Question 6 

Let's see how champions are reflected in this plot. Let's make a variable what is a 1 if that team ended up winning the tournament or a 0 otherwise. 


```r
winners <- winners %>% 
  mutate(is_champ = if_else(tourney_finish == "Champ", 1, 0), 
         is_champ = as.factor(is_champ))
```

Now, color the plot above according to our newly created variable. 

> Why did I make `is_champ` a factor? Try the plot without making that variable a factor. What changes? 

Do you see any patterns? Do they make sense to you? 

## Question 7 

There are two points that really stick out to me. All the way to the left of the x-axis, there is a team that made it to the tournament in spite of having a really bad regular season record. And around the 70% in the x-axis, there is a team that over-performed in the tournament. I want you to label these points. 

But I am not only interested in the school but also in the year this happened. Let's combine the variables for school and year to create our labels. 


```r
winners <- winners %>% 
  mutate(plot_label = paste(school, year, sep = "-"))
```

Let's also create a variable for the difference between full performance and regular season performance. 


```r
winners <- winners %>% 
  mutate(difference = full_percent - reg_percent) 
```

Now, it's up to you to label the points of interest. 

Do you see anything interesting? I'll give you a hint: the school that has overperformed the most has been the same one, one decade apart. 

## Question 8 

There's a few teams that have gone unbeaten. This means 100% performance in the regular and full seasons. Tell me what teams they are. 

Any patterns? Surprises? 
