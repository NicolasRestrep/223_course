# Chapter 2 

These are going to be some complementary exercises to practice some initial data visualization skills.

Let's begin by loading the data. We will be working with data about all Olympic Gold Medalists. 

First, we load some necessary packages. 


```r
library(tidyverse)
```

Then, we read the data in directly from the internet: 


```r
olympics  <- read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-07-27/olympics.csv')
glimpse(olympics)
```

```
## Rows: 271,116
## Columns: 15
## $ id     <dbl> 1, 2, 3, 4, 5, 5, 5, 5, 5, 5, 6, 6, 6, 6, 6, 6, 6, 6, 7, 7, 7, …
## $ name   <chr> "A Dijiang", "A Lamusi", "Gunnar Nielsen Aaby", "Edgar Lindenau…
## $ sex    <chr> "M", "M", "M", "M", "F", "F", "F", "F", "F", "F", "M", "M", "M"…
## $ age    <dbl> 24, 23, 24, 34, 21, 21, 25, 25, 27, 27, 31, 31, 31, 31, 33, 33,…
## $ height <dbl> 180, 170, NA, NA, 185, 185, 185, 185, 185, 185, 188, 188, 188, …
## $ weight <dbl> 80, 60, NA, NA, 82, 82, 82, 82, 82, 82, 75, 75, 75, 75, 75, 75,…
## $ team   <chr> "China", "China", "Denmark", "Denmark/Sweden", "Netherlands", "…
## $ noc    <chr> "CHN", "CHN", "DEN", "DEN", "NED", "NED", "NED", "NED", "NED", …
## $ games  <chr> "1992 Summer", "2012 Summer", "1920 Summer", "1900 Summer", "19…
## $ year   <dbl> 1992, 2012, 1920, 1900, 1988, 1988, 1992, 1992, 1994, 1994, 199…
## $ season <chr> "Summer", "Summer", "Summer", "Summer", "Winter", "Winter", "Wi…
## $ city   <chr> "Barcelona", "London", "Antwerpen", "Paris", "Calgary", "Calgar…
## $ sport  <chr> "Basketball", "Judo", "Football", "Tug-Of-War", "Speed Skating"…
## $ event  <chr> "Basketball Men's Basketball", "Judo Men's Extra-Lightweight", …
## $ medal  <chr> NA, NA, NA, "Gold", NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
```

We have a pretty big dataset. Look at the `medal` column. It has these unique values: 


```r
table(olympics$medal)
```

```
## 
## Bronze   Gold Silver 
##  13295  13372  13116
```

## Question 1 

In the chapter we learned how to filter datasets. Can you figure out how to keep only the Gold Medalists? It should look something like this. 


```r
gold_medalists <- olympics %>% 
  <function_name>(medal == "<something>")
```

How many rows does the resulting dataset have? 

## Question 2 

Make a plot that has year on one axis and the age of the winner on the other. What's the most appropriate plot to display these data? 

How has the age of participants change across the years? 

We are missing a lot of information because there are a lot of athletes that have the same age. This means we are overplotting. Can you think of a solution to this? 

## Question 3 

The following bit of code gives us the amount of medals that the U.S. has won across the years. 


```r
us_medals <- gold_medalists %>% 
  filter(noc == "USA") %>% 
  group_by(year) %>% 
  summarise(num_medals = n())
```

You have two columns now: one for year and one for the number of Gold Medals won that year. Plot this trajectory as a linegraph. 

What was the country's most successful year? As a bonus, can you guess why the line is so wiggly (technical term) towards the end? 

## Question 4 

Now, let's explore differences in the kind of athlete that has excelled at different events. Let's look at two hallmark events in the Olympics: gymnastics and the 100 meter dash. I am going to make a dataset that only includes data about these events. 


```r
two_events <- gold_medalists %>%
  filter(
    event == "Gymnastics Men's Individual All-Around"  |
      event == "Gymnastics Women's Individual All-Around" |
      event == "Athletics Women's 100 metres"   |
      event == "Athletics Men's 100 metres"
  ) 
```

Filter the dataset I just created so that it only contains the gymnastics events. Now, make a histogram where age is in the x-axis. 

Briefly describe this distribution. 

Now, try to see whether there are differences between female and male athletes by using the `facet_wrap()` function. What athletes tend to be older? 

## Question 5

Now, you're going to use boxplots to show me which one of the events above has taller athletes. Make a boxplot where the x-axis is event and the y-axis is height. 

Briefly describe your results. 

## Question 6 

Now, let's do another exercise. We will explore the proportion of U.S. medals that were won by male and female athletes each year. 

First, let's keep only U.S. cases. 


```r
us_medalists <- gold_medalists %>% 
  filter(noc == "USA")
```

Make a barplot where the x axis is `year`. Make sure you can see parallel lines for female and male athletes. 

> Hint: you can use `position = dodge` for this. 

Can you notice any patterns?

