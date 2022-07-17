# Chapter 4 - Data Visualization

Here, we are going to practice and reinforce some of the key ideas from chapter 4. 

## Question 1 

We are going to work with a dataset of TV Ratings taken from IMDB. Let's read it in and see what we have. 


```r
library(tidyverse)

# Read in the data 
tv_ratings <- read_csv("../Data/tv_ratings.csv")

# Glimpse the data 
glimpse(tv_ratings)
```

```
## Rows: 2,266
## Columns: 7
## $ titleId      <chr> "tt2879552", "tt3148266", "tt3148266", "tt3148266", "tt31…
## $ seasonNumber <dbl> 1, 1, 2, 3, 4, 1, 2, 1, 2, 3, 4, 5, 6, 7, 8, 1, 1, 1, 1, …
## $ title        <chr> "11.22.63", "12 Monkeys", "12 Monkeys", "12 Monkeys", "12…
## $ date         <date> 2016-03-10, 2015-02-27, 2016-05-30, 2017-05-19, 2018-06-…
## $ av_rating    <dbl> 8.4890, 8.3407, 8.8196, 9.0369, 9.1363, 8.4370, 7.5089, 8…
## $ share        <dbl> 0.51, 0.46, 0.25, 0.19, 0.38, 2.38, 2.19, 6.67, 7.13, 5.8…
## $ genres       <chr> "Drama,Mystery,Sci-Fi", "Adventure,Drama,Mystery", "Adven…
```

We notice that each row is a season-title pair. Then we get the average rating for that season of that show, and the corresponding genre. 

The first thing that we are going to look at is how rating develops across seasons, for different genres. To do this, we need shows that have lasted a while. The following bit of code counts how many seasons each show has and then keeps those shows that have had 5 seasons or more. 


```r
tv_long <- tv_ratings %>% 
  group_by(title) %>% 
  summarise(num_seasons = n()) %>% 
  ungroup() %>% 
  left_join(tv_ratings, by = "title") 

tv_long <- tv_long %>% 
  filter(num_seasons >= 5)
```

Use `tv_long` to make a line plot to trace how average ratings evolve across seasons. Remember to use the group aesthetic so that each line represents one show. 

It should look fairly messy. Can you draw any conclusions from it?

## Question 2

Facet the plot above by `genres` so that we can see patterns more clearly. 

What shows tend to last longer? Do ratings change much across seasons? Can you identify that show on `Drama, Family, Fantasy` whose ratings just plummeted?

## Question 3 

Let's look at the `genres` that show up in the best rated shows. 

First, filter the original data set - `tv_ratings` - so that it only includes rows where the average rating is higher or equal than 9. 

Make a barplot where the x-axis is `genre`. 

The result should be hard to read - the names of the genres are quite long. Add `coord_flip()` to the end of your ggplot call and watch the results get clearer. Tell me what `coord_flip()` does. 

What is the genre with the most top-rated shows? 

## Question 4 

As a comedy fan, I am quite distraught by the results. I want to compare the range of average ratings that comedies and dramas get. Surely there are many bad comedies but the best comedies should rival the best dramas. Right? 

For this, we need to do a bit of wrangling that I am going to walk you through. 

First, because the `genres` names are so convoluted, I am going to classify everything that includes the word "Comedy" as a comedy. 


```r
comedies_dramas <- tv_ratings %>% 
  mutate(is_comedy = if_else(str_detect(genres, "Comedy"), 
                             1, 
                             0)) %>% # If it contains the word comedy then 1, else 0
  filter(is_comedy == 1 | genres == "Drama") %>% # Keep comedies and dramas
  mutate(genres = if_else(genres == "Drama", # Make it so that we only have those two genres
                          "Drama", 
                          "Comedy"))

glimpse(comedies_dramas)
```

```
## Rows: 684
## Columns: 8
## $ titleId      <chr> "tt0312081", "tt0312081", "tt0312081", "tt1225901", "tt12…
## $ seasonNumber <dbl> 1, 2, 3, 1, 2, 3, 4, 5, 1, 2, 1, 25, 1, 1, 2, 3, 4, 5, 1,…
## $ title        <chr> "8 Simple Rules", "8 Simple Rules", "8 Simple Rules", "90…
## $ date         <date> 2002-09-17, 2003-11-04, 2004-11-12, 2009-01-03, 2009-11-…
## $ av_rating    <dbl> 7.5000, 8.6000, 8.4043, 7.1735, 7.4686, 7.6858, 6.8344, 7…
## $ share        <dbl> 0.03, 0.10, 0.06, 0.40, 0.14, 0.10, 0.04, 0.01, 0.48, 0.4…
## $ genres       <chr> "Comedy", "Comedy", "Comedy", "Comedy", "Comedy", "Comedy…
## $ is_comedy    <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, …
```

Now, you should have a dataset with shows that are categorized as either drama or comedies. 

Plot a density plot that shows the distribution of average ratings for both comedies and dramas. 

How does my prediction above hold? Are dramas rated higher? 

## Question 5

Let's experiment with different ways of visualizing this. First, do the same plot using histograms. 

What additional information does this give you? 

> Hint: look at the size of the bars. I probably categorized way too many shows as "comedies". I had to stack the deck.

Now, use `geom_freqpoly()`. What do you notice? Of the three plots, which one do you think it's more informative? 

## Question 6 

Let's now explore whether the actual quality of the show corresponded to how many people were paying attention. The column `share` indicates the share of viewership that that show and season acquired. We are going to examine the relationship between average rating and share of viewership. 

Take our `comedies_dramas` dataset and make a plot where average rating is on the x-axis and share on the y-axis. Use `geom_bin_2d()` to make the plot. 

What do you see? What additional information does this give you in comparison to a scatter plot? 

Now add `genres` to the fill aesthetic. What patterns do you see? Can you identify that big outlier that apparently captured the nation? 




