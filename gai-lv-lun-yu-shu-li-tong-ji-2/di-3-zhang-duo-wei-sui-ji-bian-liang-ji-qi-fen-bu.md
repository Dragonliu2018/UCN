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
  * $$ \int_{-\infty}^{+\infty}\int_{-\infty}^{+\infty}f(x,y)dxdy = F(+\infty, -\infty)=1$$ 
  * 设G是xoy平面上的一个区域，点\(x,y\)落在G内的概率为： $$ \int\int_{G}f(x,y)dxdy$$
  * 若f\(x, y\)在点\(x, y\)连续，则有 $$\frac{ ∂^2F(x,y)}{ ∂x∂y} = f(x, y)$$ 
* **分布律转分布函数：** $$F(x,y)=\sum_{x_i\leq x,y_j\leq y}p_{ij}$$ ，即对一切满足 $$x_i\leq x,y_j\leq y$$  的i, j求和

## 0x02 边缘分布





　







