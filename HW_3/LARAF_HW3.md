---
title: "Homework 3"
author: "Lara Friedlund"
date: "2/8/2019"
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


```r
fisheries <- readr::read_csv(file = "FAO_1950to2012_111914.csv")
```

```
## Warning: Duplicated column names deduplicated: 'Species (ISSCAAP group)'
## => 'Species (ISSCAAP group)_1' [4], 'Species (ASFIS species)' => 'Species
## (ASFIS species)_1' [5], 'Species (ASFIS species)' => 'Species (ASFIS
## species)_2' [6]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   `Species (ISSCAAP group)` = col_double(),
##   `Fishing area (FAO major fishing area)` = col_double()
## )
```

```
## See spec(...) for full column specifications.
```
# 1: It seems that there are multiple columns named species. Also, the columns with 1950-2012 can be formatted better.

# 2

```r
names(fisheries) = make.names(names(fisheries), unique=T)
names(fisheries)
```

```
##  [1] "Country..Country."                    
##  [2] "Species..ASFIS.species."              
##  [3] "Species..ISSCAAP.group."              
##  [4] "Species..ISSCAAP.group._1"            
##  [5] "Species..ASFIS.species._1"            
##  [6] "Species..ASFIS.species._2"            
##  [7] "Fishing.area..FAO.major.fishing.area."
##  [8] "Measure..Measure."                    
##  [9] "X1950"                                
## [10] "X1951"                                
## [11] "X1952"                                
## [12] "X1953"                                
## [13] "X1954"                                
## [14] "X1955"                                
## [15] "X1956"                                
## [16] "X1957"                                
## [17] "X1958"                                
## [18] "X1959"                                
## [19] "X1960"                                
## [20] "X1961"                                
## [21] "X1962"                                
## [22] "X1963"                                
## [23] "X1964"                                
## [24] "X1965"                                
## [25] "X1966"                                
## [26] "X1967"                                
## [27] "X1968"                                
## [28] "X1969"                                
## [29] "X1970"                                
## [30] "X1971"                                
## [31] "X1972"                                
## [32] "X1973"                                
## [33] "X1974"                                
## [34] "X1975"                                
## [35] "X1976"                                
## [36] "X1977"                                
## [37] "X1978"                                
## [38] "X1979"                                
## [39] "X1980"                                
## [40] "X1981"                                
## [41] "X1982"                                
## [42] "X1983"                                
## [43] "X1984"                                
## [44] "X1985"                                
## [45] "X1986"                                
## [46] "X1987"                                
## [47] "X1988"                                
## [48] "X1989"                                
## [49] "X1990"                                
## [50] "X1991"                                
## [51] "X1992"                                
## [52] "X1993"                                
## [53] "X1994"                                
## [54] "X1995"                                
## [55] "X1996"                                
## [56] "X1997"                                
## [57] "X1998"                                
## [58] "X1999"                                
## [59] "X2000"                                
## [60] "X2001"                                
## [61] "X2002"                                
## [62] "X2003"                                
## [63] "X2004"                                
## [64] "X2005"                                
## [65] "X2006"                                
## [66] "X2007"                                
## [67] "X2008"                                
## [68] "X2009"                                
## [69] "X2010"                                
## [70] "X2011"                                
## [71] "X2012"
```

```r
library(dplyr)
```

# 3

```r
fisheries<-
fisheries %>% 
  dplyr::rename(
    country = Country..Country.,
    commname = Species..ASFIS.species.,
    sciname = Species..ASFIS.species._2,
    spcode = Species..ASFIS.species._1,
    spgroup = Species..ISSCAAP.group.,
    spgroupname = Species..ISSCAAP.group._1,
    region = Fishing.area..FAO.major.fishing.area.,
    unit = Measure..Measure.)
```

# 4: The data is not tidy because variables (years) are being used as columns.

# 5

```r
fisheries_tidy <- 
  fisheries %>% 
  gather(num_range('X',1950:2012), key='year', value='catch')
fisheries_tidy
```

```
## # A tibble: 1,114,596 x 10
##    country commname spgroup spgroupname spcode sciname region unit  year 
##    <chr>   <chr>      <dbl> <chr>       <chr>  <chr>    <dbl> <chr> <chr>
##  1 Albania Angelsh…      38 Sharks, ra… 10903… Squati…     37 Quan… X1950
##  2 Albania Atlanti…      36 Tunas, bon… 17501… Sarda …     37 Quan… X1950
##  3 Albania Barracu…      37 Miscellane… 17710… Sphyra…     37 Quan… X1950
##  4 Albania Blue an…      45 Shrimps, p… 22802… Ariste…     37 Quan… X1950
##  5 Albania Blue wh…      32 Cods, hake… 14804… Microm…     37 Quan… X1950
##  6 Albania Bluefish      37 Miscellane… 17020… Pomato…     37 Quan… X1950
##  7 Albania Bogue         33 Miscellane… 17039… Boops …     37 Quan… X1950
##  8 Albania Caramot…      45 Shrimps, p… 22801… Penaeu…     37 Quan… X1950
##  9 Albania Catshar…      38 Sharks, ra… 10801… Scylio…     37 Quan… X1950
## 10 Albania Common …      57 Squids, cu… 32102… Sepia …     37 Quan… X1950
## # … with 1,114,586 more rows, and 1 more variable: catch <chr>
```

# 6: Both the year and catch columns are character class. There is missing/empty data in the catch column.

```r
glimpse(fisheries_tidy)
```

```
## Observations: 1,114,596
## Variables: 10
## $ country     <chr> "Albania", "Albania", "Albania", "Albania", "Albania…
## $ commname    <chr> "Angelsharks, sand devils nei", "Atlantic bonito", "…
## $ spgroup     <dbl> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, 33, 57, 31, …
## $ spgroupname <chr> "Sharks, rays, chimaeras", "Tunas, bonitos, billfish…
## $ spcode      <chr> "10903XXXXX", "1750100101", "17710001XX", "228020310…
## $ sciname     <chr> "Squatinidae", "Sarda sarda", "Sphyraena spp", "Aris…
## $ region      <dbl> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, …
## $ unit        <chr> "Quantity (tonnes)", "Quantity (tonnes)", "Quantity …
## $ year        <chr> "X1950", "X1950", "X1950", "X1950", "X1950", "X1950"…
## $ catch       <chr> "...", "...", "...", "...", "...", "...", "...", "..…
```

# 7

```r
fisheries_tidy <- 
  fisheries_tidy %>% 
  mutate(
    year= as.numeric(str_replace(year, 'X', '')), 
    catch= as.numeric(str_replace(catch, c(' F','...','-'), replacement = '')) 
    )
```

```
## Warning in evalq(as.numeric(str_replace(catch, c(" F", "...", "-"),
## replacement = "")), : NAs introduced by coercion
```

# 8: Data is tidy because varliables are no longer columns

# 9:


```r
fisheries_tidy %>% 
  select(country, spgroupname, year, catch) %>%
  filter(year>= 2008, year<=2012,
    spgroupname=="Squids, cuttlefishes, octopuses") %>%
  arrange(desc(catch))
```

```
## # A tibble: 3,725 x 4
##    country  spgroupname                      year  catch
##    <chr>    <chr>                           <dbl>  <dbl>
##  1 Peru     Squids, cuttlefishes, octopuses  2008 533414
##  2 China    Squids, cuttlefishes, octopuses  2008 462981
##  3 China    Squids, cuttlefishes, octopuses  2012 434845
##  4 Peru     Squids, cuttlefishes, octopuses  2011 404730
##  5 China    Squids, cuttlefishes, octopuses  2009 392478
##  6 China    Squids, cuttlefishes, octopuses  2011 390393
##  7 Peru     Squids, cuttlefishes, octopuses  2010 369822
##  8 China    Squids, cuttlefishes, octopuses  2012 261000
##  9 Viet Nam Squids, cuttlefishes, octopuses  2010 260000
## 10 Japan    Squids, cuttlefishes, octopuses  2011 242262
## # … with 3,715 more rows
```
# Peru, China, Vietnam, Japan, Taiwan Province of China

# 10: France

```r
cuttle <- 
  fisheries_tidy %>% 
  select(country, commname, year, catch) %>% 
  filter(year>=2008 & year<=2012) %>%
  filter(commname=="Common cuttlefish") %>%
  arrange(desc(catch))
cuttle
```

```
## # A tibble: 105 x 4
##    country  commname           year catch
##    <chr>    <chr>             <dbl> <dbl>
##  1 France   Common cuttlefish  2012 13217
##  2 France   Common cuttlefish  2011 12966
##  3 France   Common cuttlefish  2009  8076
##  4 Tunisia  Common cuttlefish  2012  7717
##  5 Tunisia  Common cuttlefish  2011  6371
##  6 Tunisia  Common cuttlefish  2008  4913
##  7 Tunisia  Common cuttlefish  2009  3924
##  8 Portugal Common cuttlefish  2010  2027
##  9 Libya    Common cuttlefish  2009  1800
## 10 Libya    Common cuttlefish  2010  1750
## # … with 95 more rows
```

