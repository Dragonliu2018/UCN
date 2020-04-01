# 第3章 多维随机变量及其分布

## 0x01 二维随机变量

### 01. 二维r.v.**定义**

　　设E是一个随机试验, 样本空间是S={e}**，**设X=X\(e\)和Y=Y\(e\)是定义在S上的r.v., 由它们构成的一个向量\(X, Y\), 叫做二维r.v.

　　**注:** 二维r.v. \(X, Y\)的性质不仅与X和Y有关，而且还 依赖于这两个r.v.的相互关系.

### 02. 二维r.v.\(联合\)分布函数

* **定义**：对于任意的实数 $$x,y$$ ，二元函数 $$F(x, y)=P \left\{(X\leq x) \bigcap (Y\leq y)\right\} = P\left\{ X\leq x, Y\leq y\right\}$$ 称为二维 $$r.v.(X,Y)$$ 的分布函数，或称为$$r.v.(X,Y)$$ 的联合分布函数
* **性质**
  * **非负规范性**：
    * $$\forall (x, y) \in R^2, 0\leq F(x,y) \leq 1,$$ 
    *  $$ F(+\infty, +\infty)=1, $$ 
    *  $$F(-\infty, -\infty)=F(x, -\infty)= F(-\infty, y)=0, $$ $$F(+\infty, -\infty)=?  F(+\infty, y)=?F(x, +\infty)=?$$ 
  * **单调不减性：固定其中一个变量，另一个单调不减**
  * **右连续性：固定其中一个变量，另一个右连续**
  * 对于任意的 $$x_1<x_2,y_1<y_2$$ ，下述不等式成立： $$F(x_2,y_2)+F(x_1,y_1)-F(x_1,y_2)-F(x_2, y_1)\geq 0$$ 

### 03. 二维离散型r.v.

* **分布律**：若二维 $$r.v.(X,Y)$$ 的所有可能取值是有限对或可列多对，则称 $$(X,Y)$$ 为离散型 $$r.v.$$ 记 $$P\left\{X=x_i, Y=y_i\right\}=p_{ij}，i=1,2,3...$$ 则有 $$p_{ij}\geq 0，\sum_i\sum_jp_{ij}=1$$ ，则称其为离散型 $$r.v.(X,Y)$$ 的分布律，或r.v.X和Y的联合分布律

### 04. 二维连续型r.v.

* **定义**：若 $$F(x,y)= \int_{-\infty}^y\int_{-\infty}^{x}f(u,v)dudv$$  ，则称 $$(X,Y)$$ 为连续型二维r.v.，其中非负函数 $$f(x,y) $$ 称为 $$(X,Y)$$ 的概率密度，或称为X和Y的联合概率密度
* **性质**：
  * $$f(x,y)\geq 0$$ 
  * $$ \int_{-\infty}^{+\infty}\int_{-\infty}^{+\infty}f(x,y)dxdy = F(+\infty, +\infty)=1$$ 
  * 设G是xoy平面上的一个区域，点\(x,y\)落在G内的概率为： $$ \int\int_{G}f(x,y)dxdy$$
  * 若f\(x, y\)在点\(x, y\)连续，则有 $$\frac{ ∂^2F(x,y)}{ ∂x∂y} = f(x, y)$$ 
* **分布律转分布函数：** $$F(x,y)=\sum_{x_i\leq x,y_j\leq y}p_{ij}$$ ，即对一切满足 $$x_i\leq x,y_j\leq y$$  的i, j求和

## 0x02 边缘分布

### 01. 边缘分布函数

* 二维r.v.\(X,Y\)关于X的边缘分布函数： $$F_X(x) = P\left\{ X\leq x\right\}=P\left\{ X\leq x ,Y<+\infty \right\}=F(x,+\infty)$$ 
* $$F_Y(x) = F(+\infty,y)$$ 

### 02. 边缘分布律

* X的分布律： $$P\left\{ X=x_i\right\}=\sum_{j=1}^{+\infty}p_{ij}=p_{i.},i=1,2,3...$$ 
* Y的分布律： $$P\left\{ Y=y_j\right\}=\sum_{i=1}^{+\infty}p_{ij}=p_{.j},j=1,2,3...$$ 
*  $$p_{i.}(i=1,2...)$$ 和 $$p_{.j}(j=1,2...)$$ 是 \(X, Y\) 关于 X 和关于 Y 的边缘分布律

### 03. 边缘概率密度

* $$f_X(x) = \int_{-\infty}^{+\infty}f(x,y)dy$$ 
* $$f_Y(y) = \int_{-\infty}^{+\infty}f(x,y)dx$$ 
* 连续型二维r.v.的均匀分布： $$f(x,y)= \begin{cases}   \frac{1}{A}  ,  & {(x,y)\in G} \\         0, & \text{其他}         \end{cases}$$ 
* 二维正态分布： $$(X,Y)\sim  N(μ_1,μ_2, σ^2_1, σ^2_2, ρ )$$ ，可得X，Y的边缘分布函数 $$X\sim (μ_1,σ^2_1) ,  Y\sim (μ_2,σ^2_2) $$ 
* **注**: 由二维随机变量\(X,Y\)的概率分布\(X,Y\)的联合分布可唯一地确定X和Y的边缘分布, 反之, 若已知 X,Y的边缘分布, 并不一定能确定它们的联合分布

## 0x03 条件分布

### 01. 二维离散型r.v.

　　设 $$p_{i.}>0,p_{.j}>0$$ ，则：

* 在 $$Y = y_j$$ 的条件下r.v.X的条件分布律： $$P\left\{X=x_i|Y=y_j\right\}=\frac{P\left\{X=x_i, Y=y_j\right\}}{P\left\{Y=y_j\right\}}=\frac{p_{ij}}{p_{.j}},i=1,2,3...$$ 
* 在 $$X = x_i$$ 的条件下r.v.Y的条件分布律： $$P\left\{Y=y_j \right|X=x_i\}=\frac{P\left\{X=x_i, Y=y_j\right\}}{P\left\{X=x_i\right\}}=\frac{p_{ij}}{p_{i.}},j=1,2,3...$$ 

### 02. 二维连续型r.v.的条件分布

* 在 Y = y 的条件下 X 的条件分布函数： $$F_{X|Y}(x|y)或P\left\{X\leq x|Y=y\right\}$$ 
* $$F_{X|Y}(x|y) = \int_{-\infty}^{x}\frac{f(x,y)}{f_Y(y)} dx$$ 
* 在条件 Y = y 下 X 的条件概率密度： $$f_{X|Y}(x|y) = \frac{f(x,y)}{f_Y(y)} $$ 

## 0x04 相互独立的随机变量

### 01. 定义

　　设\(X, Y\) 为二位随机变量，若对于所有的 x，y，有 $$P\left\{ X\leq x, Y\leq y\right\} = P\left\{X\leq x\right\}*P\left\{Y\leq y\right\}$$ ，即 $$F(x,y)=F_X(x)*F_Y(y)$$ ，则称 X 和 Y 相互独立。

### 02. 等价定义

* 当 \(X, Y\) 为离散型r.v.时，X 和 Y 独立等价于 $$P\left\{ X=x_i,Y=y_j\right\} = P\left\{X=x_i\right\} *P\left\{Y=y_j\right\}, i.j=1,2,3...$$  
* 当 \(X, Y\) 为连续型r.v.时，X 和 Y 独立等价于 $$f(x,y)=f_X(x)*f_Y(y)$$

### 03. 命题

* 设\(X, Y\)服从二维正态分布, 则X, Y相互独立的充要条件是 $$ρ=0$$ 

### 04. 重要定理

* 设 \(X1, X2, …, Xm\) 和 \(Y1, Y2, …  Yn\) 相互独立，则 Xi \(i=1,2, …,m\) 和 Yj \( j=1,2, …,n\)相互独立，又若h, g 是连续函数, 则 h\(X1, X2, …, Xm\) 和 g \(Y1, Y2, …  Yn\)  相互独立. 

## 0x05 两个r.v.的函数的分布

### 01. 和\(Z=X+Y\)的分布

#### 分布函数法求解

*  $$f_Z(z)=\int_{-\infty}^{+\infty}f(z-y, y)dy$$ 
*  $$f_Z(z)=\int_{-\infty}^{+\infty}f(x,z-x)dx$$ 

#### 卷积公式 $$f_X*f_Y$$ （X、Y相互独立）

* $$f_Z(z)=\int_{-\infty}^{+\infty}f_X(x)*f_Y(z-x)dx=\int_{-\infty}^{+\infty}f_X(z-y)*f_Y(y)dy$$ 

#### 重要结论

* 正态分布：设 $$X_k\sim N(μ_k, σ^2_k)(k=1,2,3...)且X_1,X_2,X_3,...,X_n$$ 相互独立，则它们的和 $$k_1X_1+...+k_nX_n\sim N(k_1μ_1+...+k_nμ_n, k^2_1σ^2_1+...+k^2_nσ^2_n)$$ 

### 02. 商\(Z=X/Y\)的分布

#### 分布函数求解

* $$f_Z(z)=\int_{-\infty}^{+\infty}f(zy, y)|y|dy$$ 

### 03. M=max\(X,Y\)及m=min\(X, Y\)的分布

#### 前提：X,Y相互独立, 分布函数分别为FX\(x\)和FY\(y\)，M=max\(X,Y\)，N=min\(X,Y\)

* $$F_M(z)=F_X(z)*F_Y(z) $$ 
* $$F_N(z)=1-(1-F_X(z))*(1-F_Y(z)) $$ 

#### 重要结论

* 当X1,X2,…,Xni.i.d.（独立同分布）时, 设分布函数为F\(x\)
  * $$F_{max}(z)=F(x)^n $$ 
  * $$F_{min}(z)=(1-F(x))^n$$ 

### 04. 离散型r.v. 的函数的分布

#### 前提：设X,Y是离散型r.v.且相互独立, 其分布律分别为: P{X=i}=pi,i=0,1,2,3,…,    P{Y=j}=qj,j=0,1,2,3,…, 求Z=X+Y的分布律.

* $$P\left\{X+Y=i\right\}=\sum_{k=0}^{i}p_kq_{i-k},i=0,1,2...$$ 

#### 结论

* 设X,Y是相互独立的r.v., 分别服从参数为 $$λ_1、λ_2$$ 的泊松分布, $$Z=X+Y\sim π(λ_1+λ_2)$$ 



