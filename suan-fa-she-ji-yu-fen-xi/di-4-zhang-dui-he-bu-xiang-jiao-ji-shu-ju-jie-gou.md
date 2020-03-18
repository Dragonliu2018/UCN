# 第4章 堆和不相交集数据结构

## 堆

### 0x01 应用场景

多次插入元素和寻找max、min值

### 0x02 性质

1. 几乎完全二叉树
2. 父节点 $$\geq$$ 孩子节点\(大顶堆\)

### **0x03 Sift-Up：数值变大，上移**

```cpp
void SiftUp( int H[], int i )
{
	//只有H[i]不满足堆的性质，大于父节点(变大)
	while( i>1 )//直到根节点或满足节点 
	{
		if( H[i] > H[i/2] )//与父结点互换 
		{
			int temp;
			temp = H[i];
			H[i] = H[i/2];
			H[i/2] = temp;
		}
		else
			return ; 
		i /= 2;
	} 
	return ;
}//siftup
//时间复杂度O(logn)；空间复杂度O(1)
```

### **0x04 Sift-down：数值变小，下移**

```cpp
void SiftDown( int H[], int i )
{
	//只有H[i]不满足堆的性质，小于父节点(变小)
	while( 2*i<=n )//直到叶子节点或满足节点 
	{
		i *= 2;
		if( i+1 <= n && H[i+1] > H[i] )//右节点大于左节点 
			i++;	 
		if( H[i/2] < H[i] )//与子结点互换 
		{
			int temp;
			temp = H[i];
			H[i] = H[i/2];
			H[i/2] = temp;
		}
		else
			return ;
	} 
	return ;
}//siftdown 
//时间复杂度O(logn)；空间复杂度O(1)
```

### **0x05 HeapTest：判断是否是堆**

```cpp
bool HeapTest( int H[] )
{
	//判断是否是堆 
	for( int i=n/2; i>=1; i-- )//从第1个非叶子节点开始判断 
	{
		int j=2*i;
		if( j+1<=n && H[j]<H[j+1] )//左右孩子取大 
			j++;
		if( H[i] < H[j] )//父节点<子节点 
			return 0;
	}
	return 1;
}//HeapTest 
```

### **0x06 Insert：插入元素**

```cpp
void Insert( int H[], int x )
{
	//插入元素
	n++;//堆长度+1
	H[n] = x;//赋给最后元素，
	SiftUp(H, n);//数值变大，向上调整 
}//Insert
```

### **0x07 Delete：删除元素**

```cpp
void Delete( int H[], int i ) 
{
	//删除元素
	int x, y;
	x = H[i];
	y = H[n]; 
	n--;//堆长度-1，删除元素 
	if( i == n+1 )//删除最后一个节点 
		return ; 
	H[i] = y;//与最后元素互换
	if( y >= x)//变大向上调整 
		SiftUp(H, i);
	else       //变小向下调整 
		SiftDown(H, i); 
}//Delete
//时间复杂度O(logn)；空间复杂度O(1)
```

### **0x08 DeleteMax：删除根节点**

```cpp
int DeleteMax( int H[] )
{
	//删除根节点并返回 
	int temp;
	temp = H[1];
	H[1] = H[n];//最后节点顶替根节点 
	n--;//堆长度-1 
	SiftDown(H, 1);//下移 
	return temp; 
}//DeleteMax 
```

### 0x09 HeapCreate：创建堆 -- 插入法

```cpp
void HeapMake(int H[])
{
	//插入法建堆
	int len = n;
	n = 1;//设置堆的初始长度为1
	for( int i=2; i<=len; i++ )
	{
		Insert(H, H[i]);
	} 
}//HeapMake
```

**时间复杂度**： $$\sum_{k=2}^{n}log k = logn! = O(nlogn)$$ 

### 0x0a HeapCreate: 创建堆 -- 非叶子节点下移法

```cpp
void HeapCreate(int H[])
{
	//下移法建堆 
	for( int i=n/2; i>0; i-- )//从第一个非叶子节点 
	{
		SiftDown(H, i);
	}
}//HeapCreate 
```

**时间复杂度**：

1. 树的高度： $$k = \lfloor logn\rfloor$$ 
2. $$0≤i<k$$ ，i层的节点数 $$2^i$$ 
3. i层的每个节点最多down（k-i）次
4. 整个过程，令 $$j = k-i$$  $$\sum_{i=0}^{k-1} (k-i)2^i = \sum_{j=k}^{1}j2^{k-j} = 2^k\sum_{j=1}^{k}\frac{j}{2^j} ≤n\sum_{j=1}^{k}\frac{j}{2^j}<2n$$   $$\therefore O(n)$$ 

### 0x0b HeapSort: 堆排

```cpp
void HeapSort(int H[])
{
	int len = n;//暂存数组长度
	for( int i=len; i>=2; i-- )
	{
		int temp;
		temp = H[i];//首尾互换 
		H[i] = H[1];
		H[1] = temp;
		n--;//堆长度-1 
		SiftDown(H, 1);//第一个元素下移 
	} 
	n = len;//恢复数组长度 
}//HeapSort
```

**时间复杂度**：建堆O\(n\)，for循环O\(nlogn\)； $$O(nlogn)$$ 

