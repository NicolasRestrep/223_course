# Chapter 3 

Again, we are going to go through a couple more exercises to reinforce your data wrangling skills. 

As usual, we will begin by loading the `tidyverse` (which is the collection of packages that includes all the verbs you just learned about). 


```r
library(tidyverse)
```

Before, we dealt with Olympic athletes but now we are going to get closer to the peak of human achievement: we are going to look at Mario Kart records. 

The data should be loaded from the the `Data` folder in our directory. 


```r
mario_kart <- read_csv("https://raw.githubusercontent.com/NicolasRestrep/223_course/main/Data/world_records.csv")
```

As always, have a look at the data using `glimpse()`. 

## Question 1 

First, let's keep only the records for `Three Lap`. We are interested in whole races after all. 


```r
three_laps <- mario_kart %>% filter(type == "Three Lap")
```


Anyone worth their salt knows that `"Rainbow Road"` should not even count as a regular track. How would you create a dataset that does not contain any times recorded on that infamous track? Now, save a dataset that only contains the records achieved at Rainbow Road.




## Question 2 

Use `summarize()` to get the average time at Rainbow Road and the standard deviation of the records. 

Now, do the same for the dataset that contains all other tracks. 

Notice any differences? 

## Question 3 

It's definitely unfair and uninformative to lump all non-rainbow-road tracks together. So let's use one of the more powerful tricks in the book: the `group_by` + `summarize` combo. I cannot overstate how much you will use this in your daily life as a data analyst. 

So take our dataset that includes only `Three Lap` times and group it by track, then use summarize to count how many different records have been established on each track. 

What's the track that has had the most records established in it? 

> Hint: the verb `arrange()` might come in handy here.

## Question 4 

We want to know if there are drivers who have multiple records at each track, and how many records they have. This will involve grouping by both driver and track. 

Who is the player that has recorded the most records at any one track and what track was it?

## Question 5 

We still haven't looked at the times on each track. Tell me what the average time for each track is using `group_by` and `summarize`.

What track has the highest average time?

Let me introduce you to a cool trick. The `slice` function takes a certain number of rows inside of each group. For example we can pick the lowest time for each player like this: 


```r
three_laps %>% 
  group_by(player) %>% 
  arrange(time) %>% 
  slice(1) %>% 
  head()
```

```
## # A tibble: 6 × 9
## # Groups:   player [6]
##   track         type  shortcut player system_played date       time_period  time
##   <chr>         <chr> <chr>    <chr>  <chr>         <date>     <chr>       <dbl>
## 1 Choco Mounta… Thre… Yes      ABE    NTSC          1997-06-01 1M 39.79S    99.8
## 2 Choco Mounta… Thre… Yes      abney… NTSC          2021-02-03 17.29S       17.3
## 3 Yoshi Valley  Thre… Yes      Alex G PAL           2010-11-27 33.39S       33.4
## 4 Frappe Snowl… Thre… Yes      Allen… NTSC          1997-10-31 28.22S       28.2
## 5 Wario Stadium Thre… Yes      Ben M  PAL           2002-08-22 15.48S       15.5
## 6 Frappe Snowl… Thre… Yes      Booth  NTSC          1998-09-18 27.11S       27.1
## # … with 1 more variable: record_duration <dbl>
```

`head()` is just there to make sure that I only print a small amount of names. 

Now, it's your turn to show me the best time recorded on each track

The result you get using `group_by` and `arrange` contains a lot of information. So let's use `select` so that your out displays only the name of the track and the lowest time recorded there. 

## Question 6 

Let's practice creating new variables. I am interested in the records that have held for longer than 100 days. Create a new variable that is a `1` if `record_duration` is higher than 100 or 0 otherwise. 

Now, grouping by player, tell me the total amount of long duration records each player holds. What player has the most long duration records? 

## Question 7 

We will finish by strengthening our `joining` skills. We have another dataset called `drivers` that tells us where drivers are from. 

Here's how you can read it in. 


```r
drivers <- read_csv("https://raw.githubusercontent.com/NicolasRestrep/223_course/main/Data/drivers.csv")
```

Now use `left_join` to join `three_laps` and `drivers` together. 

Now, plot a bar chart for how many records each country has. 



