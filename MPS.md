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
