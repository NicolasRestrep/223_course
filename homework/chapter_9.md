# Chapter 9

Here, we will reinforce some ideas from Chapter 9. This one is very important, not only because the content itself is important, but because you will see these ideas used and abused everywhere to support all kinds of silly arguments. A thorough understanding of these ideas will be a great BS detector when you are confronted with other people's data analyses. 

We will be using soccer data from the English Premier League to examine whether home field advantage is a thing in this league. Do teams who play at home - with their own fans - win more on average? We will use your new hypothesis testing skills to examine this question. We will use data from all games of the legendary 2015/2016 season. Don't know why it's legendary? Look it up. It's worth it. Best sports story of all time some say.  

Let's begin by reading in the data and looking at it. 


```r
pl_data <- read_csv("../Data/premier_league.csv")

glimpse(pl_data)
```

```
## Rows: 380
## Columns: 4
## $ home_team  <chr> "Bournemouth", "Chelsea", "Everton", "Leicester", "Man Unit…
## $ away_team  <chr> "Aston Villa", "Swansea", "Watford", "Sunderland", "Tottenh…
## $ score_diff <dbl> -1, 0, 0, 2, 1, -2, -2, 0, -1, -3, -1, -3, -2, 2, 0, 0, -1,…
## $ result     <chr> "aw", "d", "d", "hw", "hw", "aw", "aw", "d", "aw", "aw", "a…
```

We have 4 columns then: the home team, the away team, the score difference (from the standpoint of the home team), and the result. We have three different types of results: an away win (aw), a home win (hw), and a draw (d). What we are interested in then is the proportion of home wins. What is the rate of winning at home and is it different that mere chance? 

## Question 1 

Use your data wrangling skills to calculate the proportion of home wins during the 2015/2016 season. 

## Question 2 

Now, we are going to shuffle. We are going to examine what proportion we would expect if a home win was equally likely as any other result. This one is a bit more interesting than the examples in the chapter because there are 3 choices instead of 2. Below, you will find some incomplete code that simulates our dataset, reshuffled, 1000 times. Here, however, we assume that an away-win, a draw, and a home-win have equal probability. Finish the code, run the script, and plot the resulting proportions as a histogram.


```r
set.seed(22)

___ <- c()

for (i in 1:___) {
  
  sampled_results <- sample(c("aw", ___, "d"), 
                            ___ = 380,
                            replace = TRUE, 
                            prob = c(1/3,1/3,1/3))
  prop <- sum(___=="ht")/380
  sampled_proportions[i] <- ___
  
}
```

Describe the histogram in a sentence or two. 

## Question 3 

In this scenario, what would be the null hypothesis and the alternative hypothesis? 

## Question 4 

What would be the null distribution in this example? 

## Question 5

Say that for the significance level, we choose an alpha ($\alpha$) of 0.01. What does this mean? Is this a stringent or a rather loose test? 

> Important: 0.01 is an arbitrary number, just like 0.05 is an arbitrary number. It is important not to passively accept arbitrary conventions. For the analyses below, I want you to pick an $\alpha$ that doesn't end in 0, 1, or 5. Just to mix things up. 

## Question 6 

What would a p-value mean in this example? 

## Question 7

Using `sampled_proportions`, calculate the confidence interval that - if it were not to include the real proportion observed in question 1 - would let you reject the null hypothesis at your selected significance level. 

Can you reject the null hypothesis at the significance level you chose in question 5? Is this a stringent or an easy test? 

## Question 8

Use `get_p_value()` to calculate the p-value for observing the proportion of home victories in our dataset or higher if the null distribution was true. Interpret the result. 

## Question 9

Briefly discuss the two types of errors we can make when testing hypotheses. Which one do you think is worse? Does it depend on the context? 

