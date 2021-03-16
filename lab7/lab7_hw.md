---
title: "Lab 7 Homework"
author: "Lauren Nubla"
date: "2021-03-16"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```
<style>
div.blue { background-color:#e6f0ff; border-radius: 5px; padding: 20px;}
</style>
<div class = "blue">

# missing data

## Data
**1. For this homework, we will use two different data sets. Please load `amniota` and `amphibio`.**  

`amniota` data:  
Myhrvold N, Baldridge E, Chan B, Sivam D, Freeman DL, Ernest SKM (2015). “An amniote life-history
database to perform comparative analyses with birds, mammals, and reptiles.” _Ecology_, *96*, 3109.
doi: 10.1890/15-0846.1 (URL: https://doi.org/10.1890/15-0846.1).

```r
#setwd("/Users/lonubla/Desktop/BIS15W2021_lnubla/lab7/data")
```


```r
amniota <- readr::read_csv("data/amniota.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   class = col_character(),
##   order = col_character(),
##   family = col_character(),
##   genus = col_character(),
##   species = col_character(),
##   common_name = col_character()
## )
## i Use `spec()` for the full column specifications.
```
Had trouble loading the amniota csv as the downloaded class folder didn't contain a proper file. 

`amphibio` data:  
Oliveira BF, São-Pedro VA, Santos-Barrera G, Penone C, Costa GC (2017). “AmphiBIO, a global database
for amphibian ecological traits.” _Scientific Data_, *4*, 170123. doi: 10.1038/sdata.2017.123 (URL:
https://doi.org/10.1038/sdata.2017.123).

```r
amphibio<-readr::read_csv("data/amphibio.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   id = col_character(),
##   Order = col_character(),
##   Family = col_character(),
##   Genus = col_character(),
##   Species = col_character(),
##   Seeds = col_logical(),
##   OBS = col_logical()
## )
## i Use `spec()` for the full column specifications.
```

```
## Warning: 125 parsing failures.
##  row col           expected                                                           actual                file
## 1410 OBS 1/0/T/F/TRUE/FALSE Identified as P. appendiculata in Boquimpani-Freitas et al. 2002 'data/amphibio.csv'
## 1416 OBS 1/0/T/F/TRUE/FALSE Identified as T. miliaris in Giaretta and Facure 2004            'data/amphibio.csv'
## 1447 OBS 1/0/T/F/TRUE/FALSE Considered endangered by Soto-Azat et al. 2013                   'data/amphibio.csv'
## 1448 OBS 1/0/T/F/TRUE/FALSE Considered extinct by Soto-Azat et al. 2013                      'data/amphibio.csv'
## 1471 OBS 1/0/T/F/TRUE/FALSE nomem dubitum                                                    'data/amphibio.csv'
## .... ... .................. ................................................................ ...................
## See problems(...) for more details.
```

```r
amphibio<-janitor::clean_names(amphibio)
```
</div>

## Questions  
**2. Do some exploratory analysis of the `amniota` data set. Use the function(s) of your choice. Try to get an idea of how NA's are represented in the data.**  


```r
glimpse(amniota)
```

```
## Rows: 21,322
## Columns: 36
## $ class                                 <chr> "Aves", "Aves", "Aves", "Aves", ~
## $ order                                 <chr> "Accipitriformes", "Accipitrifor~
## $ family                                <chr> "Accipitridae", "Accipitridae", ~
## $ genus                                 <chr> "Accipiter", "Accipiter", "Accip~
## $ species                               <chr> "albogularis", "badius", "bicolo~
## $ subspecies                            <dbl> -999, -999, -999, -999, -999, -9~
## $ common_name                           <chr> "Pied Goshawk", "Shikra", "Bicol~
## $ female_maturity_d                     <dbl> -999.000, 363.468, -999.000, -99~
## $ litter_or_clutch_size_n               <dbl> -999.000, 3.250, 2.700, -999.000~
## $ litters_or_clutches_per_y             <dbl> -999, 1, -999, -999, 1, -999, -9~
## $ adult_body_mass_g                     <dbl> 251.500, 140.000, 345.000, 142.0~
## $ maximum_longevity_y                   <dbl> -999.00000, -999.00000, -999.000~
## $ gestation_d                           <dbl> -999, -999, -999, -999, -999, -9~
## $ weaning_d                             <dbl> -999, -999, -999, -999, -999, -9~
## $ birth_or_hatching_weight_g            <dbl> -999, -999, -999, -999, -999, -9~
## $ weaning_weight_g                      <dbl> -999, -999, -999, -999, -999, -9~
## $ egg_mass_g                            <dbl> -999.00, 21.00, 32.00, -999.00, ~
## $ incubation_d                          <dbl> -999.00, 30.00, -999.00, -999.00~
## $ fledging_age_d                        <dbl> -999.00, 32.00, -999.00, -999.00~
## $ longevity_y                           <dbl> -999.00000, -999.00000, -999.000~
## $ male_maturity_d                       <dbl> -999, -999, -999, -999, -999, -9~
## $ inter_litter_or_interbirth_interval_y <dbl> -999, -999, -999, -999, -999, -9~
## $ female_body_mass_g                    <dbl> 352.500, 168.500, 390.000, -999.~
## $ male_body_mass_g                      <dbl> 223.000, 125.000, 212.000, 142.0~
## $ no_sex_body_mass_g                    <dbl> -999.0, 123.0, -999.0, -999.0, -~
## $ egg_width_mm                          <dbl> -999, -999, -999, -999, -999, -9~
## $ egg_length_mm                         <dbl> -999, -999, -999, -999, -999, -9~
## $ fledging_mass_g                       <dbl> -999, -999, -999, -999, -999, -9~
## $ adult_svl_cm                          <dbl> -999.00, 30.00, 39.50, -999.00, ~
## $ male_svl_cm                           <dbl> -999, -999, -999, -999, -999, -9~
## $ female_svl_cm                         <dbl> -999, -999, -999, -999, -999, -9~
## $ birth_or_hatching_svl_cm              <dbl> -999, -999, -999, -999, -999, -9~
## $ female_svl_at_maturity_cm             <dbl> -999, -999, -999, -999, -999, -9~
## $ female_body_mass_at_maturity_g        <dbl> -999, -999, -999, -999, -999, -9~
## $ no_sex_svl_cm                         <dbl> -999, -999, -999, -999, -999, -9~
## $ no_sex_maturity_d                     <dbl> -999, -999, -999, -999, -999, -9~
```

**3. Do some exploratory analysis of the `amphibio` data set. Use the function(s) of your choice. Try to get an idea of how NA's are represented in the data.**  


```r
glimpse(amphibio)
```

```
## Rows: 6,776
## Columns: 38
## $ id                      <chr> "Anf0001", "Anf0002", "Anf0003", "Anf0004", "A~
## $ order                   <chr> "Anura", "Anura", "Anura", "Anura", "Anura", "~
## $ family                  <chr> "Allophrynidae", "Alytidae", "Alytidae", "Alyt~
## $ genus                   <chr> "Allophryne", "Alytes", "Alytes", "Alytes", "A~
## $ species                 <chr> "Allophryne ruthveni", "Alytes cisternasii", "~
## $ fos                     <dbl> NA, NA, NA, NA, NA, 1, 1, 1, 1, 1, 1, 1, 1, NA~
## $ ter                     <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1~
## $ aqu                     <dbl> 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, ~
## $ arb                     <dbl> 1, 1, 1, 1, 1, 1, NA, NA, NA, NA, NA, NA, NA, ~
## $ leaves                  <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA~
## $ flowers                 <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA~
## $ seeds                   <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA~
## $ fruits                  <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA~
## $ arthro                  <dbl> 1, 1, 1, NA, 1, 1, 1, 1, 1, NA, 1, 1, NA, NA, ~
## $ vert                    <dbl> NA, NA, NA, NA, NA, NA, 1, NA, NA, NA, 1, 1, N~
## $ diu                     <dbl> 1, NA, NA, NA, NA, NA, 1, 1, 1, NA, 1, 1, NA, ~
## $ noc                     <dbl> 1, 1, 1, NA, 1, 1, 1, 1, 1, NA, 1, 1, 1, NA, N~
## $ crepu                   <dbl> 1, NA, NA, NA, NA, 1, NA, NA, NA, NA, NA, NA, ~
## $ wet_warm                <dbl> NA, NA, NA, NA, 1, 1, NA, NA, NA, NA, 1, NA, N~
## $ wet_cold                <dbl> 1, NA, NA, NA, NA, NA, 1, NA, NA, NA, NA, NA, ~
## $ dry_warm                <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA~
## $ dry_cold                <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA~
## $ body_mass_g             <dbl> 31.00, 6.10, NA, NA, 2.31, 13.40, 21.80, NA, N~
## $ age_at_maturity_min_y   <dbl> NA, 2.0, 2.0, NA, 3.0, 2.0, 3.0, NA, NA, NA, 4~
## $ age_at_maturity_max_y   <dbl> NA, 2.0, 2.0, NA, 3.0, 3.0, 5.0, NA, NA, NA, 4~
## $ body_size_mm            <dbl> 31.0, 50.0, 55.0, NA, 40.0, 55.0, 80.0, 60.0, ~
## $ size_at_maturity_min_mm <dbl> NA, 27, NA, NA, NA, 35, NA, NA, NA, NA, NA, NA~
## $ size_at_maturity_max_mm <dbl> NA, 36.0, NA, NA, NA, 40.5, NA, NA, NA, NA, NA~
## $ longevity_max_y         <dbl> NA, 6, NA, NA, NA, 7, 9, NA, NA, NA, NA, NA, N~
## $ litter_size_min_n       <dbl> 300, 60, 40, NA, 7, 53, 300, 1500, 1000, NA, 2~
## $ litter_size_max_n       <dbl> 300, 180, 40, NA, 20, 171, 1500, 1500, 1000, N~
## $ reproductive_output_y   <dbl> 1, 4, 1, 4, 1, 4, 6, 1, 1, 1, 1, 1, 1, 1, NA, ~
## $ offspring_size_min_mm   <dbl> NA, 2.6, NA, NA, 5.4, 2.6, 1.5, NA, 1.5, NA, 1~
## $ offspring_size_max_mm   <dbl> NA, 3.5, NA, NA, 7.0, 5.0, 2.0, NA, 1.5, NA, 1~
## $ dir                     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, N~
## $ lar                     <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, N~
## $ viv                     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, N~
## $ obs                     <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA~
```

```r
skim(amphibio)
```


Table: Data summary

|                         |         |
|:------------------------|:--------|
|Name                     |amphibio |
|Number of rows           |6776     |
|Number of columns        |38       |
|_______________________  |         |
|Column type frequency:   |         |
|character                |5        |
|logical                  |2        |
|numeric                  |31       |
|________________________ |         |
|Group variables          |None     |


**Variable type: character**

|skim_variable | n_missing| complete_rate| min| max| empty| n_unique| whitespace|
|:-------------|---------:|-------------:|---:|---:|-----:|--------:|----------:|
|id            |         0|             1|   7|   7|     0|     6776|          0|
|order         |         0|             1|   5|  11|     0|        3|          0|
|family        |         0|             1|   7|  20|     0|       61|          0|
|genus         |         0|             1|   4|  17|     0|      531|          0|
|species       |         0|             1|   9|  34|     0|     6776|          0|


**Variable type: logical**

|skim_variable | n_missing| complete_rate| mean|count  |
|:-------------|---------:|-------------:|----:|:------|
|seeds         |      6772|             0|    1|TRU: 4 |
|obs           |      6776|             0|  NaN|:      |


**Variable type: numeric**

|skim_variable           | n_missing| complete_rate|    mean|      sd|    p0|  p25|    p50|    p75|    p100|hist  |
|:-----------------------|---------:|-------------:|-------:|-------:|-----:|----:|------:|------:|-------:|:-----|
|fos                     |      6053|          0.11|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|ter                     |      1104|          0.84|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|aqu                     |      2810|          0.59|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|arb                     |      4347|          0.36|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|leaves                  |      6752|          0.00|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|flowers                 |      6772|          0.00|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|fruits                  |      6774|          0.00|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|arthro                  |      5534|          0.18|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|vert                    |      6657|          0.02|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|diu                     |      5876|          0.13|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|noc                     |      5156|          0.24|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|crepu                   |      6608|          0.02|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|wet_warm                |      5997|          0.11|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|wet_cold                |      6625|          0.02|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|dry_warm                |      6572|          0.03|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|dry_cold                |      6735|          0.01|    1.00|    0.00|  1.00|  1.0|   1.00|   1.00|     1.0|▁▁▇▁▁ |
|body_mass_g             |      6185|          0.09|   94.56| 1093.77|  0.16|  2.6|   9.29|  31.83| 26000.0|▇▁▁▁▁ |
|age_at_maturity_min_y   |      6392|          0.06|    2.14|    1.18|  0.25|  1.0|   2.00|   3.00|     7.0|▇▇▆▁▁ |
|age_at_maturity_max_y   |      6392|          0.06|    2.96|    1.69|  0.30|  2.0|   3.00|   4.00|    12.0|▇▇▂▁▁ |
|body_size_mm            |      1549|          0.77|   66.65|   91.47|  8.40| 29.0|  43.00|  69.15|  1520.0|▇▁▁▁▁ |
|size_at_maturity_min_mm |      6529|          0.04|   56.63|   55.57|  8.80| 27.5|  43.00|  58.00|   350.0|▇▁▁▁▁ |
|size_at_maturity_max_mm |      6528|          0.04|   67.46|   66.34| 10.10| 32.0|  50.00|  75.50|   400.0|▇▁▁▁▁ |
|longevity_max_y         |      6417|          0.05|   11.68|    9.86|  0.17|  6.0|  10.00|  15.00|   121.8|▇▁▁▁▁ |
|litter_size_min_n       |      5153|          0.24|  530.87| 1575.73|  1.00| 18.0|  80.00| 300.00| 25000.0|▇▁▁▁▁ |
|litter_size_max_n       |      5153|          0.24| 1033.70| 2955.30|  1.00| 30.0| 186.00| 700.00| 45054.0|▇▁▁▁▁ |
|reproductive_output_y   |      2344|          0.65|    1.03|    0.43|  0.08|  1.0|   1.00|   1.00|    15.0|▇▁▁▁▁ |
|offspring_size_min_mm   |      5446|          0.20|    2.45|    1.57|  0.20|  1.4|   2.00|   3.00|    20.0|▇▁▁▁▁ |
|offspring_size_max_mm   |      5446|          0.20|    2.86|    1.94|  0.40|  1.6|   2.30|   3.50|    25.0|▇▁▁▁▁ |
|dir                     |      1079|          0.84|    0.30|    0.46|  0.00|  0.0|   0.00|   1.00|     1.0|▇▁▁▁▃ |
|lar                     |      1079|          0.84|    0.69|    0.46|  0.00|  0.0|   1.00|   1.00|     1.0|▃▁▁▁▇ |
|viv                     |      1079|          0.84|    0.01|    0.10|  0.00|  0.0|   0.00|   0.00|     1.0|▇▁▁▁▁ |

**4. How many total NA's are in each data set? Do these values make sense? Are NA's represented by values?**   


```r
naniar::miss_var_summary(amphibio) %>% 
  mutate(n_miss_sum=sum(n_miss))
```

```
## # A tibble: 38 x 4
##    variable n_miss pct_miss n_miss_sum
##    <chr>     <int>    <dbl>      <int>
##  1 obs        6776    100       170691
##  2 fruits     6774    100.      170691
##  3 flowers    6772     99.9     170691
##  4 seeds      6772     99.9     170691
##  5 leaves     6752     99.6     170691
##  6 dry_cold   6735     99.4     170691
##  7 vert       6657     98.2     170691
##  8 wet_cold   6625     97.8     170691
##  9 crepu      6608     97.5     170691
## 10 dry_warm   6572     97.0     170691
## # ... with 28 more rows
```
170,691 NA's in the amphibio data set. 


```r
naniar::miss_var_summary(amniota) %>% 
  mutate(n_miss_sum=sum(n_miss))
```

```
## # A tibble: 36 x 4
##    variable                  n_miss pct_miss n_miss_sum
##    <chr>                      <int>    <dbl>      <int>
##  1 class                          0        0          0
##  2 order                          0        0          0
##  3 family                         0        0          0
##  4 genus                          0        0          0
##  5 species                        0        0          0
##  6 subspecies                     0        0          0
##  7 common_name                    0        0          0
##  8 female_maturity_d              0        0          0
##  9 litter_or_clutch_size_n        0        0          0
## 10 litters_or_clutches_per_y      0        0          0
## # ... with 26 more rows
```
<style>
div.blue { background-color:#e6f0ff; border-radius: 5px; padding: 20px;}
</style>
<div class = "blue">

**5. Make any necessary replacements in the data such that all NA's appear as "NA".**   




**6. Use the package `naniar` to produce a summary, including percentages, of missing data in each column for the `amniota` data.**  

</div>

**7. Use the package `naniar` to produce a summary, including percentages, of missing data in each column for the `amphibio` data.**

```r
naniar::miss_var_summary(amphibio)
```

```
## # A tibble: 38 x 3
##    variable n_miss pct_miss
##    <chr>     <int>    <dbl>
##  1 obs        6776    100  
##  2 fruits     6774    100. 
##  3 flowers    6772     99.9
##  4 seeds      6772     99.9
##  5 leaves     6752     99.6
##  6 dry_cold   6735     99.4
##  7 vert       6657     98.2
##  8 wet_cold   6625     97.8
##  9 crepu      6608     97.5
## 10 dry_warm   6572     97.0
## # ... with 28 more rows
```
<style>
div.blue { background-color:#e6f0ff; border-radius: 5px; padding: 20px;}
</style>
<div class = "blue">

**8. For the `amniota` data, calculate the number of NAs in the `egg_mass_g` column sorted by taxonomic class; i.e. how many NA's are present in the `egg_mass_g` column in birds, mammals, and reptiles? Does this results make sense biologically? How do these results affect your interpretation of NA's?**  


</div>

**9. The `amphibio` data have variables that classify species as fossorial (burrowing), terrestrial, aquatic, or arboreal.Calculate the number of NA's in each of these variables. Do you think that the authors intend us to think that there are NA's in these columns or could they represent something else? Explain.**

```r
amphibio %>% 
  select(fos,ter,aqu,arb) %>% 
  naniar::miss_var_summary()
```

```
## # A tibble: 4 x 3
##   variable n_miss pct_miss
##   <chr>     <int>    <dbl>
## 1 fos        6053     89.3
## 2 arb        4347     64.2
## 3 aqu        2810     41.5
## 4 ter        1104     16.3
```
<style>
div.blue { background-color:#e6f0ff; border-radius: 5px; padding: 20px;}
</style>
<div class = "blue">
**10. Now that we know how NA's are represented in the `amniota` data, how would you load the data such that the values which represent NA's are automatically converted?**

</div>

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.  
