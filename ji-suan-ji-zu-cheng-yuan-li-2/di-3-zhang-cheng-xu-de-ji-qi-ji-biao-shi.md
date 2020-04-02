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

### 0x03 通用数据传送指令（MOV）与地址加载指令（LEA）的区别

### 0x04 给定AT&T格式的汇编指令，能够说出指令中的操作数采用的是何种寻址方式，判断出操作数的长度，并用RTL描述指令功能

### 0x05 给定不完整的AT&T格式的汇编指令，能够根据操作数的长度确定适当的指令后缀，并说明每个操作数的寻址方式及指令功能

### 0x06 给定数据传送要求，能够写出对应的汇编指令

### 0x07 常用指令类型

