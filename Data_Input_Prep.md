Data\_Loading\_Preparation
================
Daniela Quigee (dq2147)
6/16/2020

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.1     ✓ dplyr   1.0.0
    ## ✓ tidyr   1.1.0     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
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

# Reading in Year 2015
data_2015_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2015.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2014
data_2014_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2014.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2013
data_2013_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2013.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2012
data_2012_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2012.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2011
data_2011_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2011.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2010
data_2010_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2010.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2009
data_2009_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2009.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2008
data_2008_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2008.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2007
data_2007_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2007.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2006
data_2006_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2006.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2005
data_2005_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2005.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()

# Reading in Year 2004
data_2004_clearance = read_excel("data/Clearance_Rates_By_Region/Clearance_Rates_By_Region_2004.xlsx", range = "A1:I14") %>% 
  janitor::clean_names()



# Combing different years
data_clearance_region = bind_rows(
  data_2018_clearance,
  data_2017_clearance,
  data_2015_clearance,
  data_2014_clearance,
  data_2013_clearance,
  data_2012_clearance,
  data_2011_clearance,
  data_2010_clearance,
  data_2009_clearance,
  data_2008_clearance,
  data_2007_clearance,
  data_2006_clearance,
  data_2005_clearance,
  data_2004_clearance)
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

# Murder Weapons Distribution By State

``` r
########## Murder - Weapon - 2018 #####################
data_murder_weapon_2018 = read_excel("data/Murder_Weapons_By_State/Murder_Weapons_By_State_2018.xlsx", range = "A1:J52") %>% janitor::clean_names()

murder_2018_total = data_state_2018 %>% 
  select(state, state_code, murder_and_nonnegligent_manslaughter)

data_murder_weapon_2018 = left_join(
  data_murder_weapon_2018, 
  murder_2018_total,
  by = "state")

data_murder_weapon_2018 = data_murder_weapon_2018 %>% 
  mutate(
    no_info_on_weapon = murder_and_nonnegligent_manslaughter - total_number_of_murders_with_weapon_info) %>% 
  select(state, state_code, year, total_number_of_murder = murder_and_nonnegligent_manslaughter, total_number_of_murders_with_weapon_info, no_info_on_weapon, everything())


########## Murder - Weapon - 2017 #####################
data_murder_weapon_2017 = read_excel("data/Murder_Weapons_By_State/Murder_Weapons_By_State_2017.xlsx", range = "A1:J52") %>% janitor::clean_names()

murder_2017_total = data_state_2017 %>% 
  select(state, state_code, murder_and_nonnegligent_manslaughter)

data_murder_weapon_2017 = left_join(
  data_murder_weapon_2017, 
  murder_2017_total,
  by = "state")

data_murder_weapon_2017 = data_murder_weapon_2017 %>% 
  mutate(
    no_info_on_weapon = murder_and_nonnegligent_manslaughter - total_number_of_murders_with_weapon_info) %>% 
  select(state, state_code, year, total_number_of_murder = murder_and_nonnegligent_manslaughter, total_number_of_murders_with_weapon_info, no_info_on_weapon, everything())


########## Murder - Weapon - 2016 #####################
data_murder_weapon_2016 = read_excel("data/Murder_Weapons_By_State/Murder_Weapons_By_State_2016.xlsx", range = "A1:J52") %>% janitor::clean_names()

murder_2016_total = data_state_2016 %>% 
  select(state, state_code, murder_and_nonnegligent_manslaughter)

data_murder_weapon_2016 = left_join(
  data_murder_weapon_2016, 
  murder_2016_total,
  by = "state")

data_murder_weapon_2016 = data_murder_weapon_2016 %>% 
  mutate(
    no_info_on_weapon = murder_and_nonnegligent_manslaughter - total_number_of_murders_with_weapon_info) %>% 
  select(state, state_code, year, total_number_of_murder = murder_and_nonnegligent_manslaughter, total_number_of_murders_with_weapon_info, no_info_on_weapon, everything())


########## Murder - Weapon - 2015 #####################
data_murder_weapon_2015 = read_excel("data/Murder_Weapons_By_State/Murder_Weapons_By_State_2015.xlsx", range = "A1:J52") %>% janitor::clean_names()

murder_2015_total = data_state_2015 %>% 
  select(state, state_code, murder_and_nonnegligent_manslaughter)

data_murder_weapon_2015 = left_join(
  data_murder_weapon_2015, 
  murder_2015_total,
  by = "state")

data_murder_weapon_2015 = data_murder_weapon_2015 %>% 
  mutate(
    no_info_on_weapon = murder_and_nonnegligent_manslaughter - total_number_of_murders_with_weapon_info) %>% 
  select(state, state_code, year, total_number_of_murder = murder_and_nonnegligent_manslaughter, total_number_of_murders_with_weapon_info, no_info_on_weapon, everything())


########## Murder - Weapon - 2014 #####################
data_murder_weapon_2014 = read_excel("data/Murder_Weapons_By_State/Murder_Weapons_By_State_2014.xlsx", range = "A1:J52") %>% janitor::clean_names()

murder_2014_total = data_state_2014 %>% 
  select(state, state_code, murder_and_nonnegligent_manslaughter)

data_murder_weapon_2014 = left_join(
  data_murder_weapon_2014, 
  murder_2014_total,
  by = "state")

data_murder_weapon_2014 = data_murder_weapon_2014 %>% 
  mutate(
    no_info_on_weapon = murder_and_nonnegligent_manslaughter - total_number_of_murders_with_weapon_info) %>% 
  select(state, state_code, year, total_number_of_murder = murder_and_nonnegligent_manslaughter, total_number_of_murders_with_weapon_info, no_info_on_weapon, everything())


########## Murder - Weapon - 2013 #####################
data_murder_weapon_2013 = read_excel("data/Murder_Weapons_By_State/Murder_Weapons_By_State_2013.xlsx", range = "A1:J52") %>% janitor::clean_names()

murder_2013_total = data_state_2013 %>% 
  select(state, state_code, murder_and_nonnegligent_manslaughter)

data_murder_weapon_2013 = left_join(
  data_murder_weapon_2013, 
  murder_2013_total,
  by = "state")

data_murder_weapon_2013 = data_murder_weapon_2013 %>% 
  mutate(
    no_info_on_weapon = murder_and_nonnegligent_manslaughter - total_number_of_murders_with_weapon_info) %>% 
  select(state, state_code, year, total_number_of_murder = murder_and_nonnegligent_manslaughter, total_number_of_murders_with_weapon_info, no_info_on_weapon, everything())


########## Murder - Weapon - 2012 #####################
data_murder_weapon_2012 = read_excel("data/Murder_Weapons_By_State/Murder_Weapons_By_State_2012.xlsx", range = "A1:J52") %>% janitor::clean_names()

murder_2012_total = data_state_2012 %>% 
  select(state, state_code, murder_and_nonnegligent_manslaughter)

data_murder_weapon_2012 = left_join(
  data_murder_weapon_2012, 
  murder_2012_total,
  by = "state")

data_murder_weapon_2012 = data_murder_weapon_2012 %>% 
  mutate(
    no_info_on_weapon = murder_and_nonnegligent_manslaughter - total_number_of_murders_with_weapon_info) %>% 
  select(state, state_code, year, total_number_of_murder = murder_and_nonnegligent_manslaughter, total_number_of_murders_with_weapon_info, no_info_on_weapon, everything())

########## Murder - Weapon - 2011 #####################
data_murder_weapon_2011 = read_excel("data/Murder_Weapons_By_State/Murder_Weapons_By_State_2011.xlsx", range = "A1:J52") %>% janitor::clean_names()

murder_2011_total = data_state_2011 %>% 
  select(state, state_code, murder_and_nonnegligent_manslaughter)

data_murder_weapon_2011 = left_join(
  data_murder_weapon_2011, 
  murder_2011_total,
  by = "state")

data_murder_weapon_2011 = data_murder_weapon_2011 %>% 
  mutate(
    no_info_on_weapon = murder_and_nonnegligent_manslaughter - total_number_of_murders_with_weapon_info) %>% 
  select(state, state_code, year, total_number_of_murder = murder_and_nonnegligent_manslaughter, total_number_of_murders_with_weapon_info, no_info_on_weapon, everything())


# Combing different years

data_murder_weapon = bind_rows(
  data_murder_weapon_2018,
  data_murder_weapon_2017,
  data_murder_weapon_2016,
  data_murder_weapon_2015,
  data_murder_weapon_2014,
  data_murder_weapon_2013,
  data_murder_weapon_2012,
  data_murder_weapon_2011) 
```

# Crime Rates In NYC By Borough

``` r
data_NYC_crime = read_excel(
  "data/Crime_in_NYC/Crime_Data_NYC_2000_2019.xlsx",
  range = "A1:W617",
  col_types = c("numeric", "text", "text", 
                "numeric", "numeric", "numeric", 
                "numeric", "numeric", "numeric", 
                "numeric", "numeric", "numeric", 
                "numeric", "numeric", "numeric", 
                "numeric", "numeric", "numeric", 
                "numeric", "numeric", "numeric", 
                "numeric", "numeric")) %>% 
  janitor::clean_names() %>% 
  mutate(
    crime = tolower(crime)) %>% 
  select(-pct) %>% 
  filter(crime != "total seven major felony offenses") %>% 
  group_by(borough, crime) %>% 
  summarize(
    x2000 = sum(x2000),
    x2001 = sum(x2001),
    x2002 = sum(x2002),
    x2003 = sum(x2003),
    x2004 = sum(x2004),
    x2005 = sum(x2005),
    x2006 = sum(x2006),
    x2007 = sum(x2007),
    x2008 = sum(x2008),
    x2009 = sum(x2009),
    x2010 = sum(x2010),
    x2011 = sum(x2011),
    x2012 = sum(x2012),
    x2013 = sum(x2013),
    x2014 = sum(x2014),
    x2015 = sum(x2015),
    x2016 = sum(x2016),
    x2017 = sum(x2017),
    x2018 = sum(x2018),
    x2019 = sum(x2019)) %>%  
  pivot_longer(
    x2000:x2019,
    names_to = "year",
    values_to = "number",
    names_prefix = "x") 
```

    ## `summarise()` regrouping output by 'borough' (override with `.groups` argument)

``` r
data_NYC_populaton = read_excel(
  "data/Crime_in_NYC/Population_NYC_2000_2019.xlsx",
  col_types = c("text", "numeric", "numeric", 
        "numeric", "numeric", "numeric", 
        "numeric", "numeric", "numeric", 
        "numeric", "numeric", "numeric", 
        "numeric", "numeric", "numeric", 
        "numeric", "numeric", "numeric", 
        "numeric", "numeric", "numeric")) %>% 
  janitor::clean_names() %>% 
  pivot_longer(
    x2000:x2019,
    names_to = "year",
    values_to = "population",
    names_prefix = "x") 

data_NYC = left_join(data_NYC_crime, data_NYC_populaton, by = c("borough", "year"))

data_NYC = data_NYC %>% 
  mutate(
    rate_per_100_000 = round(number/(population/100000), digits = 2))


# NYC Map Data

r = GET('http://data.beta.nyc//dataset/0ff93d2d-90ba-457c-9f7e-39e47bf2ac5f/resource/35dd04fb-81b3-479b-a074-a27a37888ce7/download/d085e2f8d0b54d4590b1e7d1f35594c1pediacitiesnycneighborhoods.geojson')

nyc_map_data = readOGR(content(r,'text'), 'OGRGeoJSON', verbose = F)
```

    ## No encoding supplied: defaulting to UTF-8.

``` r
nyc_map_data_df = broom::tidy(nyc_map_data, region = "borough")
```

    ## Warning in RGEOSUnaryPredFunc(spgeom, byid, "rgeos_isvalid"): Self-intersection
    ## at or near point -73.998769409999994 40.671602049999997

    ## SpP is invalid

    ## Warning in rgeos::gUnaryUnion(spgeom = SpP, id = IDs): Invalid objects found;
    ## consider using set_RGEOS_CheckValidity(2L)

``` r
nyc_map_data_df = nyc_map_data_df %>% rename(borough = id)
```

``` r
save(data_state, file = "./data/Crime_In_US_By_State/data_state.RData")
save(data_region, file = "./data/Crime_In_US_By_Region/data_region.RData")
save(data_clearance_region, file = "./data/Clearance_Rates_By_Region/data_clearance_region.RData")
save(data_murder_weapon, file = "./data/Murder_Weapons_By_State/data_murder_weapon.RData")

save(data_NYC, file = "./data/Crime_in_NYC/data_NYC.RData")
save(nyc_map_data_df, file = "./data/Crime_in_NYC/nyc_map_data_df.RData")
```
