---
title: "Chapter 1"
author: "Nicolas Restrepo"
output: 
  html_document: 
    toc: true
    theme: united
    keep_md: true
---



These are going to be some complementary exercises to get you even more comfortable as you get used to working with R and RStudio. 

## Question 1 

Let's begin by reviewing how to install packages. Try installing three packages called `causact`, `dplyr`, and `igraph`.These will come in handy in our examples below. 

## Question 2

Load all three packages in the order they were presented above. You should get messages that look something like this. 


```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```
## 
## Attaching package: 'igraph'
```

```
## The following objects are masked from 'package:dplyr':
## 
##     as_data_frame, groups, union
```

```
## The following objects are masked from 'package:stats':
## 
##     decompose, spectrum
```

```
## The following object is masked from 'package:base':
## 
##     union
```

It is not wise to ignore these messages; reading them will often save you a lot of time. For instance, R is telling you that `igraph` is "masking" an object called `as_data_frame` from the `dplyr` package. What on earth does that mean?

Well, it turns out that `igraph` called  `as_data_frame`. It takes a graph and turns it into a dataframe. Now, it just so happens that dplyr has a function with that exact name, which takes objects at turns them into a dataframe. 

Run the following code: 


```r
df <- as_data_frame(x = c(1,2,3))
```

It should give you an error. What does it say? 

Now, run this code: 


```r
df <- dplyr::as_data_frame(x = c(1,2,3))
```

```
## Warning: `as_data_frame()` was deprecated in tibble 2.0.0.
## Please use `as_tibble()` instead.
## The signature and semantics have changed, see `?as_tibble`.
## This warning is displayed once every 8 hours.
## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was generated.
```

```r
glimpse(df)
```

```
## Rows: 3
## Columns: 1
## $ value <dbl> 1, 2, 3
```

Why did this one work? You just learned that you can invoke a specific package function by passing the package name followd by two colons and the function's name. Using this format use the `n_distinct()` function in dplyr to count the number of elements in the following collection of numbers: 


```r
x <- c(5,6,2,7,9,1)
```

In your first call to `as_data_frame`, R called the function from `igraph`. That's why it didn't work: it was expecting a graph but instead got a collection of numbers. Can you figure out why R called the function from `igraph` instead of `dplyr`? 

## Question 3 

You might think it is unfair that I made you use an unknown function `n_distinct()`. Use the `?` operator to figure out what the function does and tell me briefly in your own words. 

## Question 4 

The reason we also loaded the `causeact` package is because it includes some interesting data. As I did above, use the `glimpse()` function to look at an object called `baseballData`. 

This function gives you a ton of information. 

How many rows does the dataset have?
How many columns? 
What type of variable is the `Home` column? What about `HomeScore`? 

## Question 5

Let's play with the data a bit. We can look at the first row of the data by running the following: 


```r
baseballData[1,]
```

```
##       Date Home Visitor HomeScore VisitorScore
## 1 20100405  ANA     MIN         6            3
```

What does one row in the data represent? 

Similarly, we can select certain columns. For instance, if we want the 2nd and 3rd columns, we could do something like this. 


```r
baseballData[,2:3] %>% head()
```

```
##   Home Visitor
## 1  ANA     MIN
## 2  CHA     CLE
## 3  KCA     DET
## 4  OAK     SEA
## 5  TEX     TOR
## 6  ARI     SDN
```

What do these two columns represent? 

## Question 6 

To finish this exercises, let's review how to build our own dataframes. Let's say you have been collecting data on historical hockey goal scorers and you want to build a dataset about the top ten. You have three variables: 

- Name
- Total goals
- The year they started playing in the NHL

Here's data: 


```r
name <-
  c(
    "Wayne Gretzky",
    "Gordie Howe",
    "Jaromir Jagr",
    "Brett Hull",
    "Marcel Dionne",
    "Phil Esposito" ,
    "Mike Gartner",
    "Alex Ovechkin",
    "Mark Messier" ,
    "Steve Yzerman"
  )

goals <- c(894, 801, 766, 741, 731, 717, 708, 700, 694, 692)

year_started <- c(1979, 1946, 1990, 1986, 1971, 1963, 1979, 2005, 1979, 1983)
```

You can put all these elements together in a dataframe by using the `tibble()` function. It should look something like this: 


```r
df <- tibble( 
  <first_var_name> = name, 
  <second_var_name> = ..., 
  ... ) 
```

Now, call `glimpse()` on your newly created dataframe and see whether it works. 

