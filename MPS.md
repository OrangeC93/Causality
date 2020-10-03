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
步骤
1. randomly order list of treated subjects and control subjects
2. start with the first treated subject. Match to the control with the smallest distance (this is greedy)
3. remove the matched control from the list of available matches
4. move on to the next treated subject. Match to the control with the smallest distance.
5. repeat step 3 and 4 until you have matched all treated subjects

- 好处：（1）直接，简单，容易解释，很快
- 坏处：（1）对init order比较敏感（2）并不是最优，没有考虑到全局，有可能有bad matches

caliper： we might prefer to exclude treated subjects for whom there does not exist a good match. A bad match can be defined using caliper-maximum acceptable distance(positivity assumption would be violated). 
