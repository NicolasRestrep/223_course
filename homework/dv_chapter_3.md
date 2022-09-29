# Chapters 1-3 - Data Visualization


Here, we are going to go over some key ideas from chapters 1 through 3 from Healy's Data Visualization. 

## Question 1 

Let's do a quick exercise. We are going to examine the relationship between two variables: exercise and BMI. Exercise is measured in minutes and BMI is centered so that the average is 0 and the units represent standard deviations around 0. Let's read in the data. 


```r
library(tidyverse)
# Read in the data 
exercise_data <- read_csv("../Data/visualize_data.csv")
glimpse(exercise_data)
```

```
## Rows: 142
## Columns: 4
## $ ...1     <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18…
## $ ...2     <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18…
## $ Exercise <dbl> 55.3846, 51.5385, 46.1538, 42.8205, 40.7692, 38.7179, 35.6410…
## $ BMI      <dbl> 1.8320590, 1.7892194, 1.7321050, 1.6178724, 1.5036362, 1.3751…
```
Before, we see examine anything from the data, write down what you expect the relationship would look like. Do you think people who record more exercise will have more or less BMI? 

Now, let's look at a simple correlation between these two variables. Recall that a correlation indicates how two variables move together. A negative correlation would imply that as one increases (say exercise), the other decreases (say BMI). A positive correlation in turn indicates that as one variable increases so does the other. Run the following code and tell me what the output indicates.  


```r
cor(exercise_data$Exercise, exercise_data$BMI)
```

Let's explore this relationship visually. Make a scatterplot with exercise in the x axis and BMI in the y axis. 

What do you see? 

Yes, I tricked you. This is an example that comes from [Alberto Cairo](https://twitter.com/AlbertoCairo). It reinforces how important it is to look at your data.

Looking at presumed relationships without visualizing your data is a dangerous task, as this [experiment](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-020-02133-w#article-info) neatly shows. Always look at your data; you don't want any Gorillas or Dinosaurs in your analyses. 

## Question 2 

Many of the ideas in these chapters were already familiar to you but this is an opportunity to go deeper and really understand how the machinery of ggplot works. We are going to be working with a dataset from the `causact` package that contains information about the Human Development Index (HDI) and Corruption Index (CPI) for different countries in 2017. Begin by installing the package running `install.packages("causact")`. Load the package and glimpse the dataset: 


```r
library(causact)
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

Before we move forward, we want to know what these variables capture. Run `?corruptDF` and tell me in your own words what `CPI2017` and `HDI2017` capture.

## Question 3 

Here, we are interested in the relationship between the HDI and CPI. 

Begin by making a scatter plot that shows the relationship between these two variables. Describe the relationship that you see. 

## Question 4 

Add a layer that captures the overall relationship between these two variables using `geom_smooth()`. Use both the `lm` and `gam` methods. What are the differences? Which one do you prefer? 

## Question 5 

It would be interesting to explore if this relationship varies by region. Add a fill and color aesthetic to the graph so that the lines and points are grouped by the variable `region`. 

What do you see? Are patterns clear or is the graph too cluttered? What would be another way to get these trends by region but in a way to would be more legible? 

> Hint: think facets

## Question 6 

Using one of the options that Healy gives you in the `where to go next` section of chapter 3, reverse the scale of the x-axis. 

## Question 7 

Add a title and a subtitle to the plot. Also add a caption, where you let me know where the data comes from. 

## Question 8 

Now, that your plot about the relationship between the Human Development Index and the Corruption Perception Index is informative and sleek, you want to save it. Imagine it you want to print in a poster or send it to a supervisor. Show me code that would save the plot. 
