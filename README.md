# Maximizing Driver Revenue Through Payment Method Optimization

> **Statistical hypothesis testing and exploratory data analysis on NYC Yellow Taxi trip records to evaluate the relationship between payment method, fare amount, and trip distance.**

---

## 📌 Business Problem & Objective

In urban taxi operations, maximizing revenue per trip is important for driver earnings, fleet sustainability, and operational efficiency.

This project investigates whether **payment method (Card vs. Cash)** is associated with differences in average fare amounts and trip distances using NYC Yellow Taxi trip records.

### Core Research Question

> **Do customers who pay by card generate significantly different average fares compared with customers who pay by cash?**

The analysis uses exploratory data analysis and statistical hypothesis testing to determine whether the observed difference in average fares is statistically significant.

---

## 📊 Dataset Overview

**Source:** NYC Taxi & Limousine Commission (TLC) Yellow Taxi Trip Records

| Metric                     |       Value |
| -------------------------- | ----------: |
| Raw records                |   4,090,836 |
| Raw attributes             |          20 |
| Cleaned analytical records |   1,485,094 |
| Payment groups             | Card & Cash |

### Key Features

* `passenger_count` — Number of passengers
* `payment_type` — Payment method
* `fare_amount` — Metered fare in USD
* `trip_distance` — Trip distance in miles
* `duration` — Trip duration in minutes

The analytical dataset was cleaned using domain-based filters and statistical trimming to remove invalid or extreme observations.

---

## 🛠️ Tools & Technologies

### Programming

* Python 3.12+

### Data Processing

* Pandas
* NumPy

### Statistical Analysis

* SciPy
* Statsmodels

### Visualization

* Matplotlib
* Seaborn

### Documentation & Presentation

* Jupyter Notebook
* Markdown
* Microsoft PowerPoint

---

## 📁 Project Structure

```text
nyc-taxi-revenue-optimization-2026/
│
├── Data/
│   ├── README.md
│   └── data_dictionary_trip_records_yellow.pdf
│
├── Docs/
│   ├── README.md
│   └── Maximizing Revenue for Taxi Drivers.pptx
│
├── Notebook/
│   ├── README.md
│   └── nyc_taxi_revenue_analysis.ipynb
│
├── Visuals/
│   ├── README.md
│   ├── Distribution of Fare Amount by Payment Type.png
│   ├── Distribution of Trip Distance by Payment Type.png
│   ├── Overall Payment Preference.png
│   ├── Passenger Count by Payment Type.png
│   └── Statistical Hypothesis Testing.png
│
├── .gitignore
├── LICENSE
└── README.md
```

---

# 🔍 Key Insights & Visuals

## 1. Payment Preference

Card payments were the dominant payment method in the cleaned dataset.

| Payment Method |     Share |
| -------------- | --------: |
| 💳 Card        | **82.9%** |
| 💵 Cash        | **17.1%** |

This indicates that digital payment was already the preferred settlement method for the majority of observed trips.

---

## 2. Fare & Distance Differences

Both fare amount and trip distance exhibited right-skewed distributions.

Card-paid trips showed higher average fare and distance than cash-paid trips.

| Metric               |   Card Payment |   Cash Payment |   Difference | Relative Difference |
| -------------------- | -------------: | -------------: | -----------: | ------------------: |
| **Average Fare**     | $19.44 ± $9.20 | $16.35 ± $9.11 |   **+$3.09** |          **+18.9%** |
| **Average Distance** | 2.94 mi ± 2.16 | 2.41 mi ± 2.14 | **+0.53 mi** |          **+22.0%** |

### Interpretation

Card-paying customers had an average fare approximately **18.9% higher** than cash-paying customers.

However, this should be interpreted as an **association rather than proof that card payment causes higher fares**. The higher fares may partly reflect differences in trip distance, route, time, location, or other customer/trip characteristics.

---

## 3. Passenger Group Dynamics

Solo passengers represented the largest passenger segment.

Among the cleaned trips:

* Card payments accounted for approximately **61.3%** of all trips.
* Cash payments accounted for approximately **13.1%**.
* Card usage remained substantially higher than cash across passenger groups from 1–6 passengers.

This suggests that payment preference was not dramatically different across passenger-count categories.

### Key Observation

> Card payment remained the dominant payment method across passenger groups.

---

# 🧪 Statistical Hypothesis Testing

To determine whether the difference in average fares between card and cash transactions was statistically significant, a **Welch's Independent Two-Sample t-test** was performed.

Welch's t-test was selected because it does not require the two groups to have equal population variances.

### Hypotheses

**Null Hypothesis ($H_0$):**

$$
\mu_{card} - \mu_{cash} = 0
$$

There is no difference in average fare between card and cash transactions.

**Alternative Hypothesis ($H_a$):**

$$
\mu_{card} - \mu_{cash} \neq 0
$$

There is a statistically significant difference in average fare between card and cash transactions.

---

## 📈 Test Results

| Statistical Measure           |                                Result |
| ----------------------------- | ------------------------------------: |
| Test                          | Welch's Independent Two-Sample t-test |
| Sample Size                   |                             1,485,094 |
| t-statistic                   |                            **155.24** |
| p-value                       |                           **< 0.001** |
| Significance Level ($\alpha$) |                                  0.05 |
| Decision                      |                      **Reject $H_0$** |

### Conclusion

Because the p-value is substantially below the 0.05 significance level, we reject the null hypothesis.

> **There is strong statistical evidence of a difference in average fare between card and cash transactions in the analyzed dataset.**

The large sample size also means that even relatively small differences can become statistically significant. Therefore, **statistical significance should not be interpreted as proof of causality or business importance by itself.**

---

# 💡 Strategic Recommendations

## 1. Encourage Digital Payment Adoption

Since card payments already represent **82.9%** of observed transactions, operators could experiment with incentives such as:

* Card-linked promotions
* Digital payment rewards
* Contactless payment options
* Loyalty programs

The observed **$3.09 average fare difference** provides a potential business signal worth investigating further.

---

## 2. Improve Payment Infrastructure

Reliable payment infrastructure can reduce friction during payment.

Recommended improvements include:

* NFC/contactless payment
* Apple Pay and Google Pay compatibility
* Reliable card terminals
* Faster payment processing
* Backup payment connectivity

---

## 3. Optimize High-Value Trip Corridors

The analysis indicates that card transactions are associated with longer average trips and higher average fares.

Operators could investigate high-value corridors such as:

* Airport routes
* Business districts
* Major transportation hubs
* Tourist destinations

However, additional geospatial and time-series analysis would be required before using this finding to make routing decisions.

---

## 4. Focus on Evidence-Based Customer Segmentation

Because card usage remained dominant across passenger-count categories, payment campaigns do not necessarily need to be heavily segmented by passenger count.

Future segmentation should instead consider:

* Pickup location
* Drop-off location
* Trip distance
* Time of day
* Day of week
* Fare range

---

# 📉 Limitations

The observed relationship between payment method and fare should **not be interpreted as causal**.

Several variables could influence both payment method and fare:

* Trip distance
* Pickup/drop-off location
* Time of day
* Traffic conditions
* Airport trips
* Customer demographics
* Trip purpose
* Tip behavior

The t-test establishes statistical evidence of a difference in means, but it does not explain **why** the difference exists.

Future analysis should therefore use multivariate statistical models to control for potential confounding variables.

---

# 🚀 Future Work

### 1. Tipping Behavior Analysis

Compare tipping patterns between payment methods.

Questions to investigate:

* Do card-paying customers tip more frequently?
* What is the average tip percentage?
* How does tipping affect driver revenue?

---

### 2. Geospatial Revenue Analysis

Use pickup and drop-off zone information to identify:

* High-revenue zones
* High-demand corridors
* Airport-related trips
* Revenue hotspots

GIS-based visualization could help identify operational opportunities.

---

### 3. Time-Series Analysis

Analyze revenue and payment behavior across:

* Hours of the day
* Weekdays vs. weekends
* Months
* Peak vs. off-peak periods

This could help optimize driver shift scheduling.

---

### 4. Regression Modeling

A stronger next step would be to build a regression model such as:

$$
Fare = \beta_0 + \beta_1(Card) + \beta_2(Distance) + \beta_3(Duration) + \beta_4(Passengers) + \epsilon
$$

This would help determine whether payment method remains associated with fare **after controlling for trip characteristics**.

---

# ▶️ How to Run

## 1. Clone the Repository

```bash
git clone https://github.com/seema-kri/nyc-taxi-revenue-optimization-2026.git

cd nyc-taxi-revenue-optimization-2026
```

## 2. Create a Virtual Environment

```bash
python -m venv venv
```

### Windows

```bash
venv\Scripts\activate
```

### macOS / Linux

```bash
source venv/bin/activate
```

## 3. Install Dependencies

```bash
pip install pandas numpy scipy statsmodels matplotlib seaborn pyarrow jupyter
```

## 4. Launch the Notebook

```bash
jupyter notebook Notebook/nyc_taxi_revenue_analysis.ipynb
```

---

# 📌 Key Takeaway

The analysis found a statistically significant difference in average fare between card and cash transactions:

> **Card trips: $19.44 average fare**
> **Cash trips: $16.35 average fare**
> **Observed difference: $3.09 per trip**

While the finding provides a strong business signal, the analysis does **not establish that card payment itself causes higher revenue**. Trip distance, location, timing, and other factors may explain part of the observed difference.

The project therefore demonstrates how **EDA + statistical hypothesis testing + business interpretation** can be combined to turn transportation data into actionable insights.

---

## 📫 Connect

<p align="center">
  <a href="https://linkedin.com/in/seema-kumari-375763308">
    <img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" />
  </a>
  <a href="mailto:seemakri136@gmail.com">
    <img src="https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white" />
  </a>
  <a href="https://app.fabric.microsoft.com/links/SJ5wVO19En?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare&bookmarkGuid=c964f109-a243-4282-9765-edfe9330625c">
    <img src="https://img.shields.io/badge/Portfolio-Live_Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" />
  </a>
</p>

---

## ⭐ If you found this project useful

Feel free to explore the notebook, visualizations, and presentation to reproduce the analysis and extend the research.
