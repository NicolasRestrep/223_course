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

## Malaria 

If you are interested in public health, this could be of interest. In the folder, you will find some datasets compiled from the `malariaAtlas` package. There are three datasets here. The first contais the incidence of Malaria for each country each year. 


```r
df <- read_csv("malaria_incidence.csv")
glimpse(df)
```

```
## Rows: 508
## Columns: 4
## $ Entity                                                                               <chr> …
## $ Code                                                                                 <chr> …
## $ Year                                                                                 <dbl> …
## $ `Incidence of malaria (per 1,000 population at risk) (per 1,000 population at risk)` <dbl> …
```
The second dataset contains the deaths of malaria standardized across all ages for a given country-year. 


```r
df <- read_csv("malaria_deaths_standard.csv")
glimpse(df)
```

```
## Rows: 6,156
## Columns: 4
## $ Entity                                                                             <chr> …
## $ Code                                                                               <chr> …
## $ Year                                                                               <dbl> …
## $ `Deaths - Malaria - Sex: Both - Age: Age-standardized (Rate) (per 100,000 people)` <dbl> …
```
Finally, we have a dataset of malaria deaths but among specific age groups. 


```r
df <- read_csv("malaria_deaths_age_specific.csv")
glimpse(df)
```

```
## Rows: 30,780
## Columns: 6
## $ ...1      <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 1…
## $ entity    <chr> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", …
## $ code      <chr> "AFG", "AFG", "AFG", "AFG", "AFG", "AFG", "AFG", "AFG", "AFG…
## $ year      <dbl> 1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998, 1999, …
## $ age_group <chr> "Under 5", "Under 5", "Under 5", "Under 5", "Under 5", "Unde…
## $ deaths    <dbl> 184.6064, 191.6582, 197.1402, 207.3578, 226.2094, 236.3280, …
```

## NFL Stats (2000-2017)

If you are interested in Football, we have a a dataset of player stats in the NFL from 2000 to 2017. 


```r
df <- read_csv("nfl_stats.csv")
glimpse(df)
```

```
## Rows: 81,525
## Columns: 23
## $ ...1         <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17…
## $ name         <chr> "Duce Staley", "Lamar Smith", "Tiki Barber", "Stephen Dav…
## $ team         <chr> "PHI", "MIA", "NYG", "WAS", "IND", "BAL", "NYJ", "MIN", "…
## $ game_year    <dbl> 2000, 2000, 2000, 2000, 2000, 2000, 2000, 2000, 2000, 200…
## $ game_week    <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
## $ rush_att     <dbl> 26, 27, 13, 23, 28, 27, 30, 14, 15, 10, 20, 13, 23, 14, 2…
## $ rush_yds     <dbl> 201, 145, 144, 133, 124, 119, 110, 109, 88, 87, 84, 80, 7…
## $ rush_avg     <dbl> 7.7, 5.4, 11.1, 5.8, 4.4, 4.4, 3.7, 7.8, 5.9, 8.7, 4.2, 6…
## $ rush_tds     <dbl> 1, 1, 2, 1, 1, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 3, …
## $ rush_fumbles <dbl> 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 2, 0, 0, 0, 0, 2, 0, 1, 1, …
## $ rec          <dbl> 4, 1, 3, 4, 6, 4, 6, 2, 2, NA, 4, 3, 1, 4, 1, 1, 1, NA, N…
## $ rec_yds      <dbl> 61, 12, 25, 37, 40, 32, 34, 3, 20, NA, 29, 10, -2, 100, 1…
## $ rec_avg      <dbl> 15.3, 12.0, 8.3, 9.3, 6.7, 8.0, 5.7, 1.5, 10.0, NA, 7.3, …
## $ rec_tds      <dbl> 0, 0, 0, 0, 1, 0, 1, 0, 0, NA, 0, 0, 0, 1, 0, 0, 0, NA, N…
## $ rec_fumbles  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, NA, 0, 0, 0, 0, 0, 0, 0, NA, N…
## $ pass_att     <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, 41, NA, NA, NA, NA, N…
## $ pass_yds     <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, 290, NA, NA, NA, NA, …
## $ pass_tds     <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, 2, NA, NA, NA, NA, NA…
## $ int          <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, 0, NA, NA, NA, NA, NA…
## $ sck          <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, 2, NA, NA, NA, NA, NA…
## $ pass_fumbles <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, 0, NA, NA, NA, NA, NA…
## $ rate         <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, 102.7, NA, NA, NA, NA…
## $ position     <chr> "RB", "RB", "RB", "RB", "RB", "RB", "RB", "RB", "RB", "QB…
```

Maybe you are interested in how the salaries for different positions have evolved across the years. We have you covered. 


```r
df <- read_csv("nfl_salaries.csv")
glimpse(df)
```

```
## Rows: 800
## Columns: 11
## $ year                <dbl> 2011, 2011, 2011, 2011, 2011, 2011, 2011, 2011, 20…
## $ Cornerback          <dbl> 11265916, 11000000, 10000000, 10000000, 10000000, …
## $ `Defensive Lineman` <dbl> 17818000, 16200000, 12476000, 11904706, 11762782, …
## $ Linebacker          <dbl> 16420000, 15623000, 11825000, 10083333, 10020000, …
## $ `Offensive Lineman` <dbl> 15960000, 12800000, 11767500, 10358200, 10000000, …
## $ Quarterback         <dbl> 17228125, 16000000, 14400000, 14100000, 13510000, …
## $ `Running Back`      <dbl> 12955000, 10873833, 9479000, 7700000, 7500000, 703…
## $ Safety              <dbl> 8871428, 8787500, 8282500, 8000000, 7804333, 76527…
## $ `Special Teamer`    <dbl> 4300000, 3725000, 3556176, 3500000, 3250000, 32250…
## $ `Tight End`         <dbl> 8734375, 8591000, 8290000, 7723333, 6974666, 61333…
## $ `Wide Receiver`     <dbl> 16250000, 14175000, 11424000, 11415000, 10800000, …
```

## California Fires 

Maybe you are interested in climate change. Then, the number of California fires across years, and the damaged they have caused, might be of interest. 


```r
df <- read_csv("fires.csv")
glimpse(df)
```

```
## Rows: 83
## Columns: 4
## $ YEAR              <dbl> 1933, 1934, 1935, 1936, 1937, 1938, 1939, 1940, 1941…
## $ `NUMBER OF FIRES` <dbl> 1994, 2338, 1447, 3805, 2907, 4150, 2491, 4497, 5460…
## $ `ACRES BURNED`    <dbl> 129210, 363052, 127262, 756696, 71312, 221061, 51362…
## $ `DOLLAR DAMAGE`   <dbl> 318636, 563710, 165543, 1877147, 151584, 404225, 847…
```

## TV & Movie Ratings 

We also have a dataset that contains TV & movie ratings taken from IMDB. The dataset covers titles released between 2000 and 2019. 


```r
df <- read_csv("tv_ratings.csv")
glimpse(df)
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

## Incarceration Trends

Here's a data about the people incarcerated at the county level from 1970 to 2015. This is a big dataset so it might take a while to load. 


```r
df <- read_csv("incarceration_trends.csv")
glimpse(df)
```

```
## Rows: 1,327,797
## Columns: 9
## $ year              <dbl> 1970, 1971, 1972, 1973, 1974, 1975, 1976, 1977, 1978…
## $ state             <chr> "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL"…
## $ county_name       <chr> "Autauga County", "Autauga County", "Autauga County"…
## $ urbanicity        <chr> "small/mid", "small/mid", "small/mid", "small/mid", …
## $ region            <chr> "South", "South", "South", "South", "South", "South"…
## $ division          <chr> "East South Central", "East South Central", "East So…
## $ pop_category      <chr> "Total", "Total", "Total", "Total", "Total", "Total"…
## $ population        <dbl> 14154, 14765, 15939, 16906, 17578, 18007, 18476, 190…
## $ prison_population <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
```

