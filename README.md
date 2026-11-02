# COMPAS Analysis by Gender

In 2016, ProPublica released a study of Northpointe, Inc.'s COMPAS algorithm, which is used to estimate a defendant's risk of recidivism. The study found that COMPAS was racially biased against Black defendants by some fairness tests. This analysis replicates and adds to ProPublica's analysis to study bias against female defendants rather than Black defendants.

For race, COMPAS failed on error rates. For gender, it passed on error rates but failed on calibration, overstating female defendants' risk.

COMPAS (now sold by Equivant) has been used in courts in multiple U.S. states.

## Key findings

- **Error rates were nearly equal by gender.** False positive rates were 32.1% for women and 32.4% for men; false negative rates were 39.2% and 37.1%.
- **Calibration was unequal.** Women recidivated less often than men with the same risk label. In a Cox model, female defendants' hazard of recidivism was about two-thirds that of male defendants at every risk level (hazard ratios 0.65–0.69, with confidence intervals entirely below 1).
- **The violent score showed the same pattern.** Women received lower violent scores than comparable men, but women with the same violent label still recidivated violently less often (hazard ratios 0.48–0.70).
- **COMPAS ranked defendants about equally well within each sex.** Concordance was about 0.63 for both, and ROC AUCs were 0.69 for women and 0.70 for men.

Because women and men recidivate at different base rates in this data, no score can satisfy both calibration and equal error rates. For gender, COMPAS lands on the opposite side of that tradeoff from race.

## Data

The data and `truth_tables.py` come from ProPublica's [compas-analysis](https://github.com/propublica/compas-analysis) repository. The data covers defendants scored by COMPAS in Broward County, Florida, in 2013–2014. Recidivism is measured as a new arrest within two years.

## Methods

The analysis reruns ProPublica's tests with female defendants as the protected class, male defendants as the reference group, and race as one of several controls:

- Score distributions by sex
- Logistic regressions on the general and violent scores
- False positive and false negative rates
- Cox proportional hazards models and Kaplan-Meier survival curves
- ROC curves and AUC

Additions beyond ProPublica's analysis:

- A forest plot of hazard ratios and 95% confidence intervals
- Hazard ratios with confidence intervals for women vs. men on the violent score
- Proportional hazards tests (`cox.zph`) for each Cox model

## Files

- `COMPAS_by_gender_revised.ipynb`: the full analysis
- `COMPAS_Gender_Analysis.pdf`: the written report

## How to run

The notebook runs in Google Colab or Jupyter with Python and R (through `rpy2`). The first cell downloads the data from ProPublica's repository, and the R packages install automatically. Run all cells in order.

## Limitations

- Women are about one-fifth of the sample, so estimates for female defendants are less precise, especially for those labeled high risk and for the violent score models.
- The data records sex as a binary, so this analysis cannot assess whether COMPAS is biased against non-binary defendants.
- The data comes from one county over two years, and COMPAS may have changed since. Results may differ in other places or in the present.
- A new arrest does not necessarily mean a person reoffended.

## Note on AI use

I used AI to help edit the report and revise the code. I reviewed all changes. AI helped write this doc. I wrote the report. Cheers. 
