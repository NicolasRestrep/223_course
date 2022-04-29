---
title: "Data Documentation"
author: "Nicolas Restrepo"
output: 
  html_document:
    keep_md: true
---



Here, I will keep track of some cool datasets to use in the course. 

## UN Votes 

This is a dataset that provides information about how countries have voted in the UN National Assembly. The data comes neatly bundled in a package that you can get by running `install.packages("unvotes")`.

The package contains three datasets: 

1) `un_votes` contains all the decisions for each resolution and each country. 


```r
library(unvotes)
library(tidyverse)

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


