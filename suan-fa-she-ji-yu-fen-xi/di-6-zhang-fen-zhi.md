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

**思路**：二分搜索，如果mid值比low值大，则搜后半段；否则搜前半段。**\(求min用high，求max用low\)**

```c
int binarysearch(int arr[], int low, int high)
{
	//二分搜索求最大值
	int mid = (low + high)/2; 
	if( high-low < 2 )//结束条件 
		return max(arr[low], arr[high]);
	else
	{
		if( arr[low] < arr[mid] )//划分治理！！！
			return binarysearch(arr, mid, high);
		else
			return binarysearch(arr, low, mid-1);
	}
}//binarysearch
```

## 0x03 合并排序

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

## 0x04 分治范式

### 步骤

* 划分步骤：化成 $$p\geq 1$$ 部分
* 治理步骤：递归过程 $$\rightarrow$$  阈值 $$n_0$$
* 组合步骤：将p个部分解组合成原始数据的解 

### 分治算法

* 如果问题 $$I $$ 的规模很小，直接求解，否则进行下一步；
* 将问题划分成几乎相等的p个子问题 $$I_1,I_2...I_p$$ 
* 对于每个问题，递归调用算法，得到子问题的解；
* 组合p个子问题的解，返回 $$I$$的解

## 0x05 寻找第k小元素

### 思路

* **充要条件**：x为第k小元素 $$\Leftrightarrow$$$$|A_1|<k且|A_1|+|A_2|\geq k $$ 
* 找到1个候选值**mm：令** $$q = \lfloor \frac{p}{5}\rfloor $$ ，将A分成q组，每组5个元素\(如果不能被5整除则丢弃余数\)。将q组中的每一组进行排序，找出中项，然后选出q个中项的中项；
*  求出候选值对应的 $$A_1,A_2,A_3$$ 
* 判断mm是否满足第k小元素的条件，如果否，继续在下一个候选值进行操作：三种情况

### 代码\(Bug\)

```c
int middle(int arr[], int low, int high)
{
	//求数组的中值
	int mid;
	mid = (low + high)/2;
	sort(arr+low, arr+high); 
	return arr[mid];
}//middle 
int select(int arr[], int low, int high, int k)
{
	/*寻找第k小的元素*/
	//递归结束的判断条件 
	int p;
	p = high - low + 1;
	if( p < 44 )
	{
		sort(arr+low, arr+high);
		return arr[k+low-1];//下标	
	} 
//	将数组arr平分q组，每组5个元素，取中值的中值 
	int q;
	q = p/5;
	int M[q+1], id=1;//存放各中值 
	for( int i=0; i<q; i++ )
	{ 
		M[id++] = middle(arr, 5*i+1, 5*(i+1));
	} 
	int mm;//候选值
	mm = middle(M, 1, q);
	//将数组分成三部分（荷兰国旗问题）
	//设置两个标志位begin和end分别指向这个数组
	//的开始和末尾，然后用一个标志位cur从头开始进行遍历：
	int begin=low, end=high, cur=low;//指针
	while( cur <= end )
	{
		if( arr[cur] < mm )//放到左侧 
		{
			swap(arr[cur], arr[begin]);
            cur++;
            begin++;
		}	
		else if( arr[cur] > mm )//放到右侧 
		{
			swap(arr[cur], arr[end]);
            end--;//cur不前进 
		}
		else
			cur++;
	} 
	//判断mm是否满足第k小元素的条件(Bug: 下标问题) 
	int len1, len2;
	len1 = begin - low;
	len2 = end - begin+1;
	if( len1 >= k )
		return select(arr, low, begin-1, k+low-1);//A1
	else if( len1+len2 >= k )
		return mm;
	else
		return select(arr, end+1, high, k-len1-len2+end);//A3
}//select
```

### 算法分析

* 时间复杂度： $$O(n)$$ 
* 荷兰国旗问题：[我跳](https://www.cnblogs.com/gnuhpc/archive/2012/12/21/2828166.html)

## 0x06 快速排序

### 思路

选定一个参考值 $$arr[low]$$ ，小于他的放在左边，否则放到右边；在对两边进行排序。

### 代码

```c
int Split(int arr[], int low, int high)
{
	//划分算法，返回A[low]的新位置  
	int i, j;//指针
	i = low;
	int ref = arr[low];//参考值 
	for( j=low+1; j<=high; j++ )
	{
		if( arr[j] <= ref )
		{
			i++;
			if( i != j )
				swap(arr[i], arr[j]);//交换		
		}	
	} 
	swap(arr[low], arr[i]);//交换 
	return i;
}//Split 
void quicksort(int arr[], int low, int high)
{
	//快速排序
	if( low < high )
	{
		int pos;//A[low]的新位置 
		pos = Split(arr, low, high); 
		quicksort(arr, low, pos-1);//边界 
		quicksort(arr, pos+1, high);
	} 
}//quicksort
```

### 算法分析

* 时间复杂度： $$O(nlogn)$$ 

