# 图像滤波

## 基础知识

1.  **定义**：图像滤波，即在尽量保留图像细节特征的条件下对目标图像的噪声进行抑制，是图像预处理中不可缺少的操作，其处理效果的好坏将直接影响到后续图像处理和分析的有效性和可靠性。
2. **比喻：**我们可以把滤波器想象成一个包含加权系数的窗口，当使用这个滤波器平滑处理图像时，就把这个窗口放到图像之上，透过这个窗口来看我们得到的图像。
3. **公式：** $$O(i, j) = \sum_{m,n}I(i+m,j+n)K(m,n)$$ **** 其中O\(i, j\)是像素输出值，I\(i+m, j+n\)是像素输入值，K为滤波器（核：二维矩阵，核的不同值表示不同的算法。）
4. **种类**：低通滤波器可以消除噪声、模糊化，高通滤波器可以提取边缘。[白话文讲计算机视觉-第三讲-滤波器](https://blog.csdn.net/u013631121/article/details/80444602?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)
5. **作用**：图像滤波可以更改或者增强图像。通过滤波，可以强调一些特征或者去除图像中一些不需要的部分。滤波是一个邻域操作算子，利用给定像素周围的像素的值决定此像素的最终的输出值。常见的应用包括去噪、图像增强、检测边缘、检测角点、模板匹配等。

## 算法

### 0x01 均值滤波

1. **定义**：用其像素点周围像素的平均值代替元像素值，在滤除噪声的同时也会滤掉图像的边缘信息。
2.  **代码：**Python调用OpenCV实现均值滤波的核心函数：**result = cv2.blur\(原始图像,  核大小\)**   其中，核大小是以（宽度，高度）表示的元组形式，常见的形式包括：核大小（3，3）和（5，5）。**boxFilter**也可实现。

### 0x02 方框滤波

1. **定义**：方框滤波和均值滤波核基本一致，区别是需不需要均一化处理。
2. **代码**： OpenCV调用boxFilter\(\)函数实现方框滤波。函数：**result = cv2.boxFilter\(原始图像, 目标图像深度, 核大小, normalize属性\)**  其中，目标图像深度是int类型，通常用“-1”表示与原始图像一致；核大小主要包括（3，3）和（5，5）；normalize属性表示是否对目标图像进行归一化处理，当normalize为true时需要执行均值化处理，当normalize为false时，不进行均值化处理，实际上为求周围各像素的和，很容易发生溢出，溢出时均为白色，对应像素值为255。

### **0x03 中值滤波**

1. **定义：**中值滤波用测试像素周围邻域像素集中的中值代替原像素。中值滤波去除椒盐噪声和斑块噪声时，效果非常明显。在OpenCV中，可以使用函数medianBlur进行操作。
2. **代码**： OpenCV主要调用medianBlur\(\)函数实现中值滤波。图像平滑里中值滤波的效果最好。**dst = cv2.medianBlur\(src, ksize\)**   其中，src表示源文件，ksize表示核大小。核必须是大于1的奇数，如3、5、7等。

### 0x04 高斯滤波

1. **定义**：加权平均，距离越近的点权重越大，距离越远的点权重越小。由于图像是二维矩阵，则采用二维高斯函数\(正态分布\)$$f(x,y)= \frac{1}{2πσ^2} e^{\frac{-(x^2+y^2)}{2σ^2}}$$ 。如果原图是彩色图片，可以对RGB三个通道分别做高斯模糊。参考：[高斯模糊（高斯滤波）的原理与算法](https://blog.csdn.net/nima1994/article/details/79776802)
2. **边界处理**：把已有的点拷贝到另一面的对应位置，模拟出完整的矩阵。
3. **公式**：以 q为中心的窗口中，某一点 p在高斯滤波过程中。 权重\(空间\)： $$G(p) = \frac{1}{2πσ^2} e^{\frac{-||p-q||^2}{2σ^2}}$$ 
4. **代码**：Python中OpenCV主要调用GaussianBlur函数：**dst = cv2.GaussianBlur\(src, ksize, sigmaX\)**   其中，src表示原始图像；ksize表示核大小，核大小（N, N）必须是奇数；sigmaX表示X方向方差，主要控制权重，sigmaX小，表现在高斯曲线上就是曲线越高越尖，表现在滤波效果上就是模糊程度小（sigmaX大，表现在高斯曲线上就是曲线越矮越平缓，表现在滤波效果上就是模糊程度大）。 

```python
#encoding:utf-8
"""
@author: Dragon Liu
Operating environment: Python 3.7.1
lib:  opencv-python
Date: 2020/3/26
"""
#导入库
import cv2  
import numpy as np  
import matplotlib.pyplot as plt
 
#读取图片
img = cv2.imread('02.png')
source = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
 
#方框滤波
img_box = cv2.boxFilter(source, -1, (5,5), normalize=1)

# 均值滤波
img_blur = cv2.blur(source, (5,5))

#中值滤波
img_median = cv2.medianBlur(source, 3)

# 高斯滤波
img_Guassian = cv2.GaussianBlur(source, (5,5), 0)


#显示图形
titles = ['Source Image', 'BoxFilter Image', 'Blur Image', 
         'Median Image', 'Guassian Image']  
images = [source, img_box, img_blur, img_Guassian, img_median]  
for i in range(5):  
   plt.subplot(2, 3, i+1), plt.imshow(images[i], 'gray')  
   plt.title(titles[i])  
   plt.xticks([]),plt.yticks([])  
plt.show()  
```

参考：[我跳](https://blog.csdn.net/Eastmount/article/details/82216380?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)

### 0x05 双边滤波 --  **边缘保护滤波** 

1. **定义**：高斯滤波只考虑了周边点与中心点的空间距离来计算得到权重，会模糊掉边缘。在高斯滤波的基础上加入了像素值\(灰度\)权重项，也就是说既要考虑距离因素，也要考虑像素值差异的影响，像素值越相近，权重越大。参考：[双边滤波详解](http://www.360doc.com/content/17/0306/14/28838452_634420847.shtml)、[【图像处理】——双边滤波](https://blog.csdn.net/u013921430/article/details/84532068)
2. **公式：** 像素值权重     $$G_r= exp(-{\frac{||I_p-I_q||^2}{2σ^2_r}})$$  空间距离权重  $$G_s= exp(-{\frac{||p-q||^2}{2σ^2_s}})$$  滤波窗口内每个像素值的权重和 $$W(q) = \sum_{p\in S} G_s(p)G_r(p)$$ ---用于权重的归一化 滤波结果： $$BF = \frac {1}{W_q}\sum_{p\in S} G_s(p)G_r(p)*I_p$$ 
3. **代码**：OpenCV在Python中双边滤波函数是**cv2.bilateralFilter\(src, d, sigmaColor, sigmaSpace）**其中，src是原图片，d是领域的直径，sigmaColor和sigmaSpace是灰度值相似性高斯函数标准差和空间高斯函数标准差。时间复杂度 $$O(Nr^2)$$ 

```python
#encoding:utf-8
"""
@author: Dragon Liu
Operating environment: Python 3.7.1
lib:  opencv-python
Date: 2020/3/26
"""
#导入库
import cv2  
import numpy as np  
import matplotlib.pyplot as plt
 
#读取图片
img = cv2.imread('02.png')
source = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
 
#双边滤波
img_bilateral = cv2.bilateralFilter(source, 7, 50, 50)


#显示图形
titles = ['Source Image', 'bilateralFilter Image']  
images = [source, img_bilateral]  
for i in range(2):  
   plt.subplot(1, 2, i+1), plt.imshow(images[i], 'gray')  
   plt.title(titles[i])  
   plt.xticks([]),plt.yticks([]) #禁止输出坐标轴 
plt.show()  
```

### 0x06  引导滤波 -- **边缘保护滤波**

1. **定义**：引导滤波的思想用一张引导图像产生权重，从而对输入图像进行处理。引导滤波除了可以用于图像平滑，还可以用于HDR压缩、细节增强、图像去雾、联合上采样等图像处理任务。引导滤波中空间域的贡献自然取决于窗口的大小，即由参数 r 决定。而标准差则是评判颜色差异性的参数，窗口中标准差越大，说明局部的像素相似性越差。
2. **公式：**[【图像处理】引导滤波](https://blog.csdn.net/u013921430/article/details/99695647) ① 权重 $$W_{ij}(i,j) = \frac{1}{|ω|^2} \sum_{k:(i,j)\in ω_k} (1+ \frac{(I_i-μ_k)(I_j-μ_k)}{σ_k^2+ϵ})$$   \(局部窗口 $$ω_k$$ ；ϵ是 $$L_2$$ 范数正则化系数，防止$$a_k$$ ​过大； $$μ_k$$与 $$ σ_k$$ ​表示 $$ I_i$$ 在窗口内的均值、标准差； $$∣w∣$$ 表示窗口内像素块的总数 \) ② 结果 $$q_i = \sum_{j}{W_{ij}(I)*p_j}$$   \(q、I、p分表表示输出图像、引导图像和输入图像 ，i、j 分别表示图像中像素点的索引。权重 W 仅与引导图像 I 有关，而在双边滤波中权重 W 由输入图像自身决定。\)
3. **代码**：时间复杂度O\(N\)，当 r 与 ϵ 越大，图像被平滑的程度越大。算法框架中：r是窗口半径， $$f_{mean}(I,r)$$ 表示在\(r, r\)窗口对图像做均值滤波。大佬博客：[我跳](https://blog.csdn.net/u013921430/article/details/99695647)

![&#x56FE;1 GF&#x7B97;&#x6CD5;&#x6846;&#x67B6;](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/GF.png)

```python
# -*- coding: utf-8 -*-
"""
@First_author: 不用先生
@Second_author: Dragon Liu
Operating environment: Python 3.7.1
lib:  opencv-python
Date: 2020/3/26
"""

import cv2
import numpy as np

input_fn = '03.png'

# 函数名：my_guidedFilter_oneChannel
# 函数功能：用于单通道图像（灰度图）的引导滤波函数；
# 参数：srcImg：输入图像，为单通道图像；
# 参数：guideImg：引导图像，为单通道图像，尺寸与输入图像一致；
# 参数：rad：滤波器大小r，应该保证为奇数，默认值为9；
# 参数：eps：防止a过大的正则化参数ϵ，
# 返回：dstImg：输出图像，尺寸、通道数与输入图像吻合；
def my_guidedFilter_oneChannel(srcImg, guidedImg, rad=13, eps=0.1):

    # 转换数值类型，并归一化
    srcImg = srcImg/255.0
    guidedImg = guidedImg/255.0
    img_shape = np.shape(srcImg)#查看矩阵或者数组的维数。
    # 求引导图像和输入图像的均值图,创建0矩阵
    dstImg = np.zeros(img_shape, dtype=float)
    
    P_mean = np.zeros(img_shape, dtype=float)
    I_mean = np.zeros(img_shape, dtype=float)
    I_square_mean = np.zeros(img_shape, dtype=float)
    I_mul_P_mean = np.zeros(img_shape, dtype=float)
    var_I = np.zeros(img_shape, dtype=float)
    cov_I_P = np.zeros(img_shape, dtype=float)
    
    a = np.zeros(img_shape, dtype=float)
    b = np.zeros(img_shape, dtype=float)
    a_mean = np.zeros(img_shape, dtype=float)
    b_mean = np.zeros(img_shape, dtype=float)
    # 在(rad, rad)窗口的内对图像做均值滤波。
    P_mean = cv2.boxFilter(srcImg, -1, (rad, rad), normalize=True) 
    I_mean = cv2.boxFilter(guidedImg,-1, (rad, rad), normalize=True) 

    I_square_mean = cv2.boxFilter(np.multiply(guidedImg, guidedImg), -1, (rad, rad), normalize=True) 
    I_mul_P_mean = cv2.boxFilter(np.multiply(srcImg, guidedImg), -1, (rad, rad), normalize=True)
    
    vvar_I = I_square_mean-np.multiply(I_mean,I_mean)
    cov_I_P = I_mul_P_mean-np.multiply(I_mean,P_mean)
    
    a = cov_I_P/(var_I+eps)
    b = P_mean-np.multiply(a,I_mean)
    
    a_mean = cv2.boxFilter(a, -1, (rad, rad), normalize=True) 
    b_mean = cv2.boxFilter(b, -1, (rad, rad), normalize=True) 
    
    dstImg = np.multiply(a_mean,guidedImg)+b_mean
    
    return dstImg*255.0
    
# 函数名：my_guidedFilter_threeChannel
# 函数功能：用于三通道图像（RGB彩色图）的引导滤波函数；
# 参数：srcImg：输入图像，为三通道图像；
# 参数：guideImg：引导图像，为三通道图像，尺寸与输入图像一致；
# 参数：rad：滤波器大小r，应该保证为奇数，默认值为9；
# 参数：eps：防止a过大的正则化参数ϵ，
# 返回：dstImg：输出图像，尺寸、通道数与输入图像吻合；
def my_guidedFilter_threeChannel(srcImg, guidedImg, rad=9, eps=0.01):
    
    img_shape = np.shape(srcImg)

    dstImg = np.zeros(img_shape, dtype=float)

    for ind in range(0,img_shape[2]):
        dstImg[:,:,ind] = my_guidedFilter_oneChannel(srcImg[:,:,ind],
              guidedImg[:,:,ind], rad, eps)
    
    dstImg = dstImg.astype(np.uint8)
    
    return dstImg


def main():
    img = cv2.imread(input_fn)#读入图像
    print( np.shape(img) )

    dstimg = my_guidedFilter_threeChannel(img, img, 9 , 0.01)#输入图像作为自身的引导图
    print( np.shape(dstimg) )
    # cv2.imwrite('output.jpg',dstimg)
    cv2.imshow('output', dstimg)
    cv2.waitKey(0)
    
if __name__ == '__main__':
    main()
```









\*\*\*\*




