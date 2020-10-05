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
- Never takers: we would not learn anything about the effect of teatment of this subpopulation, as there' s no variation in treatment received.
- Compliers: take treatment when encouraged to, and do not otherwise, in this group, treatment received is randomized.
- Defiers: in this group treatment received is also randomzed, but in the opposite way.
- Always takers: in this group there's no variation in treatment received, no information about causal effect.

Causal effect: a motivation for using IV methods in general is concern about possible unmeasured confounding
- If there's unmeasured confounding, cannot marginalize over all confounders (via matching, IPTW, ect)
- IV methods do not focus on the average causal effect for the population, they focus on a **local average treatment effect**

Local average treatment effect
![image](/pictures/local_average_treatment_effect.png)
