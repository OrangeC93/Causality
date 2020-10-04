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
![image](/pictures/pseudo-population.png)

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
## IPTW estimation
