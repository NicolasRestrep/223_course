# Chapter 10  

For the last set of complementary exercises, we will go to one of the topics that have made data analysis and statistics famous: baseball. Now, I am far from an expert in baseball, but the wealth of data that the game provides makes it a space of almost endless possibilities for folks who are interested in that sort of thing. 

Chapter 10 brings some of the ideas about hypothesis testing into the realm of regression. We will review these ideas. Here, we will be looking at pitchers' data. Specifically, we are going to be looking at variables that might predict pitchers' performance. Our variable for pitchers' performance will be ERA - Earned Run Average. This basically means: how many runs did you allow your opponents to score (per nine innings). The implication is that a lower ERA means a better pitching performance. 

Let's read in and glimpse the data. 


```r
pitchers <- read_csv("../Data/Pitching.csv")
glimpse(pitchers)
```

```
## Rows: 49,430
## Columns: 30
## $ playerID <chr> "bechtge01", "brainas01", "fergubo01", "fishech01", "fleetfr0…
## $ yearID   <dbl> 1871, 1871, 1871, 1871, 1871, 1871, 1871, 1871, 1871, 1871, 1…
## $ stint    <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
## $ teamID   <chr> "PH1", "WS3", "NY2", "RC1", "NY2", "TRO", "RC1", "FW1", "PH1"…
## $ lgID     <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ W        <dbl> 1, 12, 0, 4, 0, 0, 0, 6, 18, 12, 0, 0, 1, 10, 19, 2, 16, 1, 1…
## $ L        <dbl> 2, 15, 0, 16, 1, 0, 1, 11, 5, 15, 0, 2, 0, 17, 10, 0, 16, 0, …
## $ G        <dbl> 3, 30, 1, 24, 1, 1, 3, 19, 25, 29, 1, 7, 3, 28, 31, 2, 32, 9,…
## $ GS       <dbl> 3, 30, 0, 24, 1, 0, 1, 19, 25, 29, 0, 1, 0, 28, 31, 2, 32, 0,…
## $ CG       <dbl> 2, 30, 0, 22, 1, 0, 1, 19, 25, 28, 0, 1, 0, 22, 22, 2, 31, 0,…
## $ SHO      <dbl> 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0…
## $ SV       <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 3, 0, 0, 0…
## $ IPouts   <dbl> 78, 792, 3, 639, 27, 3, 39, 507, 666, 747, 3, 88, 31, 674, 77…
## $ H        <dbl> 43, 361, 8, 295, 20, 1, 20, 261, 285, 430, 1, 50, 10, 296, 33…
## $ ER       <dbl> 23, 132, 3, 103, 10, 0, 5, 97, 113, 153, 1, 22, 4, 94, 96, 5,…
## $ HR       <dbl> 0, 4, 0, 3, 0, 0, 0, 5, 3, 4, 0, 4, 0, 9, 2, 0, 7, 0, 6, 4, 0…
## $ BB       <dbl> 11, 37, 0, 31, 3, 0, 3, 21, 40, 75, 2, 6, 3, 47, 38, 8, 39, 4…
## $ SO       <dbl> 1, 13, 0, 15, 0, 0, 1, 17, 15, 12, 0, 0, 0, 34, 23, 0, 22, 0,…
## $ BAOpp    <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ ERA      <dbl> 7.96, 4.50, 27.00, 4.35, 10.00, 0.00, 3.46, 5.17, 4.58, 5.53,…
## $ IBB      <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ WP       <dbl> 7, 7, 2, 20, 0, 0, 1, 15, 3, 44, 1, 2, 5, 48, 11, 0, 15, 3, 2…
## $ HBP      <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ BK       <dbl> 0, 0, 0, 0, 0, 0, 0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
## $ BFP      <dbl> 146, 1291, 14, 1080, 57, 3, 70, 876, 1059, 1334, 6, 160, 51, …
## $ GF       <dbl> 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 1, 5, 3, 1, 3, 0, 1, 6, 0, 1, 0…
## $ R        <dbl> 42, 292, 9, 257, 21, 0, 30, 243, 223, 362, 1, 53, 8, 288, 272…
## $ SH       <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ SF       <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ GIDP     <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
```

We have a wealth of data. If you are interested, I got this data from the amazing Lahman Database, which is truly an astounding resource. In our dataset each row represents the career stats of a player. Here, we are going to be interested in just three variables: `ERA`, `BAopp`, `WP`. The first we already covered. The last two represent the opponents' batting average and wild pitches respectively. Wild pitches are throws that were not caught by the catcher (at the pitcher's fault) *and* that caused someone to advance a base. 

One thing you might notice is that we have a fair amount of `NA`s in our variables of interest. Let's get rid of those before we start our analysis. 


```r
pitchers_cln <- pitchers %>% 
  select(ERA, BAOpp, WP) %>% 
  drop_na()
```

## Question 1 

What does it mean to start thinking of the fitted intercept and slope of a regression as point estimates? Why does this introduce uncertainty? 

## Question 2 

What is the number that quantifies that uncertainty? 

> Hint: it is the standard deviation of a point estimate. 

## Question 3 

Okay, let's dive right in. Run a linear regression with `ERA` as an outcome variable as `BAopp` as the explanatory variable. Save it as `model1`. 

Using `tidy()` describe your results. Does the coefficient make sense? Is the relationship what you expected? 

## Question 4 

Examine the standard error. Describe it in a few sentences. Are you confident in the result?

## Question 5

Examine the p-value. What does it imply about the confidence we can have in our results?

## Question 6 

Let's do an exercise that will test your skills a bit. Write a script that samples 30 pitchers and run the same analysis. Save these results as `model2`. 

Now, do the same with 100 and 1000 pitchers. Name these models, `model3` and `model4` respectively. 

Examine the p-values of each of the models. What can you notice? 

This should also be a cautionary tale. Huge samples offer the "benefit" of almost guaranteed infinitesimally small p-values. In the age of Big Data, this means that any person can take a huge dataset, make a silly argument, and call it statistically significant. 

## Question 7 

Another cautionary tale to end the course. 

Run a linear regression with `ERA` as an outcome variable as `WP` as the explanatory variable. Examine the results using `tidy()`. 

Presumably, these results are fairly counterintuitive. Wild pitches are related to better performance. 

Why can that be? It might mean that more reckless pitchers are actually better. Perhaps, they are more unpredictable. A far more plausible interpretation however is that pitchers who take more risks are both more likely to get wild pitches and more likely to succeed. 

Now, we don't know what the correct explanation is. This is the lesson here. We have a really strong relationship with an infinitesimally small p-value. In the world of mindless data analysis, we have struck gold. However, even in this beautiful scenario, we have multiple stories that are consistent with our results. P-values are never a sign that something is *causing* something else or that a variable is a key part of an explanatory mechanism. They are simply a way of describing the uncertainty around a point estimate, **conditional** on the model you have fitted. Next time someone tells you a big story around a coefficient just because it is *statistically significant*, we hope you have a question or two. 


