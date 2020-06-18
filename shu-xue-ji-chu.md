# 数学基础

## 01. 泰勒公式

### 定义

        泰勒公式是将一个在 $$x=x_0$$ 处具有n阶导数的函数 $$f(x)$$ 利用关于 $$(x-x_0)$$ 的n次多项式来逼近函数的方法。

### 公式

        若函数在包含 $$x_0$$ 的某个闭区间 $$[a,b]$$ 上具有n阶导数，且在开区间 $$(a,b)$$ 上具有 $$(n+1)$$ 阶导数，则对闭区间\[a,b\]上任意一点x，成立下式： $$f(x)=\frac{f\left(x_{0}\right)}{0 !}+\frac{f^{\prime}\left(x_{0}\right)}{1 !}\left(x-x_{0}\right)+\frac{f^{\prime \prime}\left(x_{0}\right)}{2 !}\left(x-x_{0}\right)^{2}+\ldots+\frac{f^{(n)}\left(x_{0}\right)}{n !}\left(x-x_{0}\right)^{n}+R_{n}(x)$$   
其中， $$f^{(n)}\left(x_{0}\right)$$ 表示 $$f(x)$$ 的n阶导数，等号后的多项式称为函数 $$f(x)$$ 在 $$x_0$$ 处的泰勒展开式，剩余的 $$R_n(x)$$ 是泰勒公式的余项，是 $$(x-x_0)^n$$ 的高阶无穷小。

### 常用函数的泰勒公式

1.  $$e^{x}=1+\frac{1}{1 !} x+\frac{1}{2 !} x^{2}+\frac{1}{3 !} x^{3}+o\left(x^{3}\right)$$ 
2. $$\ln (1+x)=x-\frac{1}{2} x^{2}+\frac{1}{3} x^{3}+o\left(x^{3}\right)$$ 
3. $$\sin x=x-\frac{1}{3 !} x^{3}+\frac{1}{5 !} x^{5}+o\left(x^{5}\right)$$ 
4.  $$\arcsin x=x+\frac{1}{2} \times \frac{x^{3}}{3}+\frac{1 \times 3}{2 \times 4} \times \frac{x^{5}}{5}+\frac{1 \times 3 \times 5}{2 \times 4 \times 6} \times \frac{x^{7}}{7}+o\left(x^{7}\right)$$ 
5. $$\cos x=1-\frac{1}{2 !} x^{2}+\frac{1}{4 !} x^{4}+o\left(x^{4}\right)$$ 
6. $$\frac{1}{1-x}=1+x+x^{2}+x^{3}+o\left(x^{3}\right)$$ 
7. $$(1+x)^{a}=1+\frac{a}{1 !} x+\frac{a(a-1)}{2 !} x^{2}+\frac{a(a-1)(a-2)}{3 !} x^{3}+o\left(x^{3}\right)$$ 

