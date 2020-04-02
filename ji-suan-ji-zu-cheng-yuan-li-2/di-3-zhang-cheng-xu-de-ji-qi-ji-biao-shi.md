# 第3章 程序的机器级表示

![&#x8DEF;&#x7EBF;&#x56FE;](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-03-30_22-23-24.jpg)

## IA32系统指令系统概述

### 0x01 支持的数据类型

![](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-04-02_16-56-01.jpg)

### 0x02 寄存器组织

![](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-04-02_17-12-18.jpg)

**标志寄存器**

![](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-04-02_17-16-06.jpg)

### 0x03 寻址方式\(保护模式下\)

1. 寻址方式：根据指令给定信息得到操作数或操作数地址
2. 操作数所在的位置：指令中\(**立即寻址**\)、寄存器中\(**寄存器寻址**\)、存储单元中\(属于存储器操作数，按字节编址\)：**其他寻址方式**
3. 存储器操作数的寻址方式与微处理器的工作模式有关
4. 指令中对操作数的有效地址的描述与操作数的数据结构有关！

![](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-04-02_17-25-59.jpg)

### 0x04 传送指令

#### 01. 通用数据传送指令 ——寄存器之间或寄存器和存储器之间交换数据

* MOV：一般传送，包括movb、movw和movl等
* MOVS：符号扩展传送，如movsbw、movswl等
* MOVZ：零扩展传送，如movzwl、movzbl等
* XCHG：数据交换
* PUSH/POP：pushl,popl，入栈/出栈 \(注意：**栈存储区是从高地址向低地址增长的**\)

#### 02. 地址传送指令

* LEA：加载有效地址，如leal \(%edx,%eax\), %eax”的功能为R\[eax\]←R\[edx\]+R\[eax\]，执行前，若R\[edx\]=i，R\[eax\]=j，则指令执行后，R\[eax\]=i+j

#### 03. 输入输出指令 ——I/O端口与寄存器之间交换数据

* IN和OUT

#### 04. 标志传送指令 ——标志寄存器和栈存储区之间交换数据

* PUSHF、POPF：将EFLAG压栈，或将栈顶内容送EFLAG

### 0x03 通用数据传送指令（MOV）与地址加载指令（LEA）的区别

　　LEA指令实际上是MOV指令的变形。它的指令形式是从内存读取数据到寄存器，但实际上他并没有引用内存。他的第一个操作数看上去是个内存引用，但该指令并不是从指定位置读入数据，而是将有效地址写入到目的操作数。

## 讨论

### 0X01 阅读以下AT&T格式汇编指令，请用RTL语言描述每条指令的功能，并说明传送的操作数的长度。

![](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-04-02_22-16-43.jpg)

### 0x02 阅读以下AT&T格式汇编指令，根据操作数长度确定适当的指令后缀，并说明每个操作数的寻址方式。

```bash
movl  	%eax, (%esp) 	      寄存器寻址 、位移
movw	8(%ebp), %dx          位移、寄存器寻址
movb    $0xFF, %bl	        立即数、寄存器寻址
pushb    $0xFF              立即数        
movw	8(%ebp,%edx,4), %ax   基址加比例变址加位移、寄存器寻址
movw	%dx, 20(%ebp)	        寄存器取寻址、位移
leal	8(%ecx,%edx,4), %eax  寄存器寻址、寄存器寻址
```

### 0x03 给定数据传送要求，写出对应的汇编指令

![](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-04-02_22-52-32.jpg)



