# Statistics
- [Statistics](#statistics)
  - [0. A/B testing vs. hypothesis testing](#0-ab-testing-vs-hypothesis-testing)
  - [1. A/B Testing](#1-ab-testing)
  - [2. Hypothesis Testing (Continuous Data)](#2-hypothesis-testing-continuous-data)
    - [One-sample T-Test](#one-sample-t-test)
    - [Two-Sample T-Test (Independent)](#two-sample-t-test-independent)
    - [Paired Samples (Dependent Groups)](#paired-samples-dependent-groups)
      - [Paired T-Test](#paired-t-test)
      - [Wilcoxon Signed-Rank Test (Non-Parametric)](#wilcoxon-signed-rank-test-non-parametric)
    - [One-Way ANOVA](#one-way-anova)
    - [Mann-Whitney U Test (Non-Parametric)](#mann-whitney-u-test-non-parametric)
  - [3. Hypothesis Testing (Categorical Data)](#3-hypothesis-testing-categorical-data)
    - [Chi-Squared Test of Independence](#chi-squared-test-of-independence)
  - [More info](#more-info)

## 0. A/B testing vs. hypothesis testing

| Concept            | Definition                                                                                                                                                         | Focus                                                                  |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------- |
| Hypothesis Testing | The general statistical framework for testing any assumption (e.g., "Is the average height of men different from women?", "Does this drug lower blood pressure?"). | Statistical Validity: P-values, confidence intervals, null hypotheses. |
| A/B Testing        | A specific experimental design applied to product/marketing where you split traffic into two groups to see which performs better.                                  | Business Decision: "Which version makes more money/conversions?"       |

## 1. A/B Testing

## 2. Hypothesis Testing (Continuous Data)

Comparing means (e.g., Average Revenue Per User, Time on Site).

### One-sample T-Test

Checks if a sample mean differs from a known population mean or specific value (e.g., "Is our average delivery time really 30 mins?").

```python
from scipy import stats

data = [31, 29, 30, 32, 30, 31, 32]
target_value = 30

stat, p_val = stats.ttest_1samp(data, target_value)
print(f"P-value: {p_val:.4f}")
```
> **Docs:** [Scipy ttest_1samp](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_1samp.html)


### Two-Sample T-Test (Independent)

Compares the means of two independent groups (e.g., Control vs. Treatment).

**Assumption:** Variances are equal (if not, use `equal_var=False` for Welch’s t-test).

```python
from scipy import stats

group_a = [23, 25, 28, 30, 22]
group_b = [28, 30, 32, 29, 31]

# equal_var=False performs Welch's t-test (safer default)
stat, p_val = stats.ttest_ind(group_a, group_b, equal_var=False)
```
> **Docs:** [Scipy ttest_ind](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_ind.html)

### Paired Samples (Dependent Groups)
Comparing the same subjects at two different times (e.g., Before vs. After) or matched pairs.

#### Paired T-Test
Comparing the same subjects at two different times (e.g., Before vs. After) or matched pairs.
Checks if the mean difference between paired observations is zero. Used when the *differences* are normally distributed.

```python
from scipy import stats

before = [30, 29, 31, 32, 33]
after  = [28, 27, 29, 31, 30]

# ttest_rel = "Related" samples
stat, p_val = stats.ttest_rel(before, after)
print(f"P-value: {p_val:.4f}")

```
> **Docs:** [Scipy ttest_rel](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_rel.html)

#### Wilcoxon Signed-Rank Test (Non-Parametric)

The alternative to the Paired T-Test when the differences are **not normal**. It ranks the magnitude of the changes.

```python
from scipy import stats

# checks if the distribution of the differences is symmetric around zero
stat, p_val = stats.wilcoxon(before, after)
```
> **Docs:** [Scipy Wilcoxon](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.wilcoxon.html)

### One-Way ANOVA

Compares means across 3+ groups. If P < 0.05, at least one group is different. You need post-hoc tests (e.g. Tukey's HSD) to find *which* one.

```python
from scipy import stats

group_1 = [85, 86, 88]
group_2 = [90, 92, 93]
group_3 = [95, 96, 98]

stat, p_val = stats.f_oneway(group_1, group_2, group_3)
```
> **Docs:** [Scipy f_oneway](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.f_oneway.html)

> **Note:** There are other types of ANOVA such as 
### Mann-Whitney U Test (Non-Parametric)

The alternative to the T-test when data is **not normal** (skewed) or sample size is small. Compares medians/rankings rather than means.

```python
from scipy import stats

stat, p_val = stats.mannwhitneyu(group_a, group_b)
```
> **Docs:** [Scipy mannwhitneyu](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.mannwhitneyu.html)

> **Note:** If you need to analyze the magnitude or exact numerical differences (e.g. revenue), use bootstrapping instead of Mann-Whitney.


## 3. Hypothesis Testing (Categorical Data)

Comparing counts/proportions (e.g., Clicked vs. Didn't Click).

### Chi-Squared Test of Independence

Determines if two categorical variables are related. (e.g., Is "Device Type" associated with "Churn Rate"?).

**Requirement:** All expected cell counts > 5.

```python
from scipy.stats import chi2_contingency

# Contingency Table:
#           | Churned | Retained
# Mobile    |   30    |   70
# Desktop   |   20    |   80
data = [[30, 70], [20, 80]]

stat, p, dof, expected = chi2_contingency(data)
print(f"P-value: {p:.4f}")
```
> **Docs:** [Scipy chi2_contingency](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.chi2_contingency.html)


## More info

* [ANOVA - ES](https://cienciadedatos.net/documentos/pystats09-analisis-de-varianza-anova-python)
* [Statistics with Python](https://cienciadedatos.net/en/statistics-python)