---
title: "Homework 1"
author: "Lara Friedlund"
date: "1/25/2019"
output: 
  html_document: 
    keep_md: yes
---

```r
5-3*2
```

```
## [1] -1
```


```r
8/2**2
```

```
## [1] 2
```


```r
(5-3)*2
```

```
## [1] 4
```


```r
(8/2)**2
```

```
## [1] 16
```


```r
blackjack<-c(140,-20,70,-120,240)
roulette<-c(60,50,120,-300,10)
```

```r
days<-c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")
```

```r
names(blackjack)<-days
names(roulette)<-days
```

```r
total_blackjack<-sum(blackjack)
total_blackjack
```

```
## [1] 310
```


```r
total_roulette<-sum(roulette)
total_roulette
```

```
## [1] -60
```


```r
total_week<-c(blackjack,roulette)
total_week
```

```
##    Monday   Tuesday Wednesday  Thursday    Friday    Monday   Tuesday 
##       140       -20        70      -120       240        60        50 
## Wednesday  Thursday    Friday 
##       120      -300        10
```

```r
total_week_matrix<-matrix(total_week, nrow = 2, byrow = T)
colnames(total_week_matrix)<-days
total_week_matrix
```

```
##      Monday Tuesday Wednesday Thursday Friday
## [1,]    140     -20        70     -120    240
## [2,]     60      50       120     -300     10
```


```r
total_week_by_day<-colSums(total_week_matrix)
total_week_by_day
```

```
##    Monday   Tuesday Wednesday  Thursday    Friday 
##       200        30       190      -420       250
```

```r
##Monday and Friday seem lucky!
##Thursdays are not quite as lucky
```


```r
mean(blackjack)
```

```
## [1] 62
```

```r
mean(roulette)
```

```
## [1] -12
```

```r
##On average, you will earn more from blackjack and lose on roulette. Therefore, stick to blackjack.
```

