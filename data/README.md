# Data

Data files placed in this in this folder. 

This project analyzes global economic recovery patterns from 2018 to 2024, focusing on how different countries rebounded following the COVID-19 pandemic. The primary goal is to evaluate variations in GDP growth and GDP per capita across OECD and non-OECD nations and to visualize how economic resilience differs by income level and region.

## GDP Growth (Annual, 2018–2024)

**Dataset name:** `GDP_Growth_Clean_Concise_Dataset_2018_2024_Annual`  
**Source:** OECD Quarterly Real GDP Growth – converted to annual averages for cross-national comparison.

**Description:**  
This dataset measures the annual GDP growth rate (%) for 54 countries and economic regions from 2018 through 2024. 
It was derived from OECD’s original Quarterly Real GDP Growth table, which reports percentage changes in real GDP (seasonally adjusted, chain-linked volumes). Because quarterly data can fluctuate due to short-term shocks, we converted it into annualized averages to emphasize broader macroeconomic recovery patterns.

Quarterly growth captures volatility (e.g., rapid collapse and rebound in 2020), but for comparing countries with differing seasonal cycles, annual aggregation smooths out noise and allows alignment with the World Bank’s yearly GDP per capita indicators.
This ensures both datasets share a common temporal frequency (one observation per year) and can be merged for cross-variable analysis.

Each row represents one country, and columns correspond to annual GDP growth rates (%).
Missing values (NA) represent unavailable or incomplete OECD data for certain years or regional aggregates.

**Key variables:**
- `Time period`: Country name  
- `2018–2024`: Annual GDP growth rate (%) for each year  

**Dimensions:**  
Rows: 54 Columns: 8

**Glimpse():**

$ `Time period` <chr> "Country", "Australia", "Austria", "Belgium", "Canada", "Chile", "Colombia", "Costa Rica", …

$ `2018`        <dbl> NA, 2.8349175, 2.4842210, 1.8779685, 2.7429634, 3.9900295, 2.5643243, 2.6159044, 2.8303059,…

$ `2019`        <dbl> NA, 1.9154753, 1.7549763, 2.4428900, 1.9084319, 0.6343675, 3.1868554, 2.4175118, 3.5657766,…

$ `2020`        <dbl> NA, -2.01405865, -6.31825516, -4.79296338, -5.03823342, -6.14347479, -7.18591414, -4.273354…

$ `2021`        <dbl> NA, 5.444144, 4.923092, 6.254434, 5.950528, 11.314920, 10.801198, 7.935762, 4.029018, 6.500…

$ `2022`        <dbl> NA, 4.1186486, 5.3309726, 3.9562583, 4.5574856, 2.1539936, 7.3282773, 4.5514918, 2.8471707,…

$ `2023`        <dbl> NA, 2.02487154, -0.78624418, 1.71412162, 1.75311380, 0.52136798, 0.71238003, 5.11192183, 0.…

$ `2024`        <dbl> NA, 1.06699758, -0.65908974, 1.07062666, 0.97378519, 2.64431155, 1.59828185, 4.32122430, 1.…

**Interpretation:**

This dataset is critical for tracking economic contraction and recovery:
- The 2020 values show a sharp global downturn during the COVID-19 crisis.
- The 2021–2022 values illustrate a rebound, especially among high-income and export-driven economies.
- Subsequent years (2023–2024) indicate whether recovery stabilized or slowed.
- By analyzing this data across OECD and non-OECD members, we can quantify which economies demonstrated resilience, stagnation, or continued volatility.
  

## GDP per Capita (PPP, Annual, 2018–2024)

**Dataset name:** `GDP_Per_Capita_2018_2024_Annual_OECD_Non_OECD`  
**Source:** World Bank – World Development Indicators, harmonized with OECD PPP conversion metrics.

**Description:**  
This dataset presents each country’s GDP per capita (in constant 2017 PPP US dollars) from 2018 to 2024. The data were collected from the World Bank’s World Development Indicators (WDI) and cleaned to remove metadata, unify headers, and standardize column formats. 

Using Purchasing Power Parity (PPP) ensures fair comparison across economies with different price levels, while expressing values in constant 2017 international dollars removes inflation effects. This lets us distinguish between real income growth and nominal increases due to price changes.

Each row represents a country, and each column corresponds to its GDP per capita for a specific year.
Some columns originally contained character strings (e.g., "65002.659138000003") and were converted to numeric values for analysis.

**Key variables:**
- `Time period...1`: Country name  
- `Time period...2`: Unit of measurement (“US dollars per person, PPP converted”)  
- `2018–2024`: Annual GDP per capita (USD PPP)  

**Dimensions:**  
Rows: 47 Columns: 9

**Glimpse():**

$ `Time period...1` <chr> "Country", "Australia", "Austria", "Belgium", "Canada", "Chile", "Colombia", "Costa Ric…

$ `Time period...2` <chr> "Combined unit of measure", "US dollars per person, PPP converted", "US dollars per per…

$ `2018`            <dbl> NA, 53051.72, 56654.55, 52466.55, 49982.65, 25496.43, 15814.70, 21312.71, 42016.46, 572…

$ `2019`            <dbl> NA, 53602.04, 60370.46, 56712.36, 50498.96, 25733.10, 16712.41, 23082.52, 46139.56, 605…

$ `2020`            <dbl> NA, 56821.62, 58522.84, 56119.62, 48590.72, 25236.62, 15950.51, 21778.79, 45675.06, 627…

$ `2021`            <chr> NA, "65002.659138000003", "62998.849713000003", "60668.644834999999", "56995.206995", "…

$ `2022`            <chr> NA, "72576.307081000006", "70865.595503999997", "68157.888133999993", "63578.2977259999…

$ `2023`            <chr> NA, "73401.167048000003", "71173.472523999997", "69102.712924000007", "64462.9339439999…

$ `2024`            <chr> NA, "73888.300352999999", "73427.587778000001", "72289.394943000007", "65532.718214", "…

**Interpretation:**
This dataset reflects living standards and economic capacity.

- Increases from 2021 onward suggest countries where individual wealth recovered alongside national GDP.
- Comparisons between OECD (typically high-income) and non-OECD (developing/emerging) economies reveal persistent inequality in recovery pace and magnitude.
- Combining this with GDP growth data allows us to test whether wealthier nations also recovered faster or simply maintained higher baselines.

## Integration and Use:
The two datasets are merged by Country and Year to enable joint analysis of economic output (growth) and living standards (income per person).
Together, they support multiple layers of analysis:

- Economic recovery trajectories after the COVID-19 pandemic (2019–2024)
- Cross-regional comparisons between OECD and non-OECD economies
- Temporal correlations between GDP growth and GDP per capita
- Regression and visualization of income level vs. growth rate over time

These integrated data form the empirical foundation for the project’s exploratory data analysis and visualizations, helping identify which countries experienced the strongest recoveries and how those patterns align with income group and region.
