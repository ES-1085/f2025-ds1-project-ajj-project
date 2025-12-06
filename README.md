Measuring Post-Covid Economic Recovery Across Nations
================
by AJJ

## Summary

The COVID-19 pandemic caused one of the most severe and synchronized global economic contractions in modern history. Although nearly all countries experienced sharp declines in GDP during 2020, their post-pandemic recoveries were far from uniform. Understanding these differences is important for assessing global economic resilience, identifying which countries rebounded the fastest, and evaluating how factors such as income level, geographic region, and OECD membership shaped recovery trajectories. To study these dynamics, we used two OECD datasets: Annual Real GDP Growth (OECD and Non-OECD Countries) and Annual GDP and Consumption Per Capita, covering 2018–2024. These datasets allowed us to examine economic conditions before, during, and after the pandemic. Our project focuses on four countries: the United States, Denmark, India, and South Africa. Then we used their outcomes to compare both OECD and non-OECD economies and to highlight variation between advanced and emerging economies.


## Methods

Our analysis draws on two datasets we collected from open dataset website. We merged and cleaned these datasets, and converted the information into quarterly format to enable a clearer comparison of pre-pandemic, pandemic-year, and post-pandemic trends. We removed large multi-country blocs such as the EU to avoid overlapping observations, and focused on the analysis on four countries: the United States, Denmark, India, and South Africa. These were selected to contrast OECD and non-OECD experiences and to highlight differences between advanced and emerging economies.

We conducted exploratory data analysis to summarize GDP growth distributions, identify outliers, and examine how recovery patterns varied across countries and regions. We analyzed time-series trends using line plots, explored regional differences through boxplots, and examined the relationship between income level and recovery strength through a scatterplot of GDP per capita versus post-pandemic GDP growth. In addition, we looked at average post-2021 growth through other plots using different variables to visualize and interpret relative performance across nations. All methods relied on descriptive statistics and comparative visualization rather than predictive or causal modeling.

## Analysis 

The analysis reveals clear differences in the speed and stability of post-pandemic economic recovery among the four selected countries. Although all nations experienced a sharp contraction in 2020, the magnitude of their rebounds varied substantially. India underwent the deepest initial decline yet also achieved the strongest and most rapid recovery, displaying sharp positive growth rates throughout 2021–2024. This pattern is characteristic of emerging economies with high pre-pandemic volatility and strong post-shock momentum. In contrast, the United States and Denmark which are both high-income OECD members demonstrated slower but more stable recoveries, with moderate GDP growth and fewer large swings. South Africa showed the slowest and most fragile rebound, reflecting ongoing structural challenges and limited economic momentum relative to the other three countries. These comparisons directly answer our central research question: India recovered the fastest after COVID-19, followed by the United States and Denmark, while South Africa experienced the weakest recovery. This ranking remained consistent across visualizations and aligns with broader global patterns in which emerging economies often display higher post-pandemic growth rates than advanced economies.

Next, we examined how GDP growth relates to GDP per capita during the recovery period. The scatterplot analysis reveals a clear inverse relationship: wealthier countries tended to have lower post-pandemic growth, while lower-income countries grew more rapidly. The United States and Denmark cluster with other high-income economies showing slower but stable growth. India, with a much lower GDP per capita, stands out as a strong positive outlier, demonstrating that income level strongly shapes the pace of recovery. South Africa, despite its lower income, remained closer to the stagnating end, illustrating that low income alone does not guarantee rapid rebound. Overall, the negative trendline suggests that the global recovery was uneven, with advanced economies regaining stability more slowly and emerging economies showcasing faster but often more inconstant growth. 

Throughout the project, we faced some limitations. Relying primarily on GDP growth and GDP per capita restricted our ability to capture the full complexity of economic recovery, as factors such as inflation, employment, government stimulus, and public health responses were not included. Also, our focus on only four countries limited the generalizability of the findings, and the use of OECD data underrepresented informal economic activity, particularly in emerging economies. Moreover, the dataset ends in 2024, meaning long-term recovery patterns beyond this period remain unobserved. Future research could expand the set of countries analyzed, incorporate additional economic and social indicators, or apply causal and predictive models to understand the drivers of recovery more precisely. Exploring policy responses such as fiscal stimulus, vaccination rates, or labor-market shifts could further clarify why some nations recovered more quickly than others. Extending the analysis beyond 2024 would also help assess the durability of the post-pandemic rebound. That way, future work could build a more comprehensive understanding of how nations respond to global economic shocks.


## Conclusions

Overall, the project demonstrates that the post-COVID economic recovery was highly uneven across countries and regions. India exhibited the strongest rebound among the selected cases, reflecting broader regional trends in which South Asia recovered rapidly. The United States and Denmark showed slower growth typical of high-income OECD countries, while South Africa’s weaker performance illustrated the challenges faced by some emerging economies. The inverse relationship between GDP growth and GDP per capita reinforces the pattern that wealthier countries experienced more modest but stable recoveries, whereas lower-income countries tended to grow more quickly following the global downturn. 


## Handout

Our handout can be found [here](handout/Measuring-Post-Covid-Economic-Recovery-Across-Nations.pdf). You can update the filename and extension of your handout, currently it is called handout.pdf

## Memo

A link to the code and how we created our graphics in our memo can be found [here](memo/memo.html).

## Data

“Quarterly Real GDP Growth - OECD Countries.” OECD Data Explorer, data-explorer.oecd.org/vis?df%5Bds%5D=dsDisseminateFinalDMZ&df%5Bid%5D=DSD_NAMAIN1%2540DF_QNA_EXPENDITURE_GROWTH_OECD&df%5Bag%5D=OECD.SDD.NAD&df%5Bvs%5D=1.1&dq=Q.....B1GQ......G1.&ly%5Bcl%5D=TIME_PERIOD&ly%5Brw%5D=REF_AREA&to%5BTIME_PERIOD%5D=false&lo=30&lom=LASTNPERIODS&vw=ov&lc=en&pg=0. Accessed 24 Oct. 2025. 

Include a citation for your data here. See
<http://libraryguides.vu.edu.au/c.php?g=386501&p=4347840> for guidance
on proper citation for datasets. If you got your data off the web, make
sure to note the retrieval date.

## References

List any references here. You should, at a minimum, list your data
source.
