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
