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

The data for our group project is sourced from the OECD, specifically from two datasets: “Annual Real GDP Growth - OECD and Non-OECD Countries” and “Annual GDP and Consumption Per Capita - OECD and Non-OECD Countries.”
The first dataset provides annual GDP growth figures for OECD member states and selected non-member countries covering the years 2018-2024, while the second dataset reports GDP and consumption per capita over the same period. Together, these datasets allow us to analyze how different nations recovered economically following the severe disruptions of the COVID-19 pandemic. The selected time frame enables us to trace economic trajectories before, during, and after the pandemic, helping us understand both the immediate impact and the long-term recovery patterns.

After data cleaning, our combined dataset contains fewer than 500 data points, with x observations and x variables. We excluded large economic blocs such as the EU or G7 to focus exclusively on national-level performance and to avoid potential data overlap. For our analysis, we will focus on four countries: the United States, Denmark, South Africa, and India. Two of these nations are OECD members, while the other two are not. This is a deliberate choice to highlight contrasts between advanced and emerging economies. 

Moreover, we plan to add a few additional variables to our dataset by categorizing the levels of economic recovery into performance groups. These categories may include classifications such as stagnating, recovering, and booming. This transformation will allow us to better visualize and compare how selected countries performed during the post-Covid recovery period, providing clearer insights into the relative strength and pace of their economic rebounds.

For this project, our research focuses on the varying levels of economic recovery around the world following the COVID-19 pandemic. We aim to closely examine the observations in our datasets to identify potential patterns (such as geographic or regional trends) that reveal which countries recovered quickly and which continued to face significant challenges. 
Some of the questions we hope to explore include: 

* Are there identifiable geographic patterns indicating which countries were more effective in rebounding economically? 
* How much did the average year-on-year GDP growth rates vary across countries and regions, and were there any notable outliers?
* What factors might explain why some countries recovered more successfully than others? We plan to compare and analyze selected countries. 
* How can we meaningfully categorize countries into groups such as stagnating, recovering, and booming, and what does the global distribution of these categories reveal about overall recovery trends?
* Among our four selected economies, which performed best, and what key drivers contributed to their relative success?


## 2. Data

``` r
GDP_Data <- read_excel("/cloud/project/data/Annual_GDP_Growth_OECD_and_non_OECD.xlsx")

GDP_Per_Capita <- read_excel("/cloud/project/data/Annual GDP Per Capita OECD and Non-OECD.xlsx.xlsx")
```

``` r
# View(Annual_GDP_Growth_OECD_and_non_OECD)

# View(Annual_GDP_Per_Capita_OECD_and_Non_OECD_xlsx)
```

``` r
dim(GDP_Data)
```

    ## [1] 47  8

``` r
dim(GDP_Per_Capita)
```

    ## [1] 47   9

``` r
glimpse(GDP_Data)
```

    ## Rows: 47    
    ## Columns: 8
    ## $ `Time period` <chr> "Country", "Australia", "Austria", "Belgium", "Canada", "Chile", "Colombia", "Costa Rica", "Czechi…
    ## $ `2018`        <dbl> NA, 2.8349175, 2.4842210, 1.8779685, 2.7429634, 3.9900295, 2.5643243, 2.6159044, 2.8303059, 1.8600…
    ## $ `2019`        <dbl> NA, 1.9154753, 1.7549763, 2.4428900, 1.9084319, 0.6343675, 3.1868554, 2.4175118, 3.5657766, 1.7113…
    ## $ `2020`        <dbl> NA, -2.01405865, -6.31825516, -4.79296338, -5.03823342, -6.14347479, -7.18591414, -4.27335432, -5.…
    ## $ `2021`        <chr> NA, "5.4441441719999997", "4.923091748", "6.2544339530000004", "5.9505280410000001", "11.314920488…
    ## $ `2022`        <chr> NA, "4.1186485880000001", "5.3309725969999997", "3.9562582700000002", "4.5574855740000002", "2.153…
    ## $ `2023`        <chr> NA, "2.0248715439999998", "-0.78624417999999996", "1.7141216210000001", "1.7531137960000001", "0.5…
    ## $ `2024`        <chr> NA, "1.0669975759999999", "-0.65908973800000004", "1.070626659", "0.97378519100000005", "2.6443115…


``` r
glimpse(GDP_Per_Capita)
```

    ## Rows: 47
    ## Columns: 9
    ## $ `Time period` <chr> "Country", "Australia", "Austria", "Belgium", "Canada", "Chile", "Colombia", "Costa Rica", "Czechi…
    ## $ ...2          <chr> "Combined unit of measure", "US dollars per person, PPP converted", "US dollars per person, PPP co…
    ## $ `2018`        <dbl> NA, 53051.72, 56654.55, 52466.55, 49982.65, 25496.43, 15814.70, 21312.71, 42016.46, 57231.33, 3720…
    ## $ `2019`        <dbl> NA, 53602.04, 60370.46, 56712.36, 50498.96, 25733.10, 16712.41, 23082.52, 46139.56, 60568.74, 4065…
    ## $ `2020`        <dbl> NA, 56821.62, 58522.84, 56119.62, 48590.72, 25236.62, 15950.51, 21778.79, 45675.06, 62700.58, 4069…
    ## $ `2021`        <chr> NA, "65002.659138000003", "62998.849713000003", "60668.644834999999", "56995.206995", "28761.63259…
    ## $ `2022`        <chr> NA, "72576.307081000006", "70865.595503999997", "68157.888133999993", "63578.297725999997", "30392…
    ## $ `2023`        <chr> NA, "73401.167048000003", "71173.472523999997", "69102.712924000007", "64462.933943999997", "32305…
    ## $ `2024`        <chr> NA, "73888.300352999999", "73427.587778000001", "72289.394943000007", "65532.718214", "34082.53673…

```r
glimpse(gdp_growth_long)
```

    ## Rows: 322
    ## Columns: 3
    ## $ Year       <int> 2018, 2019, 2020, 2021, 2022, 2023, 2024, 2018, 2019, 2020, 2021, 2022, 2023, 2024, 2018, 2019, 2020,…
    ## $ GDP_Growth <dbl> 2.8349175, 1.9154753, -2.0140586, 5.4441442, 4.1186486, 2.0248715, 1.0669976, 2.4842210, 1.7549763, -…
    ## $ Country    <chr> "Australia", "Australia", "Australia", "Australia", "Australia", "Australia", "Australia", "Austria",…

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
names(GDP_Data)
```

    ## [1] "Time period" "2018"        "2019"        "2020"        "2021"        "2022"        "2023"        "2024"       

``` r
names(GDP_Per_Capita)
```

    ## [1] "Time period" "...2"        "2018"        "2019"        "2020"        "2021"        "2022"        "2023"       
    ## [9] "2024"       
