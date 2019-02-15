---
title: "Homework 4"
author: "Lara Friedlund"
date: "2/15/2019"
output: 
  html_document: 
    keep_md: yes
---

```r
library(tidyverse)
```

```
## ── Attaching packages ──────────────────────────── tidyverse 1.2.1 ──
```

```
## ✔ ggplot2 3.1.0       ✔ purrr   0.3.0  
## ✔ tibble  2.0.1       ✔ dplyr   0.8.0.1
## ✔ tidyr   0.8.2       ✔ stringr 1.4.0  
## ✔ readr   1.3.1       ✔ forcats 0.3.0
```

```
## Warning: package 'tibble' was built under R version 3.5.2
```

```
## Warning: package 'purrr' was built under R version 3.5.2
```

```
## Warning: package 'stringr' was built under R version 3.5.2
```

```
## ── Conflicts ─────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
life_history <- readr::read_csv("mammal_lifehistories_v2.csv")
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

```r
life_history <- 
  life_history %>% 
  dplyr::rename(
          genus        = Genus,
          wean_mass    = `wean mass`,
          max_life     = `max. life`,
          litter_size  = `litter size`,
          litters_yr   = `litters/year`
          )
life_history
```

```
## # A tibble: 1,440 x 13
##    order family genus species   mass gestation newborn weaning wean_mass
##    <chr> <chr>  <chr> <chr>    <dbl>     <dbl>   <dbl>   <dbl>     <dbl>
##  1 Arti… Antil… Anti… americ… 4.54e4      8.13   3246.    3         8900
##  2 Arti… Bovid… Addax nasoma… 1.82e5      9.39   5480     6.5       -999
##  3 Arti… Bovid… Aepy… melamp… 4.15e4      6.35   5093     5.63     15900
##  4 Arti… Bovid… Alce… busela… 1.50e5      7.9   10167.    6.5       -999
##  5 Arti… Bovid… Ammo… clarkei 2.85e4      6.8    -999  -999         -999
##  6 Arti… Bovid… Ammo… lervia  5.55e4      5.08   3810     4         -999
##  7 Arti… Bovid… Anti… marsup… 3.00e4      5.72   3910     4.04      -999
##  8 Arti… Bovid… Anti… cervic… 3.75e4      5.5    3846     2.13      -999
##  9 Arti… Bovid… Bison bison   4.98e5      8.93  20000    10.7     157500
## 10 Arti… Bovid… Bison bonasus 5.00e5      9.14  23000.    6.6       -999
## # … with 1,430 more rows, and 4 more variables: AFR <dbl>, max_life <dbl>,
## #   litter_size <dbl>, litters_yr <dbl>
```

#1

```r
library(skimr)
```

```
## Warning: package 'skimr' was built under R version 3.5.2
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
## ── Variable type:character ──────────────────────────────────────────
##  variable missing complete    n min max empty n_unique
##    family       0     1440 1440   6  15     0       96
##     genus       0     1440 1440   3  16     0      618
##     order       0     1440 1440   7  14     0       17
##   species       0     1440 1440   3  17     0     1191
## 
## ── Variable type:numeric ────────────────────────────────────────────
##     variable missing complete    n      mean         sd   p0  p25     p50
##          AFR       0     1440 1440   -408.12     504.97 -999 -999    2.5 
##    gestation       0     1440 1440   -287.25     455.36 -999 -999    1.05
##  litter_size       0     1440 1440    -55.63     234.88 -999    1    2.27
##   litters_yr       0     1440 1440   -477.14     500.03 -999 -999    0.38
##         mass       0     1440 1440 383576.72 5055162.92 -999   50  403.02
##     max_life       0     1440 1440   -490.26     615.3  -999 -999 -999   
##      newborn       0     1440 1440   6703.15   90912.52 -999 -999    2.65
##    wean_mass       0     1440 1440  16048.93   5e+05    -999 -999 -999   
##      weaning       0     1440 1440   -427.17     496.71 -999 -999    0.73
##      p75          p100     hist
##    15.61     210       ▆▁▁▁▁▁▇▁
##     4.5       21.46    ▃▁▁▁▁▁▁▇
##     3.83      14.18    ▁▁▁▁▁▁▁▇
##     1.15       7.5     ▇▁▁▁▁▁▁▇
##  7009.17       1.5e+08 ▇▁▁▁▁▁▁▁
##   147.25    1368       ▇▁▁▃▂▁▁▁
##    98    2250000       ▇▁▁▁▁▁▁▁
##    10          1.9e+07 ▇▁▁▁▁▁▁▁
##     2         48       ▆▁▁▁▁▁▁▇
```

#2

```r
data(msleep)
msleep
```

```
## # A tibble: 83 x 11
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl>
##  1 Chee… Acin… carni Carn… lc                  12.1      NA        NA    
##  2 Owl … Aotus omni  Prim… <NA>                17         1.8      NA    
##  3 Moun… Aplo… herbi Rode… nt                  14.4       2.4      NA    
##  4 Grea… Blar… omni  Sori… lc                  14.9       2.3       0.133
##  5 Cow   Bos   herbi Arti… domesticated         4         0.7       0.667
##  6 Thre… Brad… herbi Pilo… <NA>                14.4       2.2       0.767
##  7 Nort… Call… carni Carn… vu                   8.7       1.4       0.383
##  8 Vesp… Calo… <NA>  Rode… <NA>                 7        NA        NA    
##  9 Dog   Canis carni Carn… domesticated        10.1       2.9       0.333
## 10 Roe … Capr… herbi Arti… lc                   3        NA        NA    
## # … with 73 more rows, and 3 more variables: awake <dbl>, brainwt <dbl>,
## #   bodywt <dbl>
```


```r
msleep %>% 
  summarize(number_nas= sum(is.na(life_history)))
```

```
## # A tibble: 1 x 1
##   number_nas
##        <int>
## 1          0
```
#There are 0 NA's in the data which is unlikely since the life history dataset is full of -999 which seems to be a replacement of an NA value. Side note: why pipe msleep?

#3

```r
life_history <- 
  life_history %>% 
  na_if(-999.0)
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
## ── Variable type:character ──────────────────────────────────────────
##  variable missing complete    n min max empty n_unique
##    family       0     1440 1440   6  15     0       96
##     genus       0     1440 1440   3  16     0      618
##     order       0     1440 1440   7  14     0       17
##   species       0     1440 1440   3  17     0     1191
## 
## ── Variable type:numeric ────────────────────────────────────────────
##     variable missing complete    n      mean         sd    p0   p25    p50
##          AFR     607      833 1440     22.44      26.45  0.7   4.5   12   
##    gestation     418     1022 1440      3.86       3.62  0.49  0.99   2.11
##  litter_size      84     1356 1440      2.8        1.77  1     1.02   2.5 
##   litters_yr     689      751 1440      1.64       1.17  0.14  1      1   
##         mass      85     1355 1440 407701.39 5210474.99  2.1  61.15 606   
##     max_life     841      599 1440    224.03     189.74 12    84    192   
##      newborn     595      845 1440  12126.55  118408.21  0.21  4.4   43.7 
##    wean_mass    1039      401 1440  60220.5   953857.17  2.09 20.15 102.6 
##      weaning     619      821 1440      3.97       5.38  0.3   0.92   1.69
##      p75          p100     hist
##    28.24     210       ▇▂▁▁▁▁▁▁
##     6         21.46    ▇▂▂▁▁▁▁▁
##     4         14.18    ▇▃▂▁▁▁▁▁
##     2          7.5     ▇▂▃▁▁▁▁▁
##  8554          1.5e+08 ▇▁▁▁▁▁▁▁
##   288       1368       ▇▆▂▁▁▁▁▁
##   542.5  2250000       ▇▁▁▁▁▁▁▁
##  2000          1.9e+07 ▇▁▁▁▁▁▁▁
##     4.84      48       ▇▁▁▁▁▁▁▁
```


```r
life_history %>%
  purrr::map_df(~ sum(is.na(.)))%>% 
  tidyr::gather(variables, num_nas) %>% 
  arrange(desc(num_nas))
```

```
## # A tibble: 13 x 2
##    variables   num_nas
##    <chr>         <int>
##  1 wean_mass      1039
##  2 max_life        841
##  3 litters_yr      689
##  4 weaning         619
##  5 AFR             607
##  6 newborn         595
##  7 gestation       418
##  8 mass             85
##  9 litter_size      84
## 10 order             0
## 11 family            0
## 12 genus             0
## 13 species           0
```
#Wean mass has the most NA's (1039) followed by max_life, litters_yr, and weaning.

#4

```r
life_history %>%
  group_by(order) %>% 
  summarize(n())
```

```
## # A tibble: 17 x 2
##    order          `n()`
##    <chr>          <int>
##  1 Artiodactyla     161
##  2 Carnivora        197
##  3 Cetacea           55
##  4 Dermoptera         2
##  5 Hyracoidea         4
##  6 Insectivora       91
##  7 Lagomorpha        42
##  8 Macroscelidea     10
##  9 Perissodactyla    15
## 10 Pholidota          7
## 11 Primates         156
## 12 Proboscidea        2
## 13 Rodentia         665
## 14 Scandentia         7
## 15 Sirenia            5
## 16 Tubulidentata      1
## 17 Xenarthra         20
```

#5 (max life recorded in months according to metadata)

```r
life_history %>%
  mutate(lifespan=max_life/12) %>% 
  group_by(order) %>%
  summarize(min=min(lifespan, na.rm=TRUE),
            max=max(lifespan, na.rm=TRUE),
            mean=mean(lifespan, na.rm=TRUE),
            sd=sd(lifespan, na.rm=TRUE),
            total=n())
```

```
## # A tibble: 17 x 6
##    order            min    max  mean     sd total
##    <chr>          <dbl>  <dbl> <dbl>  <dbl> <int>
##  1 Artiodactyla    6.75  61    20.7   7.70    161
##  2 Carnivora       5     56    21.1   9.42    197
##  3 Cetacea        13    114    48.8  27.7      55
##  4 Dermoptera     17.5   17.5  17.5  NA         2
##  5 Hyracoidea     11     12.2  11.6   0.884     4
##  6 Insectivora     1.17  13     3.85  2.90     91
##  7 Lagomorpha      6     18     9.02  3.85     42
##  8 Macroscelidea   3      8.75  5.69  2.39     10
##  9 Perissodactyla 21     50    35.5  10.2      15
## 10 Pholidota      20     20    20    NA         7
## 11 Primates        8.83  60.5  25.7  11.0     156
## 12 Proboscidea    70     80    75     7.07      2
## 13 Rodentia        1     35     6.99  5.30    665
## 14 Scandentia      2.67  12.4   8.86  5.38      7
## 15 Sirenia        12.5   73    43.2  30.3       5
## 16 Tubulidentata  24     24    24    NA         1
## 17 Xenarthra       9     40    21.3   9.93     20
```

#6

```r
life_history %>% 
  group_by(order) %>% 
  summarize(mean_gestation=mean(gestation, na.rm=TRUE),
            mean_newborn_mass=mean(newborn, na.rm=TRUE),
            mean_wean_mass=mean(wean_mass, na.rm=TRUE),
            total=n()) %>% 
  arrange(desc(mean_gestation))
```

```
## # A tibble: 17 x 5
##    order          mean_gestation mean_newborn_mass mean_wean_mass total
##    <chr>                   <dbl>             <dbl>          <dbl> <int>
##  1 Proboscidea             21.3           99523.         600000       2
##  2 Perissodactyla          13.0           27015.         382191.     15
##  3 Cetacea                 11.8          343077.        4796125      55
##  4 Sirenia                 10.8           22878.          67500       5
##  5 Hyracoidea               7.4             231.            500       4
##  6 Artiodactyla             7.26           7082.          51025.    161
##  7 Tubulidentata            7.08           1734            6250       1
##  8 Primates                 5.47            287.           2115.    156
##  9 Xenarthra                4.95            314.            420      20
## 10 Carnivora                3.69           3657.          21020.    197
## 11 Pholidota                3.63            276.           2006.      7
## 12 Dermoptera               2.75             35.9           NaN       2
## 13 Macroscelidea            1.91             24.5           104.     10
## 14 Scandentia               1.63             12.8           102.      7
## 15 Rodentia                 1.31             35.5           135.    665
## 16 Lagomorpha               1.18             57.0           715.     42
## 17 Insectivora              1.15              6.06           33.1    91
```


