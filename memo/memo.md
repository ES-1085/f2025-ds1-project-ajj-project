Project memo
================
AJJ

This document should contain a detailed account of the data clean up for
your data and the design choices you are making for your plots. For
instance you will want to document choices you’ve made that were
intentional for your graphic, e.g. color you’ve chosen for the plot.
Think of this document as a code script someone can follow to reproduce
the data cleaning steps and graphics in your handout.

``` r
library(tidyverse)
library(broom)
library(gganimate)
library(scales)
```

## Data Clean Up Steps for Overall Data

### Step 1: Load and Inspect Dataset

```{r}
GDP_Data <- read_excel("/cloud/project/data/Annual_GDP_Growth_OECD_and_non_OECD.xlsx")
# View(Annual_GDP_Growth_OECD_and_non_OECD)

GDP_Per_Capita <- read_excel("/cloud/project/data/Annual GDP Per Capita OECD and Non-OECD.xlsx.xlsx")
# View(Annual_GDP_Per_Capita_OECD_and_Non_OECD_xlsx)
```

### Step 2: Rename Columns and Pivot Longer

```{r}
gdp_clean <- GDP_Data |>
rename(Country = `Time Period`) |>   # rename for clarity
filter(Country != "Country") |>       # remove header-like cell
pivot_longer(cols = starts_with("20"),
names_to = "Year",
values_to = "GDP_Growth") |>
mutate(Year = as.integer(Year))
```

Description:
The dataset originally had years (2018–2024) as columns, which makes it wide. pivot_longer() converts it into a tidy long format with Year and GDP_Growth columns, making it easier to plot over time.

### Step 3: Categorize Countries by Growth Type

```{r}
gdp_clean <- gdp_clean |>
mutate(Growth_Category = case_when(
GDP_Growth > 4 ~ "Booming",
GDP_Growth > 0 & GDP_Growth <= 4 ~ "Recovering",
GDP_Growth <= 0 ~ "Stagnating"
))
```


## Plots

### ggsave example for saving plots

``` r
p1 <- starwars |>
  filter(mass < 1000, 
         species %in% c("Human", "Cerean", "Pau'an", "Droid", "Gungan")) |>
  ggplot() +
  geom_point(aes(x = mass, 
                 y = height, 
                 color = species)) +
  labs(x = "Weight (kg)", 
       y = "Height (m)",
       color = "Species",
       title = "Weight and Height of Select Starwars Species",
       caption = paste("This data comes from the starwars api: https://swapi.py43.com"))


ggsave("example-starwars.png", width = 4, height = 4)

ggsave("example-starwars-wide.png", width = 6, height = 4)
```

### Plot 1: \_\_\_\_\_\_\_\_\_

#### Data cleanup steps specific to plot 1

``` r
# This section is optional and depends on if you have some data cleaning steps specific to a particular plot
```

#### Final Plot 1

### Plot 2: \_\_\_\_\_\_\_\_\_

### Plot 3: \_\_\_\_\_\_\_\_\_\_\_

Add more plot sections as needed. Each project should have at least 3
plots, but talk to me if you have fewer than 3.

### Plot 4: \_\_\_\_\_\_\_\_\_\_\_
