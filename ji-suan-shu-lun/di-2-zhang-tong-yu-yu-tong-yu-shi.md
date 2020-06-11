# 第2章 同余与同余式

## 2.1 同余的概念与性质

### 0x01 理论知识

**同余定义**：给定一个正整数 m，如果用 m 去除任意两个整数 a 和 b 所得的余数相同，则称 a 和 b 模 m 同余， 记作 $$a \equiv b(\bmod m)$$ ；如果余数不同， 则称 a 和 b 模 m不同余， 记作 $$a \not\equiv b(\bmod m)$$ 。

**同余性质：**

1. $$a \equiv b(\bmod m)$$ 等价条件是 $$m | a-b$$ ，即 $$a=b+m t$$ ， t是整数。特别地， $$a \equiv 0(\bmod m) \Leftrightarrow m|a$$ 
2. 自反性：$$a \equiv a(\bmod m)$$ 
3. 对称性：$$\text {若}a \equiv b(\mathrm{mod} m), \text { 则 } b \equiv a(\bmod m)$$ 
4. 传递性： $$a \equiv b(\mathrm{mod} m), \quad b \equiv c(\mathrm{mod} m), \text { 则 } a \equiv c(\mathrm{mod} m)$$ 
5. 加减法： $$a \equiv b(\mathrm{mod} m), \quad c \equiv d(\mathrm{mod} m), \text { 则 } a \pm c \equiv b \pm d(\mathrm{mod} m)$$ ，特别地，对任意整数 k， $$a \pm k \equiv b \pm k(\bmod m)$$ 
6. 乘法： $$a \equiv b(\mathrm{mod} m), \quad c \equiv d(\mathrm{mod} m), \quad \text { 则 } a c \equiv b d(\mathrm{mod} m)$$ ，特别地，对任意整数 k ， $$a k \equiv b k(\bmod m)$$ （性质5.6推广： $$\text { 若 } a_{i} \equiv b_{i}(\mathrm{mod} m), \quad i=1, \cdots, k$$，对于任意整数 x ，有 $$\sum_{i=1}^{k} a_{i} x^{i} \equiv \sum_{i=1}^{k} b_{i} x^{i}(\bmod m)$$ ）
7. 除法：若 $$a \equiv b(\mathrm{mod} m), a=a_{1} d, \quad b=b_{1} d, \text { 且 }(d, m)=1$$ ，则 $$a_{1} \equiv b_{1}(\bmod m)$$ 
8. 乘法2： $$\text { 若 } a \equiv b(\bmod m), \text { 对任意正整数 } k, \text { 有 } a k \equiv b k(\bmod m k)$$ 
9. 除法2： $$\text { 若 } a \equiv b(\bmod m), \quad d |(a, b, m), \text { 则 } \frac{a}{d} \equiv \frac{b}{d}\left(\bmod \frac{m}{d}\right)$$ 
10. 最小公倍数：$$\text { 若 } a \equiv b\left(\bmod m_{i}\right), \quad i=1, \cdots, k, \quad \text { 则 } a \equiv b\left(\bmod \left[m_{1}, m_{2}, \dots, m_{k}\right]\right)$$ 
11. 因子： $$\text {若 } a \equiv b(\mathrm{mod} m), \quad d | m, \text { 则 } a \equiv b(\mathrm{mod} d)$$ 
12. 同余与最大公因数：$$\text { 若 } a \equiv b(\bmod m), \text { 则 }(a, m)=(b, m)$$ \(若 $$m|a,则m|b$$ \)

### 0x02 应考试题

* 同余性质12

![&#x6574;&#x9664;&#x4E0E;&#x540C;&#x4F59;](../.gitbook/assets/snipaste_2020-06-11_18-16-38.jpg)

## 2.2 剩余类与剩余系

### 0x01 理论知识

**剩余类定义**：设 $$m \in Z^{+}, \text {令 } K_{a}=\{x | x \equiv a(\bmod m)\}$$ ，称 $$K_a$$ 为模m的一个剩余类， 记作 $$a(\bmod m)$$ 。剩余类中的任一元素称为这个剩余类的代表。（同余关系是整数集合上的一种等价关系，因此可以用同余对整数集合 进行划分，形成剩余类）

**剩余类性质**：（由等价关系的性质易知，剩余类是由同余关系关系导出的等价类，因此满足等价类的所有性 质）

1. 每个剩余类都是一个非空集合；
2. 任意一个整数一定属于模 m的某一个剩余类，同一个剩余类中的数模 m同余，不同剩余类中的数模m不同余；
3. 对于模m的任意两个剩余类 $$K_{a} \text { 和 } K_{b}, \text { 要么 } K_{a}=K_{b}, \text { 要么 } K_{a} \cap K_{b}=\varnothing$$ 
4. 模 m的两两不同的剩余类有m个，且这m个剩余类的并集是全体整数。
5. 若 a，b在同一个剩余类中，即 $$a \equiv b(\bmod m)$$ ，由同余的性质12知， $$(a, m)=(b, m)$$，因此，若 $$(a, m)=1$$ ，则 $$K_a$$ 中所有数都与 m互质，此时， $$K_a$$ 称为与模 m 互质的剩余类。

**剩余系定义**：设 $$m \in Z^{+}, \quad K_{0}, K_{1}, \cdots, K_{m-1}$$ 模 m的 m个两两不同的剩余类，从每个剩余类 $$K_i$$ 中取出一个代表 $$a_i$$ ， $$a_{0}, a_{1}, \cdots, a_{m-1}$$ 叫做模m的一个完全剩余系。这 $$\varphi(m)$$ 个与 m互质的整数组成模m的一个简化剩余系。 $$0,1, \cdots, m-1$$ 称为模 m 的最小非负完全剩余系 ；当 m 是偶数时， $$-m / 2, \cdots,-1,0,1, \cdots, m / 2-1$$ 或 $$-m / 2+1, \cdots,-1,0,1, \cdots, m / 2$$ ，当 m 是奇数时， $$-(m-1) / 2, \cdots,-1,0,1, \cdots,(m-1) / 2$$ ，称为模 m的绝对最小完全剩余系。

**剩余系性质**： 

1. m个整数做成模 m的一个完全剩余系的充要条件是两两对模 m不同余； $$\varphi(m)$$ 个整数做成模 m 的一个简化剩余系的充要条件是两两对模 m 不同余且每个数都与 m 互质。
2. $$\text {设 } m \in Z^{+}, \quad(a, m)=1$$ ，任意整数 b ，若 x 遍历模 m的一个完全剩余系，则 $$a x+b$$ 也遍历模 m的一个完全剩余系。若 x 遍历模 m的一个简化剩余系，则ax也遍历模 m的一个简化剩余系。
3. 设 $$m_1$$ 和 $$m_2$$ 是互质的两个整数，若 $$x_1$$ 和 $$x_2$$ 分别遍历模 $$m_1$$ 和 $$m_2$$ 的一个完全剩余系，则 $$m_{1} x_{2}+m_{2} x_{1}$$ 遍历模 $$m_{1} m_{2}$$ 的一个完全剩余系。若 $$x_1$$ 和 $$x_2$$ 分别遍历模 $$m_1$$ 和 $$m_2$$ 的一个简化剩余系，则 $$m_{1} x_{2}+m_{2} x_{1}$$ 遍历模 $$m_{1} m_{2}$$ 的一个简化剩余系。

**欧拉函数定义**：一个完全剩余系中，与m互质的数的个数称为欧拉函数， 记作 $$\varphi(m)$$ 。（百度定义：在数论，对正整数n，欧拉函数是小于或等于n的正整数中与n互质的数的数目） 

**欧拉函数计算**：

1. 设 $$m_1$$ 和 $$m_2$$ 是互质的两个整数，则$$\varphi\left(m_1m_{2}\right)=\varphi\left(m_{1}\right) \cdot \varphi\left(m_{2}\right)$$ 
2. $$\varphi\left(p^{n}\right)=p^{n}-p^{n-1}$$ ， $$\varphi\left(p\right)=p-1$$ 
3. $$\text { 设 } a=p_{1}^{\alpha_{1}} p_{2}^{\alpha_{2}} \cdots p_{k}^{\alpha_{k}}, \text { 则 } \varphi(a)=a\left(1-\frac{1}{p_{1}}\right)\left(1-\frac{1}{p_{2}}\right) \cdots\left(1-\frac{1}{p_{k}}\right)$$ 

## 2.3 欧拉定理与费马小定理及其在 RSA 公钥密码算法中的应用

### 0x01 理论知识

**欧拉定理**：设m为大于 1 的正整数， $$(a, m)=1$$ ，则 $$a^{\varphi(m)} \equiv 1(\bmod m)$$ 

**费马小定理**：设 p 为素数，则 $$a^{p} \equiv a(\bmod p)$$ 

**应用\(RSA公钥密码算法\)：**此部分老师没做详细介绍，不是考试内容，故放到博客。[我跳](http://dragonliu.tk/2020/06/11/RSA%E5%8A%A0%E5%AF%86%E7%AE%97%E6%B3%95/)

### 0x02 应考试题

* 欧拉定理

![](../.gitbook/assets/snipaste_2020-06-11_20-51-43.jpg)

* 费马小定理+同余性质10\(最小公倍数\)

![](../.gitbook/assets/snipaste_2020-06-11_21-37-18.jpg)

## 2.4 同余式的概念及一次同余式

### 0x01 理论知识

**同余式定义**：设整系数多项式 $$f(x)=a_{n} x^{n}+a_{n-1} x^{n-1}+\cdots+a_{1} x+a_{0}$$ ，m 是一个正整数，则 $$f(x) \equiv 0(\bmod m)$$ 叫做模m的同余式。若 $$a_{n} \not\equiv 0(\bmod m)$$ ，则 n 叫做上式的次数。

## 2.5 孙子定理

### 0x01 理论知识

## 2.6 素数模高次同余式

### 0x01 理论知识

## 2.7 一般高次同余式的解数和解法

### 0x01 理论知识

