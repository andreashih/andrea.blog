---
layout: post
title: "練習 | 用 `rtweet` 和 `quanteda` 整理 twitter 上的武漢肺炎日文資料"
author: "Andrea Shih"
categories: journal
tags: [practice]
image: pill.jpg
---


在看 [quanteda tutorials](https://tutorials.quanteda.io/language-specific/japanese/) 的時候發現了 `quanteda` 內建的日文斷詞功能，因此想用 `rtweet` 爬爬看 twitter 上有關 "コロナウイルス" 的資料，再用 `quanteda` 處理。

&nbsp;

### 1. 使用 `rtweet` 前先[處理 rate limit](https://github.com/ropensci/rtweet/issues/266)

```r
library(rtweet)
get_timeline_unlimited <- function(users, n){
  
  if (length(users) ==0){
    return(NULL)
  }
  
  rl <- rate_limit(query = "get_timeline")
  
  if (length(users) <= rl$remaining){
    print(glue("Getting data for {length(users)} users"))
    tweets <- get_timeline(users, n, check = FALSE)  
  }else{
    
    if (rl$remaining > 0){
      users_first <- users[1:rl$remaining]
      users_rest <- users[-(1:rl$remaining)]
      print(glue("Getting data for {length(users_first)} users"))
      tweets_first <- get_timeline(users_first, n, check = FALSE)
      rl <- rate_limit(query = "get_timeline")
    }else{
      tweets_first <- NULL
      users_rest <- users
    }
    wait <- rl$reset + 0.1
    print(glue("Waiting for {round(wait,2)} minutes"))
    Sys.sleep(wait * 60)
    
    tweets_rest <- get_timeline_unlimited(users_rest, n)  
    tweets <- bind_rows(tweets_first, tweets_rest)
  }
  return(tweets)
}
```

### 2. 先試爬 1000 筆有 "コロナウイルス" hashtag 的推文

```r
rt <- search_tweets("#コロナウイルス", n = 1000, 
                      include_rts = FALSE, encoding = "UTF-8")
```

### 3. `quanteda` 中的日文斷詞功能

```r
library(quanteda)
toks_virus <- tokens(rt$text)
```
#### 看一下大概長什麼樣子

```r
head(toks_virus[[20]], 100)
```

### 4. KWIC

```r
kwic(toks_virus, "コロナ", window = 5, valuetype = "regex") %>%
  knitr::kable(align = "c")
```

***-to be continued***
