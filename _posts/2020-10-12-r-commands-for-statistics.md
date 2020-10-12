---
layout: post
title: "筆記 | R Commands for Statistics"
author: "Andrea Shih"
categories: journal
tags: [notes]
image: stat.jpg
---

這學期修統計學，寫作業時花了不少時間查找如何在 R 上做計算，因此把筆記寫在這裡，方便以後使用。

以下虛構資料紀錄十位學生期末考前一晚的睡眠小時數和期末考分數：

| id | time | grades |
|----|------|--------|
| 1  | 7    | 80     |
| 2  | 8    | 75     |
| 3  | 8.5  | 45     |
| 4  | 4    | 50     |
| 5  | 3    | 60     |
| 6  | 3.5  | 70     |
| 7  | 10   | 65     |
| 8  | 2    | 55     |
| 9  | 9.5  | 25     |
| 10 | 7.5  | 85     |


&nbsp;

### 1. Load data
```r
setwd("C:/Users/user/Desktop") # set working directory

library(readr)
sleep_grades <- read_csv("C:/Users/user/Desktop/sleep_grades.csv")

time <- sleep_grades$time
grades <- sleep_grades$grades 
```
若資料為 `list`，可先轉換成一個 `numeric vector`。以下為範例：
```r
your_data <-  list(1, 2, 3, 4, 5)
your_data_new <- as.numeric(unlist(your_data))
your_data_new

## [1] 1 2 3 4 5
```
範例資料不需轉換即可使用，接下來將以睡眠時間 `time` 作為例子進行計算。

&nbsp;

### 2. `Mean`, `Median`, and `Mode`

平均數及中位數可以使用下列 commands 來計算：
```r
mean(time) 

## [1] 6.3

median(time) 

## [1] 7.25
```
眾數無法用 `mode(time)` 取得，
```r
mode(time)

## [1] "numeric"
```
需先定義函數 `getmode`，才能取得。
```r
getmode <- function(v) {
    uniqv <- unique(v)
    uniqv[which.max(tabulate(match(v, uniqv)))]
}

getmode(time) 

## [1] 7
```
&nbsp;

### 3. `Geometric Mean`

欲計算幾何平均數，需先定義函數 `geo_mean`：
```r
geo_mean <- function(data) {
    log_data <- log(data)
    gm <- exp(mean(log_data[is.finite(log_data)]))
    return(gm)
}

geo_mean(time)

## [1] 5.565025
```
&nbsp;

### 4. `Variance`, `Standard Deviation`, and `Coefficient of Variation`

變異數及標準差可以使用下列 commands 得知：
```r
var(time)

## [1] 8.455556

sd(time) 

## [1] 2.907844
```
變異係數可由下列算式得知：
```r
sd(time) / mean(time) * 100

## [1] 46.15625
```
&nbsp;

### 5. `Quartiles` and `Interquartile Range`

四分位數可使用以下 commands 取得：
```r
quantile(time)

##     0%    25%    50%    75%   100% 
##  2.000  3.625  7.250  8.375 10.000
```
四分位距的計算方式：
```r
IQR(time)

## [1] 4.75
```
或是：
```r
quantile(time, 3/4) - quantile(time, 1/4)

##  75% 
## 4.75
```
&nbsp;

接下來計算睡眠時間 `time` 和成績 `grades` 的關係。

&nbsp;

### 6. `Covariance` and `Coefficient of Correlation`

共變異數和相關係數的計算方式如下：
```r
cov(time, grades)

## [1] -4.5

cor(time, grades)

## [1] -0.08562272
```
&nbsp;

### 7. `Linear Model`

可以透過最小平方法，得出一條回歸線。
```r
fit <- lm(grades ~ time)
fit

## 
## Call:
## lm(formula = grades ~ time)
## 
## Coefficients:
## (Intercept)         time  
##     64.3528      -0.5322
```
所以這條直線就是：

> *grades* = 64.3528 + (-0.5322) \* *time*

&nbsp;

### 8. `Coefficient of Determination` (`R^2`)

承上述的線性回歸函數，R 平方可以用以下 commands 取得：
```r
summary(fit)$r.squared

## [1] 0.007331251
```

&nbsp;

### 9. References
[How to coerce a list object to type 'double'](https://stackoverflow.com/questions/12384071/how-to-coerce-a-list-object-to-type-double)

[R - Mean, Median and Mode](https://www.tutorialspoint.com/r/r_mean_median_mode.htm)

[Linear Regression](http://r-statistics.co/Linear-Regression.html)

[Geometric Mean: is there a built-in?](https://stackoverflow.com/questions/2602583/geometric-mean-is-there-a-built-in)

&nbsp;

<span>Photo by <a href="https://unsplash.com/@isaacmsmith?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Isaac Smith</a> on <a href="https://unsplash.com/s/photos/data?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>
