# 第3章 数据结构

## 树

* **性质** 1. 任何两个结点只有一条通路 2. n个结点，\(n - 1\)条边 3. 再加一条边就构成回路 4. 深度\(根节点是第0层\)，高度\(树最深度\)
* **完全二叉树（满二叉树）** 1. n个结点，$$\lfloor \frac {n}{2}\rfloor$$个叶节点，$$\lceil \frac {n}{2}\rceil$$个非叶子节点 2. 高度$$\lfloor logn\rfloor$$

{% hint style="success" %}
**证明：**  
设完全二叉树的结点总数n，高度为k  
 $$2^0+2^1+...+2^k = n\\ 2^{k+1}-1=n\\  2^k \leq n < 2^{k+1}\\ k \leq log n < {k+1}\\ \therefore k = \lfloor logn\rfloor$$ 
{% endhint %}

* **几乎完全二叉树（完全二叉树）** 1. 存储形式：数组 2. 高度$$\lfloor logn\rfloor$$

{% hint style="success" %}
**证明：**  
设几乎完全二叉树的结点总数n，高度为k  
 $$2^k \leq n \leq 2^{k+1}-1\\ 2^k \leq n < 2^{k+1}\\ k \leq log n < {k+1}\\ \therefore k = \lfloor logn\rfloor$$ 
{% endhint %}



\*\*\*\*



  




