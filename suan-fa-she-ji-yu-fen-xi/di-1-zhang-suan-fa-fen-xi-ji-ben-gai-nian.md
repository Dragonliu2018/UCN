# 第1章 算法分析基本概念

## 二分搜索

* **代码**

```c
int BinarySearch(int x)//二分搜索 
{
	int low, high, mid, ans=0;
	low = 1;
	high = len;
	while( low<=high && ans==0 )
	{
		mid = (low + high) / 2;
		if( x == arr[mid] )//找到
			ans = mid; 
		else if( x < arr[mid] )//搜索左半段 
			high = mid - 1;
		else			//搜索右半段 
			low = mid + 1;
	}
	return ans;
}//BinarySearch
```

* **分析** 最大比较次数是 $$\lfloor log n \rfloor + 1$$ ，时间复杂度O\(log n\)。
* **应用** [**我跳**](http://dragonliu.tk/2020/03/09/%E4%BA%8C%E5%88%86%E6%90%9C%E7%B4%A2/)\*\*\*\*

## 合并两个已排序的表

* **代码（bug）**

```cpp
void merge(int a[], int p, int q, int r)
{
	int b[r-p+1];//辅助数组(数组大小与下标有问题)
	int s, t, k;//三个下标指示 
	s = p;
	t = q + 1;
	k = p;
	while( s<=q && t<=r )
	{
		if( a[s]<=a[t] )//a[s]小 
		{
			b[k] = a[s];
			s++;
		}
		else//a[t]小 
		{
			b[k] = a[t];
			t++;
		}
		k++;//数组b下标前移 
	} 
	if( s == q+1 )//前半段数组已加入数组b 
	{
		for( ; t<=r; t++ )
		{
			b[k++] = a[t];
		}
	} 
	else//后半段数组已加入数组b
	{
		for( ; s<=q; s++ )
		{
			b[k++] = a[s];
		}
	} 
	for( int i=p; i<=r; i++ )//将数组b赋值到数组a 
		a[i] = b[i];
}//merge
```

* **分析** 　　设大小为n1、n2\(n1&lt;=n2\)的数组合并为一个数组\(n\)，则比较次数为n1~n；数组b中每个元素被赋值一次，然后再从数组b到数组a赋值一次，共计2n次。时间复杂度为O\(n\)。 
* **选择排序**

```c
void selectSort(int arr[], int len)
{
	for( int i=1; i<len; i++ )
	{
		int k = i;
		for( int j=i; j<=len; j++ )//查找第i小的元素 
		{
			if( arr[j] < arr[k] )
				k = j;
		}
		if( k != i )//交换arr[i]与arr[k] 
		{
			int temp;
			temp = arr[i];
			arr[i] = arr[k];
			arr[k] = temp;
		} 
	}
}//selectSort
```

* **分析** 　　元素比较次数：\(n-1\) + \(n-2\) + ... + 1 = $$\frac {n(n-1)}{2}$$ ；元素交换次数：0~n-1，每次交换需要3次赋值，故0~3\(n-1\)。时间复杂度 $$O(n^2)$$ 
* **插入排序**

```c
void insertSort(int arr[], int len)
{
	for( int i=2; i<=len; i++ )//arr[1]是有序的 
	{
		int temp = arr[i], t = i-1;
		while( t>0 && arr[t]>temp )//将arr[i]插入到有序的arr[1..i-1] 
		{
			arr[t+1] = arr[t];
			t--;
		} 
		arr[t+1] = temp;//赋值
	}
}//insertSort
```

* **分析** 比较次数：n-1~$$\frac {n(n-1)}{2}$$\(非降序，降序且元素各不相同\)；赋值次数：比较次数+\(n-1\)；时间复杂度 $$O(n^2)$$。
* **合并排序**

```c
void bottumUpSort(int arr[], int n)
{
	int t = 1;//合并序列的右端 
	while( t < n )
	{
		int s, i=0;//合并序列长度、合并序列的左端  
		s = t; 
		t = 2*s;
		while( i+t <= n ) 
		{
			merge(arr, i+1, i+s, i+t);
			i += t; 
		} 
		if( i+s < n )//剩余k个元素（2组） 
			merge(arr, i+1, i+s, n);
	} 
}//bottomUpSort
```

* **分析** 时间复杂度O\(nlog n\).

## 时间复杂度

* O：上界， $$ \lim_{n \to +\infty}  \frac{f(n)}{g(n)} \neq \infty \to		f(n) = O(g(n))$$，f没有g的常数倍增长的快；
* Ω：下界， $$ \lim_{n \to +\infty}  \frac{f(n)}{g(n)} \neq 0 \to		f(n) = Ω(g(n))$$，f的增长至少与g的常数倍相同；
* Θ：确切界限， $$ \lim_{n \to +\infty}  \frac{f(n)}{g(n)} = c(c \neq0) \to		f(n) = Θ(g(n))$$
* o：复杂性类， $$ \lim_{n \to +\infty}  \frac{f(n)}{g(n)} =0\to		f(n) = o(g(n))$$

{% hint style="info" %}
1. $$f(n) = Θ(g(n)) \Leftrightarrow f(n) = O(g(n))　and　 f(n) = Ω(g(n))$$
2.  $$ f(n) = Ω(g(n))  \Leftrightarrow f(n) = O(g(n))$$ 
3. O类似于 $$\leq$$ ，Ω类似于 $$\geq$$ ，Θ类似于 $$=$$ ，o类似于 $$<$$ 
{% endhint %}

{% hint style="warning" %}
1. $$1<log log n<log n<\sqrt{n}<n<nlog n< n^2 < 2^n <n!<n^n<2^{n^2}$$ 
2. $$logn^k = klogn=Θ(logn)$$ 
3. $$log n!= \sum_{j=1}^n {logj}= O(nlogn)$$ 
{% endhint %}

* **空间复杂度**
* **平摊分析**

## 题目

### 0x01 用 _Θ_ 符号表示下列函数：

\(d\) $$\frac {n!} {2^n}+n^{\frac {n}{2}}：Θ(n^{\frac {n}{2}})$$ 

