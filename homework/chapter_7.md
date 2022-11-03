---
title: "Chapter 7"
author: "Nicolas Restrepo"
output: 
  html_document: 
    toc: true
    theme: united
    keep_md: true
---



Here, we are going to practice and reinforce some of the ideas that we encountered in chapter 5. Sampling is crucial for understanding any type of data analysis. When you are presented with brand new set of data, it is always useful to think: what groups or populations am I capturing in these data? To what groups or populations can I extrapolate insights I draw from these data? Do I have enough data? To answer these questions, it is essential to grasp sampling; to think about how features of a population might (or might not) make their way to our spreadsheets. 

Say we are interested in finding out the proportion of science Nobel prizes that have been awarded to people born in the US. We could easily Google this, the information is available. But imagine that for some reason we are only able to access portions of the data - i.e. samples. How would we go about finding this proportion and how confident would we be in our findings. 

Let's begin by loading in a data frame containing all Nobel prize winners. 


```r
library(tidyverse)
library(here)
library(moderndive)
theme_set(theme_minimal())

nobel_winners <- read_csv(here("Data", "nobel_winners.csv"))
```

We've talked about it in class once before, but `here::here()` is a function that allows you to find any file inside any subfolder inside your project. So I'm telling R to find a `Data` folder and then grab the `nobel_winners.csv` file inside. **here** is a very handy package when you're dealing with complicated projects with many subfolders.

Given that we are only interested in scientific Nobel prizes, let's get rid of the Nobel Peace prize. We will also create a column that indicates whether the recipient was born in the US. 


```r
nobel_winners_flt <- nobel_winners %>% 
  filter(category != "Peace") %>% 
  mutate(is_us = if_else(birth_country == "United States of America", 1, 0))
```

Now, what is the *true* proportion of US-born Nobel prize winners?


```r
true_prop <- nobel_winners_flt %>% 
  group_by(is_us) %>% 
  summarise(prop = n()/nrow(nobel_winners_flt))

ggplot() + 
  coord_cartesian(xlim = c(0,1), ylim = c(0,1)) + 
  geom_vline(xintercept = true_prop[2,2][[1]], linetype = "dashed")  + 
  labs(x = "Proportion")
```

![](chapter_7_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

Now, let's say our friend gives us a random sample of 25 Nobel winners and we calculate our proportion. How far off would we be? 


```r
set.seed(33)
# Random sample 
our_sample <- sample_n(nobel_winners_flt, 
                       size = 25, 
                       replace = F)

sample_prop <- our_sample %>% 
  group_by(is_us) %>% 
  summarise(prop = n()/nrow(our_sample))

# How does our proportion look like? 
ggplot() + 
  coord_cartesian(xlim = c(0,1), ylim = c(0,1)) + 
  geom_vline(xintercept = true_prop[2,2][[1]], linetype = "dashed")  + 
  geom_vline(xintercept = sample_prop[2,2][[1]], linetype = "dotted", col = "red") +
  labs(x = "Proportion")
```

![](chapter_7_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

We are way above, almost at 50%! 

## Question 1 

Let's explore some of the vocabulary provided in the chapter. 
- In this scenario, what is the population? 
- What is the sampling frame? 
- What does the black line represent? (hint: the word population is in the name). 
- What does the red line represent? 

## Question 2 

Okay, you probably know what we are doing next. We are going to take repeated samples of differing sizes and explore what the results look like, much like we did in the chapter. This will reinforce the ideas of sampling variability and sample size, which are key. 

We will use the `rep_sample_n()` function from the **moderndive** package. (This is actually a copy of a function from the **infer** package, so it's the sort of function you could continue to use in the future.)

Using this function, take 50 samples of 25 winners each. Plot your results. Be sure to add the mean proportion of your samples and the true proportion we calculated above. HINT: `summarize()` is going to be useful here. 

## Question 3 

Now, use this function to take 50 samples of 100 winners each. Plot your results in the same way that you did above. 

Which one of the two distributions varies more. Can you explain why? 

## Question 4 

Calculate the standard deviation of your samples collected using a size of 25 and a size of 100. Do these results support your argument above? What does this imply about sample size? What happens to the variability in our estimates as the sample size increases 

## Question 5 

Now, repeat the same steps above to find the proportion of women who have been awarded the Nobel prize. Draw samples of 100 scientists at a time and plot your distribution of proportions.

## Question 6 

The last question is a bit different. Please watch [this video](https://www.youtube.com/watch?v=jvoxEYmQHNM) referenced in the ModernDive book, then explain the **Central Limit Theorem** it in your own words. Be as concise as you can (i.e., use no more than 3-4 sentences) but convince me you really understand the basic idea.
