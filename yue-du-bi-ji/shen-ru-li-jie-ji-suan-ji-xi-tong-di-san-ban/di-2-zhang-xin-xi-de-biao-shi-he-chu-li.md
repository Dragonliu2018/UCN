# 第2章 信息的表示和处理

## 0x01 打印程序对象的字节表示

```c
typedef unsigned char* byte_point;

void show_bytes(byte_point start, size_t len){
	//按字节顺序打印
	size_t i;
//	for( i = 0; i < len; i++ )
//		printf("%.2x", start[i]);
	for( i = len; i > 0; i-- )//小端表示法，逆向输出 
		printf("%.2x", start[i-1]);
	printf("\n"); 
}//show_bytes

void show_int(int x){
	//输出int型
	show_bytes((byte_point) &x, sizeof(int)); 
}//show_int

void show_float(float x){
	//输出float型
	show_bytes((byte_point) &x, sizeof(float)); 
}//show_float

void show_pointer(void *x){
	//输出指针型 
	show_bytes((byte_point) &x, sizeof(void *)); 
}//show_pointer
```

