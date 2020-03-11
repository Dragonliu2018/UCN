# 第2章 数学预备知识

## 求和的积分近似

* f\(x\)单调递减： $$\int_{m}^{n+1}f(x)dx \leq \sum_{j=m}^n {f(j)} \leq \int_{m-1}^{n}f(x)dx$$ 
* f\(x\)单调递增： $$\int_{m-1}^{n}f(x)dx \leq \sum_{j=m}^n {f(j)} \leq \int_{m}^{n+1}f(x)dx$$

## 递推关系

* f\(n\) = a \* f\(n-1\)，等比数列， $$S_n = \frac{a_1(1-q^n)}{1-q}(q\neq1)$$ 
* f\(n\) = a1 f\(n-1\) + a2 f\(n-2\)，特征方程： $$x^2 - a_1x-a_2 = 0$$ 特征根： $$r_1、r_2$$ $$f(n)= \begin{cases} c_1r_1^n+c_2r_2^n, & \text {$r_1 \neq r_2$} \\ c_1r_1^n+c_2*n*r_2^n, & \text{$r_1 = r_2$} \end{cases}$$ ，使用f\(1\)、f\(2\)求得c1、c2





