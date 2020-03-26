# 第6章 分治

## 0x01 Max 和 Min

### 思路

将数组一分为二，前、后半部分求max1，max2，再取两者的max。

### 代码

```c
pair<int, int> minmax(int arr[], int low, int high)
{
	//求解数组的min和max 
	pair<int, int> pa1, pa2, ans;
	if( low < high )//约束条件
	{
		int mid = (low + high)/2;
		pa1 = minmax(low, mid);
		pa2 = minmax(mid+1, high);
	}
	int Min, Max;
	Min = min(pa1.first, pa2.first);
	Max = max(pa1.second, pa2.second);
	ans = make_pair(Min, Max);
	return ans;
}//minmax
```

### 算法分析

* 时间复杂度： 比较次数 $$C(n) =  \begin{cases}         1,  & {n=2} \\   2C(\frac{n}{2})+2, & {n>2}         \end{cases}$$ ， $$O(n)$$ 

## 0x02 二分搜索

### 思路

将数组一分为二，搜索值与mid值对比，如果大就搜后半段，反之搜前半段。

### 代码

```c
int binarysearch(int arr[], int low, int high, int val)
{
	//二分搜索
	if( low > high )//结束条件 
		return 0;
	else
	{
		int mid = (low + high)/2;
		if( val == arr[mid] ) 
			return mid;
		else if( val > arr[mid] )
			return binarysearch(arr, mid+1, high, val);
		else 
			return binarysearch(arr, low, mid-1, val);
	}
}//binarysearch
```

### 算法分析

* 时间复杂度： 比较次数 $$C(n) =  \begin{cases}         1,  & {n=1} \\   C(\lfloor \frac{n}{2}\rfloor)+1, & {n>1}         \end{cases}$$ ， $$O(logn)$$ 

### k旋转数组的最大元素\(O\(logn\)\)

**思路**：二分搜索，如果mid值比high值大，则搜前半段；否则搜后半段

## 合并排序

### 思路

将数组一分为二，前后半段分别排序，然后合并。

### 代码

```c
void mergesort(int arr[], int low, int high)
{
	//合并排序
	if( low < high )
	{
		int mid = (low + high)/2;
		mergesort(arr, low, mid);
		mergesort(arr, mid+1, high);
		merge(arr, low, mid, high);
	} 
}//mergesort
```

### 算法分析

* 时间复杂度：比较次数 $$C(n) =  \begin{cases}         0,  & {n=1} \\   2C( \frac{n}{2})+n-1, & {n>1}         \end{cases}$$ ， $$O(nlogn)$$ 
* 算法调用顺序：前序遍历；处理的顺序：后序遍历
* 空间复杂度： $$Θ(n)$$ 

