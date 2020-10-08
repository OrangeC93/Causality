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
Marginal structural models: model for the mean of potential outcomes
- marginal: model that is not conditional on the confounders (population average)
- structural: model for potential outcomes, **not observed outcomes**

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
Estimation in MSMs: 不能直接用regression estimation方法，因为有confounding，所以we can create the pseudo population(otained from IPTW) which is free from confounding (assuming ignorability and positivity), we can therefore estimate MSM parameters by solving estimating equations for the observed data of pseudo population
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
Why do weights matter: larger weights lead to noisier estimates of causal effects, an extremely large weight means that the probability of that treatment was very small, thus large weights indicate near violation of the positivity assumption

Checking weights: 
- plot weight vs density or index vs sort(weight)
- summary statistics of weights

Further intuition: bootstrapping
- randomly sample, with replacement, from the original sample
- estimate parameters
- repeat steps 1 and 2 many times
- the standard deviation of bootsrap estimates is an estimate of standard error

## Remedies for large weights
Investigative step with very large weights:
- what's unusual about them?
- is there a problem with their data
- is there a problem with the propensity score model

方法1： trimming the tails, removing treated subjects whose propensity scores are above the 98th and control subjects whose propensity scores are below the 2nd, reminder: trimming the tails changes the population

方法2： weight truncation
- step1: determin a max allowable weight
  - could be a specific value
  - could be based on a percentile
- step2: if a weight is greater than the maximum allowable, set it to the maximum allowable value

- Trucation leads to bias but smaller variance, no trucation leads to unbiased, larger variance, truncating extremely large weights can result in estimators with lower mean squared error

## Doubly robust estimators
IPTW estimation:
![image](/pictures/iptw_estimation.png)

Regression based:
![image](/pictures/regression_based.png)

Doubly robust estimators(augmented IPTW estimarots): is an estimator that is unbiased if either the propensity score model or the outcome regression model are correctly specified
![image](/pictures/doubly_robust_estimator.png)
- In general, AIPTW estimators should be more efficient than regular IPTW estimators

## Example in R
- ipw and sandwich (robust variance estimator)
