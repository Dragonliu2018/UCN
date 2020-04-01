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

* **思路** 利用二维数组存储求解，行表示k，列表示n。
* **代码**

```c
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
	return f[k][n];
}//bin
```

* **算法分析** 时间复杂度：O\(n\*k\)

