# 🚕 Maximizing Driver Revenue Through Payment Method Optimization

**Statistical hypothesis testing and exploratory data analysis on 1.4M+ NYC Yellow Taxi trip records to evaluate whether payment method is associated with differences in fare amount and trip distance, using Python, SciPy, and Statsmodels.**

## Table of Contents
- [Overview](#overview)
- [Business Problem](#business-problem)
- [Dataset Description](#dataset-description)
- [Tools & Technologies](#tools--technologies)
- [Project Structure](#project-structure)
- [Data Cleaning & Preparation](#data-cleaning--preparation)
- [EDA & Key Insights](#eda--key-insights)
- [Statistical Hypothesis Testing](#statistical-hypothesis-testing)
- [Visuals](#visuals)
- [Strategic Recommendations](#strategic-recommendations)
- [Limitations](#limitations)
- [How to Run This Project](#how-to-run-this-project)
- [Future Work](#future-work)
- [Author & Contact](#author--contact)

## Overview

This project investigates whether payment method (card vs. cash) is associated with differences in average fare and trip distance across NYC Yellow Taxi trips. It combines exploratory data analysis with formal statistical hypothesis testing, translating the result into concrete, evidence-based recommendations for taxi operators and drivers.

## Business Problem

In urban taxi operations, maximizing revenue per trip matters for driver earnings, fleet sustainability, and operational efficiency.

**Core research question:** Do customers who pay by card generate significantly different average fares compared with customers who pay by cash?

## Dataset Description

Source: [NYC Taxi & Limousine Commission (TLC) Yellow Taxi Trip Records](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)

| Metric | Value |
|---|---|
| Raw records | 4,090,836 |
| Raw attributes | 20 |
| Cleaned analytical records | 1,485,094 |
| Payment groups | Card & Cash |

Key fields: `passenger_count`, `payment_type`, `fare_amount`, `trip_distance`, `duration`. Full field definitions: [`Data/data_dictionary_trip_records_yellow.pdf`](Data/data_dictionary_trip_records_yellow.pdf).

## Tools & Technologies

| Category | Tools |
|---|---|
| **Language** | Python 3.12+ |
| **Data Processing** | Pandas, NumPy |
| **Statistical Analysis** | SciPy, Statsmodels |
| **Visualization** | Matplotlib, Seaborn |
| **Documentation** | Jupyter Notebook, Markdown, PowerPoint |

## Project Structure

```
nyc-taxi-revenue-optimization-2026/
├── Data/
│   ├── README.md
│   └── data_dictionary_trip_records_yellow.pdf
├── Docs/
│   ├── Maximizing Revenue for Taxi Drivers.pdf
│   ├── Maximizing Revenue for Taxi Drivers.pptx
│   └── README.md
├── Notebook/
│   ├── README.md
│   └── nyc_taxi_revenue_analysis.ipynb
├── Visuals/
│   ├── Distribution of Fare Amount by Payment Type.png
│   ├── Distribution of Trip Distance by Payment Type.png
│   ├── Overall Payment Preference.png
│   ├── Passenger Count by Payment Type.png
│   ├── Statistical Hypothesis Testing.png
│   └── README.md
├── .gitignore
├── LICENSE
└── README.md
```

## Data Cleaning & Preparation

The raw dataset (4,090,836 records, 20 attributes) was reduced to 1,485,094 analytical records through domain-based filters and statistical trimming, removing invalid fares, zero-distance trips, and extreme outliers that would otherwise distort mean-based comparisons. Full methodology documented in the [analysis notebook](Notebook/nyc_taxi_revenue_analysis.ipynb).

## EDA & Key Insights

**Payment preference.** Card was the dominant payment method in the cleaned dataset.

| Payment Method | Share |
|---|---|
| 💳 Card | **82.9%** |
| 💵 Cash | **17.1%** |

**Fare and distance differences.** Both metrics were right-skewed, with card-paid trips consistently higher on both dimensions.

| Metric | Card Payment | Cash Payment | Difference | Relative Difference |
|---|---:|---:|---:|---:|
| Average Fare | $19.44 ± $9.20 | $16.35 ± $9.11 | **+$3.09** | **+18.9%** |
| Average Distance | 2.94 mi ± 2.16 | 2.41 mi ± 2.14 | **+0.53 mi** | **+22.0%** |

Card-paying customers had an average fare approximately 18.9% higher than cash-paying customers. This is an association, not proof that card payment causes higher fares. The difference may partly reflect trip distance, route, time, location, or other customer and trip characteristics.

**Passenger group dynamics.** Solo passengers were the largest segment. Card payments accounted for roughly 61.3% of all trips, cash for about 13.1%, with card usage remaining substantially higher than cash across all passenger-count groups (1 to 6 passengers). Payment preference was not dramatically different across passenger-count categories.

## Statistical Hypothesis Testing

A **Welch's Independent Two-Sample t-test** was used to determine whether the fare difference between card and cash transactions was statistically significant. Welch's test was chosen because it does not require the two groups to have equal population variances.

**Null hypothesis (H₀):** μ(card) − μ(cash) = 0. No difference in average fare between card and cash transactions.

**Alternative hypothesis (Hₐ):** μ(card) − μ(cash) ≠ 0. A statistically significant difference exists.

| Statistical Measure | Result |
|---|---:|
| Test | Welch's Independent Two-Sample t-test |
| Sample size | 1,485,094 |
| t-statistic | **155.24** |
| p-value | **< 0.001** |
| Significance level (α) | 0.05 |
| Decision | **Reject H₀** |

Because the p-value is well below 0.05, the null hypothesis is rejected: there is strong statistical evidence of a difference in average fare between card and cash transactions in this dataset. With a sample this large, even small differences can reach statistical significance, so this result should not be read as proof of causality or business importance on its own.

## Visuals

![Overall Payment Preference](Visuals/Overall%20Payment%20Preference.png)

![Distribution of Fare Amount by Payment Type](Visuals/Distribution%20of%20Fare%20Amount%20by%20Payment%20Type.png)

![Distribution of Trip Distance by Payment Type](Visuals/Distribution%20of%20Trip%20Distance%20by%20Payment%20Type.png)

![Passenger Count by Payment Type](Visuals/Passenger%20Count%20by%20Payment%20Type.png)

![Statistical Hypothesis Testing](Visuals/Statistical%20Hypothesis%20Testing.png)

## Strategic Recommendations

**1. Encourage digital payment adoption.** Card already represents 82.9% of transactions. The observed $3.09 average fare difference is a business signal worth testing through card-linked promotions, digital payment rewards, and loyalty programs.

**2. Improve payment infrastructure.** Reduce payment friction with NFC/contactless support, Apple Pay and Google Pay compatibility, reliable card terminals, and backup connectivity.

**3. Optimize high-value trip corridors.** Card transactions associate with longer, higher-fare trips. Airport routes, business districts, and transportation hubs are worth investigating further, pending additional geospatial and time-series analysis.

**4. Use evidence-based segmentation.** Since card usage stayed dominant across passenger-count groups, campaigns don't need heavy segmentation by passenger count. Segment instead by pickup/drop-off location, trip distance, time of day, day of week, and fare range.

## Limitations

The relationship between payment method and fare should not be interpreted as causal. Trip distance, pickup/drop-off location, time of day, traffic conditions, airport trips, customer demographics, trip purpose, and tipping behavior could all influence both payment method and fare simultaneously. The t-test establishes that a difference in means exists, not why it exists. Future work should use multivariate models to control for these confounders.

## How to Run This Project

1. **Clone the repository**
   ```bash
   git clone https://github.com/seema-kri/nyc-taxi-revenue-optimization-2026.git
   cd nyc-taxi-revenue-optimization-2026
   ```
2. **Create a virtual environment**
   ```bash
   python -m venv venv
   ```
   Windows: `venv\Scripts\activate`
   macOS/Linux: `source venv/bin/activate`
3. **Install dependencies**
   ```bash
   pip install pandas numpy scipy statsmodels matplotlib seaborn pyarrow jupyter
   ```
4. **Launch the notebook**
   ```bash
   jupyter notebook Notebook/nyc_taxi_revenue_analysis.ipynb
   ```
5. **Read the full write-up**: [`Docs/Maximizing Revenue for Taxi Drivers.pdf`](Docs/Maximizing%20Revenue%20for%20Taxi%20Drivers.pdf)

## Future Work

- **Tipping behavior analysis.** Compare tipping frequency and percentage across payment methods, and its effect on driver revenue.
- **Geospatial revenue analysis.** Use pickup/drop-off zone data to identify high-revenue zones, demand corridors, and airport-related revenue hotspots.
- **Time-series analysis.** Analyze revenue and payment behavior by hour, weekday vs. weekend, and season to inform driver shift scheduling.
- **Regression modeling.** Fit `Fare = β₀ + β₁(Card) + β₂(Distance) + β₃(Duration) + β₄(Passengers) + ε` to test whether payment method remains associated with fare after controlling for trip characteristics.

## Key Takeaway

**Card trips: $19.44 average fare. Cash trips: $16.35 average fare. Observed difference: $3.09 per trip, statistically significant (p < 0.001).**

The analysis does not establish that card payment itself causes higher revenue. Trip distance, location, timing, and other factors likely explain part of the gap. The project demonstrates how EDA, statistical hypothesis testing, and business interpretation combine to turn raw transportation data into an actionable, evidence-backed recommendation.

## Author & Contact

**Seema Kumari**, Data Analyst
📧 [seemakri136@gmail.com](mailto:seemakri136@gmail.com) · 🔗 [LinkedIn](https://linkedin.com/in/seema-kumari-375763308)

*Open to opportunities, collaborations, and conversations around data analytics.*

If you found this project helpful, please consider giving it a ⭐ on GitHub — it helps a lot!
