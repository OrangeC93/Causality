## 因果关系的种种小迷惑
- 假的相关性：在一段时间内，有些变量会产生看似高度相关的走向，这是所谓的causally unrelated. 比如：缅因州的离婚率和人工黄油使用率。
- 传说：比如Bill Smith活到了105岁，他说他的秘诀是每天吃个turnip，这个只能说明两者同时发生，但是并不能说明吃turnip能让他长寿也不代表其他人这样做也会长寿。
- 科学报道：新闻总是引导性的用因果相关词，但是却没有任何依据，比如：positive link between video games and academic performance, study suggests.
- 逆向因果：即使存在因果关系，有时候也说不清到底谁是因谁是果，比如：绿化和运动，喜欢运动的人更喜欢住在绿化多的地方？还是绿化多的地方吸引了喜欢运动的人。

## 潜在结果和反设事实
- treatment(exposure) and outcome: 假设我们关心treatment A 对 outcome Y 的因果效应
  - 实验组: 接不接种流感疫苗 A=1 接种 A=0 没有接种
  - 结果: 人得流感的时间
- 潜在结果（在treatment decision还没定下来前）: what we would see under each possible treatment option
  - Y1: 接种疫苗下，多长时间人会得流感
  - Y0: 没有接种疫苗下，多长时间人会得流感
- 反设事实（在treatment decision定下来后）：如果实验组是A=1，那么反设事实就是Y0，如果实验组是A=0, 那么反设事实就是Y1

## 假设干预
- 可以干预性：变量的因果影响是可以被人工干预的
  - 必须只有一个版本的实验组（no hidden versions of treatment）：比如想要看BMI对健康的影响，但是控制BMI到特定的值可能会有很多方法，比如吸烟，不吃饭等，所以weight不能直接人工干预，这会导致很多结果
- 不可变变量：无法改变不可变变量，比如种族，年龄，性别
  - 改变不可变变量变成可变变量：比如种族 = 简历上的种族，肥胖 = 肥胖手术，社会地位 = 红包

什么是因果影响：there's a only causal effect if Y1 != Y0, 也就是说既需要知道Y1也需要知道Y0，并且两个不”相等“

## 因果关系
- Average Causal Effect: E(Y1-Y0) average value of Y if everyone was treated with A1 minus average value of Y if everyone was treated with A=0
  - 例子 Regional A=1 vs genral A=0 anesthesia for hip fracture surgery on risk of major pulmonary complications
  - 假设 E（Y1-Y0） = -0.1 代表 the probability of major pulmonary complications is lower by 0.1 if given regional anesthesia compared with general anesthesia

- Conditioning vs Setting: E（Y1-Y0）！= E（Y|A=1）- E（Y|A=0）原因是 expected value of Y given A=1 限制了subpopulation of people who had A=1 actually, 而他们可能跟whol额population 不同
  - E（Y|A=1）means of Y among people with A=1
  - E（Y1) means of Y if the whole population was treated with A=1

- 其他的因果影响
  - E（Y1/Y0）: causal relative risk
  - E（Y1-Y0|A=1）: causal effect of treatment on the treated
  - E（Y1-Y0|V=v）:average causal effect in the subpopulation with covariate V=v

