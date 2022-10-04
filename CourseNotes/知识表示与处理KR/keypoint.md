# ALC 及推理

## 定义

- 内涵式定义：define a term by specifying the necessary and sufficient conditions of being it
- 外延式定义：define a term by listing everything that falls under that definition
- 看待世界的方式：面向对象
	- existence：能与物理世界交互的能力
	- being：任何存在的事物
	- becoming：being 的辩护
	- entity：独立存在的 being
		- 一个 entity 展示给这个世界的所有信息都是形成这个entity 的必要条件
	- concept：一种在某些特点一致的群体
- 知识表示 vs. 机器学习
	- 内涵式定义 vs. 外延式定义
	- 机器学习算法评价：它有多大能力去在 training data 上学习一个“内涵式定义”，再用这个定义在 test data 上展现其学习能力

## 语言

- 理想的知识表示语言
	- 有足够的表达力表示物理世界中的知识
	- 人类可以理解它的语义
	- 机器可以理解它的语义，且该语言可计算（数学语言）
- formal language：
	- 特点
		- 有确定的字母表（意味着语言中单词的组成只能使用字母表里面的元素） 
		- 有确定的语法规则（意味着必须按照这个语法规则组成复杂短语或句子）
		-  有确定的语义解释（意味着必须按照这个方法去解释句子中的每个元素）
			- 自然语言不满足这一点
	- 分类
		- programming language
		- logical language
		- 自然语言的模糊性：六点半左右、黄色偏灰

## 本体

- 定义：a formal， explicit specification of a shared conceptualization
	- conceptualization 指的是一个 physical world 的抽象
	- explicit definition: a definition which formally sets out the meaning of a concept or expression， as by specifying **necessary and sufficient conditions** for being it

## 描述逻辑 DL

- 是一阶谓词逻辑 FOPL 的可判定子集
	- FOPL 不可判定
- OWL 是 DL 的编程语言
- ![](attachments/Pasted%20image%2020220618110344.png)
	- object property 的值域是 individual 或 class
	- data property 的值域是数据，类似于 metadata
- 一些成分
	- 类层面的知识叫 Terminology Box（TBox）/ concept hierarchy
	- 实体层面的知识的集合叫做 Assertional TBox（ABox）
	- Role Box（RBox）
		- H：role inclusion
	- 传递性
		- ALC + transitivity = S
		- 语义 $∀x∀y∀z((r(x， y)∧r(y， z)) → r(x， z))$
	- 如果有 RBox，则KB = TBox + ABox + RBox
		- 如果没有，则KB = TBox + ABox
		- 一般来说，一个本体等于一个 KB
	- axiom 可以表示所有 KB 里的东西，规定并不严格
- DL
	- 语法：表达力取决于哪些运算符可以被用来构建 complex concept / role
	- 语义：基于集合论和模型论
		- Interpretation：两部分
			- domain
			- 解释函数

## 推理

- 常见的推理运算包括： 
	1.  验证两个 concepts 之间是否存在 inclusion（subsumption）关系（equivalence 关系验证 可以转化成两个 inclusions 关系验证，下面涉及 equivalence 的地方也是一样） 
	2. 验证一个 individual 是否属于某个 concept（membership）
	3. 验证两个 individual 之间是否存在某二元关系（membership）
	4. 计算哪些 concepts 之间存在 inclusion 关系 
	5. 计算每一个 individual 都属于哪些 concept 
	6. 计算哪些对儿 individuals 存在二元关系
	7. 验证一个 ontology 是否 consistent（部分文献也叫 satisfiable）
	8. 验证一个 concept 是否 satisfiable
	9. ……
- 12378：Boolean questions；456：Non-Boolean questions
	- 1237 $\rightarrow$ 8
- 除了 7，背景知识（TBox、ABox）的增加对结果有影响

### 8. Concept Satisfiability

- Concept satisfiability 的问题只和 TBox 有关，和ABox 没关系。无论添加任何 ABox axioms 到 背景知识里面，都不影响一个 concept 的 satisfiability
	- 因为是**可满足性**，而不是是否被满足
- without TBox：Tableau，构建 $\mathcal I$ 使 C 非空
	- 先 NNF
	- ![](attachments/Pasted%20image%2020220618114401.png)![](attachments/Pasted%20image%2020220618114411.png)![](attachments/Pasted%20image%2020220618114426.png)![](attachments/Pasted%20image%2020220618114437.png)
	- branching 只需要存在一个能满足就行
- with TBox
	- 先转化 GCI 成 $C\sqsubseteq D\iff\top\sqsubseteq\neg C\sqcup D$
	- ![](attachments/Pasted%20image%2020220618115454.png)

### 7. Ontology Consistency

- 为什么要做：不一致的 ontology 没有意义
- 定义
	- 对于 GCI：$\mathcal I \models C\sqsubseteq D\iff C^{\mathcal I}\subseteq D^{\mathcal I}$
	- 对于 assertion：$\mathcal I \models C(a)\iff a^{\mathcal I}\in C^{\mathcal I}$
- check $C\sqsubseteq D$
	- TBox 增加 $\top\sqsubseteq \neg C\sqcup D$
	- 然后 check $\neg C\sqcup D$ 的 satisfiable 问题
	- 如果包含 ABox：直接加到 S 系统里，并对这个 individual 应用 universal rule 的更新（此时不必要加一个 $x:\neg C\sqcup D$ 再开始计算了

### 1. Concept Inclusion

- check $C\sqsubseteq D$
- 没有 TBox：
	- S 初始化为 $x:\neg(\neg C\sqcup D)$ 跑 Tableau
	- $\neg(\neg C\sqcup D)$ 不可满足则有 $C\sqsubseteq D$
- 有 TBox
	- 用 universal rule 进行类似的处理

### 2. Concept Membership

- check $a:C$
- 没有 KB
	- 说明 $C^{\mathcal I}$ 就是整个 domain
	- 转化成 $\neg C$ 的 satisfiability 问题，不可满足则 $a:C$ 成立
- 有 KB
	- 将 KB 所有 axiom 以某种形式加到 S 中
		- GCI 就变成 $\top\sqsubseteq\neg C\sqcup D$
		- assertion 就直接放进去
	- S 中添加 $a:\neg C$ 跑 tableau 验证可满足性

### 3. Role Membership

- 类似 2

## 问题和算法

- 决定性问题（decision problem）
	- 给定输入，输出一定是 yes 或 no 的问题
- 可决定的（decidable）
	- 对于一个 decision problem，如果存在一个 algorithm 使得在客观事实是 yes 的时候返回 yes，或者在客观事实是 no 的时候返回 no，则说明该问题是可决定的 (decidable)
	- 反例：一阶谓词的 validity checking
- 算法三个性质
	- 终止性：给定任何输入，该算法都会在有限步骤内终止 (不存在算法无限运行下去)
	- 正确性：对于一个 concept C 进行 satisfiability checking，如果 Tableau 返回 yes，则客观事实上 C 一定是 consistent 
		- 不存在算法返回了 yes，但是客观事实 C 是 unsatisfiable 的;或者返回了 no，客观事实是 satisfiable 的
	- 完备性：对于客观事实是 satisfiable 的 concept C，Tableau 都能返回 yes；对于客观事实是 unsatisfiable 的 concept C，Tableau 都能返回 no
		- 不存在一种情况，只针对某些 satisfiable 的 concept，算法才返回 yes；而对于另一些，算法计算不了
- decision precedure：需要满足以上三个性质
- Tableau 可以解决 ALC 上的标准推理问题
	- 包括 EL，但对 EL 来说不是最有效的

# EL 推理

- 只有 $C$, $r$, $\top$, $\sqcap$, $\exists$
	- ALC = EL + $\neg$
- 用来判断是否 $C\sqsubseteq_\mathcal T D$
- EL Terminology: 一些 $C\sqsubseteq D,C\equiv D$ 的集合，其中每个 concept 至多在左边出现一次
	- 不同于 EL TBox

## pre-processing

- 将 $\mathcal T$ 转化成 normal form $\mathcal T'$![](attachments/Pasted%20image%2020220618202548.png)
- 算法![](attachments/Pasted%20image%2020220618202943.png)

## 算法

- 初始化 $S(A)=A$, $R(r)=\emptyset$![](attachments/Pasted%20image%2020220618202853.png)
	- 顺序没有关系
- $A\sqsubseteq_\mathcal T B\iff B\in S(A)$

# FOPL 数据库

## World Assumption

- CWA（Closed World Assumption）：不知道的是错的
- OWA（Open World Assumption）：不知道的是不知道的

## 一阶逻辑

- vs. 命题逻辑、描述逻辑：
	- 有 variable，需要 variable assignment 函数
	- 真值由 assignment $\alpha$ 和 interpretation $\mathcal I$ 共同决定
		- $\alpha$ 负责解释将变量解释成常量
		- $\mathcal I$ 负责解释谓词和常量
	- $\mathcal I,\alpha\models F(x_1,x_2,\cdots,x_n)\iff\mathcal I\models F(\alpha(x_1),\alpha(x_2),\cdots,\alpha(x_n))$
- 变量
	- free：没有被 exists 或者 forall 限制
	- bound：被 exists 或者 forall 限制
- 表达式
	- closed：所有变量都被 bound
		- 不需要 assignment，可以直接由 $\mathcal I$ 决定真值
	- open：存在 free 的变量
		- 没有赋值时不能确定真值
- 语义！！！！！？？？？？

## FOPL Query

- 是一个一阶逻辑表达式，使用 n 元关系谓词，其中项的类型只有 variable（没有 constant 和 function（不是 predicate！））
	- 变量分为两种类型：free / answer variable，bound / quantified variable
	- query 的元数只计算表达式里 free variable 的数量（但是作为 FOPL formula 元数是包括 bound variable 的

## 使用一阶逻辑的 Database 存储数据

- ground sentence：一个为真的 formula，形如 $P(c_1,c_2,\cdots,c_n)$，其中 $c_i$ 全部是 constants
	- constants 就是 individual symbol
- database instance：一个 ground sentence 的有限集合 $\mathcal D$
- Ind($\mathcal D$)：$\mathcal D$ 里的 individual symbol 集合

### Database Query Answering

- n-ary query $Q$ 可以看作一个 mapping，输入 $\mathcal D$，输出 Ind($\mathcal D$)$^n$
	- n = 0：Boolean query，yes / no under CWA，yes / no / don't know under OWA
		- 传统关系数据库默认 CWA
- CWA 下，可以把 $\mathcal D$ 当作一个解释 $\mathcal I_D$ 来看待：
	- $\Delta^{\mathcal I}=$ ind($\mathcal D$)
	- 对于谓词 $P$，$(a_1,a_2,\cdots,a_{n})\in P^{\mathcal I_\mathcal D}\iff P(a_1,a_2,\cdots,a_n)\in D$
		- 为什么解释出来不是现实的元素？因为本来就不是真正的解释，只是用来表示数据库而已
	- $(a_1,\cdots,a_n)$ 是 $F(x_1,\cdots,x_n)$ 的 answer 的条件是 $\mathcal I_D\models F(a_1,\cdots,a_n)$
- OWA 下：
	- 模型是可以扩充的，因此 Ind($A$) $\subseteq$ domain 而非 = domain
	- $(a_1,\cdots,a_n)$ 是 $F(x_1,\cdots,x_n)$ 的 certanswer 的条件是 $\mathcal I\models F(a_1,\cdots,a_n)$ for all $\mathcal I\in$ Mod($\mathcal D$)，其中 Mod($\mathcal D$) 是 $\mathcal D$ 所有模型的集合（可以扩展）。形式化地定义，$\mathcal I\in$ Mod($\mathcal D$) if:
		- Ind($\mathcal D$) $\subseteq \Delta^\mathcal I$
		- if $P(a_1,\cdots,a_n)\in \mathcal D$, then $(a_1,\cdots,a_n)\in P^{\mathcal I_\mathcal D}$

## 使用描述逻辑的 ABox 存储数据

- 上面用的是基于一阶逻辑的 Database，这里用描述逻辑的 ABox
- $\mathcal I\in Mod(\mathcal A)$ if
	- $Ind(A)\subseteq\Delta^\mathcal I$
	- if $C(a)\in\mathcal A$, then $a\in C^\mathcal I$
	- if $r(a,b)\in\mathcal A$, then $(a,b)\in r^\mathcal I$

### ALC

- 给定 ALC ABox $\mathcal A$ 和 query $C(x)$
- 验证 $a$ 是不是一个 certanswer，相当于验证 $\mathcal A$ 的所有 model 是不是都是 $C(a)$ 的 model
- 转化为 $\mathcal A\;\cup\sim C(a)$ 是否可满足（即 $\mathcal A\cup \{a:\neg C\}$），如果 unsatisfiable，则是 certanswer，否则不是

### EL

- 构建 $\mathcal T$ 和 $\mathcal A$ 的解释 (S & R)，看能不能解释 $C(a)$
- 类似于 EL 的推理算法，但是多了 ABox
- ![](attachments/Pasted%20image%2020220618210904.png)![](attachments/Pasted%20image%2020220618210957.png)![](attachments/Pasted%20image%2020220618211013.png)
- 最后的解释为
	- $d\in A^{\mathcal I_{\mathcal T, \mathcal A}}$ if $A\in S(d)$
	- $(d_1,d_2)\in r^{\mathcal I_{\mathcal T,\mathcal A}}$ if $(d_1,d_2)\in R(r)$