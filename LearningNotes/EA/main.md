- 主动学习 🧑‍🎓
	- identify the most valuable data to query their labels
- Submodular function
	- 可以理解为一个边际效用递减的函数
	- submodular mutual information: 相似程度
	- submodular conditional gain
	- Submodular conditioanl mutual information
- ![](attachments/Pasted%20image%2020220705192515.png)
- batch-mode

- SPC: Sparsity Preserved Crossover Operator
- SPM: Sparsity Preserved Mutation Operator

- [贝叶斯优化](贝叶斯优化.md) ❄
	- 感觉高斯过程和 aquisicition function 的具体形式得了解一下
- [多目标贝叶斯优化](多目标贝叶斯优化.md)

- transformer 🚗
	- [知乎](https://zhuanlan.zhihu.com/p/410776234) 行向量举例，怪的一批
	- attention model
	- attention is all you need Q, K, V matrix
- vision transformer

- [embedding](embedding.md) 🛏
	- encoder
	- decoder

- EA 算法的基本框架 🌴

- 标准化流 Normalization Flow ⏳

- 蒙特卡罗方法 MC 🕸
	- 近似计算积分，两种方法：
		1. 通过随机采样直接估计面积![](attachments/Pasted%20image%2020220623201915.png)
		2.  用 $f(x)(b-a)$ 来近似 $\int_{a}^b f(x)\mathrm dx$，其中 $f(x)$ 通过多次采样求平均

- QD: Quality Diversity
	- MAP-Elites family 算法
		- CMA-MAE

- 黑盒优化
	- model the landscape: 贝叶斯优化 BO
	- model the gradient: OpenAI-ES
	- model the distribution: CMA-ES
	- 用 GAN

- 和地科合作 ![](attachments/Pasted%20image%2020220705190055.png)

- ![](attachments/Pasted%20image%2020220707190245.png)

- ![](attachments/Pasted%20image%2020220707195102.png)
	- crossover operator：交叉算子

- 拟阵 Matroid
	- $M = (E,\mathcal I)$
	- $E$：gound set
	- $\mathcal I$：independent set
		- $\emptyset\in\mathcal I$
		- If $A\in\mathcal I$ and $B\subset A$, then $B\in\mathcal I$
		- If $A\in\mathcal I,B\in\mathcal I$ and $|B|>|A|$（基数）, then there is $b\in B\backslash A$ with $A\cup\{x\}\in\mathcal I$

- MGDA：multiobjective 随机梯度下降算法


