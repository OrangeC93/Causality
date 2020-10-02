## Confounding（混淆变量）
Confounders are often defined variables that affect treatment and affect the outcome.
- 如果我assign treatment on 投币器，会影响到treatment但是不会影响outcome，那么投币器就不是confounder
- 如果一个人有癌症家族史，他更会得癌症（the outcome），但是家族史并不是影响treatment decision的因素，那么家族史不是一个confounder
- 如果老人有得心脑血管疾病的可能（the outcome）而且他更可能服用他汀类药物（the treatment），那么年龄就是一个confounder

Confounder control
- 发现一组X变量能hold住ignorability假设，那么这组变量就足以控制confounding
- 利用统计方法来控住这些变量并且估测因果影响

## Causal Graphs(因果图表)
好处：（1）发现哪个变量需要控制（2）能让假设更明显 ignorability

简单图表
- A->Y A影响Y, A and Y are knowns as nodes and vertices, it might not be a single A or Y
- A-Y A和Y有关系

DAG(directed acyclic graphs直接的非循环图表)
（1）no undirected paths (2）no cycles

- A->Z: A是Z的父亲，Z是A的孩子
- A->Z->D: D是A的后代

## DAG之间的关系和概率矩阵
DAG encode assumptions about dependencies between nodes/varaibles
- 哪些变量相互independent
- 哪些变量仙湖conditionally independent

例如：D->A->B C
- P(C|A,B,D)=P(C), 说明C独立于其他所有变量
- P(B|A,C,D)=P(B|A)
- P(B|D)!=P(B),说明BD是marginally dependent
- P(D|A,B,C)=P(D|A)

Decomposition: start with roots(nodes with no parents), proceed down the descendant line, always conditioning on parents

例如：D->A->B C
- P(A,B,C,D) = P(C)P(D)P(A|D)P(B|A)

例如：D->A D->B->C
- P(A,B,C,D) = P(D)P(A|D)P(B|D)P(C|B)

例如：D->A->C D->B->C
- P(A,B,C,D) = P(D)P(A|D)P(B|D)P(C|A,B)

一个DAG只有一个probability distribution但是一个probability distribution可能对应多个DAG
