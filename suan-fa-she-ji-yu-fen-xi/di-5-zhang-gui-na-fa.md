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

**思路**：如果能对A\[i+1...n\]排序，就能对A\[i...n\]排序。

**时间复杂度**：元素比较次数C\(n\)，  
①  $$C(n) =  \begin{cases}  0  & {n=1} \\   C(n-1)+(n-1), & {n\geq 2}  \end{cases}$$    
② $$C(n)=\sum_{j=1}^{n-1}j = \frac{n(n-1)}{2}$$   
③ $$ O(n^2)$$ 

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

**思路**：如果能对A\[1...i\]排序，就能对A\[1...i+1\]排序。  
**时间复杂度**：与选择排序一样。

## 整数幂

