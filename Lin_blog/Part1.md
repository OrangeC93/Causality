blog Yishi Lin：https://dango.rocks/categories/%E5%9B%A0%E6%9E%9C%E6%8E%A8%E6%96%AD/

现实案例：
- 在 feeds 流里刷到一个新推荐策略（treatment）的内容的用户留存(outcome)更高，他们的高留存是因为这个推荐策略导致的吗，这个策略究竟对留存的提升有多大效果？
- 上周投放了某游戏广告(treatment)的用户登录率(outcome)更高，他们的高登录率有多大程度是由广告带来的，有多大程度是由于他们本身就是高潜力用户？

为什么需要因果推断：
1. 相关性不等于因果关系
2. A/B test可以，但是有局限性（时间，流量，用户体验，很难全部尝试）

定义：
- Treatment：是否受到干预
- Potential outcome：怎样潜在结果
- Observed outcome：观察值如何

两种效应：
- ATE 平均因果效应 ATE = E(Y1- Y2)
- ATT 干预组平均因果效应 ATE = E(Y1- EY2|T=1)
