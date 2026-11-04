# Customer Analytics: What Drives a Purchase? (Python-stats)

A statistical analysis of 500 customers to find out what is linked to a customer buying. Most things turned out not to matter. One thing did: **online customers buy 53.6% of the time, against 40.3% for offline customers (p = 0.0039).**

## Question
What is linked to a customer buying (`Purchased = Yes`)?

## Data
- 500 customers and 15 columns (7 numeric, 8 text), with no missing values and no repeated rows.
- 46.6% of customers made a purchase, so there is a good mix of buyers and non-buyers.
- Ages run from 18 to 64, and the average income is about 70,600.
- Provided by the Imarticus module. The CSV is not included in this repository. To run the notebook, put it in the same folder.

## What I did
1. **Loaded and checked the data:** size, types, missing values, duplicates.
2. **Built an automatic EDA report** with `ydata-profiling` and read its alerts instead of just generating it.
3. **Explored the data:** histograms, category counts and a correlation heatmap. The numeric columns are only weakly correlated (strongest r is about 0.09).
4. **Wrote three testable hypotheses** (with the help of GenAI) and screened every yes/no and category column against `Purchased`.
5. **Ran the main test**, then checked it was not a fluke.
6. **Wrote a business summary.**

## Results
| Hypothesis | Test | Result |
|---|---|---|
| Online use is linked to purchasing | Chi-square | χ² = 8.31 (df = 1), p = 0.0039, **linked** |
| Product category is linked to purchasing | Chi-square | χ² = 5.02, p = 0.170, no link |
| Discount users spend a different amount | Welch t-test | t = 1.01, p = 0.312, no link |

**How solid is the online result?**
- Without continuity correction: p = 0.0030. Fisher's exact test: p = 0.0031.
- It passes a Bonferroni correction for the 7 variables screened (threshold 0.0071).
- After adjusting for 11 other variables in a logistic regression, the odds ratio is 1.73 (95% CI 1.21–2.49, p = 0.003).
- The effect is small: Cramér's V is about 0.13. The 95% intervals (about 47–60% against 35–46%) don't overlap.

This shows a link, not proof of cause.

## Tools
Python, pandas, NumPy, SciPy, statsmodels, Matplotlib, Seaborn, ydata-profiling, Jupyter Notebook.

## Files
- `Customer_Analytics_Project.ipynb`: the full analysis
- `customer_eda_report.html` and `online_vs_purchase.png`: created when you run the notebook

## How GenAI was used
This was a GenAI-assisted module project. I used GenAI to suggest hypotheses and draft the business summary. The notebook records the prompts, and I edited the AI draft's wording.

## Author
Meer Adeen Ali · Hyderabad · [LinkedIn](https://www.linkedin.com/in/adeen-ali) · [GitHub](https://github.com/Adeen0504)

Built during the Imarticus Postgraduate Program in Data Science and Analytics with GenAI.
