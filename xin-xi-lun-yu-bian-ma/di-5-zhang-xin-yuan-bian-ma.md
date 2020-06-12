# 第5章 信源编码

1. 编码分为信源编码和信道编码，其中信源编码又分为无失真和限失真。
2. 香农三大极限定理：无失真信源编码定理为第一极限定理，信道编码定理\(包括离散和连续信道\)为第二极限定理，限失真信源编码定理为第三极限定理。
3. 由于信源符号之间存在分布不均匀和相关性，使得信源存在冗余度，信源编码的主要任务就是减少冗余，提高编码效率。
4. 信源编码的基本途径有两个：使序列中的各个符号尽可能地相互独立，即解除相关性；使编码中各个符号出现的概率尽可能地相等，即概率均匀化。
5. 信源编码的作用： 1\)  符号变换：使信源的输出符号与信道

## 5.1 编码的概念

### **01. 码的分类**

1. 定长码：固定长度的码，码中所有码字的长度
2. 变长码：可变长度码，码中的码字长短不一

### 02. 分组码的属性

![&#x7801;&#x7684;&#x5206;&#x7C7B;](../.gitbook/assets/snipaste_2020-06-09_23-00-59.jpg)

1. 奇异码和非奇异码：若信源符号和码字是一一对应的，则该
2. 唯一可译码：任意有限长的码元序列，只能被唯一地分割
3. 非即时码和即时码：唯一可译码中又分为非即时码和即时码

   不是其它码字的前缀部分，有时叫做异前

### 03. 码树

1. 码树与码字对应：
   1. 树根：码字的起点
   2. 树枝数：码的进制数
   3. 节点：码字或码字的一部分
   4. 节数：码长
   5. 非满树：变长码
   6. 满树：等长码
2. 这样构造的码满足即时码的条件，因为从树根到每一个终端节点所走的路径均不相同，故一定满足对前缀的限制。
3. Kraft不等式：即时码（也是唯一可译码）

## 5.2 无失真信源编码定理

## 5.3 限失真信源编码定理

## 5.4 常用信源编码方法

### 01. 哈夫曼编码

### 02. 算术编码

### 03. LZ编码

### 04. 游程编码

### 05. 矢量量化编码

### 06. 预测编码

### 07. 交换编码
