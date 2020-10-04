## Observational studies

随机实验： treatment A would be determined by coin toss-effectively erasing the arrow from X to A, so there's no backdoor path from A to Y. The distribution of pre treated variable X that affect Y are the same in both treatment groups (covariate balance). Thus, if the outcome distribution ends up differing, it will not be because of differences in X, X is dealt with at the design phase.

Why not always randomize:
- 很贵
- 有时候不道德
- 不愿意参加
- 需要一段时间出结果（但是往往已经无效了）

观察实验：
- 计划的 prospective, observational studies with active data collection
- 已有数据 retrospective, passive data collection 

观察的时候，the distribution of X will differ between treatment groups

Matching方法: 可以将观察实验变成more randomized实验，主要思想就是match individuals in the treated group A=1 to individuals in the control group A=0 on the covariates X

Matching好处：（1）在设计实验的步骤就控制住confounders，因此不用手动修改outcome（2）可以保证positivity assumption（3）outcome计算也变得很简单（4）matching之后就可以认为是个随机实验

## Overview of Matching
Single covariate: 很简单

Multiple covariates：很难 match on full set of covariates. 在一个随机实验中，treated和control subject are not perfect matches either, the distribution of covariates is balanced between groups 叫做 stochastic balance，matching **closely** on covariates can achieve stochastic balance

目标人群：注意到我们 making the distribution of covariates in the control population(对照组) look like that in the treated population（实验组）, 因此，you're estimating causal effect of treatment (实验组) on the treated

Fine balance: 实际中很难找到完美的matches，因此我们可以接受一个non ideal matches 如果treated和control group 有同样的distribution of covaraites.

Number of matches:
- One to one (pair mathcing): match exactly one control to every treated subject
- Many to on: match some fixed number K controls to every treated subject
- Variable: sometimes match 1, sometimes more than 1, control to treated subjects

## Matching directly on confounders
如何match： some metric of closeness (1) Mahalanobis distance 马哈拉诺比斯 (2) robust Mahalanobis distance

Mahalanobis distance: 可以认为是square root of the sum of squared distances between each covariate scaled by the covariance matrx, 

Robust Mahalanobis distance: Mahalanobis distance可能会受到outliers影响, 但是ranks might be more relevant, eg highest and 2nd highest ranked values of covariates perhaps should be treated as similar, even if the values are far apart.

## Greedy(nearest-neighbor) matching 
步骤:
1. randomly order list of treated subjects and control subjects
2. start with the first treated subject. Match to the control with the smallest distance (this is greedy)
3. remove the matched control from the list of available matches
4. move on to the next treated subject. Match to the control with the smallest distance.
5. repeat step 3 and 4 until you have matched all treated subjects

好处：（1）直接，简单，容易解释，很快

坏处：（1）对init order比较敏感（2）并不是最优，没有考虑到全局，有可能有bad matches，参考optimal matching

Caliper: we might prefer to exclude treated subjects for whom there does not exist a good match. A bad match can be defined using caliper-maximum acceptable distance(if no matches within caliper, positivity assumption would be violated, so excludng these subjects makes assumption more realistc, drawback is that population is harder to define). 

## Optimal matching

优点和缺点：最小化全局distance，计算较慢

Sparse optimal matching: 加一些constraints which can be imposed to make optimal matching computationally feasible for larger data sets. 比如：match within hospitals in a multi-site clinical study, match within primary disease category.

## Accessing balance
Did matching work? 
- hypothesis test: test for a difference in means between treated and controls for each covariate, 2 sample t-test, calculate p value. 但是，p value 和sample size有关系，如果sample size很大，容易导致small difference也容易导致small p value

- Standardized differene: the difference in means between groups, divided by the pooled standard deviation.
  - smd = (Xt-Xc)/sqrt((St^2+Sc^2)/2)
  - 好处：不依赖sample size
  - Rule of thumb：（1）value<0.1 indicate adequate balance (2) value 0.1-0.2 are not too alarming (3) values>0.2 indicate serious imbalance

举例
![Image](/pictures/smd_eg.png)

## Analyzign data after matching

randomization test 也叫 permutation tests, exact test, 主要思想：
- 计算test statistic from observed data
- 假设null hypothesis of no treatment effect 是真的
- 随机permute treatment assignment within pairs and 重新计算test statistic
- 重复多次，观察how unusual observed statistic is

举例（分类）
![Image](/pictures/mps_1.png)
![Image](/pictures/mps_2.png)
![Image](/pictures/mps_3.png)

工具包：
- McNemar test（分类）: 以上描述的等于McNemar test，r包里面有个macnemar.test(matrix)，直接可以用
- ttest（continious data）
- logistic regression, stratified cox model, generalized estimating equations


## Sensitivity analysis
Possible hidden bias: 
- overt bias: there was imbalanced on observed covariates
- hidden bias: 可能会遗落一些 unobserved confounders

Hidden bias: R packages sensitivity22k
- πj和πk是probability that person j receives treatment, 假设jkmatched，那么πj和πk应该相等，there‘s no hidden bias
![Image](/pictures/sensitivity_analysis.png)
- 假设 we have evidence of a treatment effect，也就是系数=1，没有hidden bias
- 提高系数 until evidence of treatment effect goes away(no longer statistically significant)
  - 如果this happens when 系数=1.11， 说明very sensitive to unmeasured confounding (hidden bias)
  - 如果this happens when 系数=5， 说明 not very sensitive to unmeasured confounding (hidden bias)

## Propensity score
Propensity score: the probability of receiving treatment rather than control, given covariates X. Define A=1 for treatment and A=0 for control, denote the rppensity score for subject i by πi, πi=P(A=1|Xi).

比如：age was the only X variable and older people were more likely to get treatment. Then the propensity score would be larger for older ages P(A=1|age=60) > P(A=1|age=30), if person i has a propensity score value of 0.3, that means that, given their particular covariate values, there's a 30% chance they will be treated.

Balancing score: there're 2 subjects have the same value of propensity score, but they possibly have different covaraite values X. Despite the different covaraite values, they were both equally likely to have been treated, which means that both subjects' X is just as likely to be found in the treatment. If you restrict to a subpopulation of subjects who have the same value of the propensity score, there should be balance in the two treatment groups.
- P(X=x|π(X)=p, A=1) = P(X=x|π(X)=p, A=0)
- 如果 we match on the propensity score, we should achieve balance
  - considering we assumed ignorability - that treatment is randomized given X
  - conditioning on the propensity score, is conditioning on an allocation probability
  
估算propensity score
- randomized trial， 一般来说是知道的 P(A=1|X) = P（A=1）= 0.5
- observational study, it'll be unkown, 需要估算
  - 需要估算 P(A=1|X)， 可以用logistic regression, fit a model outcome A（因变量, treatment A=0 或者A=1）, covariates X（自变量s）, from the model get the predicted probability for each subject, that's estimated propensity score.

## Propensity score matching
Overlap: plot the propensity score distribution for treated and control group
- If it's well overlap, the positivity assumption seems reasonable

Trimming tails: if there's a lack of overlap, trimming the tails is an option, which means removing subjects who have extreme values of the propensity score.
- For example, removing:
  - control subjects whose propensity score is then than the minimum in the treatment 
  - treated subjects whose propensity score is greater than the maximum in the control group
 - Trimming the tails makes the positivity assumption more reasonalbe, preventing extrapolation

Matching: 
- 方法1: compute a distance between the propensity score for each treated subject with every control, then use nearest neighbor or optimal matching as before. 
- 事实上: logit(log-odds) of the propensity score is often used, rather than the propensity score itself
  - The propensity score is bounded betwen [0,1], makeing many values seem similar
  - Logit of the propensity score is unbounded, this transformation essentially stretches the distribution, while preserving ranks
  - Match on logit(π) rather than π

Caliper: 有个容忍的max distance，实际上一般用0.2 * sd of logit of the propensity score(当计算完propensity score from 逻辑回归, 然后take logit transform of the propensity score, then calculate the sd of the ransformed variable, set the caliper to 0.2 times the value from sd), it commonly done in practice because it semms to work well, but it's somewhat arbitrary, small caliper-less bias, more varaince.

## R example

