Data\_Loading\_Preparation
================
Daniela Quigee (dq2147)
6/16/2020

``` r
library(tidyverse)
```

    ## ── Attaching packages ────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.1     ✓ dplyr   1.0.0
    ## ✓ tidyr   1.1.0     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ───────────────────────────────────────────── tidyverse_conflicts() ──
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

# Crime Rates In US By State

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

# Reading in Year 2015
data_state_2015 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2015.xlsx", range = "A1:K51") %>% 
  janitor::clean_names() 

# Reading in Year 2014
data_state_2014 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2014.xlsx", range = "A1:K51") %>% 
  janitor::clean_names() 

# Reading in Year 2013
data_state_2013 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2013.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2012
data_state_2012 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2012.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2011
data_state_2011 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2011.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2010
data_state_2010 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2010.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2009
data_state_2009 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2009.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2008
data_state_2008 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2008.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2007
data_state_2007 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2007.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2006
data_state_2006 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2006.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2005
data_state_2005 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2005.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2004
data_state_2004 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2004.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2003
data_state_2003 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2003.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2002
data_state_2002 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2002.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2001
data_state_2001 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2001.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 2000
data_state_2000 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_2000.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()

# Reading in Year 1999
data_state_1999 = read_excel("data/Crime_In_US_By_State/Crime_In_US_By_State_1999.xlsx", range = "A1:K51") %>% 
  janitor::clean_names()



# Combing different years
data_state = bind_rows(
  data_state_2018,
  data_state_2017,
  data_state_2016,
  data_state_2015,
  data_state_2014,
  data_state_2013,
  data_state_2012,
  data_state_2011,
  data_state_2010,
  data_state_2009,
  data_state_2008,
  data_state_2007,
  data_state_2006,
  data_state_2005,
  data_state_2004,
  data_state_2003,
  data_state_2002,
  data_state_2001,
  data_state_2000,
  data_state_1999)
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

# Crime Rates In US By Region

``` r
data_region_info = read_excel("data/Crime_In_US_By_Region/Region_State.xlsx",
                              range = "A1:C101") %>% 
  janitor::clean_names()

# Reading in Year 2018
data_region_2018 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2018.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2017
data_region_2017 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2017.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2016
data_region_2016 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2016.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2015
data_region_2015 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2015.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2014
data_region_2014 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2014.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2013
data_region_2013 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2013.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2012
data_region_2012 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2012.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2011
data_region_2011 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2011.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2010
data_region_2010 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2010.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2009
data_region_2009 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2009.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2008
data_region_2008 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2008.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2007
data_region_2007 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2007.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2006
data_region_2006 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2006.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2005
data_region_2005 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2005.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 

# Reading in Year 2004
data_region_2004 = read_excel("data/Crime_In_US_By_Region/Crime_In_US_By_Region_2004.xlsx", range = "A1:Q14") %>% 
  janitor::clean_names() 


# Combing different years
data_region = bind_rows(
  data_region_2018,
  data_region_2017,
  data_region_2016,
  data_region_2015,
  data_region_2014,
  data_region_2013,
  data_region_2012,
  data_region_2011,
  data_region_2010,
  data_region_2009,
  data_region_2008,
  data_region_2007,
  data_region_2006,
  data_region_2005,
  data_region_2004)
```

``` r
data_region = data_region %>% 
  select(
    -murder_and_nonnegligent_manslaughter,
    -rape,
    -robbery,
    -burglary,
    -aggravated_assault,
    -larceny_theft,
    -motor_vehicle_theft,
    -population)
  
  
# Long-Format for the Data 
data_region = pivot_longer(
  data_region,
  murder_and_nonnegligent_manslaughter_rate_per_100_000:motor_vehicle_theft_rate_per_100_000,
  names_to = "variable_name",
  values_to = "statistic")

# Including Region-State info
data_region = left_join(data_region_info, data_region, by = "region")
```

# Clearance Rates In US By Region

``` r
# Reading in Year 2018
data_2018_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2018.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2017
data_2017_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2017.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()



# Combing different years
data_clearance_region = bind_rows(
  data_2018_clearance,
  data_2017_clearance)
```

``` r
# Long-Format for the Data 
data_clearance_region = pivot_longer(
  data_clearance_region,
  murder_and_nonnegligent_manslaugther_percent_cleared_by_arrest:motor_vehicle_theft_percent_cleared_by_arrest,
  names_to = "variable_name",
  values_to = "percent_cleared_by_arrest")

# Including Region-State info
data_clearance_region = left_join(data_region_info, data_clearance_region, by = "region")
```

``` r
save(data_state, file = "./data/Crime_In_US_By_State/data_state.RData")
save(data_region, file = "./data/Crime_In_US_By_Region/data_region.RData")
save(data_clearance_region, file = "./data/Clearance_Rates_By_Region/data_clearance_region.RData")
```
