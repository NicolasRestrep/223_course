---
title: "MD1 Model Answer"
author: "Professor Vaisey"
output: 
  html_document:
    keep_md: true
---

# Question 1

First I will install some packages. Since I only want to do this one time (not every time I render this document) I am going to set the "chunk option" `eval=FALSE`. This tells R not to "evaluate" (i.e., execute) this block of code.


```r
install.packages("causact")
install.packages("dplyr")
install.packages("igraph")
```

# Question 2

Now that those are installed, I can load them.


```r
library(causact)
library(dplyr)
```

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

```r
library(igraph)
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

I got the warning messages, as anticipated.


```r
# df <- as_data_frame(x = c(1, 2, 3))
```

I tried to run the code above but (as expected!) it gave me an error. It said that x "wasn't a graph object." I'm not sure what that means! For now, I commented out the code so I can render the document later.


```r
df <- dplyr::as_data_frame(x = c(1, 2, 3))
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

This worked but, as expected, it gave me a warning. It's telling me I should be using `as_tibble()` instead. I'm not sure exactly what that means, but at least I didn't get an error message!

As the homework said, putting the package name followed by two colons will make sure I get the function I want. So let me try this with another function.


```r
x <- c(5, 6, 2, 7, 9, 1)
dplyr::n_distinct(x)
```

```
## [1] 6
```

OK this worked, but I'm not totally sure what it's doing at this point.

I think earlier R was using the `igraph` version of `as_data_frame()` instead of the `dplyr` version of `as_data_frame()` because it was "masked." I guess R uses the last-loaded version of a function so I have to be careful in which order I load packages! Or if I really want to be sure which version of a function I'm using, I'd better prefix it with the package name and two colons.

# Question 3

When I type `?n_distinct()` it brings up the help file for that function. Apparently it counts the number of unique values in a vector.

# Question 4


```r
glimpse(baseballData)
```

```
## Rows: 12,145
## Columns: 5
## $ Date         <int> 20100405, 20100405, 20100405, 20100405, 20100405, 2010040…
## $ Home         <fct> ANA, CHA, KCA, OAK, TEX, ARI, ATL, CIN, HOU, MIL, NYN, PI…
## $ Visitor      <fct> MIN, CLE, DET, SEA, TOR, SDN, CHN, SLN, SFN, COL, FLO, LA…
## $ HomeScore    <int> 6, 6, 4, 3, 5, 6, 16, 6, 2, 3, 7, 11, 1, 3, 4, 2, 4, 3, 0…
## $ VisitorScore <int> 3, 0, 8, 5, 4, 3, 5, 11, 5, 5, 1, 5, 11, 5, 6, 1, 3, 6, 3…
```

This dataset has 12,145 rows and 5 columns. The `Home` column is a "factor" type variable and `HomeScore` is an integer variable.

# Question 5


```r
baseballData[1,]
```

```
##       Date Home Visitor HomeScore VisitorScore
## 1 20100405  ANA     MIN         6            3
```

This is the first row of the `baseballData` dataset. It looks like it has information about a single game of baseball.


```r
baseballData[,2:3] |> head()
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

This function shows me two columns of the baseball data. The first is the acronym for the home team, the second is the acronym of the away team.

# Question 6

As requested, I'm going to pretend to make a hockey dataset. I will cut and paste the "data" from the assignment first:


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

year_started <- c(1979, 1946, 1990, 1986, 1971, 1963, 1979,
                  2005, 1979, 1983)
```

It looks like that actually worked. I have `goals`, `name`, and `year_started` in my environment now.

Now I will put these together in a tibble.


```r
hockey_data <- tibble(
  name = name,
  goals = goals,
  year_started = year_started
)

glimpse(hockey_data)
```

```
## Rows: 10
## Columns: 3
## $ name         <chr> "Wayne Gretzky", "Gordie Howe", "Jaromir Jagr", "Brett Hu…
## $ goals        <dbl> 894, 801, 766, 741, 731, 717, 708, 700, 694, 692
## $ year_started <dbl> 1979, 1946, 1990, 1986, 1971, 1963, 1979, 2005, 1979, 1983
```

Looks like it worked!
