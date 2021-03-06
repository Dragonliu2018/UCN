---
description: P54 P61
---

# 第3章 平方剩余与原根

## 3.0 学习目标

* **初级（计算为主）**：利用欧拉判别条件、勒让德符号和雅可比符号判断平方剩余，合数模平方剩余的判断，一般二次同余式解的判断及求解，指数、原根、指标的计算。
* **进阶（推理证明为主）**：灵活应用平方剩余理论，灵活掌握指数、原根和指标的性质。

## 3.1 二次同余式与平方剩余的概念

### 0x01 理论知识

**平方剩余定义：**设 m 是正整数，若同余式 $$x^{2} \equiv a(\bmod m), \quad(a, m)=1 $$ 有解，则 a 叫做模 m 的平方剩余；否则，a 叫做模 m 的平方非剩余。

**判断二次同余式是否有解：**二次同余式的一般形式 $$ax^2+bx+c\equiv0(\bmod m)$$ 

1. 利用同余性质化简；
2. 将整数m分解为素数幂的乘积 $$m=p_{1}^{\alpha_{1}} p_{2}^{\alpha_{2}} \cdots p_{k}^{\alpha_{k}}$$ ，上述同余式等价于同余式组 $$a x^{2}+b x+c \equiv 0\left(\bmod p_{i}^{\alpha_{i}}\right)$$ ， $$i=1, \cdots, k$$ ，所以只需讨论 $$a x^{2}+b x+c \equiv 0\left(\bmod p^{\alpha}\right)$$
3. 这里可以利用同余性质因子：若模p无解，则上式无解。有解 $$x_1$$ 时，若 $$\left(f^{\prime}\left(x_{1}\right), p\right)=1$$ ，则对应上式一个解，判断结束；否则无法判断，继续执行第4步
4. 当 $$\left(4 a, p^{\alpha}\right)=1$$ 时，将上式两边同乘以 4a 可化为 $$(2 a x+b)^{2} \equiv b^{2}-4 a c\left(\bmod p^{\alpha}\right)$$ ，此时令 $$y=2 a x+b$$ ， $$A=b^{2}-4 a c$$， 上式就变为 $$y^{2} \equiv A\left(\bmod p^{\alpha}\right)$$ 
5. 当 $$\left(4 a, p^{\alpha}\right) \neq 1$$ 时，要么可以直接分析出 $$ax^2+bx+c\equiv0(\bmod m)$$ 是否有解，要么可以用其它方法将其转化为 $$y^{2} \equiv A\left(\bmod p^{\alpha}\right)$$ 的形式

**求解模m的所有平方剩余：**

1. 写出模m的简化剩余系；
2. 将其代入同余式 $$x^{2} \equiv a(\bmod m), \quad(a, m)=1 $$ ，同余式右边的就是平方剩余。
3. 注：若m是素数，简化剩余系可用绝对最小完全剩余系\(去掉0\)，便于计算\(只算正数即可\)。

### 0x02 应考试题

* 求解模m的所有平方剩余

![](../.gitbook/assets/snipaste_2020-06-10_14-58-10.jpg)

## 3.2 模为奇素数的平方剩余与平方非剩余

### 0x01 理论知识

**欧拉判别条件：**设 p 为奇素数，\(a,  p\) = 1，则 a 为模 p 的平方剩余的充分与必要条件是 $$a^{\frac{p-1}{2}} \equiv 1(\bmod p)$$ ，而 a 为模 p 的平方非剩余的充分与必要条件是 $$a^{\frac{p-1}{2}} \equiv-1(\bmod p)$$ ；且若 a 为模 p 的平方剩余，则同余式 $$x^{2} \equiv a(\bmod p)$$ 恰有两个解。

**模p性质：**设 p 为奇素数，则模 p 的简化剩余系中平方剩余与非平方剩余的个数各为 $$\frac{p-1}{2}$$ ，且 $$\frac{p-1}{2}$$  个平方剩余分别与序列 $$1^{2}, 2^{2}, \cdots,\left(\frac{p-1}{2}\right)^{2}$$ 中的一个数同余，且仅与一个数同余。

**勒让德符号定义：**设 p 为奇素数，对于任意整数 a ，定义 a 对 p 的勒让德符号如下： $$\left(\frac{a}{p}\right)=\left\{\begin{array}{l}\text { 1, 若 } a \text { 是模 } p \text { 的平方剩余 } \\ -1, \text { 若 } a \text { 是模 } p \text { 的平方非剩余 } \\ 0, \text { 若 } p | a\end{array}\right.$$ 

**勒让德符号性质：**

* **欧拉判别条件**：设 p 为奇素数，对于任意整数 a ，有 $$\left(\frac{a}{p}\right) \equiv a^{\frac{p-1}{2}}(\bmod p)$$ 。
* **性质1：** $$\left(\frac{1}{p}\right)=1,\left(\frac{-1}{p}\right)=(-1)^{\frac{p-1}{2}}$$ ，即当 p = 4m+1 时，-1是平方剩余；而当p=4m-1时，-1是平方非剩余；
* **性质2：** $$\text { 若 } a \equiv b(\bmod p), \quad \text { 则 }\left(\frac{a}{p}\right)=\left(\frac{b}{p}\right)$$ 
* **性质3：** $$\left(\frac{a b}{p}\right)=\left(\frac{a}{p}\right)\left(\frac{b}{p}\right),$$ 特别地，若 $$p \nmid b$$ ，则 $$\left(\frac{a b^{2}}{p}\right)=\left(\frac{a}{p}\right)\left(\frac{b}{p}\right)\left(\frac{b}{p}\right)=\left(\frac{a}{p}\right)$$ \(推广： $$\left(\frac{a_{1} a_{2} \cdots a_{n}}{p}\right)=\left(\frac{a_{1}}{p}\right)\left(\frac{a_{2}}{p}\right) \cdots\left(\frac{a_{n}}{p}\right)$$ \)
* **性质4：** $$\left(\frac{2}{p}\right)=(-1)^{\frac{p^{2}-1}{8}}$$ ，即当 $$p=8 m \pm 1$$ 时，2 是平方剩余，而当 $$p=8 m \pm 3$$ ，2 是平方非剩余
* **性质5\(二次反转定律\)：**若 p 和 q 为互质的奇素数，则 $$\left(\frac{q}{p}\right)=(-1)^{\frac{p-1}{2} \cdot \frac{q-1}{2}}\left(\frac{p}{q}\right)$$ 
* 设 $$a=\pm 2^{\alpha_{0}} q_{1}^{\alpha_{1}} q_{2}^{\alpha_{2}} \cdots q_{k}^{\alpha_{k}}$$ 则 $$\left(\frac{a}{p}\right)=\left(\frac{\pm 1}{p}\right) \cdot\left(\frac{2}{p}\right)^{\alpha_{0}} \cdot\left(\frac{q_{1}}{p}\right)^{\alpha_{1}} \ldots .\left(\frac{q_{k}}{p}\right)^{\alpha_{k}}$$ ，这样计算 $$\left(\frac{a}{p}\right)$$ 的问题就归结于计算下面的3种值： $$\left(\frac{\pm 1}{p}\right),\left(\frac{2}{p}\right),\left(\frac{q}{p}\right)(p, q \text { 均为奇素数 })$$ 

**雅可比符号定义：**设 $$m=p_{1} p_{2} \cdots p_{r}$$ 为奇素数的乘积，对任意整数 a ，定义 a 对 p 的雅可比符号为 $$\left(\frac{a}{m}\right)=\left(\frac{a}{p_{1}}\right)\left(\frac{a}{p_{2}}\right) \cdots\left(\frac{a}{p_{r}}\right)$$ ，其中， $$\left(\frac{a}{p_{i}}\right) 是 a 对 p_{i}$$ 的勒让德符号。  
**注**：雅可比符号并不能判断 $$x^{2} \equiv a(\bmod m)$$ 是否有解，用处是计算勒让德符号。

**雅可比符号性质：**

* **性质1：** $$\left(\frac{1}{m}\right)=1,\left(\frac{-1}{m}\right)=(-1)^{\frac{m-1}{2}}$$
* **性质2：** $$\text { 若 } a \equiv b(\bmod m), \quad \text { 则 }\left(\frac{a}{m}\right)=\left(\frac{b}{m}\right)$$ 
* **性质3：** $$\left(\frac{a b}{m}\right)=\left(\frac{a}{m}\right)\left(\frac{b}{m}\right),$$ 特别地，若 $$(b,m)=1$$ ，则 $$\left(\frac{a b^{2}}{m}\right)=\left(\frac{a}{m}\right)\left(\frac{b}{m}\right)\left(\frac{b}{m}\right)=\left(\frac{a}{m}\right)$$ 
* **性质4：** $$\left(\frac{2}{m}\right)=(-1)^{\frac{m^{2}-1}{8}}$$ 
* **性质5\(二次反转定律\)：**若m和 n 都是大于 1 的奇数，则 $$\left(\frac{m}{n}\right)=(-1)^{\frac{n-1}{2} \cdot \frac{m-1}{2}}\left(\frac{n}{m}\right)$$ 

### 0x02 应考试题

* 勒让德符号判断同余式是否有解

![&#x5B9A;&#x4E49;3.2.1](../.gitbook/assets/snipaste_2020-06-10_16-12-22.jpg)

* 使用雅可比符号计算勒让德符号

![](../.gitbook/assets/snipaste_2020-06-10_21-34-05.jpg)

## 3.3 模为合数的平方剩余与平方非剩余

### 0x01 理论知识

**合数模**： $$x^{2} \equiv a(\bmod m),(a, m)=1$$ ，设 $$m=2^{\alpha} p_{1}^{\alpha_{1}} p_{2}^{\alpha_{2}} \ldots p_{k}^{\alpha_{k}}$$ ，则其有解的充要条件为 $$\left\{\begin{aligned} x^{2} \equiv & a\left(\bmod 2^{\alpha}\right) \\ x^{2} \equiv & a\left(\bmod p_{1}^{\alpha_{1}}\right) \\ \vdots & \\ x^{2} \equiv & a\left(\bmod p_{k}^{\alpha_{k}}\right) \end{aligned}\right.$$ 有解，且有解时，合数模式的解数与上述同余式组各解的乘积相等。

**素数幂合数模：** $$x^{2} \equiv a\left(\bmod p^{\alpha}\right), \quad(a, p)=1$$ 有解的充要条件是 $$\left(\frac{a}{p}\right)=1$$ ，且有解时解数为 2。

**2的幂合数模：** $$x^{2} \equiv a\left(\bmod 2^{\alpha}\right), \quad(a, 2)=1$$ 有解的充要条件是：当 $$\alpha=1$$ 时，一解；当 $$\alpha=2$$ 时， $$a \equiv 1(\bmod 4)$$ ，且有解时解数为 2；当 $$\alpha \geq 3$$ 时， $$a \equiv 1(\bmod 8)$$ ，且有解时解数为 4。

**一般合数模：**设 $$m=2^{\alpha} p_{1}^{\alpha_{1}} p_{2}^{\alpha_{2}} \ldots p_{k}^{\alpha_{k}}$$ ，则有解的充要条件是：当 $$\alpha=2$$ 时， $$a \equiv 1(\bmod 4)$$； 当 $$\alpha \geq 3$$ 时， $$a \equiv 1(\bmod 8)$$ 且 $$\left(\frac{a}{p_{i}}\right)=1, i=1, \ldots k$$ ；  
有解时，  若 $$\alpha=0 或 1, $$ 则解数为 $$2^{k} $$； $$若 \alpha=2, 则解数为 2^{k+1} ;若 \alpha \geq 3,则解数为 2^{k+2}$$ 。

### 0x02 应考试题

## 3.4 指数及其基本性质

### 0x01 理论知识

**指数定义：**设m是大于1的整数，\(a, m\) = 1，则使得同余式 ****$$a^{\gamma} \equiv 1(\bmod m)$$ ****成立的最小正整数 $$\gamma$$ 叫做 a 对模 m 的指数，记作 $$ord_m(a)$$ 。如果 a 对模 m 的指数是 $$\phi(m)$$ ，则 a 叫做模 m 的一个原根。

**模m的指数表**：m的简化剩余系中所有数对模m的指数做成的表。

**指数性质**：

1.  设（a，m）= 1， $$ord_m(a)=\delta$$ ，则 $$1=a^0, a^1,\dots a^{\delta-1 }$$ 对模m两两不同余。特别地，a是模m的一个原根当且仅当 $$1=a^0, a^1,\dots a^{\delta-1 }$$ 是模m的一个简化剩余系。
2. 设m是大于1的整数，（a，m）= 1，则 $$a^{k} \equiv a^{s}(\bmod m)$$ 成立的充分与必要条件是 $$k \equiv s\left(\bmod \operatorname{ord}_{m}(a)\right)$$ 。特别地， $$a^{k} \equiv 1(\bmod m)$$ 的充分与必要条件是 $$k \equiv 0\left(\bmod \operatorname{ord}_{m}(a)\right)$$ ，即 $${ord}_{m}(a)|k$$ 。
3. 设m是大于1的整数，（a，m）=1，则 $$\operatorname{ord}_{m}(a) | \varphi(m)$$ 
4. 若a对模m的指数是 $$\delta_1 \delta_{2}$$ ， $$\delta_1>0$$ ， $$\delta_2>0$$ ，则 $$a^{\delta_1}>0$$ 对模m的指数是 $$\delta_{2}$$ 。

**求解指数**：

1. 法①：从1开始代入，直至 $$\varphi(m)$$ ，同时利用同余性质；
2. 法②：只代入 $$\varphi(m)$$ 的正因子。

### 0x02 应考试题

* 求解指数\(表\)1：利用同余性质简化计算

![&#x6CD5;1 &#x6C42;10&#x7684;&#x7B80;&#x5316;&#x5269;&#x4F59;&#x7CFB;&#x7684;&#x6307;&#x6570;](../.gitbook/assets/snipaste_2020-06-03_23-06-25.jpg)

* 求解指数\(表\)2：要求某个与 m互质的整数 a 的指数，只需验证 $$ \varphi(m)$$ 的所有正因数是否是 a 的指数即可。

![&#x6CD5;2 &#x5229;&#x7528;&#x63A8;&#x8BBA;3.4.2](../.gitbook/assets/snipaste_2020-06-04_09-18-22.jpg)

* 证明：若x对模m的指数是a，y对模m的指数是b，并且（a，b）= 1，则xy对模m的指数为ab。 

![&#x63A8;&#x8BBA;3.4.1 + &#x540C;&#x4F59;&#x6027;&#x8D28;](../.gitbook/assets/tim-tu-pian-20200604094734.jpg)

## 3.5 原根

### 0x01 理论知识

**原根存在定理：**模m的原根存在的充分与必要条件是 m = 2，4， $$p^{\alpha}$$ 或 $$2 p^{\alpha}$$ ，其中 p 为单质数。

**原根判别定理：**设 $$\phi(m)$$ 的所有不同素因数为 $$q_1,q_2, …, q_k$$ ，则 g 是模m原根的一个充分必要条件是 $$g^{\varphi(m) / q_{i}} \not \equiv 1(\bmod m), \quad( i=1,2, \cdots, k)$$ 

**指数性质4推广:** $$\text { 设 }(a, m)=1, \quad \operatorname{ord}_{m}(a)=\delta, \quad k \geq 0, \text { 则 } \operatorname{ord}_{m}\left(a^{k}\right)=\delta /(k, \delta)$$ 

**指数相同1:**  设 $$(a, m)=1, \operatorname{ord}_{m}(a)=\delta, \operatorname{ord}_{m}\left(a^{k}\right)=s$$ ，若 $$(k, \delta)=1$$ ，则 $$\operatorname{ord}_{m}(a)=\operatorname{ord}_{m}\left(a^{k}\right)$$ ，因此在模 m 的简化剩余系中，与 a 指数相同的数有$$\varphi\left(\operatorname{ord}_{m}(a)\right) $$ 个。

**指数相同2:**  a 是模 m 的一个原根，则当 $$(k, \varphi(\mathrm{m}))=1$$ ， $$a^k$$ 也是模 m 的一个原根，若原根的有 $$\phi(\phi(\mathrm{m}))$$ 个。

**求解所有原根**

1. 写出简化剩余系
2. 根据**定理3.5.2**从最小的开始试，得到一个原根
3. 根据得到的原根生成 $$\phi(\phi(\mathrm{m}))$$ 个原根。

### 0x02 应考试题

* 求解原根\(1\)：求解模10的所有原根。定理3.5.2

![&#x6C42;&#x89E3;&#x6240;&#x6709;&#x539F;&#x6839;](../.gitbook/assets/tim-tu-pian-20200605210937.jpg)

* 求解原根\(2\)：已知5是模23的一个原根，找出模23的所有原根。推论3.5.2

![](../.gitbook/assets/snipaste_2020-06-05_21-14-31.jpg)

* 如果知道了模m的一个原根a，则利用 定理3.4.1 可以用a表示出模m的一个简化剩余系，再利用 定理3.5.3，可以计算出简化剩余系中每个元素模m的指数。 

![](../.gitbook/assets/snipaste_2020-06-05_21-21-26.jpg)

## 3.6 指标

### 0x01 理论知识

**指标定义：**设 g 是模 m 的一个原根， 任意与 m 互质的整数 a ， 存在唯一整数 $$\gamma$$ ， $$1 \leq \gamma \leq \varphi(m)$$ ，使得 $$g^{\gamma} \equiv a(\bmod m)$$ 成立，这个整数 $$\gamma$$ 叫做以 g 为底的 a 对模 m 的指标或离散对数。记为 $$\gamma=\operatorname{ind}_{g} a \quad \text { (或 ind } a, \text { 或 }log_g a)$$ \(**注：**此处的指标与之前学的对数完全一致，仅仅加上取模的条件。\)

**指标性质：**

* **性质1\(指数性质2的特例\)**： $$\text { 若 } g^{\gamma_{2}} \equiv g^{\gamma_{1}}(\bmod m), \text { 则 } \gamma_{1} \equiv \gamma_{2}(\bmod \varphi(m))$$ 
* **性质2**：设 g 是模 m 的一个原根， $$a_{1}, a_{2}, \cdots ; a_{n}$$ ****是与 m 互质的 n 个整数，则$$ \operatorname{ind}_{g}\left(a_{1} a_{2} \cdots a_{n}\right) \equiv \operatorname{ind}_{g}\left(a_{1}\right)+\operatorname{ind}_{g}\left(a_{2}\right)+\cdots+\operatorname{ind}_{g}\left(a_{n}\right)(\bmod \varphi(m)) \$$ ，特别地， $$\operatorname{ind}_{g}\left(a^{n}\right) \equiv \operatorname{nind}_{g}(a)(\bmod \varphi(m))$$ 

**n次剩余定义：**如果 n 次同余式 $$x^{n} \equiv a(\bmod m),(a, m)=1$$ 有解，则 a 叫做模 m的 n 次剩余；否则， a 叫做模m的 n 次非剩余。

**n次剩余判定定理：**设 g 是模m的一个原根，则 $$x^{n} \equiv a(\bmod m),(a, m)=1$$ 有解的充分与必要条件是 $$(n, \varphi(m)) | \text { ind }_{g} a$$ ，且在有解的情况下，解数为 $$(n, \varphi(m))$$ 。

**求解高次同余式：**利用指标表和上述指标的性质， 当 $$m=2,4, p^{\alpha} \text { 或 } 2 p^{\alpha}$$ 时，可以得出如下求解方法：

1. 化成该形式 $$x^{n} \equiv a(\bmod m),(a, m)=1$$ 
2. 求模m的一个原根 g；
3. 求以 g 为底的模m的指标表；
4. 查指标表求 a 对应的指标；
5. 求解一次同余式 $$ny=\operatorname{ind} a(\bmod \varphi(m))$$ 
6. 再次查表，求以 y 为指标对应的数，即为解。

### 0x02 应考试题

* 求解简化剩余系中的指标：如果 g 是模 m 的一个原根， 则当 $$\gamma$$ 遍历模 $$\phi(\mathrm{m})$$ 的非负最小完全剩余系时， $$g^{\gamma}$$ 遍历模 m 的简化剩余系

![](../.gitbook/assets/snipaste_2020-06-10_22-45-53.jpg)

![](../.gitbook/assets/snipaste_2020-06-10_22-46-11.jpg)

* 求解高次同余式

![](../.gitbook/assets/snipaste_2020-06-10_22-47-51.jpg)

