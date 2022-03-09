## Diagnosis and Analysis of High-speed Transmission Eqiopment based on Ensemble Learning
- 高速齿轮，发电风车用的（？

- 多同构传感器
- 知识结构化迁移
- 学习目标有明显的代价差异和序关系
	- 停机检修要代价

### 数据获得

### 特征提取
- 要先正规化
- 直方图信号 $\rightarrow$ 正规化信号

- 固有频率、固有频率整数倍、故障频率
- 载波、旁瓣波形、envelop（包络线）
- 信息熵：$Ent = \sum_{x}-p(x)\log p(x)=\mathbb{E}[-\log p(x)]=\mathbb{E}[\frac{1}{\log p(x)}]$
	- 出现频率越低，信息越多，信息熵越高
	- log 是因为表示用二进制编码需要多长

### 分类模型
- 归约类别，减少类别数量
- 类别不平衡
	- 用 easy ensemble
- 集成学习模型