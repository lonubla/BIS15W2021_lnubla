---
title: "Lab 3 Homework"
author: "Lauren Nubla"
date: "2021-01-24"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

```r
??mammals
```

2. Store these data into a new data frame `sleep`.

```r
sleep <- data.frame(msleep)
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  

```r
glimpse(sleep)
```

```
## Observations: 83
## Variables: 11
## $ name         <chr> "Cheetah", "Owl monkey", "Mountain beaver", "Greater sho…
## $ genus        <chr> "Acinonyx", "Aotus", "Aplodontia", "Blarina", "Bos", "Br…
## $ vore         <chr> "carni", "omni", "herbi", "omni", "herbi", "herbi", "car…
## $ order        <chr> "Carnivora", "Primates", "Rodentia", "Soricomorpha", "Ar…
## $ conservation <chr> "lc", NA, "nt", "lc", "domesticated", NA, "vu", NA, "dom…
## $ sleep_total  <dbl> 12.1, 17.0, 14.4, 14.9, 4.0, 14.4, 8.7, 7.0, 10.1, 3.0, …
## $ sleep_rem    <dbl> NA, 1.8, 2.4, 2.3, 0.7, 2.2, 1.4, NA, 2.9, NA, 0.6, 0.8,…
## $ sleep_cycle  <dbl> NA, NA, NA, 0.1333333, 0.6666667, 0.7666667, 0.3833333, …
## $ awake        <dbl> 11.9, 7.0, 9.6, 9.1, 20.0, 9.6, 15.3, 17.0, 13.9, 21.0, …
## $ brainwt      <dbl> NA, 0.01550, NA, 0.00029, 0.42300, NA, NA, NA, 0.07000, …
## $ bodywt       <dbl> 50.000, 0.480, 1.350, 0.019, 600.000, 3.850, 20.490, 0.0…
```

```r
dim(sleep)
```

```
## [1] 83 11
```

<style>
div.blue { background-color:#e6f0ff; border-radius: 5px; padding: 20px;}
</style>
<div class = "blue">
4. Are there any NAs in the data? How did you determine this? Please show your code.  

</div>

5. Show a list of the column names is this data frame.

```r
colnames(sleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```

6. How many herbivores are represented in the data? 
There are 32 herbivores in the data set. 

```r
table(sleep$vore)
```

```
## 
##   carni   herbi insecti    omni 
##      19      32       5      20
```

7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
large <- subset(sleep, bodywt>=200)
small <- subset(sleep, bodywt<=1)
```

8. What is the mean weight for both the small and large mammals?
mean weight for large animals = 1747.071
mean weight for small animals = 0.2596667

```r
large_weight <- large[ ,11]
mean(large_weight)
```

```
## [1] 1747.071
```


```r
small_weight <- small[ ,11]
mean(small_weight)
```

```
## [1] 0.2596667
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  
On average, small animals sleep longer.

```r
large_sleep <- large[ ,6]
mean(large_sleep)
```

```
## [1] 3.3
```


```r
small_sleep <- small[ ,6]
mean(small_sleep)
```

```
## [1] 12.65833
```

10. Which animal is the sleepiest among the entire dataframe?
The little brown bat is the sleepiest

```r
all_sleep <- data.frame(sleep$name)
all_sleep <- cbind(all_sleep, sleep$sleep_total)
all_sleep
```

```
##                        sleep.name sleep$sleep_total
## 1                         Cheetah              12.1
## 2                      Owl monkey              17.0
## 3                 Mountain beaver              14.4
## 4      Greater short-tailed shrew              14.9
## 5                             Cow               4.0
## 6                Three-toed sloth              14.4
## 7               Northern fur seal               8.7
## 8                    Vesper mouse               7.0
## 9                             Dog              10.1
## 10                       Roe deer               3.0
## 11                           Goat               5.3
## 12                     Guinea pig               9.4
## 13                         Grivet              10.0
## 14                     Chinchilla              12.5
## 15                Star-nosed mole              10.3
## 16      African giant pouched rat               8.3
## 17      Lesser short-tailed shrew               9.1
## 18           Long-nosed armadillo              17.4
## 19                     Tree hyrax               5.3
## 20         North American Opossum              18.0
## 21                 Asian elephant               3.9
## 22                  Big brown bat              19.7
## 23                          Horse               2.9
## 24                         Donkey               3.1
## 25              European hedgehog              10.1
## 26                   Patas monkey              10.9
## 27      Western american chipmunk              14.9
## 28                   Domestic cat              12.5
## 29                         Galago               9.8
## 30                        Giraffe               1.9
## 31                    Pilot whale               2.7
## 32                      Gray seal               6.2
## 33                     Gray hyrax               6.3
## 34                          Human               8.0
## 35                 Mongoose lemur               9.5
## 36               African elephant               3.3
## 37           Thick-tailed opposum              19.4
## 38                        Macaque              10.1
## 39               Mongolian gerbil              14.2
## 40                 Golden hamster              14.3
## 41                          Vole               12.8
## 42                    House mouse              12.5
## 43               Little brown bat              19.9
## 44           Round-tailed muskrat              14.6
## 45                     Slow loris              11.0
## 46                           Degu               7.7
## 47     Northern grasshopper mouse              14.5
## 48                         Rabbit               8.4
## 49                          Sheep               3.8
## 50                     Chimpanzee               9.7
## 51                          Tiger              15.8
## 52                         Jaguar              10.4
## 53                           Lion              13.5
## 54                         Baboon               9.4
## 55                Desert hedgehog              10.3
## 56                          Potto              11.0
## 57                     Deer mouse              11.5
## 58                      Phalanger              13.7
## 59                   Caspian seal               3.5
## 60                Common porpoise               5.6
## 61                        Potoroo              11.1
## 62                Giant armadillo              18.1
## 63                     Rock hyrax               5.4
## 64                 Laboratory rat              13.0
## 65          African striped mouse               8.7
## 66                Squirrel monkey               9.6
## 67          Eastern american mole               8.4
## 68                     Cotton rat              11.3
## 69                       Mole rat              10.6
## 70         Arctic ground squirrel              16.6
## 71 Thirteen-lined ground squirrel              13.8
## 72 Golden-mantled ground squirrel              15.9
## 73                     Musk shrew              12.8
## 74                            Pig               9.1
## 75            Short-nosed echidna               8.6
## 76      Eastern american chipmunk              15.8
## 77                Brazilian tapir               4.4
## 78                         Tenrec              15.6
## 79                     Tree shrew               8.9
## 80           Bottle-nosed dolphin               5.2
## 81                          Genet               6.3
## 82                     Arctic fox              12.5
## 83                        Red fox               9.8
```


```r
max(all_sleep[,2])
```

```
## [1] 19.9
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
