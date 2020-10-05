## Intuition for Inverse Probability of Treatment Weighting (IPTW)
思路：rather than match, we could use all of the data, but down-weight some and up weight others.
- For treated subjects, weight by the inverse of P(A=1|X)
- For control subjects, weight by the inverse of P(A=0|X)

![image](/pictures/weights.png)
## More intuition for IPTW estimation
Observational studies
- In an observational study certain groups are oversampled relative to the hypothetical sample from a randomized trial
  - There's confounding in the original population
  - IPTW creates a pseudo-population where treatment assignment no longer depends on X
    - No confounding in the pseudo population
![image](/pictures/pseudo_population.png)

Estimator: 
![image](/pictures/estimator.png)

## Marginal structural models
Marginal structural models: model for the mean of potenial outcomes
- marginal: model that is not conditional on the confounders (population average)
- structural: model for ppotential outcomes, **not observed outcomes**

Linear MSM
![image](/pictures/linear_msm.png)

Logistic MSM
![image](/pictures/logistic_msm.png)

MSM with effect Modification
- MSMs can also include effect modifiers
- Suppose V is a variable that modifies the effect of A
- A linear MSM with effect modification
![image](/pictures/msm_effect_modification.png)

General MSM
![image](/pictures/general_msm.png)

## IPTW estimation
Estimation in MSMs: 不能直接用regression estimation方法，因为有从founding，所以we can create the pseudo population(otained from IPTW) which is free from confounding(assuming ignorability and positivity), we can therefore estimate MSM parameters by solving estimating equations for the observed data of pseudo population
![image](/pictures/estimation_msm.png)

具体步骤：
1. estimate propensity score
2. create weights
  - 1 divied by propensity score for treated subjects
  - 1 divided by 1 minus the propensity score for control subjects
3. specify the msm interest
4. use software to fit a weighted generalized linear model
5. use asymptotic(sandwich) variance estimator(or bootstrapping)
  - this accounts for fact that pseudo population might be larger than sample size

## Assessng balance
Balance after weighting: covariate balance can be checked on the weighted sample using standarized difference: in a table or in a plot.

Standardized differences after weighting: same idea, except on weighted means and weighted variances. 

If imbalance after weighting
- Can refine propensity score model
  - interactions
  - non linearity
- Can then reassess balance

## Distribution of weights
Why do weights matter: larger weights lead to noisier estimates of causal effects

Further intuition: bootstrapping
- randomly sample, with replacement, from the original sample
- estimate parameters
- repeat steps 1 and 2 many times
- the standard deviation of bootsrap estimates is an estimate of standard error
