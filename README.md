# A/B Testing Analysis for Promotional Banner Performance

## 1. Project Overview

This project analyzes the result of an A/B test designed to compare the effectiveness of two promotional banner designs.

The main objective is to determine whether displaying the promotional price as a final price, such as **99K**, leads to a higher conversion rate than displaying the discount amount, such as **-100K**.

The analysis focuses on customer purchase behavior using a binary conversion variable, `is_buy`, where:

- `1` means the customer made a purchase
- `0` means the customer did not make a purchase

The dataset contains customer-level records assigned into two experimental groups:

- **Group 1:** Banner A
- **Group 2:** Banner B

---

## 2. Business Problem

The business wants to understand which promotional message performs better in driving customer purchases.

Two banner formats are compared:

| Group | Banner Type | Description |
|---|---|---|
| Group 1 | Banner A | Displays the final promotional price, e.g. 99K |
| Group 2 | Banner B | Displays the discount amount, e.g. -100K |

The key business question is:

> Does Banner A generate a higher conversion rate than Banner B?

---

## 3. Dataset Description

The analysis uses a CSV file named:

```text
abtesting.csv
```

Main columns used in the analysis:

| Column | Description |
|---|---|
| customer_id | Unique customer identifier |
| group | Experimental group assignment |
| is_buy | Purchase indicator, where 1 = purchased and 0 = not purchased |

---

## 4. Methodology

The analysis follows these main steps:

### Step 1: Load the Dataset

The dataset is loaded using `pandas`.

```python
import pandas as pd

df = pd.read_csv('data/abtesting.csv')
df.head()
```

### Step 2: Check Group Distribution

The number of records in each group is calculated to understand the sample distribution.

```python
group_counts = df['group'].value_counts()
total_records = df.shape[0]
```

### Step 3: Split Data by Group

The dataset is separated into two groups:

```python
df_group1 = df[df['group'] == 1]
df_group2 = df[df['group'] == 2]
```

### Step 4: Calculate Conversion Rate

For each group, the conversion rate is calculated as:

```text
Conversion Rate = Number of Buyers / Total Users
```

```python
buyers_group1 = df_group1[df_group1['is_buy'] == 1].shape[0]
total_group1 = df_group1.shape[0]
proportion_group1 = buyers_group1 / total_group1

buyers_group2 = df_group2[df_group2['is_buy'] == 1].shape[0]
total_group2 = df_group2.shape[0]
proportion_group2 = buyers_group2 / total_group2
```

---

## 5. Hypothesis Testing

A two-proportion z-test is used because:

- The experiment compares two independent groups
- The target variable is binary: buy or not buy
- The sample size is sufficiently large

### Null Hypothesis

```text
H0: Conversion Rate A = Conversion Rate B
```

There is no difference in conversion rate between the two banners.

### Alternative Hypothesis

```text
H1: Conversion Rate A > Conversion Rate B
```

Banner A, which displays the final promotional price, generates a higher conversion rate than Banner B.

---

## 6. Key Results

Based on the analysis:

| Metric | Banner A / Group 1 | Banner B / Group 2 |
|---|---:|---:|
| Conversion Rate | ~34.6% | ~29.0% |

Additional results:

| Metric | Value |
|---|---:|
| Absolute Difference | ~5.54 percentage points |
| Relative Difference | ~16.2% |
| Z-score | ~-10.453 |
| p-value | < 0.0001 |

The p-value is much smaller than common significance levels such as:

```text
alpha = 0.05
alpha = 0.01
```

Therefore, the null hypothesis is rejected.

---

## 7. Statistical Conclusion

The difference in conversion rate between the two banner designs is statistically significant.

This means the observed difference is unlikely to be caused by random variation.

Banner A performs significantly better than Banner B in terms of customer conversion.

---

## 8. Business Conclusion

The result suggests that customers respond better to seeing the final promotional price directly, rather than seeing the discount amount.

In this experiment:

- Banner A achieved a higher conversion rate
- Banner B performed worse than Banner A
- The difference is statistically significant
- Banner A should be kept as the preferred design

### Final Decision

```text
Do not use Banner B.
Continue using Banner A.
```

---

## 9. Possible External Factors

Although the result is statistically significant, several external factors may affect the validity of the A/B test:

- Test timing
- Marketing campaigns running at the same time
- User device differences
- Customer purchase history
- Market conditions
- Technical issues
- User learning effect
- Randomization quality

To improve the reliability of future tests, it is recommended to:

- Ensure random group assignment
- Run both versions at the same time
- Monitor external factors
- Analyze results by customer segments
- Repeat the test if necessary

---

## 10. Tools Used

- Python
- Pandas
- Statistical hypothesis testing
- Two-proportion z-test
- Google Colab / Jupyter Notebook

---

## 11. Project Files

Suggested GitHub repository structure:

```text
ab-testing-banner-analysis/
│
├── README.md
├── ab_testing_analysis.ipynb
├── abtesting.csv
```

---

## 12. How to Run

Clone this repository:

```bash
git clone https://github.com/your-username/ab-testing-banner-analysis.git
```

Install required packages:

```bash
pip install -r requirements.txt
```

Run the notebook or Python script:

```bash
python ab_testing_analysis.py
```

---

## 13. Recommended Improvements

Future analysis can be improved by:

- Adding confidence intervals for conversion rates
- Performing segment-level analysis
- Checking sample balance between groups
- Visualizing conversion rates with bar charts
- Calculating statistical power
- Testing multiple promotional messages
- Estimating business impact in revenue or profit

---

## 14. Summary

This project demonstrates how A/B testing can support data-driven decision-making in marketing and product optimization.

The analysis shows that Banner A, which displays the final price, performs better than Banner B, which displays the discount amount. The result is statistically significant and supports the decision to continue using Banner A.
