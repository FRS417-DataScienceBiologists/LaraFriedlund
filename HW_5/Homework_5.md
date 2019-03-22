---
title: "Homework 5"
author: "Lara Friedlund"
date: "March 22, 2019"
output: 
  html_document: 
    fig_caption: yes
    keep_md: yes
---
---
title: "HW5"
author: "Lara Friedlund"
output: 
  html_document: 
    fig_caption: yes
    keep_md: yes
---
##Mammals Life History

#1 Load the data.

```r
library(tidyverse)
```

```
## -- Attaching packages -------------------------------------------------------------------------------------------------------- tidyverse 1.2.1 --
```

```
## v ggplot2 3.1.0     v purrr   0.2.5
## v tibble  1.4.2     v dplyr   0.7.8
## v tidyr   0.8.2     v stringr 1.3.1
## v readr   1.3.1     v forcats 0.3.0
```

```
## -- Conflicts ----------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```


```r
life_history <- readr::read_csv(file = "data/mammal_lifehistories_v2.csv")
```

```
## Parsed with column specification:
## cols(
##   order = col_character(),
##   family = col_character(),
##   Genus = col_character(),
##   species = col_character(),
##   mass = col_double(),
##   gestation = col_double(),
##   newborn = col_double(),
##   weaning = col_double(),
##   `wean mass` = col_double(),
##   AFR = col_double(),
##   `max. life` = col_double(),
##   `litter size` = col_double(),
##   `litters/year` = col_double()
## )
```


#2 Use your preferred function to have a look. Do you notice any problems?

```r
library(skimr)
```

```
## Warning: package 'skimr' was built under R version 3.5.3
```

```
## 
## Attaching package: 'skimr'
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```


```r
life_history %>%
  skimr::skim()
```

```
## Skim summary statistics
##  n obs: 1440 
##  n variables: 13 
## 
## -- Variable type:character ----------------------------------------------------------------------------------------------------------------------
##  variable missing complete    n min max empty n_unique
##    family       0     1440 1440   6  15     0       96
##     Genus       0     1440 1440   3  16     0      618
##     order       0     1440 1440   7  14     0       17
##   species       0     1440 1440   3  17     0     1191
## 
## -- Variable type:numeric ------------------------------------------------------------------------------------------------------------------------
##      variable missing complete    n      mean         sd   p0  p25     p50
##           AFR       0     1440 1440   -408.12     504.97 -999 -999    2.5 
##     gestation       0     1440 1440   -287.25     455.36 -999 -999    1.05
##   litter size       0     1440 1440    -55.63     234.88 -999    1    2.27
##  litters/year       0     1440 1440   -477.14     500.03 -999 -999    0.38
##          mass       0     1440 1440 383576.72 5055162.92 -999   50  403.02
##     max. life       0     1440 1440   -490.26     615.3  -999 -999 -999   
##       newborn       0     1440 1440   6703.15   90912.52 -999 -999    2.65
##     wean mass       0     1440 1440  16048.93   5e+05    -999 -999 -999   
##       weaning       0     1440 1440   -427.17     496.71 -999 -999    0.73
##      p75          p100     hist
##    15.61     210       <U+2586><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587><U+2581>
##     4.5       21.46    <U+2583><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
##     3.83      14.18    <U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
##     1.15       7.5     <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
##  7009.17       1.5e+08 <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
##   147.25    1368       <U+2587><U+2581><U+2581><U+2583><U+2582><U+2581><U+2581><U+2581>
##    98    2250000       <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
##    10          1.9e+07 <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
##     2         48       <U+2586><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
```


#3 There are NA's. How are you going to deal with them?

```r
life_history <- life_history %>% 
  na_if("-999")
```


```r
life_history
```

```
## # A tibble: 1,440 x 13
##    order family Genus species   mass gestation newborn weaning `wean mass`
##    <chr> <chr>  <chr> <chr>    <dbl>     <dbl>   <dbl>   <dbl>       <dbl>
##  1 Arti~ Antil~ Anti~ americ~ 4.54e4      8.13   3246.    3           8900
##  2 Arti~ Bovid~ Addax nasoma~ 1.82e5      9.39   5480     6.5           NA
##  3 Arti~ Bovid~ Aepy~ melamp~ 4.15e4      6.35   5093     5.63       15900
##  4 Arti~ Bovid~ Alce~ busela~ 1.50e5      7.9   10167.    6.5           NA
##  5 Arti~ Bovid~ Ammo~ clarkei 2.85e4      6.8      NA    NA             NA
##  6 Arti~ Bovid~ Ammo~ lervia  5.55e4      5.08   3810     4             NA
##  7 Arti~ Bovid~ Anti~ marsup~ 3.00e4      5.72   3910     4.04          NA
##  8 Arti~ Bovid~ Anti~ cervic~ 3.75e4      5.5    3846     2.13          NA
##  9 Arti~ Bovid~ Bison bison   4.98e5      8.93  20000    10.7       157500
## 10 Arti~ Bovid~ Bison bonasus 5.00e5      9.14  23000.    6.6           NA
## # ... with 1,430 more rows, and 4 more variables: AFR <dbl>, `max.
## #   life` <dbl>, `litter size` <dbl>, `litters/year` <dbl>
```


#4 Where are the NA's? 

```r
life_history %>%
  purrr::map_df(~ sum(is.na(.)))%>% 
  tidyr::gather(variables, num_nas) %>% 
  arrange(desc(num_nas))
```

```
## # A tibble: 13 x 2
##    variables    num_nas
##    <chr>          <int>
##  1 wean mass       1039
##  2 max. life        841
##  3 litters/year     689
##  4 weaning          619
##  5 AFR              607
##  6 newborn          595
##  7 gestation        418
##  8 mass              85
##  9 litter size       84
## 10 order              0
## 11 family             0
## 12 Genus              0
## 13 species            0
```


#5 Some of the variable names will be problematic. Let's rename them here as a final tidy step.

```r
life_history <- life_history %>%
  dplyr::rename(genus = "Genus", wean_mass = "wean mass", max_life = "max. life", litter_size = "litter size", litters_yr = "litters/year")
```


```r
life_history
```

```
## # A tibble: 1,440 x 13
##    order family genus species   mass gestation newborn weaning wean_mass
##    <chr> <chr>  <chr> <chr>    <dbl>     <dbl>   <dbl>   <dbl>     <dbl>
##  1 Arti~ Antil~ Anti~ americ~ 4.54e4      8.13   3246.    3         8900
##  2 Arti~ Bovid~ Addax nasoma~ 1.82e5      9.39   5480     6.5         NA
##  3 Arti~ Bovid~ Aepy~ melamp~ 4.15e4      6.35   5093     5.63     15900
##  4 Arti~ Bovid~ Alce~ busela~ 1.50e5      7.9   10167.    6.5         NA
##  5 Arti~ Bovid~ Ammo~ clarkei 2.85e4      6.8      NA    NA           NA
##  6 Arti~ Bovid~ Ammo~ lervia  5.55e4      5.08   3810     4           NA
##  7 Arti~ Bovid~ Anti~ marsup~ 3.00e4      5.72   3910     4.04        NA
##  8 Arti~ Bovid~ Anti~ cervic~ 3.75e4      5.5    3846     2.13        NA
##  9 Arti~ Bovid~ Bison bison   4.98e5      8.93  20000    10.7     157500
## 10 Arti~ Bovid~ Bison bonasus 5.00e5      9.14  23000.    6.6         NA
## # ... with 1,430 more rows, and 4 more variables: AFR <dbl>,
## #   max_life <dbl>, litter_size <dbl>, litters_yr <dbl>
```

##Ggplot 


```r
options(scipen=999)
```

#6 What is the relationship between newborn body mass and gestation? Make a scatterplot that shows this relationship.

```r
life_history %>% 
  ggplot(aes(x=newborn, y=gestation))+
  geom_point()+
  labs(title = "Newborn Body Mass vs. Gestation", x = "Newborn Mass", y = "Gestation")+ 
  theme(plot.title = element_text(size = rel(1.5), hjust = 0.5))
```

```
## Warning: Removed 673 rows containing missing values (geom_point).
```

![](Homework_5_files/figure-html/unnamed-chunk-11-1.png)<!-- -->


#7 You should notice that because of the outliers in newborn mass, we need to make some changes. We didn't talk about this in lab, but you can use scale_x_log10() as a layer to correct for this issue. This will log transform the y-axis values.

```r
life_history %>%
  ggplot(aes(x=newborn, y=gestation))+
  geom_point()+
  scale_x_log10()+
  labs(title = "Newborn Body Mass vs. Gestation", x = "Newborn Mass", y = "Gestation")+
  theme(plot.title = element_text(size = rel(1.5), hjust = 0.5))
```

```
## Warning: Removed 673 rows containing missing values (geom_point).
```

![](Homework_5_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

#8 Now that you have the basic plot, color the points by taxonomic order.

```r
life_history %>%
  ggplot(aes(x=newborn, y=gestation, color=order))+
  geom_point()+
  scale_x_log10()+
  labs(title = "Newborn Body Mass vs. Gestation", x = "Newborn Mass", y = "Gestation")+
  theme(plot.title = element_text(size = rel(1.5), hjust = 0.5))
```

```
## Warning: Removed 673 rows containing missing values (geom_point).
```

![](Homework_5_files/figure-html/unnamed-chunk-13-1.png)<!-- -->


#9 Lastly, make the size of the points proportional to body mass.

```r
life_history %>%
  ggplot(aes(x=newborn, y=gestation, color=order, size=mass))+
  geom_point()+
  scale_x_log10()+
  labs(title = "Newborn Body Mass vs. Gestation", x = "Newborn Mass", y = "Gestation")+
  theme(plot.title = element_text(size = rel(1.5), hjust = 0.5))
```

```
## Warning: Removed 691 rows containing missing values (geom_point).
```

![](Homework_5_files/figure-html/unnamed-chunk-14-1.png)<!-- -->


#10 Make a plot that shows the range of lifespan by order.

```r
life_history %>% 
  ggplot(aes(x=order, y=max_life, fill=order))+
  geom_boxplot()+
  coord_flip()+
  scale_y_log10()+
  labs(title = "Lifespan by Taxonomic Order", x = "Taxonomic Order", y = "Lifespan", fill="Taxonomic Order")
```

```
## Warning: Removed 841 rows containing non-finite values (stat_boxplot).
```

![](Homework_5_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

