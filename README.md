# Non-Parametric-Survival-Analysis-2-Log-Rank-Non-Parametric-Survival-Analysis-Test-
Explore the Log-Rank Test in survival analysis, comparing survival times among groups using Kaplan-Meier curves and multivariate log-rank tests.

# Log-Rank Test

This repository explores the Log-Rank Test, a non-parametric statistical method widely used in survival analysis to assess differences in survival times between groups. By comparing Kaplan-Meier survival curves generated for different groups, the Log-Rank Test determines if there are significant disparities in survival experiences over time. The demonstration utilizes a drug relapse dataset, investigating the time taken for individuals on drugs to relapse, with treatment categories represented by the 'herco' variable. After data preprocessing and stratifying survival curves, the multivariate log-rank test is performed to evaluate differences in survival distributions among drug categories.

```python
# Log-Rank Test Procedure
import matplotlib.pyplot as plt
from lifelines import KaplanMeierFitter
from lifelines.statistics import logrank_test

# Assuming df_DrugRelapse is your DataFrame
kmf = KaplanMeierFitter()

# Stratify by the 'herco' variable
drug_categories = df_DrugRelapse['herco'].unique()

# Plot and compare Kaplan-Meier survival curves
plt.figure(figsize=(10, 6))
for category in drug_categories:
    subset_data = df_DrugRelapse[df_DrugRelapse['herco'] == category]
    kmf.fit(subset_data['time'], event_observed=subset_data['censor'], label=f'Drug Category: {category}')
    kmf.plot_survival_function()

# Add plot labels and legend
plt.title('Stratified Kaplan-Meier Survival Curves by Drug Category')
plt.xlabel('Time')
plt.ylabel('Survival Probability')
plt.legend()
plt.show()

# Perform log-rank test
from lifelines.statistics import multivariate_logrank_test
results = multivariate_logrank_test(df_DrugRelapse['time'], df_DrugRelapse['herco'], event_observed=df_DrugRelapse['censor'])
print(results)
```

This project provides a comprehensive guide to the Log-Rank Test, aiding researchers and practitioners in survival analysis by offering practical demonstrations and interpretations of statistical tests.
