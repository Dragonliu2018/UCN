# 第4章 堆和不相交集数据结构

## 堆

### 0x01 应用场景

多次插入元素和寻找max、min值

### 0x02 性质

1. 几乎完全二叉树
2. 父节点 $$\geq$$ 孩子节点\(大顶堆\)

### **0x03 代码**

#### **1. Sift-Up：数值变大，上移**

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

#### **2. Sift-down：数值变小，下移**

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

#### **3. HeapTest：判断是否是堆**

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

#### **4. Insert：插入元素**

```cpp
void Insert( int H[], int x )
{
	//插入元素
	n++;//堆长度+1
	H[n] = x;//赋给最后元素，
	SiftUp(H, n);//数值变大，向上调整 
}//Insert
```

#### **5. Delete：删除元素**

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

#### **6. DeleteMax：删除根节点**

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

\*\*\*\*











