---
title: Some interesting R packages - Broom
author: FAN Min
date: '2020-12-28'
slug: []
categories:
  - R
tags: []
comment: yes
description: ''
reward: yes
toc: yes
---

A package for extracting information from build-in statistical testing and models.
<!--more-->

## Summary
Some build-in functions for statistical analysis is not user-friendly. In other words, the users like me are so lazy. For example, it is hard for extracting values from regression model. I used to write a function to extract. Now I found a well-designed package **broom** designing for model extraction.

## Regression

When conducting a regression model in R, the output is unstructural and hard to export.

```r
lm_model <- lm(data=iris,Sepal.Length~Sepal.Width)
summary(lm_model)
```

```
## 
## Call:
## lm(formula = Sepal.Length ~ Sepal.Width, data = iris)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -1.5561 -0.6333 -0.1120  0.5579  2.2226 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   6.5262     0.4789   13.63   <2e-16 ***
## Sepal.Width  -0.2234     0.1551   -1.44    0.152    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.8251 on 148 degrees of freedom
## Multiple R-squared:  0.01382,	Adjusted R-squared:  0.007159 
## F-statistic: 2.074 on 1 and 148 DF,  p-value: 0.1519
```

Now, the following package **broom** can help to generate a data frame for exporting.


```r
library('broom')
tidy(lm_model)
```

```
## # A tibble: 2 x 5
##   term        estimate std.error statistic  p.value
##   <chr>          <dbl>     <dbl>     <dbl>    <dbl>
## 1 (Intercept)    6.53      0.479     13.6  6.47e-28
## 2 Sepal.Width   -0.223     0.155     -1.44 1.52e- 1
```

As above, the result was transformed into data.frame format.

The other details can be exported by **augment()**


```r
head(augment(lm_model))
```

```
## # A tibble: 6 x 8
##   Sepal.Length Sepal.Width .fitted .resid .std.resid    .hat .sigma .cooksd
##          <dbl>       <dbl>   <dbl>  <dbl>      <dbl>   <dbl>  <dbl>   <dbl>
## 1          5.1         3.5    5.74 -0.644     -0.786 0.0136   0.826 0.00426
## 2          4.9         3      5.86 -0.956     -1.16  0.00678  0.824 0.00462
## 3          4.7         3.2    5.81 -1.11      -1.35  0.00739  0.823 0.00680
## 4          4.6         3.1    5.83 -1.23      -1.50  0.00673  0.822 0.00763
## 5          5           3.6    5.72 -0.722     -0.883 0.0171   0.826 0.00677
## 6          5.4         3.9    5.66 -0.255     -0.314 0.0318   0.828 0.00162
```


## Hypothesis testing

```r
db <- data.frame(value = 1: 100, group= rep(c("a","b"),50))
ttest_db <-t.test(db$value~db$group)
tidy(ttest_db)
```

```
## # A tibble: 1 x 10
##   estimate estimate1 estimate2 statistic p.value parameter conf.low conf.high
##      <dbl>     <dbl>     <dbl>     <dbl>   <dbl>     <dbl>    <dbl>     <dbl>
## 1       -1        50        51    -0.171   0.864       98.    -12.6      10.6
## # … with 2 more variables: method <chr>, alternative <chr>
```
