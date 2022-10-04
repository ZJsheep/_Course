# Distributed Model Reuse: FedPAN
- 发给局部进行训练
- 收集客户端更新的模型，然后服务器聚合
	- 简单方法：直接各个参数取平均 FedAvg
- 痛难点：
	- Non-IID：各个孤岛数据不是独立同分布的，有五种形式：
	- p(x|y) reads as "p x given y"
	- 所以要用区别化的方法对待每一个客户（client）
	- 神经网络重排不变性：神经元位置可能不一样，直接取平均可能不是同一个数据。
- 现有解决方案：神经元对齐
	- Indian buffet process（IBP？）、Chinese restaurant process（很耗时
	- Optimal Transport
	- 都是后处理对齐：聚合代价较高
- 提出解决方案：
	- 已有方案：Nested Dropout
		- 瞎几把丢掉一些神经元，效果反而可能变好
		- 使网络变得专用、稳定
		- 几何分布：第 i+1 个位置，前 i 个不丢，第 i+1（？） 个丢的概率 $P(i)=p^i(1-p)$ 
		- 会损失信息
	- 不用有序，只要位置相关
		- ？？？
		- 用多个不同频率的周期函数来表示位置信息（可以拟合任何周期函数
		- Position Aware Neurons（PAN）
		- 每个神经元输出加上或者乘以一个位置编码
## 应用
### 多 app 智能业务感知
- Sufficient Redundant