# 第7章 动态规划

## 0x01 Fibonacci数列\(ing\)

* **思路** 循环迭代，避免递归，也可用一维数组存储。
* **代码**

```c
long long fib(int n)
{
	//求Fibonacci数列
	long long f1 = 1, f2 = 1, ans = 1;
	for( int i=3; i<=n; i++ )
	{
		ans = f1 + f2;
		f1 = f2;
		f2 = ans;
	}
	return ans;
}//fib
```

* **算法分析** 时间复杂度：O\(n\)；如果利用数组，则空间复杂度：O\(n\)。时间复杂度为O\(logn\)的fn求值算法

## 0x02 二项式系数

* **思路** 利用二维数组存储求解，行表示k，列表示n；也可利用一维数组。
* **代码**

```c
//二维数组
long long bin(int n, int k)
{
	//求组合数C(n, k) 
	long long f[n+1][n+1];
	//初始化 
	for( int i=0; i<=k; i++ ){ 
		for( int j=1; j<=n; j++ ){
			if( i==0 || i==j )
				f[i][j] = 1;
			else
				f[i][j] = 0;
		}
	}
	//求解C(n, k)
	for( int i=1; i<=k; i++ ){
		for( int j=i+1; j<=n; j++ )
			f[i][j] = f[i-1][j-1] + f[i][j-1];
	} 
	//除去冗余的元素计算，按行遍历
	for( int i=1; i<=k; i++ ){
		for( int j=i+1; j<=i+n-k; j++ )
			f[i][j] = f[i-1][j-1] + f[i][j-1];
	} 
	//除去冗余的元素计算，按斜线遍历
	for( int d=1; d<=n-k; d++ ){
		for( int i=1; i<=k; i++ )
			f[i][i+d] = f[i-1][i+d-1] + f[i][i+d-1];
	}
	return f[k][n];
}//bin
```

```c
//一维数组
long long bin1(int n, int k)
{
	//利用一维数组求解组合数C(n, k)
	//按行遍历 
	if( n == k )//C(n, n)
		return 1;
	long long f[n-k+1];
	for( int i=1; i<=n-k; i++ ){ //初始化 
		f[i] = 1;
	} 
	for( int d=1; d<=k; d++ ){
		f[1] = f[1] + 1;
		for( int j=2; j<=n-k; j++ )
			f[j] = f[j] + f[j-1];
	} 
	return f[n-k];
	//按斜线遍历
	if( k == 0 )//C(n, 0)
		return 1;
	long long arr[k+1];
	for( int i=1; i<=k; i++ ){ //初始化 
		arr[i] = 1;
	}  
	for( int d=1; d<=n-k; d++ ){
		arr[1] = arr[1] + 1;
		for( int j=2; j<=k; j++ )
			arr[j] = arr[j] + arr[j-1];
	}
	return arr[k];
}//bin1
```

* **算法分析** 时间复杂度：O\(n\*k\)；空间复杂度：① $$O(n^2)$$ 、②\_1 $$O(n-k)$$ ②\_2 $$O(k)$$ 

## 0x03 从甲到乙最小代价

![](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-04-02_10-50-54.jpg)

* **思路**  $$M[ j][i]$$ 中存储的是甲到桥 $$B_{ij}$$ 左侧的最小代价
* **代码**

```c
smallestcost( )
{   
//利用辅助数组
	  M[1,2][1, 2, …, n] ; 
    M[1][1] = S01; M[2][1]=S02;
    for (i=2; i≤n; i++)
    { 
		    M[1][i]=min{M[1][i-1]+Ci-1,1+Si-1,1, M[2][i-1] +Ci-1,2+Si-1,3};
       	M[2][i]=min{M[1][i-1]+Ci-1,1+Si-1,2, M[2][i-1] +Ci-1,2+Si-1,4};
    }
    return min{M[1][n]+Cn1+Sn1, M[2][n] +Cn2+Sn2};
}//smallestcost
smallestcost( )
{   
//临时变量
	  T1 = S01; T2=S02;
    for (i=2; i≤n; i++)
    { 
		    T3=min{T1+Ci-1,1+Si-1,1, T2 +Ci-1,2+Si-1,3};
       	T2=min{T1+Ci-1,1+Si-1,2, T2 +Ci-1,2+Si-1,4};      
		    T1=T3; 
	  }
    return min{T1+Cn1+Sn1, T2 +Cn2+Sn2};
}//smallestcost

```

* **算法分析** 时间复杂度： $$O(n)$$ 

## 0x04 动态规划算法

* **使用情景**：分解为许多重复的小问题，保存小问题的计算结果，减少重复计算
* **特点**：
  * 分析一个最优解决方案应该具备的结构 
  * 递归定义最优解决方案 
  * 自底向上构建解决算法
* 步骤：
  * 最优解决方案的结构
  * 递归的解决方案
  * 自底向上的实现算法

## 0x05 最长公共子序列

* **思路**：  $$L[i][j]$$ 表示 A\[i\] 与 B\[j\] 的最长公共子序列，则 $$L[i][j]=\begin{cases} 0,& \text{若 i = 0 或 j = 0} \\L[i-1][j-1] + 1,& \text{若 i > 0 , j > 0 和 Ai = Bi} \\max(L[i][j-1], L[i-1][j]),& \text{若 i > 0 , j > 0 和 $Ai \neq Bi$}\end{cases}$$ 
* **代码**

```c
int Lcs(char a[], char b[])
{
	//最长公共子序列长度
	int n = strlen(a), m = strlen(b);
	int L[n+1][m+1];
	//初始化
	for( int i=0; i<=n; i++ ){
		L[i][0] = 0;
	} 
	for( int j=0; j<=m; j++ ){
		L[0][j] = 0;
	} 
	//计算其他两种情况
	for( int i=1; i<=n; i++ ){
		for( int j=1; j<=m; j++ ){
			if( a[i-1] == b[j-1] )//char数组下标从0开始 
				L[i][j] = L[i-1][j-1] + 1;
			else
				L[i][j] = max(L[i-1][j], L[i][j-1]);
		}
	} 
	return L[n][m];
}//Lcs
```

* **算法分析** 时间复杂度： $$O(n)$$ 

