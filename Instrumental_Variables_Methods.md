## Introduction to instrumental variables
Confounding
![image](/pictures/confounding_review.png)
Unmeasured confounding: (1)ignorability asuumption violated (2) biased estimates of causal effects (3) we cannot control for confounders and average over the distribution if we don't observe them all

Instrumental variables: an alternative causal inference method that doesn't rely on the ignorability assumption

Here, Z is an IV: Z->A->Y A<-X->Y
- Z affects treatment A, but not directly affect the outcome Y
- Think of Z as encouragement 

举例 (1)Concern: could be unmeasured confounders (2)Challenge: not ethical to randomly assign smoking to pregnant woman
- A: smoking during pregnancy yes or no 
- Y: birthweight
- X: parity, mother's age, weight ect
- Z: randomize to either receive encouragement to stop smoking Z=1 or receive usual care Z=0

Encouragement design: an intention-to-treat analysis would focus on the causal effect of encouragement
- E(Y z=1) - E(Y z=0)

What can we say about the causal effect of smoking itself: IV methods

## Randomized trials with noncompliance
Randomize trial:
- Z: randomization to treatment 
- A: treatment received
- Y: outcome
- Note: typically, not everyone assigned treatment will actually receive the treatment(non-compliance不服从)

Potential treatment:
- Az=1 = A1 (could ended up to treated or not treated)
- Az=0 = A0

Causal effect of assignment on receipt
- We can think of the average causal effect of treatment assignment on treatment received as E(A1-A0)
  - This is proportion treated if everyone had been assigned to received treatment, minus the proportion treated if no one had been assigned to receive the treatment, if perfect compliance, this would be 1
  - This is generally estimable from observed data as by randomization and consistency
  - E(A1) = E(A|Z=1)  E(A0) = E(A|Z=0)

## Compliance classes
Potential values of treatment: we can  classify people based on potential treatment
![image](/pictures/potential_treatment.png)
- Never takers(从来不做): we would not learn anything about the effect of teatment of this subpopulation, as there' s no variation in treatment received.
- Compliers(让你做啥你做啥): take treatment when encouraged to, and do not otherwise, in this group, treatment received is randomized.
- Defiers(让你做啥你反着来): in this group treatment received is also randomzed, but in the opposite way.
- Always takers(啥都做): in this group there's no variation in treatment received, no information about causal effect.

Causal effect: a motivation for using IV methods in general is concern about possible unmeasured confounding
- If there's unmeasured confounding, cannot marginalize over all confounders (via matching, IPTW, ect)
- IV methods do not focus on the average causal effect for the population, they focus on a **local average treatment effect**

Local average treatment effect
![image](/pictures/local_average_treatment_effect.png)
- This is causal bacause it contrasts counterfactuals in a common population
- Know as complier average causual effect (CACE)
  - This is a causal effect in subpopulation
  - A local causal effect
  - No inference about defiers, always takers, or never takers

Observed data
![image](/pictures/observed_treatment_effect.png)

Identifiability
- Compliance classes are also known as principle strata, these are latent (not directly observable)

## Assumptions
Assumptions about IVs if
- It's associated with the treatment
- It affects the outcome only throught its effect on treatment
  - This is known as the **exclusion restriction** which means Z cannot directly, or indirectly through its effect on U, affect the outcome

Identification challenge

**Monotonicity assumption: there's no defiers**
- No one consistently does the opposite of what they are told
- It is called monotonicity because the assumption is that the probability of treatment should increase with more encouragement

![image](/pictures/monotonicity.png)
Now we will have enough data for causal effect estimation

## Causal effect identification and estimation
Goal: estimate E(Ya=1 - Ya=0|compliers)

首先：let's begin with something we can identify, IIT effect
- E(Yz=1 - Yz=0) = E(Y|Z=1) - E(Y|Z=0)

![image](/pictures/y_z_1.png)
- Expected value of Y among people assigned treatment is a weighted average of the expected value of Y given Z=1 in the 3 subpopulation
- Note: among always takers and never takers, Z does nothing
  - E(Y|Z=1, always takers) = E(Y|always takers)
  - E(Y|Z=1, never takers) = E(Y|never takers)

整理后：
![image](/pictures/整理公式.png)

相减后：
![image](/pictures/整理后公式.png)

再次整理后：
![image](/pictures/整理后公式2.png)

第三次整理后：
![image](/pictures/整理后公式3.png)

最终公式：
![image](/pictures/最终公式.png)

总结
- IV require 2 key assumptions, the strongest of which is the exclusion restriction
- If one also makes the monotonicity assumption, then the complier average causal effect is identified
  - An estimator of it is just the standard ITT effect estimate divided by an estimate of the proportion of compliers
  - The ITT effect will in general be an under estimate of the CACE
## IVs in observational studies
如何发现IV:(1) It affects treatment can be checked with data（2）The validity of the exclusion restricion assumption will largely need to rely on subject matter knowledge

Example1: calendar time as IV
![image](/pictures/IV_eg1.png)
- It is associated with treatment received (sulfonylureas popular early, metformin popular late
- Exclusion restriction: calendar time could be associated with the outcome if other treatment practices or patient behavior changed during that time

Example2: distance as iv
![image](/pictures/Iv_eg2.png)

Other examples:
![image](/pictures/IV_egs.png)
## Two stage least squares
Two stage least squares is a method for estimating a causal effect in the instrumental variables setting
- Stage 1
![image](/pictures/stage1.png)
- Stage 2
![image](/pictures/stage2.png)
## Weak instruments

## R example
