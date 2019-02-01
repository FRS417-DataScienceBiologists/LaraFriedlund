---
title: "Homework 2"
author: "Lara Friedlund"
date: "2/1/2019"
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
## ✔ ggplot2 3.1.0     ✔ purrr   0.3.0
## ✔ tibble  2.0.1     ✔ dplyr   0.7.8
## ✔ tidyr   0.8.2     ✔ stringr 1.3.1
## ✔ readr   1.3.1     ✔ forcats 0.3.0
```

```
## Warning: package 'tibble' was built under R version 3.5.2
```

```
## Warning: package 'purrr' was built under R version 3.5.2
```

```
## ── Conflicts ─────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

# 1: Proceedings of the National Academy of Sciences

```r
data("msleep")
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
?msleep
```

# 2:

```r
names(msleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"       
##  [5] "conservation" "sleep_total"  "sleep_rem"    "sleep_cycle" 
##  [9] "awake"        "brainwt"      "bodywt"
```


```r
summary(msleep)
```

```
##      name              genus               vore          
##  Length:83          Length:83          Length:83         
##  Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character  
##                                                          
##                                                          
##                                                          
##                                                          
##     order           conservation        sleep_total      sleep_rem    
##  Length:83          Length:83          Min.   : 1.90   Min.   :0.100  
##  Class :character   Class :character   1st Qu.: 7.85   1st Qu.:0.900  
##  Mode  :character   Mode  :character   Median :10.10   Median :1.500  
##                                        Mean   :10.43   Mean   :1.875  
##                                        3rd Qu.:13.75   3rd Qu.:2.400  
##                                        Max.   :19.90   Max.   :6.600  
##                                                        NA's   :22     
##   sleep_cycle         awake          brainwt            bodywt        
##  Min.   :0.1167   Min.   : 4.10   Min.   :0.00014   Min.   :   0.005  
##  1st Qu.:0.1833   1st Qu.:10.25   1st Qu.:0.00290   1st Qu.:   0.174  
##  Median :0.3333   Median :13.90   Median :0.01240   Median :   1.670  
##  Mean   :0.4396   Mean   :13.57   Mean   :0.28158   Mean   : 166.136  
##  3rd Qu.:0.5792   3rd Qu.:16.15   3rd Qu.:0.12550   3rd Qu.:  41.750  
##  Max.   :1.5000   Max.   :22.10   Max.   :5.71200   Max.   :6654.000  
##  NA's   :51                       NA's   :27
```

# 3

```r
msleep %>%
  select(bodywt,name,genus) %>%
  arrange(desc(bodywt))
```

```
## # A tibble: 83 x 3
##    bodywt name                 genus        
##     <dbl> <chr>                <chr>        
##  1  6654  African elephant     Loxodonta    
##  2  2547  Asian elephant       Elephas      
##  3   900. Giraffe              Giraffa      
##  4   800  Pilot whale          Globicephalus
##  5   600  Cow                  Bos          
##  6   521  Horse                Equus        
##  7   208. Brazilian tapir      Tapirus      
##  8   187  Donkey               Equus        
##  9   173. Bottle-nosed dolphin Tursiops     
## 10   163. Tiger                Panthera     
## # … with 73 more rows
```

#4

```r
large <- msleep %>% 
  select(bodywt,sleep_total,name,genus) %>% 
  filter(bodywt>=200) %>% 
  arrange(desc(bodywt))
glimpse(large)
```

```
## Observations: 7
## Variables: 4
## $ bodywt      <dbl> 6654.000, 2547.000, 899.995, 800.000, 600.000, 521.0…
## $ sleep_total <dbl> 3.3, 3.9, 1.9, 2.7, 4.0, 2.9, 4.4
## $ name        <chr> "African elephant", "Asian elephant", "Giraffe", "Pi…
## $ genus       <chr> "Loxodonta", "Elephas", "Giraffa", "Globicephalus", …
```

```r
large
```

```
## # A tibble: 7 x 4
##   bodywt sleep_total name             genus        
##    <dbl>       <dbl> <chr>            <chr>        
## 1  6654          3.3 African elephant Loxodonta    
## 2  2547          3.9 Asian elephant   Elephas      
## 3   900.         1.9 Giraffe          Giraffa      
## 4   800          2.7 Pilot whale      Globicephalus
## 5   600          4   Cow              Bos          
## 6   521          2.9 Horse            Equus        
## 7   208.         4.4 Brazilian tapir  Tapirus
```

```r
small <- msleep %>% 
  select(bodywt,sleep_total,name,genus) %>% 
  filter(bodywt<=1) %>% 
  arrange(desc(bodywt))
glimpse(small)
```

```
## Observations: 36
## Variables: 4
## $ bodywt      <dbl> 1.000, 0.920, 0.900, 0.770, 0.743, 0.728, 0.550, 0.4…
## $ sleep_total <dbl> 8.3, 16.6, 15.6, 10.1, 9.6, 9.4, 10.3, 17.0, 12.5, 1…
## $ name        <chr> "African giant pouched rat", "Arctic ground squirrel…
## $ genus       <chr> "Cricetomys", "Spermophilus", "Tenrec", "Erinaceus",…
```

```r
small
```

```
## # A tibble: 36 x 4
##    bodywt sleep_total name                      genus       
##     <dbl>       <dbl> <chr>                     <chr>       
##  1  1             8.3 African giant pouched rat Cricetomys  
##  2  0.92         16.6 Arctic ground squirrel    Spermophilus
##  3  0.9          15.6 Tenrec                    Tenrec      
##  4  0.77         10.1 European hedgehog         Erinaceus   
##  5  0.743         9.6 Squirrel monkey           Saimiri     
##  6  0.728         9.4 Guinea pig                Cavis       
##  7  0.55         10.3 Desert hedgehog           Paraechinus 
##  8  0.48         17   Owl monkey                Aotus       
##  9  0.42         12.5 Chinchilla                Chinchilla  
## 10  0.37         19.4 Thick-tailed opposum      Lutreolina  
## # … with 26 more rows
```

#5

```r
mean(large$sleep_total)
```

```
## [1] 3.3
```

#6

```r
mean(small$sleep_total)
```

```
## [1] 12.65833
```

#7

```r
msleep %>% 
  filter(sleep_total>=18) %>% 
  select(name,genus,order,sleep_total) %>% 
  arrange(order,sleep_total)
```

```
## # A tibble: 5 x 4
##   name                   genus      order           sleep_total
##   <chr>                  <chr>      <chr>                 <dbl>
## 1 Big brown bat          Eptesicus  Chiroptera             19.7
## 2 Little brown bat       Myotis     Chiroptera             19.9
## 3 Giant armadillo        Priodontes Cingulata              18.1
## 4 North American Opossum Didelphis  Didelphimorphia        18  
## 5 Thick-tailed opposum   Lutreolina Didelphimorphia        19.4
```

