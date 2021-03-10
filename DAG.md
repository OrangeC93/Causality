## Confounding（混淆变量）
Confounders are often defined variables that affect treatment and affect the outcome.
- 如果我assign treatment on 投币器，会影响到treatment但是不会影响outcome，那么投币器就不是confounder
- 如果一个人有癌症家族史，他更会得癌症（the outcome），但是家族史并不是影响treatment的因素，那么家族史不是一个confounder
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

## Paths and associations
- Fork形状： D<-E->F，DF有关
- Chain形状：D->E->F，DF有关 
- 反叉子形状：D->E<-F，E是碰撞机，但是DF无关

## Conditional independence (d-separation)
Blocking: paths can be blocked by conditioning on nodes in the path
- Folk Block: A<-G->B, AB有关
  - If we condition on G, the path from A to B is blocked
- Chain Block: A->G->B, AB有关
  - If we hold G fixed, make the same for AB, AB are not associated
- Collider Block: A->G<-B, AB无关, 但是如果conditioning On G, AB would be associated
  - 比如AB是两个开关，G是灯
  - AB开了会y影响G，但是AB无关
  - 如果G关掉了（conditioning）如果A开着，B就得关着，AB产生了association

Rules for d separation: D here stands for dependence. So, what we're thinking of is a path that has a dependency between nodes and we want to know does a set of variable C remove the dependency. So, we will say that it desperate them:

A path is d separated by a set of nodes C if:
- it contains a chain D -> E -> F and the middle part is in C
- it contains a fork D <- E ->F and the middle part is in C
- it contains an inverted fork D -> E <- F and the middle part is not in C, nor any decendants of it

Definition of d seperation: two nodes, A and B, are d-separated by a set of nodes C if it blocks every path from A to B, then given C, A and B are dependent. 
![image](/pictures/ignorability_assumption.png)

## Confounding revisited
What matters is not identifying specific confounder, but a set of variables that're sufficient to control for confounding. In order to do that, we need to block backdoor path from treatment to outcome.

Frontdoor path: from A to Y is the one that begins with an arrow emanating out of A
- 比如： A->Y X->A, X->Y. A->Y is the frontdoor path from A to Y, A directly affects Y.
- 比如： A->Z->Y X->A, X->Y. A->Z->Y is the frontdoor path from A to Y，A affects Y indirectly though its effect on Z. 如果我们想知道A对Y的影响, 此时不用control Z.
- Causual mediation analysis involves understanding frontdoor paths from A to Y, 这个chapter不涉及这个

Backdoor path: from A to Y that travel arrows going into A
- 比如 A->Y X->A, X->Y, 这里 A<-X->Y is the backdoor path from A to Y
- To sufficiently control for confounding, must identify a set of variables that block all backdoor paths from Trea tment to outcome.

## 方法1：Backdoor path criterion
Sufficient sets of confounders: a set of variables X is sufficient to control for confounding if: 
- It blocks all backdoor paths from treatment to outcome 
- It doesn't include any descendants of treatment

例子见pictures folder
![image](/pictures/dag_eg1.png)
![image](/pictures/dag_eg4.png)
![image](/pictures/dag_eg3.png)
![image](/pictures/dag_eg2.png)


DAG的方法虽然好，但是现实生活中，很难画出fairly accurate DAG.

## 方法2：Disjunctive cause criterion
另一个variable selection方法叫：Disjunctive cause criterion，控制所有影响treatment和outcome的variables

举例：
- observed pre treatment variables {MWV}
- unobserved pre treatment variables {U1U2}
- 假设我们知道WV are causes of AY or both, M is not a cause of either A or Y

因此：
1. use all pre treatment covariates {MWV}
2. use variables based on disjunctive {WV}

总结：
- 并不能选出最小set of variables to controlfor
- but it's conceptually simpler
- is guaranteed to select a set of variables that are sufficient to control for confounding, if (1) such a set exist (2)we correctly identify all of the observed causes of A and Y
