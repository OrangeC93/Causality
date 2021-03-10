## 假因果关系
- 假的相关性：在一段时间内，有些变量会产生看似高度相关的走向，这是所谓的causally unrelated. 比如：缅因州的离婚率和人工黄油使用率。
- 传说：比如Bill Smith活到了105岁，他说他的秘诀是每天吃个turnip，这个只能说明两者同时发生，但是并不能说明吃turnip能让他长寿也不代表其他人这样做也会长寿。
- 科学报道：新闻总是引导性的用因果相关词，但是却没有任何依据，比如：positive link between video games and academic performance, study suggests.
- 逆向因果：即使存在因果关系，有时候也说不清到底谁是因谁是果，比如：绿化和运动，喜欢运动的人更喜欢住在绿化多的地方？还是绿化多的地方吸引了喜欢运动的人。

## 潜在结果和反设事实
- treatment(exposure) and outcome: 假设我们关心treatment A 对 outcome Y 的因果效应
  - 实验组: 接不接种流感疫苗 A=1 接种 A=0 没有接种
  - 结果: 人得流感的时间
- 潜在结果（在treatment decision还没定下来前）: what we would see under each possible treatment option
  - Y1: 接种疫苗下A1，多长时间人会得流感
  - Y0: 没有接种疫苗下A0，多长时间人会得流感
- 反设事实（在treatment decision定下来后）：如果实验组是A=1，那么反设事实就是Y0，如果实验组是A=0, 那么反设事实就是Y1

## 假设干预
- 可以干预性：变量的因果影响是可以被人工干预的
  - 必须只有一个版本的实验组（no hidden versions of treatment）：比如想要看BMI对健康的影响，但是控制BMI到特定的值可能会有很多方法，比如吸烟，不吃饭等，所以weight不能直接人工干预，这会导致很多结果
- 不可变变量：无法改变不可变变量，比如种族，年龄，性别
  - 改变不可变变量变成可变变量：比如种族 = 简历上的种族，肥胖 = 肥胖手术，社会地位 = 红包

什么是因果影响：there's a only causal effect if Y1 != Y0, 也就是说既需要知道Y1也需要知道Y0，并且两个不”相等“

## 因果结果
- Average Causal Effect 平均因果影响: E(Y1-Y0) 
  - Average value of Y if everyone was treated with A1 minus average value of Y if everyone was treated with A=0
  - 例子 regional A=1 vs general A=0 anesthesia for hip fracture surgery on risk of major pulmonary complications
  - 解释： 假设 E（Y1-Y0） = -0.1 代表 the probability of major pulmonary complications is lower by 0.1 if given regional anesthesia compared with general anesthesia

- Conditioning vs Setting: E（Y1-Y0）！= E（Y|A=1）- E（Y|A=0）原因是 expected value of Y given A=1 限制了subpopulation of people who had A=1 actually, 而他们可能跟whole population 不同
  - E（Y|A=1）means of Y among people with A=1
  - E（Y1) means of Y if the whole population was treated with A=1

- 其他的因果影响
  - E（Y1/Y0）: causal relative risk
  - E（Y1-Y0|A=1）: causal effect of treatment on the treated
  - E（Y1-Y0|V=v）:average causal effect in the subpopulation with covariate V=v

## 因果关系假设 （AB TEST 满足以下所有假设）
- SUTVA(stable unit treatment value assumption): 
  - no interference 用户相互独立无干扰
  - one version of treatment 个体潜在结果和最终观察结果只跟自己有关
  - 具有社交属性的实验，很难完全保证SUTVA
- Consistency assumption：the potential outcome under treatment A=a, Ya is equal to the observed outcome if the actual treatment received is A=a 也就是假设潜在结果和观察到的结果是一致的
- Ignorability assumption：given pre treatment covariates X, treatment assignment is independent from the potential outcomes(是否treated和potential outcom是相互独立的), 也就是Y0,Y1 独立 A|X
- Positivity assumption: for every set of values for X, treatment asignment was not determinitstic，也就是treatment assignment是随机的，如果不成立的话，可以适当移除特殊用户群

## 分层
Conditioning and Marginalizing:
- Average causal effect as the expected value of Y1 minus Y0. We didn't say given X. Because we needed to condition on X to be able to link the observed outcome to the potential outcome. 
- Marginal causual effect, meaning that does not include conidtioning on X, we'll just average over the X. 

Stratification which is one way that causal effects can be estimated or identified. Essentially, you would **stratify(meaning conditioning)** on important variables, and then **average** over the distribution of those variables which is also known as standardization. 

- Obtain a treatment effect within each stratum and then across stratum
- Then weighting by the probability (size) of each stratum

举例：对比两种糖尿病的治疗方法(treatment)：沙格列汀和西他列汀，outcome是MACE(主要不良心脏事件)，问题是沙格列汀用户在过去更可能会吃一些OAD的药(covariates)，而这种药会有更高的MACE风险

解决方案：
- 在两类subpopulations：用户过去有用过OAD，用户过去没有用过OAD 计算沙格列汀和西他列汀用户的MACE
- 然后计算加权均值（根据proportion of people in subpopulation），如果在以前OAD使用变量中，treatment can be thought of as randomized，这就是因果影响

Raw data
- probability of MACE given Saxa=yes: 350/4000
- probability of MACE given Saxa=no: 500/7000
- Saxa group observed to have higher risk

通过stratification data 可以发现：
- Saxa users are more likely to have prior OAD use 
- People with prior OAD use at higher risk for MACE

Mean potential outcome for saxa:
![Image](/pictures/stratification1.png)
Mean potential outcome for sitagliptin:
![Image](/pictures/stratification2.png)

So what we can see here is that the, once we marginalize we end up with the mean of the expected value for saxagliptin and sitagliptin is exactly the same, it's 7.7% in each group. So, in other words, the potential outcome is exactly the same if you gave everybody saxagliptin versus everybody sitagliptin. In principle, that's a very effective way to get a causal effect.

问题：
- 这可能会有many X varaibles needed to achieve ignorability，
- 导致很多空值
  - For example, if you stratify on age and blood pressure, there'll be many combinations of age and blood pressure for which you have no data
  - Thus, we need alternatives to standardization: 
## Incident user and active comparator designs
举例：瑜伽对血压有影响吗？
- incident user：完全没做过瑜伽 vs 从某一时间点开始，开始做瑜伽
- comparator design：看看其他运动对血压影响
