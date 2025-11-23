Project proposal
================
AJJ: Armin, Jiwon, Jamari

``` r
library(tidyverse)
library(broom)
library(readxl)
library(dplyr)
library(ggplot2)
library(ggrepel)
library(gganimate)  
library(scales)  
```

``` r
# install.packages("gganimate")
# install.packages("gifski")
# install.packages("png")
```

## 1. Introduction

The data for our group project is sourced from the OECD, specifically
from two sources: “Annual Real GDP Growth - OECD and Non-OECD Countries”
and “Annual GDP and Consumption Per Capita - OECD and Non-OECD
Countries.” The first dataset provides annual GDP growth figures for
OECD member states and selected non-member countries covering the years
2018-2024, while the second dataset reports GDP and consumption per
capita over the same period. Together, these datasets allow us to
analyze how different nations recovered economically following the
severe disruptions of the COVID-19 pandemic. The selected time frame
enables us to trace economic trajectories before, during, and after the
pandemic, helping us understand both the immediate impact and the
long-term recovery patterns.

After data cleaning, our datasets contained fewer than 750 combined data
points, with 46 observations and 8 variables in each initial dataset,
before further changes were made down the line. We excluded large
economic blocs such as the EU or G7 to focus exclusively on
national-level performance and to avoid potential data overlap. For our
analysis, we will focus primarily on four countries: the United States,
Denmark, South Africa, and India. Two of these nations are OECD members,
while the other two are not. This is a deliberate choice to highlight
contrasts between advanced and emerging economies.

Moreover, we plan to add a few additional variables to our dataset by
categorizing the levels of economic recovery into performance groups.
These categories may include classifications such as recovering and
booming. This transformation will allow us to better visualize and
compare how selected countries performed during the post-Covid recovery
period, providing clearer insights into the relative strength and pace
of their economic rebounds.

For this project, our research focuses on the varying levels of economic
recovery around the world following the COVID-19 pandemic. We aim to
closely examine the observations in our datasets to identify potential
patterns (such as geographic or regional trends) that reveal which
countries recovered quickly and which continued to face significant
challenges. Some of the questions we hope to explore include:

- Are there identifiable geographic patterns indicating which countries
  were more effective in rebounding economically?
- How much did the average year-on-year GDP growth rates vary across
  countries and regions, and were there any notable outliers?
- What factors might explain why some countries recovered more
  successfully than others? We plan to compare and analyze selected
  countries.
- How can we meaningfully categorize countries into groups such as
  recovering and booming, and what does the global distribution of these
  categories reveal about overall recovery trends?
- Among our four selected economies, which performed best, and what key
  drivers contributed to their relative success?

## 2. Data

``` r
GDP_Data <- read_excel("/cloud/project/data/Annual_GDP_Growth_OECD_and_non_OECD.xlsx")
# View(GDP_Data)

GDP_Per_Capita <- read_excel("/cloud/project/data/Annual GDP Per Capita OECD and Non-OECD.xlsx.xlsx")
# View(GDP_Per_Capita)
```

``` r
dim(GDP_Data)
```

    ## [1] 47  8

``` r
dim(GDP_Per_Capita)
```

    ## [1] 47  9

``` r
glimpse(GDP_Data)
```

    ## Rows: 47
    ## Columns: 8
    ## $ `Time period` <chr> "Country", "Australia", "Austria", "Belgium", "Canada", …
    ## $ `2018`        <dbl> NA, 2.8349175, 2.4842210, 1.8779685, 2.7429634, 3.990029…
    ## $ `2019`        <dbl> NA, 1.9154753, 1.7549763, 2.4428900, 1.9084319, 0.634367…
    ## $ `2020`        <dbl> NA, -2.01405865, -6.31825516, -4.79296338, -5.03823342, …
    ## $ `2021`        <chr> NA, "5.4441441719999997", "4.923091748", "6.254433953000…
    ## $ `2022`        <chr> NA, "4.1186485880000001", "5.3309725969999997", "3.95625…
    ## $ `2023`        <chr> NA, "2.0248715439999998", "-0.78624417999999996", "1.714…
    ## $ `2024`        <chr> NA, "1.0669975759999999", "-0.65908973800000004", "1.070…

``` r
glimpse(GDP_Per_Capita)
```

    ## Rows: 47
    ## Columns: 9
    ## $ `Time period` <chr> "Country", "Australia", "Austria", "Belgium", "Canada", …
    ## $ ...2          <chr> "Combined unit of measure", "US dollars per person, PPP …
    ## $ `2018`        <dbl> NA, 53051.72, 56654.55, 52466.55, 49982.65, 25496.43, 15…
    ## $ `2019`        <dbl> NA, 53602.04, 60370.46, 56712.36, 50498.96, 25733.10, 16…
    ## $ `2020`        <dbl> NA, 56821.62, 58522.84, 56119.62, 48590.72, 25236.62, 15…
    ## $ `2021`        <chr> NA, "65002.659138000003", "62998.849713000003", "60668.6…
    ## $ `2022`        <chr> NA, "72576.307081000006", "70865.595503999997", "68157.8…
    ## $ `2023`        <chr> NA, "73401.167048000003", "71173.472523999997", "69102.7…
    ## $ `2024`        <chr> NA, "73888.300352999999", "73427.587778000001", "72289.3…

``` r
names(GDP_Data)
```

    ## [1] "Time period" "2018"        "2019"        "2020"        "2021"       
    ## [6] "2022"        "2023"        "2024"

``` r
names(GDP_Per_Capita)
```

    ## [1] "Time period" "...2"        "2018"        "2019"        "2020"       
    ## [6] "2021"        "2022"        "2023"        "2024"

## 3. Data analysis plan

The variables we will be visualizing to explore our research question
are the following:

- GDP_growth: Core measure of economic recovery; allows comparison
  across countries and time.
- GDP_Per_Capita: Core measure of economic recovery per person within a
  geographich region; allows comparison across countries and time.
- Timeline: Time-series analysis to see trends over time between 2018 to
  2024.
- Country: Compare recovery across nations and regions.
- Recovery_category: Helps visualize and compare group-level
  performance; categorized as “Recovering” and “Booming”.
- Continent/region: Explore geographic patterns in recovery

Other additional data we may explore are datasets which will categorize
the levels of economic recovery from COVID-19 into performance groups.
These categories may include classifications such as recovering and
booming. This transformation will allow us to better visualize and
compare how different countries performed during the post-Covid recovery
period, providing clearer insights into the relative strength and pace
of their economic rebounds.

Our goal for the project is to examine the differences in economic
recovery across OECD countries from the COVID-19 pandemic. We will
observe using GDP growth data ranging from 2018 to 2024, as well as
measuring GDP Per Capita data during the same time period. Our view
comes from different statistics which categorize countries that
experienced the fastest and most sustained economic recoveries.

We’ll start with exploratory data analysis to help us understand trends
and the structure of our dataset. We’ll summarize tendencies, and other
important information the dataset provides. Once we understand the
dataset, then we’ll begin to visualize and explore the recovery patterns
within the time period, while distinguishing geography, and economics.

- GDP_growth: GDP growth is the variable representing the annual
  percentage change. It is the main measure of economic recovery, and
  allows us to compare within countries and time periods.

- GDP_Per_Capita: GDP Per Capita is the variable representing the annual
  GDP percentage change per individual in a geographic region. It is one
  of the main measures of economic recovery, and allows us to compare
  within countries and time periods. It provides a similar, yet slightly
  different metric to just GDP growth by additionally exploring how
  citizens’ wealth grew over the selected time period.

- Timeline: The dataset starts in 2018 to 2024, which gives us
  information on GDP before, during, and after the pandemic. Looking at
  the times before and present day will directly provide us with the
  recovery time and sustainability.

- Country: We’ll use this variable to compare the economic recoveries
  across nations. Differences can range due to policies or resource
  factors that may limit a nation’s growth or have it thrive.

- Recovery_category: We’ll classify countries as Recovering or Booming
  based on their post pandemic GDP growth averages. This will allow us
  to visualise and for our group to make an analysis.

- Continent/Region: From this we’ll be able to identify patterns from
  different regions, and how different regions were affected and able to
  recover faster/slower.

Exploratory Data Analysis:

We’ll start by cleaning the dataset by removing unnecessary information
and converting the dataset to quarterly time. Then we’ll identify
countries with the highest/lowest GDP growth past the pandemic. We can
do this by using histograms and boxplots to identify outliers in the
dataset. Lastly, we’ll summarize the dataset. We’ll show who had the
strongest recovery post pandemic, and how consistent the patterns were
within each region:

``` r
names(GDP_Per_Capita)[1] <- "Country"
```

``` r
# make all column names characters  
names(GDP_Data) <-
  as.character(names(GDP_Data))

# convert all "year" columns (2018–2024) to characters before pivoting
GDP_Data <-
  GDP_Data %>%
  mutate(across(matches("^20"), as.character))

# pivot longer using the original "Time Period" column  
gdp_growth_long <- GDP_Data %>%
  pivot_longer(
    cols = matches("^20"),       # selects 2018–2024 columns
    names_to = "Year",
    values_to = "GDP_Growth"
  ) %>%
  mutate(
    Year = as.integer(Year),     # turn "2018" → 2018
     GDP_Growth = as.numeric(GDP_Growth),
    Country = `Time period`
  ) %>%
  select(-`Time period`)

gdp_growth_long <- gdp_growth_long %>%
  filter(Country != "Country")

GDP_Per_Capita <- GDP_Per_Capita %>%
  filter(str_trim(Country) != "Country") %>%
  select(-2)

glimpse(gdp_growth_long)
```

    ## Rows: 322
    ## Columns: 3
    ## $ Year       <int> 2018, 2019, 2020, 2021, 2022, 2023, 2024, 2018, 2019, 2020,…
    ## $ GDP_Growth <dbl> 2.8349175, 1.9154753, -2.0140586, 5.4441442, 4.1186486, 2.0…
    ## $ Country    <chr> "Australia", "Australia", "Australia", "Australia", "Austra…

``` r
summary_stats <- gdp_growth_long %>%
  group_by(Year) %>%
  summarize(
    mean_growth = mean(GDP_Growth, na.rm = TRUE),
    median_growth = median(GDP_Growth, na.rm = TRUE),
    sd_growth = sd(GDP_Growth, na.rm = TRUE),
    min_growth = min(GDP_Growth, na.rm = TRUE),
    max_growth = max(GDP_Growth, na.rm = TRUE),
    .groups = "drop"
  )

print(summary_stats)
```

    ## # A tibble: 7 × 6
    ##    Year mean_growth median_growth sd_growth min_growth max_growth
    ##   <int>       <dbl>         <dbl>     <dbl>      <dbl>      <dbl>
    ## 1  2018        3.02         2.82       1.90      -2.62       7.69
    ## 2  2019        2.26         2.15       1.63      -2.00       6.1 
    ## 3  2020       -3.94        -3.84       3.50     -10.9        7.15
    ## 4  2021        6.87         6.39       2.59       2.68      16.3 
    ## 5  2022        3.92         3.71       2.58      -1.23      12.0 
    ## 6  2023        1.43         0.976      2.29      -2.74       8.83
    ## 7  2024        1.67         1.39       1.69      -1.34       6.72

``` r
post_pandemic_growth <- gdp_growth_long %>%
  filter(Year >= 2021) %>%
  group_by(`Country`) %>%
  summarize(avg_growth_post_pandemic = mean(GDP_Growth, na.rm = TRUE)) %>%
  arrange(desc(avg_growth_post_pandemic))
```

``` r
gdp_growth_long <- gdp_growth_long %>%
  mutate(`Country` = str_replace(`Country`, pattern = "·  ", replacement = ""))
```

Planned Data Visualization: - Line Plots: to represent the time
periods - Box Plots: to separate data between regions - Bar Charts: to
compare the average GDP growth by each country - Scatter Plot: to
represent the recovery time vs. GDP growth

``` r
# Filter for your four focus countries
focus_countries <- c("United States", "Denmark", "South Africa", "India")

(plot1_gdp_trends <- gdp_growth_long %>%
  filter(`Country` %in% focus_countries) %>%
  ggplot(aes(x = Year, y = GDP_Growth, color = `Country`, group = `Country`)) +
  geom_line(size = 1.2) +
  geom_point(size = 2) +
  labs(
    title = "GDP Growth Trends (2018–2024)",
    subtitle = "Tracking Pre-, During-, and Post-COVID Economic Growth",
    x = "Year",
    y = "GDP Growth (%)",
    color = "Country",
    caption = "Source: OECD Data (Annual Real GDP Growth, 2018–2024)"
  ) +
  theme_minimal(base_size = 13) +
  theme(legend.position = "bottom") + 
  scale_color_viridis_d() +
    ylim(-10, NA) +
    annotate("text", x = 2020, y = -7, label = "COVID Outbreak", color = "black", size = 4, vjust = 1.5))
```

<img src="proposal_files/figure-gfm/growth-over-time-1.png" alt="Line chart showing GDP growth for Denmark, India, South Africa, and the United States from 2018-2024. All countries have positive growth before 2020, fall sharply in 2020, then recover in 2021. India rebounds the most, nearing 10%, while the others return to low positive growth through 2024."  />

``` r
ggsave("plot1_gdp_trends.png", plot = plot1_gdp_trends, width = 7, height = 5)
plot1_gdp_trends
```

<img src="proposal_files/figure-gfm/growth-over-time-2.png" alt="Line chart showing GDP growth for Denmark, India, South Africa, and the United States from 2018-2024. All countries have positive growth before 2020, fall sharply in 2020, then recover in 2021. India rebounds the most, nearing 10%, while the others return to low positive growth through 2024."  />

``` r
post_pandemic_growth <- gdp_growth_long %>%
  filter(Year >= 2021) %>%
  group_by(`Country`) %>%
  summarize(avg_growth_post_pandemic = mean(GDP_Growth, na.rm = TRUE)) %>%
  arrange(desc(avg_growth_post_pandemic))

plot2_post_pandemic <- post_pandemic_growth %>%
  slice_max(avg_growth_post_pandemic, n = 15) %>%
  ggplot(aes(x = reorder(`Country`, avg_growth_post_pandemic), y = avg_growth_post_pandemic)) +
  geom_col(fill = "#0072B2") +
  coord_flip() +
  labs(
    title = "Top 15 Countries by GDP Growth (2021–2024)",
    subtitle = "Post-COVID Economic Recovery Strength",
    x = "Country",
    y = "GDP Growth (%)",
  ) +
  theme_minimal(base_size = 13)

ggsave("plot2_post_pandemic.png", plot = plot2_post_pandemic, width = 7, height = 5)
plot2_post_pandemic
```

<img src="proposal_files/figure-gfm/avg-post-pandemic-growth-1.png" alt="Bar chart showing the top 15 countries by average GDP growth from 2021 to 2024. Bars run horizontally with countries on the y-axis and GDP growth on the x-axis. India has the highest average growth at about 8%, followed by Türkiye, Ireland, and China near 6%, with the remaining countries showing growth between roughly 4% and 5%."  />

``` r
# Step 1: Categorize countries based on post-pandemic average growth
gdp_growth_long_cat <- gdp_growth_long %>%
  filter(Year >= 2021) %>%
  group_by(`Country`) %>%
  mutate(
    avg_growth = mean(GDP_Growth, na.rm = TRUE),
    Recovery_Category = case_when(
      avg_growth > 0 & avg_growth <= 3 ~ "Recovering",
      avg_growth > 3 ~ "Booming",
      TRUE ~ NA_character_
    )
  ) %>%
  ungroup()

# Step 2: Remove any rows with NA in Recovery_Category
gdp_growth_long_cat <- gdp_growth_long_cat %>%
  filter(!is.na(Recovery_Category))

# Step 3: Create box plot
plot3_box <- gdp_growth_long_cat %>%
  ggplot(aes(x = Recovery_Category, y = GDP_Growth, fill = Recovery_Category)) +
  geom_boxplot(alpha = 0.8, outlier.color = "gray30") +
  labs(
    title = "GDP Growth Distribution by Recovery Category (2021–2024)",
    subtitle = "Excluding countries with missing or incomplete GDP growth data",
    x = "Recovery Category",
    y = "GDP Growth (%)",
    ) +
  scale_fill_manual(values = c(
    "Recovering" = "#F1C40F",
    "Booming" = "#2ECC71"
  )) +
  theme_minimal(base_size = 13) +
  theme(legend.position = "none") +
  scale_fill_viridis_d()

# Step 4: Save and display plot
ggsave("plot3_box.png", plot = plot3_box, width = 5, height = 4)
plot3_box
```

<img src="proposal_files/figure-gfm/growth-distribution-by-recovery-1.png" alt="Box plot comparing GDP growth distribution for two recovery categories from 2021 to 2024. The x-axis shows “Booming” and “Recovering,” and the y-axis shows GDP growth in percent. The “Booming” group has higher median growth and a wider range of values, including an upper outlier, while the “Recovering” group shows lower median growth and a narrower spread."  />

``` r
# Region classification (simple)
region_map <- tibble(
  Country = unique(GDP_Data$`Time period`),
  Region = case_when(
    Country %in% c("United States", "Canada", "Mexico") ~ "North America",
    Country %in% c("Denmark", "France", "Germany", "United Kingdom", "Italy", "Spain",
                   "Norway","Sweden","Finland","Netherlands","Belgium","Switzerland") ~ "Europe",
    Country %in% c("Türkiye") ~ "Middle East",
    Country %in% c("South Africa") ~ "Africa",
    TRUE ~ "Other"
  )
)

gdp_region <- GDP_Data %>%
  pivot_longer(
    cols = matches("^20"),
    names_to = "Year",
    values_to = "GDP_Growth"
  ) %>%
  mutate(
    Country = `Time period`,
    Year = as.integer(Year),
    GDP_Growth = as.numeric(GDP_Growth)
  ) %>%
  select(-`Time period`) %>%
  left_join(region_map, by="Country")


focus_countries <- c("United States", "Denmark", "Türkiye", "South Africa")
gdp_region <- gdp_region %>%
  mutate(Highlight = ifelse(Country %in% focus_countries, "Focus", "Other"))

focus_colors <- c(
  "United States" = "#0072B2",
  "Denmark"       = "#009E73",
  "Türkiye"        = "#D55E00",
  "South Africa"  = "#CC79A7"
)

plot_region_covid <- gdp_region %>%
  ggplot(aes(x = Year, y = GDP_Growth, group = Country)) +

  # COVID shading
  annotate("rect",
           xmin = 2019.5, xmax = 2020.5,
           ymin = -Inf, ymax = Inf,
           fill = "red", alpha = 0.1) +

  # Other countries
  geom_line(
    data = gdp_region %>% filter(Highlight == "Other"),
    aes(color = Region),
    alpha = 0.3,
    linewidth = 0.7
  ) +

  # Highlighted countries
  geom_line(
    data = gdp_region %>% filter(Highlight == "Focus"),
    aes(color = Country),
    linewidth = 2
  ) +

  geom_point(
    data = gdp_region %>% filter(Highlight == "Focus"),
    aes(color = Country),
    size = 2.5
  ) +

  geom_text_repel(
    data = gdp_region %>% filter(Highlight == "Focus"),
    aes(label = Country, color = Country),
    size = 5,
    show.legend = FALSE
  ) +

  scale_color_manual(
    values = c(
      "North America"="darkgreen",
      "Europe"="darkblue",
      "Africa"="orange",
      "Middle East"="purple",
      "Other"="grey70",
      focus_colors
    )
  ) +

  labs(
    title = "GDP Growth by Region (2018–2024)",
    subtitle = "COVID-19 recession in 2020 is highlighted\nYear: {frame_along}",
    x = "Year",
    y = "GDP Growth (%)",
    color = "Region / Highlighted Countries"
  ) +
  theme_minimal(base_size = 16) +
  theme(legend.position = "bottom") +
  transition_reveal(Year)

animate(
  plot_region_covid,
  fps = 9,
  duration = 10,
  width = 750,
  height = 500,
  renderer = gifski_renderer()
)

unique(GDP_Data$`Time period`)
```
