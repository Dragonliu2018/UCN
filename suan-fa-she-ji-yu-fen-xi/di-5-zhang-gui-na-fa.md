# 第5章 归纳法

## 实例

### 0x01 汉诺塔

```cpp
void hanoi(int n, char one, char two, char three)
{
	if(n>1)						//递归条件 
	{
		hanoi(n-1,one,three,two);//step 1
		move(one, three);         //step 2
		hanoi(n-1,two,one,three);//step 3
	}
	else move(one,three);		//基线条件
}
```

### 0x02 选择排序

```cpp
void SelectSort(int arr[], int i)
{
	if( i < n )
	{
		int k = i;
		for( int j=i+1; j<=n; j++ )//找到arr[i...n]的min
		{
			if( arr[j] < arr[k] )
				k = j;
		}
		if( k != i )//互换 
		{
			int temp;
			temp = arr[k];
			arr[k] = arr[i];
			arr[i] = temp;
		} 
		SelectSort(arr, i+1);//转换成小事件 
	}
}//SelectSort
```

* **思路**：如果能对A\[i+1...n\]排序，就能对A\[i...n\]排序。
* **时间复杂度**：元素比较次数C\(n\)， ①  $$C(n) =  \begin{cases}  0  & {n=1} \\   C(n-1)+(n-1), & {n\geq 2}  \end{cases}$$   ② $$C(n)=\sum_{j=1}^{n-1}j = \frac{n(n-1)}{2}$$  ③ $$ O(n^2)$$ 

### 0x03 插入排序

```cpp
void InsertSort(int arr[], int i)
{
	if( i > 1 )
	{
		InsertSort(arr, i-1);//转换成小规模 
		int temp, j;
		temp = arr[i];
		j = i-1;
		while( j>0 && arr[j]>temp )//将arr[i]插入到有序序列中 
		{
			arr[j+1] = arr[j];
			j--; 
		} 
		arr[j+1] = temp;
	}
}//InsertSort
```

* **思路**：如果能对A\[1...i\]排序，就能对A\[1...i+1\]排序。
* **时间复杂度**：与选择排序一样。

## 整数幂

* **归纳法思路**：如果能算出 $$x^b(b = \lfloor\frac{n}{2} \rfloor)$$ ，就能算出 $$x^n$$ 
* **时间复杂度**： $$O(logn)$$ 

```cpp
int power(int x, int m)
{
	int ans;
	if( m == 0 )//终止条件 
		ans = 1;
	else//递归过程 
	{
		ans = power(x, m/2);//小规模问题
		ans *= ans;//平方 
		if( m%2 == 1 )//幂次为奇数 
			ans *= x; 
	}
	return ans;
}//power
```

* **循环迭代法**：从前向后、从后向前
* **时间复杂度**： $$O(logn)$$ 

![&#x56FE;1 &#x4ECE;&#x524D;&#x5411;&#x540E;](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-03-19_08-25-33.jpg)

![&#x56FE;2 &#x4ECE;&#x540E;&#x5411;&#x524D;](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-03-19_08-32-3.jpg)

* **试题**：将实数x变成二维矩阵求解

![&#x56FE;3 &#x6574;&#x6570;&#x5E42;&#x8BD5;&#x9898;](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-03-19_08-4.jpg)

## 多项式求值

* **思路**：从前向后、从后向前
* **时间复杂度**： $$O(n)$$ 

```cpp
//从前向后
int Horner(int arr[], int x)
{
	int ans = 0;
	for( int i=n; i>=0; i-- )
		ans = ans*x + arr[i]
	return ans;
}//Horner
//从后向前
int Horner(int arr[], int x)
{
	int ans = arr[0];
	int temp = 1;//存放x的i次方 
	for( int i=1; i<=n; i++ )
	{
		temp *= x;
		ans += arr[i]*temp;
	} 
	return ans;
}//Horner 
```

## 寻找多数元素

* **定义**：多数元素是出现次数大于 $$\frac{n}{2}$$ 的元素
* **结论**：在原序列中去掉两个不相同的元素，多数元素不变
* **思路**：寻找可能的多数元素，判断其是否是多数元素
* **时间复杂度**： $$O(n)$$ 

```cpp
int candidate(int m)
{
	//利用结论找出arr[m...n]可能的多数元素 
	int j=m+1, ans=arr[m];
	int count=1;
	while( j<n && count>0 )
	{
		if( arr[m] == arr[j] )	
			count++;
		else
			count--;
		j++;
	}
	if( j == n )//终止条件 
		return ans;
	else//小规模事件 
		return candidate(j+1); 
}//candidate 
int majority()
{
	//寻找多数元素，没有则返回-666
	int ans;
	ans = candidate(1);//可能的多数元素
	int num=0;
	for( int i=1; i<=n; i++ )//判断是否是多数元素 
		if( arr[i] == ans )
			num++;
	if( num > n/2 )
		return ans;
	else
		return -666; 
}//majority
```

