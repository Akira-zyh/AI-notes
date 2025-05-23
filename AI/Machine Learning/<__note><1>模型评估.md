# 术语

| 术语名称                                                 | 术语简介              |
| ---------------------------------------------------- | ----------------- |
| 错误率                                                  | 分类错误的样本占样本总数的比例   |
| 精度                                                   | $1-\text{错误率}$    |
| 误差                                                   | 实际预测输出与样本真实输出的差异  |
| 训练误差(经验误差)                                           | 训练集上的误差           |
| 泛化误差                                                 | 新样本上的误差           |
| [[<_explaination><1>过拟合与欠拟合#过拟合(Overfitting)\|过拟合]]  | 过于学习训练样本，导致泛化能力下降 |
| [[<_explaination><1>过拟合与欠拟合#欠拟合(Underfitting)\|欠拟合]] | 学习能力低下            |

# 评估方法

> 将数据集$D$==分为训练集`S`和测试集`T`==

## 留出法(hold-out)


> [!note] 留出法 hold-out
> **直接将$D$分为两个互斥集合，分别作为训练集`S`和测试集`T`** $$D = S \cup T \text{,} \; \varnothing = S \cap T$$
> 其中
>> 训练集`S`用于训练模型（==大约$\frac{2}{3}\sim\frac{4}{5}$的样例==）
>> 测试集`T`用于评估测试误差 $\rightarrow$ 作为泛化误差的估计（==至少包含30个样例==）

### 注意的问题

1. 训练/测试集的划分要尽可能保持数据分布的一致性
> 例如：分类任务中至少要保证样本的类别比例相似（ i.e. **分层采样**）

2. 确定了训练/测试集的样本比例，仍存在多种数据集$D$的划分方式

3. 单次使用留出法得到的估计结果不可靠，一般采用==若干次随机划分、重复进行实验评估==后，结果**取平均值作为留出法的评估结果**


## 交叉验证法(cross validation)/ k折交叉验证(k-fold cross validation)

![[截屏2025-01-20 09.26.21.png]]


> [!NOTE] 交叉验证 cross validation
> 将数据集$D$划分为`k`个**大小相似互斥**的子集，从$D$中[[<__note><1>模型评估#留出法(hold-out)#注意的问题|分层抽样]]得到
> 然后
>> 每次用**`k-1`个子集的并集**作为训练集，**剩下的一个子集**作为测试集

### 注意的问题

> [!info] `p`次`k`折交叉验证
> 1. 数据集$D$划分`k`个子集的方式不唯一，存在因样本划分不同导致引入的差别
>> **Remedy**：随机使用不同的划分重复`p`次（$\text{一共 }p*q\text{ 次训练/测试}$），最终评估这==`p`次`k`折交叉验证结果的均值==

假设数据集$D$中包含`m`个样本，若$k=m$，则得到**留一法(LOO)**


> [!NOTE] 留一法(LOO)
> 1. k=数据集$D$中样本个数，k个子集都只含一个样本，**划分方式唯一**
> 2. 训练集与数据集只相差一个样本，**评估结果往往比较准确**
> 3. **计算开销大**

## 自助法(bootstrapping) / 有返回采样


> [!NOTE] 核心思想——有返回采样产生数据集$D'$
> 给定含有`m`个样本的数据集$D$，==每次从$D$中随机挑选一个样本==，**拷贝**入$D'$，==重复`m`次==，得到含有`m`个样本的数据集$D'$
>> 样本在$m$次抽样中**始终不被采到**的概率约为36.8%$$\lim_{m \rightarrow \infty} \bigg(1 - \frac{1}{m}\bigg)^m \mapsto \frac{1}{e} \approx 0.368$$
>> 
 

> [!NOTE] 包外估计（out-of-bag estimate）
> 实际评估和期望评估的模型都使用$m$个样本，且仍然有数据总量的$\frac{1}{3}$可以用于测试，产生的测试结果叫做包外估计

### 优势
1. ==数据集较小，难以有效划分训练/训练集==时，很有用
2. 能从初始数据集中产生==多个不同的训练集==


### 劣势
1. 自助法产生的数据集改变了初始数据集的分布，会引入**估计偏差**

