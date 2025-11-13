Project proposal
================
AJJ: Armin, Jiwon, Jamari

``` r
library(tidyverse)
library(broom)
library(readxl)
library(dplyr)
```

## 1. Introduction

The data used in our group project is sourced from the OECD,
specifically from the dataset “Quarterly Real GDP Growth – OECD
Countries.” This dataset provides quarterly GDP growth figures for OECD
member nations, covering the period from 2018 Q2 to 2025 Q2. The purpose
of collecting this data is to examine how nations recovered economically
following the devastating impacts of the COVID-19 pandemic, with a
particular focus on comparing the varying degrees of recovery across
countries.

Our dataset from the OECD contains 1,523 data points, 31 variables, and
54 observations. We plan to exclude the “Non-OECD economies” observation
since it contains no data. To fill this gap, our team is considering
incorporating an additional dataset from the World Bank Group, which
tracks GDP growth for both OECD and non-OECD countries. This will allow
us to develop a more comprehensive and comparative view of national
economic performance. We plan to later narrow in on 4 countries: USA,
Denmark, South Africa, and India. We will analyze their economic
performance and compare it to global post-covid performance.

Moreover, we plan to add a few additional variables to our dataset by
categorizing the levels of economic recovery into performance groups.
These categories may include classifications such as stagnating,
recovering, and booming. This transformation will allow us to better
visualize and compare how different countries performed during the
post-Covid recovery period, providing clearer insights into the relative
strength and pace of their economic rebounds.

For this project, our research focuses on the varying levels of economic
recovery around the world following the COVID-19 pandemic. We aim to
closely examine the observations in our dataset to identify potential
patterns (such as geographic or regional trends) that reveal which
countries recovered quickly and which continued to face significant
challenges.

Some of the questions we hope to explore include:

- Are there clear geographic patterns indicating which countries were
  more effective in rebounding economically?
- How much did the average year-on-year GDP growth rates vary across
  countries and continents, and were there any notable outliers?
- What factors might explain why some countries recovered more
  successfully than others? We plan to compare and analyze selected
  countries.
- How can we categorize countries into groups such as stagnating,
  recovering, and booming, and what does the global distribution of
  these categories reveal about overall recovery trends?

## 2. Data

``` r
GDP_Growth_Clean_Concise_Dataset_2018_2024_Annual <- read_excel("/cloud/project/data/GDP Growth - Clean Concise Dataset 2018-2024 Annual.xlsx")
# View(GDP_Growth_Clean_Concise_Dataset_2018_2024_Annual)
World_Bank_Clean_Dataset <- read_csv("/cloud/project/data/World Bank - Clean Dataset.csv")
```

    ## New names:
    ## • `` -> `...3`
    ## • `` -> `...4`
    ## • `` -> `...5`
    ## • `` -> `...6`
    ## • `` -> `...7`
    ## • `` -> `...8`
    ## • `` -> `...9`

    ## Warning: One or more parsing issues, call `problems()` on your data frame for details,
    ## e.g.:
    ##   dat <- vroom(...)
    ##   problems(dat)

    ## Rows: 278 Columns: 9
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (3): Data Source, World Development Indicators, ...3
    ## dbl (6): ...4, ...5, ...6, ...7, ...8, ...9
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# View(World_Bank_Clean_Dataset)
```

``` r
dim(GDP_Growth_Clean_Concise_Dataset_2018_2024_Annual)
```

    ## [1] 54  8

``` r
dim(World_Bank_Clean_Dataset)
```

    ## [1] 278   9

``` r
glimpse(GDP_Growth_Clean_Concise_Dataset_2018_2024_Annual)
```

    ## Rows: 54
    ## Columns: 8
    ## $ `Time period` <chr> "Country", "Australia", "Austria", "Belgium", "Canada", …
    ## $ `2018`        <dbl> NA, 2.8349175, 2.4842210, 1.8779685, 2.7429634, 3.990029…
    ## $ `2019`        <dbl> NA, 1.9154753, 1.7549763, 2.4428900, 1.9084319, 0.634367…
    ## $ `2020`        <dbl> NA, -2.01405865, -6.31825516, -4.79296338, -5.03823342, …
    ## $ `2021`        <dbl> NA, 5.444144, 4.923092, 6.254434, 5.950528, 11.314920, 1…
    ## $ `2022`        <dbl> NA, 4.1186486, 5.3309726, 3.9562583, 4.5574856, 2.153993…
    ## $ `2023`        <dbl> NA, 2.02487154, -0.78624418, 1.71412162, 1.75311380, 0.5…
    ## $ `2024`        <dbl> NA, 1.06699758, -0.65908974, 1.07062666, 0.97378519, 2.6…

``` r
glimpse(World_Bank_Clean_Dataset)
```

    ## Rows: 278
    ## Columns: 9
    ## $ `Data Source`                  <chr> "<<<<<<< HEAD", NA, "Last Updated Date"…
    ## $ `World Development Indicators` <chr> NA, NA, "10/7/2025", NA, NA, "10/7/25",…
    ## $ ...3                           <chr> NA, NA, NA, NA, NA, NA, NA, "Indicator …
    ## $ ...4                           <dbl> NA, NA, NA, NA, NA, NA, NA, 2019.000000…
    ## $ ...5                           <dbl> NA, NA, NA, NA, NA, NA, NA, 2020.000000…
    ## $ ...6                           <dbl> NA, NA, NA, NA, NA, NA, NA, 2021.000000…
    ## $ ...7                           <dbl> NA, NA, NA, NA, NA, NA, NA, 2022.000000…
    ## $ ...8                           <dbl> NA, NA, NA, NA, NA, NA, NA, 2023.000000…
    ## $ ...9                           <dbl> NA, NA, NA, NA, NA, NA, NA, 2024.000000…

## 3. Data analysis plan

The variables we will be visualizing to explore our research question
are the following:

- GDP_growth: Core measure of economic recovery; allows comparison
  across countries and time.
- Quarter: Time-series analysis to see trends over time between 2018 Q2
  to 2025 Q2.
- Country: Compare recovery across nations and regions.
- Recovery_category: Helps visualize and compare group-level
  performance; categorized as “Stagnating,” “Recovering,” “Booming”.
- Continent/region: Explore geographic patterns in recovery

Other additional data we may explore are datasets which will categorize
the levels of economic recovery from COVID-19 into performance groups.
These categories may include classifications such as stagnating,
recovering, and booming. This transformation will allow us to better
visualize and compare how different countries performed during the
post-Covid recovery period, providing clearer insights into the relative
strength and pace of their economic rebounds.

- Very preliminary exploratory data analysis, including some summary
  statistics and visualizations, along with some explanation on how they
  help you learn more about your data. (You can add to these later as
  you work on your project.)

- The data visualization(s) that you believe will be useful in exploring
  your question(s).

``` r
names(GDP_Growth_Clean_Concise_Dataset_2018_2024_Annual)
```

    ## [1] "Time period" "2018"        "2019"        "2020"        "2021"       
    ## [6] "2022"        "2023"        "2024"

``` r
names(World_Bank_Clean_Dataset)
```

    ## [1] "Data Source"                  "World Development Indicators"
    ## [3] "...3"                         "...4"                        
    ## [5] "...5"                         "...6"                        
    ## [7] "...7"                         "...8"                        
    ## [9] "...9"
