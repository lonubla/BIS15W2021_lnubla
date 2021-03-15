---
title: "Lab 4 Homework"
author: "Lauren"
date: "2021-03-15"
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

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
homerange <- read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_character(),
##   mean.mass.g = col_double(),
##   log10.mass = col_double(),
##   mean.hra.m2 = col_double(),
##   log10.hra = col_double(),
##   preymass = col_double(),
##   log10.preymass = col_double(),
##   PPMR = col_double()
## )
## i Use `spec()` for the full column specifications.
```

```r
homerange
```

```
## # A tibble: 569 x 24
##    taxon  common.name   class   order   family genus species primarymethod N    
##    <chr>  <chr>         <chr>   <chr>   <chr>  <chr> <chr>   <chr>         <chr>
##  1 lake ~ american eel  actino~ anguil~ angui~ angu~ rostra~ telemetry     16   
##  2 river~ blacktail re~ actino~ cyprin~ catos~ moxo~ poecil~ mark-recaptu~ <NA> 
##  3 river~ central ston~ actino~ cyprin~ cypri~ camp~ anomal~ mark-recaptu~ 20   
##  4 river~ rosyside dace actino~ cyprin~ cypri~ clin~ fundul~ mark-recaptu~ 26   
##  5 river~ longnose dace actino~ cyprin~ cypri~ rhin~ catara~ mark-recaptu~ 17   
##  6 river~ muskellunge   actino~ esocif~ esoci~ esox  masqui~ telemetry     5    
##  7 marin~ pollack       actino~ gadifo~ gadid~ poll~ pollac~ telemetry     2    
##  8 marin~ saithe        actino~ gadifo~ gadid~ poll~ virens  telemetry     2    
##  9 marin~ lined surgeo~ actino~ percif~ acant~ acan~ lineat~ direct obser~ <NA> 
## 10 marin~ orangespine ~ actino~ percif~ acant~ naso  litura~ telemetry     8    
## # ... with 559 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <chr>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```


**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

```r
glimpse(homerange)
```

```
## Rows: 569
## Columns: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fishe~
## $ common.name                <chr> "american eel", "blacktail redhorse", "cent~
## $ class                      <chr> "actinopterygii", "actinopterygii", "actino~
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprini~
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae"~
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cli~
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fundu~
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recapt~
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2", ~
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00,~
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600,~
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, 3~
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437,~
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home range~
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic",~
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ect~
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimmi~
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "car~
## $ dimension                  <chr> "3D", "2D", "2D", "2D", "2D", "2D", "2D", "~
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, N~
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA, ~
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, NA~
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 20~
```

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild       dimension            preymass         log10.preymass   
##  Length:569         Length:569         Min.   :     0.67   Min.   :-0.1739  
##  Class :character   Class :character   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Mode  :character   Median :    53.75   Median : 1.7304  
##                                        Mean   :  3989.88   Mean   : 2.0188  
##                                        3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                                        Max.   :130233.20   Max.   : 5.1147  
##                                        NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
taxon_var <- homerange$taxon
```

```r
homerange$taxon <- as.factor(homerange$taxon)
class(homerange$taxon)
```

```
## [1] "factor"
```

```r
levels(taxon_var)
```

```
## NULL
```

```r
homerange$order <- as.factor(homerange$order)
class(homerange$order)
```

```
## [1] "factor"
```

```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"    "afrosoricida"       "anguilliformes"    
##  [4] "anseriformes"       "apterygiformes"     "artiodactyla"      
##  [7] "caprimulgiformes"   "carnivora"          "charadriiformes"   
## [10] "columbidormes"      "columbiformes"      "coraciiformes"     
## [13] "cuculiformes"       "cypriniformes"      "dasyuromorpha"     
## [16] "dasyuromorpia"      "didelphimorphia"    "diprodontia"       
## [19] "diprotodontia"      "erinaceomorpha"     "esociformes"       
## [22] "falconiformes"      "gadiformes"         "galliformes"       
## [25] "gruiformes"         "lagomorpha"         "macroscelidea"     
## [28] "monotrematae"       "passeriformes"      "pelecaniformes"    
## [31] "peramelemorphia"    "perciformes"        "perissodactyla"    
## [34] "piciformes"         "pilosa"             "proboscidea"       
## [37] "psittaciformes"     "rheiformes"         "roden"             
## [40] "rodentia"           "salmoniformes"      "scorpaeniformes"   
## [43] "siluriformes"       "soricomorpha"       "squamata"          
## [46] "strigiformes"       "struthioniformes"   "syngnathiformes"   
## [49] "testudines"         "tetraodontiformes<U+00A0>" "tinamiformes"
```


**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  

```r
taxa <- homerange%>% 
  select(taxon,common.name,class,order,family,genus,species)
taxa
```

```
## # A tibble: 569 x 7
##    taxon     common.name       class      order     family    genus    species  
##    <fct>     <chr>             <chr>      <fct>     <chr>     <chr>    <chr>    
##  1 lake fis~ american eel      actinopte~ anguilli~ anguilli~ anguilla rostrata 
##  2 river fi~ blacktail redhor~ actinopte~ cyprinif~ catostom~ moxosto~ poecilura
##  3 river fi~ central stonerol~ actinopte~ cyprinif~ cyprinid~ campost~ anomalum 
##  4 river fi~ rosyside dace     actinopte~ cyprinif~ cyprinid~ clinost~ funduloi~
##  5 river fi~ longnose dace     actinopte~ cyprinif~ cyprinid~ rhinich~ cataract~
##  6 river fi~ muskellunge       actinopte~ esocifor~ esocidae  esox     masquino~
##  7 marine f~ pollack           actinopte~ gadiform~ gadidae   pollach~ pollachi~
##  8 marine f~ saithe            actinopte~ gadiform~ gadidae   pollach~ virens   
##  9 marine f~ lined surgeonfish actinopte~ percifor~ acanthur~ acanthu~ lineatus 
## 10 marine f~ orangespine unic~ actinopte~ percifor~ acanthur~ naso     lituratus
## # ... with 559 more rows
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
table(taxa$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```


**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.** 

```r
table(homerange$trophic.guild)
```

```
## 
## carnivore herbivore 
##       342       227
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
herbi<- filter(homerange, trophic.guild == "herbivore")
herbi
```

```
## # A tibble: 227 x 24
##    taxon  common.name   class   order  family  genus species primarymethod N    
##    <fct>  <chr>         <chr>   <fct>  <chr>   <chr> <chr>   <chr>         <chr>
##  1 marin~ lined surgeo~ actino~ perci~ acanth~ acan~ lineat~ direct obser~ <NA> 
##  2 marin~ orangespine ~ actino~ perci~ acanth~ naso  litura~ telemetry     8    
##  3 marin~ bluespine un~ actino~ perci~ acanth~ naso  unicor~ telemetry     7    
##  4 marin~ redlip blenny actino~ perci~ blenni~ ophi~ atlant~ direct obser~ 20   
##  5 marin~ bermuda chub  actino~ perci~ kyphos~ kyph~ sectat~ telemetry     11   
##  6 marin~ cherubfish    actino~ perci~ pomaca~ cent~ argi    direct obser~ <NA> 
##  7 marin~ damselfish    actino~ perci~ pomace~ chro~ chromis direct obser~ <NA> 
##  8 marin~ twinspot dam~ actino~ perci~ pomace~ chry~ biocel~ direct obser~ 18   
##  9 marin~ wards damsel  actino~ perci~ pomace~ poma~ wardi   direct obser~ <NA> 
## 10 marin~ australian g~ actino~ perci~ pomace~ steg~ apical~ direct obser~ <NA> 
## # ... with 217 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <chr>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```

```r
carni<-filter(homerange,trophic.guild == "carnivore")
carni
```

```
## # A tibble: 342 x 24
##    taxon   common.name   class   order  family genus species primarymethod N    
##    <fct>   <chr>         <chr>   <fct>  <chr>  <chr> <chr>   <chr>         <chr>
##  1 lake f~ american eel  actino~ angui~ angui~ angu~ rostra~ telemetry     16   
##  2 river ~ blacktail re~ actino~ cypri~ catos~ moxo~ poecil~ mark-recaptu~ <NA> 
##  3 river ~ central ston~ actino~ cypri~ cypri~ camp~ anomal~ mark-recaptu~ 20   
##  4 river ~ rosyside dace actino~ cypri~ cypri~ clin~ fundul~ mark-recaptu~ 26   
##  5 river ~ longnose dace actino~ cypri~ cypri~ rhin~ catara~ mark-recaptu~ 17   
##  6 river ~ muskellunge   actino~ esoci~ esoci~ esox  masqui~ telemetry     5    
##  7 marine~ pollack       actino~ gadif~ gadid~ poll~ pollac~ telemetry     2    
##  8 marine~ saithe        actino~ gadif~ gadid~ poll~ virens  telemetry     2    
##  9 marine~ giant treval~ actino~ perci~ caran~ cara~ ignobi~ telemetry     4    
## 10 lake f~ rock bass     actino~ perci~ centr~ ambl~ rupest~ mark-recaptu~ 16   
## # ... with 332 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <chr>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
carni_hra<-carni$mean.hra.m2
mean(carni_hra, na.rm = T)
```

```
## [1] 13039918
```

```r
herbi_hra <-herbi$mean.hra.m2
mean(herbi_hra, na.rm=T)
```

```
## [1] 34137012
```
Herbivores have a larger mean than the carnivores

**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  

```r
deer <- select(homerange, "family", "genus", "species", "mean.mass.g", "log10.mass")
deer <- filter(deer, family=="cervidae")
deer
```

```
## # A tibble: 12 x 5
##    family   genus      species     mean.mass.g log10.mass
##    <chr>    <chr>      <chr>             <dbl>      <dbl>
##  1 cervidae alces      alces           307227.       5.49
##  2 cervidae axis       axis             62823.       4.80
##  3 cervidae capreolus  capreolus        24050.       4.38
##  4 cervidae cervus     elaphus         234758.       5.37
##  5 cervidae cervus     nippon           29450.       4.47
##  6 cervidae dama       dama             71450.       4.85
##  7 cervidae muntiacus  reevesi          13500.       4.13
##  8 cervidae odocoileus hemionus         53864.       4.73
##  9 cervidae odocoileus virginianus      87884.       4.94
## 10 cervidae ozotoceros bezoarticus      35000.       4.54
## 11 cervidae pudu       puda              7500.       3.88
## 12 cervidae rangifer   tarandus        102059.       5.01
```

```r
arrange(deer,log10.mass)
```

```
## # A tibble: 12 x 5
##    family   genus      species     mean.mass.g log10.mass
##    <chr>    <chr>      <chr>             <dbl>      <dbl>
##  1 cervidae pudu       puda              7500.       3.88
##  2 cervidae muntiacus  reevesi          13500.       4.13
##  3 cervidae capreolus  capreolus        24050.       4.38
##  4 cervidae cervus     nippon           29450.       4.47
##  5 cervidae ozotoceros bezoarticus      35000.       4.54
##  6 cervidae odocoileus hemionus         53864.       4.73
##  7 cervidae axis       axis             62823.       4.80
##  8 cervidae dama       dama             71450.       4.85
##  9 cervidae odocoileus virginianus      87884.       4.94
## 10 cervidae rangifer   tarandus        102059.       5.01
## 11 cervidae cervus     elaphus         234758.       5.37
## 12 cervidae alces      alces           307227.       5.49
```
The largest deer is the genus alces


**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**    

```r
snakes <- filter(homerange, taxon=="snakes")
arrange(snakes,mean.hra.m2)
```

```
## # A tibble: 41 x 24
##    taxon  common.name   class  order  family genus  species  primarymethod N    
##    <fct>  <chr>         <chr>  <fct>  <chr>  <chr>  <chr>    <chr>         <chr>
##  1 snakes namaqua dwar~ repti~ squam~ viper~ bitis  schneid~ telemetry     11   
##  2 snakes eastern worm~ repti~ squam~ colub~ carph~ viridis  radiotag      10   
##  3 snakes butlers gart~ repti~ squam~ colub~ thamn~ butleri  mark-recaptu~ 1    
##  4 snakes western worm~ repti~ squam~ colub~ carph~ vermis   radiotag      1    
##  5 snakes snubnosed vi~ repti~ squam~ viper~ vipera latastei telemetry     7    
##  6 snakes chinese pit ~ repti~ squam~ viper~ gloyd~ shedaoe~ telemetry     16   
##  7 snakes ringneck sna~ repti~ squam~ colub~ diado~ punctat~ mark-recaptu~ <NA> 
##  8 snakes cottonmouth   repti~ squam~ viper~ agkis~ piscivo~ telemetry     15   
##  9 snakes redbacked ra~ repti~ squam~ colub~ oocat~ rufodor~ telemetry     21   
## 10 snakes gopher snake  repti~ squam~ colub~ pituo~ catenif~ telemetry     4    
## # ... with 31 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <chr>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```
The namaqua dwarf adder has the smallest homerange. It is the smallest adder in the world measuring about 20 cm in length. It is greyish-brown in color and burrows itself in the sand with only the top of its head and its eyes exposed in order to strike its prey. They are most active during the day time. 

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
