---
title: "Homework 6.2"
author: "Stephen Vaisey"
date: "2022-10-25"
output: 
  html_document: 
    toc: true
    theme: united
    keep_md: true
---



For this assignment you are going to use the `bikes` dataset we began analyzing in class. You can get that dataset from the **bayesrules** package. Once **bayesrules** is installed, you can begin.


```r
library(tidyverse)
library(moderndive)
theme_set(theme_minimal())
```

Load the data and take a look.


```r
data(bikes, package = "bayesrules")
glimpse(bikes)
```

```
## Rows: 500
## Columns: 13
## $ date        <date> 2011-01-01, 2011-01-03, 2011-01-04, 2011-01-05, 2011-01-0…
## $ season      <fct> winter, winter, winter, winter, winter, winter, winter, wi…
## $ year        <int> 2011, 2011, 2011, 2011, 2011, 2011, 2011, 2011, 2011, 2011…
## $ month       <fct> Jan, Jan, Jan, Jan, Jan, Jan, Jan, Jan, Jan, Jan, Jan, Jan…
## $ day_of_week <fct> Sat, Mon, Tue, Wed, Fri, Sat, Mon, Tue, Wed, Thu, Fri, Sat…
## $ weekend     <lgl> TRUE, FALSE, FALSE, FALSE, FALSE, TRUE, FALSE, FALSE, FALS…
## $ holiday     <fct> no, no, no, no, no, no, no, no, no, no, no, no, no, yes, n…
## $ temp_actual <dbl> 57.39952, 46.49166, 46.76000, 48.74943, 46.50332, 44.17700…
## $ temp_feel   <dbl> 64.72625, 49.04645, 51.09098, 52.63430, 50.79551, 46.60286…
## $ humidity    <dbl> 80.5833, 43.7273, 59.0435, 43.6957, 49.8696, 53.5833, 48.2…
## $ windspeed   <dbl> 10.749882, 16.636703, 10.739832, 12.522300, 11.304642, 17.…
## $ weather_cat <fct> categ2, categ1, categ1, categ1, categ2, categ2, categ1, ca…
## $ rides       <int> 654, 1229, 1454, 1518, 1362, 891, 1280, 1220, 1137, 1368, …
```

## Question 0

Before analyzing a dataset, it's good to know some stuff about it. Answer the following questions:

* how many rows are in the dataset?
* what does each row represent?
* what dates does the dataset cover?
* what is the highest observed ridership in the dataset?
* what was the highest wind speed recorded in the dataset?

## Question 1

What is the correlation between number of rides and what the temperature feels like (in Fahrenheit)? What is the correlation between the number of rides and wind speed (miles per hour)?

## Question 2

Using the approximation that a mile is equal to 1.61 kilometers, convert `windspeed` to kilometers per hour. Call the new variable `wind_kph` and add it to the `bikes` data frame. What is the correlation between wind speed in MPH and wind speed in KPH? Explain why in enough detail that I know you understand.

## Question 3

Estimate two simple regressions:

* predict rides as a function of wind speed in MPH
* predict rides as a function of wind speed in KPH

Use `get_regression_table()` or `broom::tidy()` to display the results. This will give you two sets of an intercept and a slope. If any coefficients are the same between models, explain why. If any coefficients are different between models, explain why. Make sure to give me enough detail to convince me you understand.

## Question 4

Using the models from above, tell me what the predicted ridership would be if the wind is blowing at 20 KPH. What would the predicted ridership be if thd wind is blowing at 20 MPH?

## Question 5

Let's get more realistic and move to multiple regression. We're going to use `temp_feel` in addition to wind speed. But we don't want to use Fahrenheit. So make a new variable called `temp_c` that is a conversion of `temp_feel` to Celsius and add it to the `bikes` dataframe. (You may have to look up how to do this conversion.)

With this new variable, estimate a multiple regression that predicts rides as an additive function of `wind_kph` and `temp_c` (that is, no interaction). Interpret both of the slope coefficients using the following language:

"For a _____ increase in _____, the model expects a _____ increase in _____."

Now interpret the intercept.

## Question 6

Using the multiple regression you just estimated, give me ridership predictions for the following situations:

* SITUATION 1: temp = 25C, wind = 15 KPH
* SITUATION 2: temp = 15C, wind = 5 KPH
* SITUATION 3: temp = 10C, wind = 40 KPH

You can do this manually (using R as a calculator) or you might find the following code useful:


```r
pred_df <- tibble(
  situation = 1:3,
  temp_c = c(25, 15, 10),
  wind_kph = c(15, 5, 40)
)
```

## Question 7

Let's add another predictor into the mix. Estimate a new model that uses `weekend` in addition to the predictors already in the model. Display the model results. Interpret the coefficient on `weekend` using a complete sentence.

## Question 8

If the temperature and the wind speed are average, what is the expected ridership for a weekend day? What is the expected ridership for a weekday? Show the code that gets you your answers.

## Question 9

You can use `get_regression_points()` or `predict()` to see how the model did at predicting each individual value of `rides`. Use one of these functions to find the date with the _largest absolute residual_. That is, find the day where the model is most wrong about predicted ridership. Why do you think the model is so wrong on this day?
