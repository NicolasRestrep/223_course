---
title: "Data Documentation"
author: "Nicolas Restrepo"
output: 
  html_document: 
    toc: true
    theme: united
    keep_md: true
---



Here, I will keep track of some cool datasets to use in the course. 

## UN Votes 

This is a dataset that provides information about how countries have voted in the UN National Assembly. The data comes neatly bundled in a package that you can get by running `install.packages("unvotes")`.

The package contains three datasets: 

1) `un_votes` contains all the decisions for each resolution and each country. 


```r
# Load the packages
library(unvotes)
library(tidyverse)

# Eagle eye view of the data
glimpse(un_votes)
```

```
## Rows: 869,937
## Columns: 4
## $ rcid         <dbl> 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, …
## $ country      <chr> "United States", "Canada", "Cuba", "Haiti", "Dominican Re…
## $ country_code <chr> "US", "CA", "CU", "HT", "DO", "MX", "GT", "HN", "SV", "NI…
## $ vote         <fct> yes, no, yes, yes, yes, yes, yes, yes, yes, yes, yes, yes…
```

2) `un_roll_calls` includes information about each roll call: what the vote was about, when it happened, and what was being discussed: 


```r
glimpse(un_roll_calls)
```

```
## Rows: 6,202
## Columns: 9
## $ rcid          <int> 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18,…
## $ session       <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
## $ importantvote <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
## $ date          <date> 1946-01-01, 1946-01-02, 1946-01-04, 1946-01-04, 1946-01…
## $ unres         <chr> "R/1/66", "R/1/79", "R/1/98", "R/1/107", "R/1/295", "R/1…
## $ amend         <int> 1, 0, 0, 0, 1, 1, 0, 1, 0, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1,…
## $ para          <int> 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0,…
## $ short         <chr> "AMENDMENTS, RULES OF PROCEDURE", "SECURITY COUNCIL ELEC…
## $ descr         <chr> "TO ADOPT A CUBAN AMENDMENT TO THE UK PROPOSAL REFERRING…
```
3) `un_roll_call_issues` relates each vote to broader themes. 


```r
# View data 
glimpse(un_roll_call_issues)
```

```
## Rows: 5,745
## Columns: 3
## $ rcid       <int> 77, 9001, 9002, 9003, 9004, 9005, 9006, 128, 129, 130, 131,…
## $ short_name <chr> "me", "me", "me", "me", "me", "me", "me", "me", "me", "me",…
## $ issue      <fct> Palestinian conflict, Palestinian conflict, Palestinian con…
```

```r
# How many votes per issue? 
un_roll_call_issues %>% 
  count(issue, sort = T)
```

```
## # A tibble: 6 × 2
##   issue                                    n
##   <fct>                                <int>
## 1 Arms control and disarmament          1092
## 2 Palestinian conflict                  1061
## 3 Human rights                          1015
## 4 Colonialism                            957
## 5 Nuclear weapons and nuclear material   855
## 6 Economic development                   765
```

## Causact 

The `causact` package is designed to help with the construction and use of causal models. However, it also contains some interesting datasets. Let's highlight a couple. 

As usual, you can get this package by running `install.packages("causact")`

### Baseball

`baseballData` contains the final scores of 12,145 baseball games played in 2010. 


```r
library(causact)
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
### Corruption 

If you are more into international relations and development, `corruptDF` contains information about the human development index and the corruption perception index for different countries. 


```r
glimpse(corruptDF)
```

```
## Rows: 174
## Columns: 7
## $ country     <chr> "Afghanistan", "Albania", "Algeria", "Angola", "Argentina"…
## $ region      <chr> "Asia Pacific", "East EU Cemt Asia", "MENA", "SSA", "Ameri…
## $ countryCode <chr> "AFG", "ALB", "DZA", "AGO", "ARG", "ARM", "AUS", "AUT", "A…
## $ regionCode  <chr> "AP", "ECA", "MENA", "SSA", "AME", "ECA", "AP", "WE/EU", "…
## $ population  <int> 35530081, 2873457, 41318142, 29784193, 44271041, 2930450, …
## $ CPI2017     <int> 15, 38, 33, 19, 39, 35, 77, 75, 31, 65, 36, 28, 68, 44, 75…
## $ HDI2017     <dbl> 0.498, 0.785, 0.754, 0.581, 0.825, 0.755, 0.939, 0.908, 0.…
```

### NTC Tickets

`ticketsDF` contains observations of the number of tickets written by NYC precincts each day between 2014 and 2015.


```r
glimpse(ticketsDF)
```

```
## Rows: 55,167
## Columns: 4
## $ precinct      <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
## $ date          <date> 2014-01-01, 2014-01-02, 2014-01-03, 2014-01-04, 2014-01…
## $ month_year    <chr> "01-2014", "01-2014", "01-2014", "01-2014", "01-2014", "…
## $ daily_tickets <int> 17, 67, 17, 42, 54, 109, 115, 119, 154, 95, 38, 37, 91, …
```

