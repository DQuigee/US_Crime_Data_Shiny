Data\_Loading\_Preparation
================
Daniela Quigee (dq2147)
6/16/2020

``` r
library(tidyverse)
```

    ## ── Attaching packages ──────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.1     ✓ dplyr   1.0.0
    ## ✓ tidyr   1.1.0     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ─────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readxl)
library(httr)
library(rgdal)
```

    ## Loading required package: sp

    ## rgdal: version: 1.5-10, (SVN revision 1006)
    ## Geospatial Data Abstraction Library extensions to R successfully loaded
    ## Loaded GDAL runtime: GDAL 2.4.2, released 2019/06/28
    ## Path to GDAL shared files: /Library/Frameworks/R.framework/Versions/4.0/Resources/library/rgdal/gdal
    ## GDAL binary built with GEOS: FALSE 
    ## Loaded PROJ runtime: Rel. 5.2.0, September 15th, 2018, [PJ_VERSION: 520]
    ## Path to PROJ shared files: /Library/Frameworks/R.framework/Versions/4.0/Resources/library/rgdal/proj
    ## Linking to sp version:1.4-2

``` r
library(rgeos)
```

    ## rgeos version: 0.5-3, (SVN revision 634)
    ##  GEOS runtime version: 3.7.2-CAPI-1.11.2 
    ##  Linking to sp version: 1.4-1 
    ##  Polygon checking: TRUE

# Crime In US By State

``` r
# Reading in Year 2018
data_state_2018 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2018.xlsx", range = "A1:K51") %>% 
  janitor::clean_names() 

# Reading in Year 2017
data_state_2017 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2017.xlsx", range = "A1:K51") %>% 
  janitor::clean_names() 

# Reading in Year 2016
data_state_2016 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2016.xlsx", range = "A1:K51") %>% 
  janitor::clean_names() 



# Combing different years
data_state = bind_rows(
  data_state_2018,
  data_state_2017,
  data_state_2016)
```

``` r
data_state = data_state %>% 
  mutate(
    murder_and_nonnegligent_manslaughter_rate_per_100_000 = round(murder_and_nonnegligent_manslaughter/(population/100000), digits = 2),
    rape_rate_per_100_000 = round(rape/(population/100000), digits = 2),
    robbery_rate_per_100_000 = round(robbery/(population/100000), digits = 2),
    aggravated_assault_rate_per_100_000 = round(aggravated_assault/(population/100000), digits = 2),
    burglary_rate_per_100_000 = round(burglary/(population/100000), digits = 2),
    larceny_theft_rate_per_100_000 = round(larceny_theft/(population/100000), digits = 2),
    motor_vehicle_theft_rate_per_100_000 = round(motor_vehicle_theft/(population/100000),  digits = 2)) %>% 
  select(
    -murder_and_nonnegligent_manslaughter,
    -rape,
    -robbery,
    -burglary,
    -aggravated_assault,
    -larceny_theft,
    -motor_vehicle_theft,
    -population) %>% 
  pivot_longer(
    murder_and_nonnegligent_manslaughter_rate_per_100_000:motor_vehicle_theft_rate_per_100_000,
    names_to = "variable_name",
    values_to = "statistic")
```

``` r
save(data_state, file = "./data/Crime_In_US_By_State//data_state_time.RData")
```
