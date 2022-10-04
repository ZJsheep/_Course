### Parent Selection (Chap. 5.2)

- Fitness proportion
- Ranking
  - Linear
  - Exponential
  - How to implement the probability
- Tournament
- Over-selection for large population

### Theory (Chap. 16)

- 最重要的 Scheme theory
	- e.g. Holland 算了 SGA 里的结果
	- Building block theorem: 短的、低阶的、健康度高的 building block 更容易存活
	- 缺陷
		- Deception：健康的组装出不健康的，及其反面
		- Hitchhiking：不健康的基因搭顺风车
		- 只考虑到 destructive effect，没看到 constructive effect（指 building block theorem 及类似分析
- 与 Scheme 相对的 Gene Linkage
	- Estimation of Distribution Alg
		- 频率当概率，训练贝叶斯网络，然后采样出下一代
	- 其他也这样，先求分布再采样
- Dynmic System：mixing matrix，selection matrix，构成一个力场将基因型拉向最优点
- Markov Chain：每个种群都是一个状态，太多了
- 一些指标：统计量、化归主义，takeover time，mixing time
- 还有连续空间中的 EA 分析
- NFL

### 一些随记

- Michigan-style LCS 和强化学习结合，不是很理解

- 感觉可以去了解一下概率图模型 PGM，分为两类：
	- 有向图：贝叶斯网络 BN
	- 无向图：马尔可夫随机场

- 模型蒸馏

