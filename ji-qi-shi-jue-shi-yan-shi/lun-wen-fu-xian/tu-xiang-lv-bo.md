# 窗口感知的高斯引导滤波+图像滤波整理

## 基础知识

1.  **定义**：图像滤波，即在尽量保留图像细节特征的条件下对目标图像的噪声进行抑制，是图像预处理中不可缺少的操作，其处理效果的好坏将直接影响到后续图像处理和分析的有效性和可靠性。
2. **比喻：**我们可以把滤波器想象成一个包含加权系数的窗口，当使用这个滤波器平滑处理图像时，就把这个窗口放到图像之上，透过这个窗口来看我们得到的图像。
3. **公式：** $$O(i, j) = \sum_{m,n}I(i+m,j+n)K(m,n)$$ **** 其中O\(i, j\)是像素输出值，I\(i+m, j+n\)是像素输入值，K为滤波器（核：二维矩阵，核的不同值表示不同的算法。）
4. **种类**：低通滤波器可以消除噪声、模糊化，高通滤波器可以提取边缘。[白话文讲计算机视觉-第三讲-滤波器](https://blog.csdn.net/u013631121/article/details/80444602?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)
5. **作用**：图像滤波可以更改或者增强图像。通过滤波，可以强调一些特征或者去除图像中一些不需要的部分。滤波是一个邻域操作算子，利用给定像素周围的像素的值决定此像素的最终的输出值。常见的应用包括去噪、图像增强、检测边缘、检测角点、模板匹配等。

## 非学习类型算法

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
Date: 2020/3/16
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
3. **代码**：OpenCV在Python中双边滤波函数是**cv2.bilateralFilter\(src, d, sigmaColor, sigmaSpace）**时间复杂度 $$O(Nr^2)$$  **① s**rc是输入图像； ② d是在过滤期间使用的每个像素邻域的直径，如果输入d非0，则sigmaSpace由d计算得出，如果sigmaColor没输入，则sigmaColor由sigmaSpace计算得出； ③ sigmaColor是灰度值相似性高斯函数标准差，色彩空间的标准方差，一般尽可能大， 较大的参数值意味着像素邻域内较远的颜色会混合在一起， 从而产生更大面积的半相等颜色； ④ sigmaSpace是空间高斯函数标准差，坐标空间的标准方差\(像素单位\)，一般尽可能小。 参数值越大意味着只要它们的颜色足够接近，越远的像素都会相互影响。 当d &gt; 0时，它指定邻域大小而不考虑sigmaSpace。 否则，d与sigmaSpace成正比。

```python
#encoding:utf-8
"""
@author: Dragon Liu
Operating environment: Python 3.7.1
lib:  opencv-python
Date: 2020/3/16
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

#### **1. 定义**

　　引导滤波的思想用一张引导图像产生权重，从而对输入图像进行处理。引导滤波除了可以用于图像平滑，还可以用于HDR压缩、细节增强、图像去雾、联合上采样等图像处理任务。引导滤波中空间域的贡献自然取决于窗口的大小，即由参数 r 决定。而标准差则是评判颜色差异性的参数，窗口中标准差越大，说明局部的像素相似性越差。

#### **2. 公式：**[【图像处理】引导滤波](https://blog.csdn.net/u013921430/article/details/99695647)

1. **权重** $$W_{ij}(i,j) = \frac{1}{|ω|^2} \sum_{k:(i,j)\in ω_k} (1+ \frac{(I_i-μ_k)(I_j-μ_k)}{σ_k^2+ϵ})$$   \(局部窗口 $$ω_k$$ ；ϵ是 $$L_2$$ 范数正则化系数，防止$$a_k$$ ​过大； $$μ_k$$与 $$ σ_k$$ ​表示 $$ I_i$$ 在窗口内的均值、标准差； $$∣w∣$$ 表示窗口内像素块的总数 \)
2. **结果** $$q_i = \sum_{j}{W_{ij}(I)*p_j}$$   \(q、I、p分表表示输出图像、引导图像和输入图像 ，i、j 分别表示图像中像素点的索引。权重 W 仅与引导图像 I 有关，而在双边滤波中权重 W 由输入图像自身决定。\)

#### **3. 代码1\(引导滤波\)**：

　　第一个代码块是手写实现引导滤波。时间复杂度O\(N\)，当 r 与 ϵ 越大，图像被平滑的程度越大。伪代码中：r是窗口半径， $$f_{mean}(I,r)$$ 表示在\(r, r\)窗口对图像做均值滤波。大佬博客：[我跳](https://blog.csdn.net/u013921430/article/details/99695647)   
　　第二个代码块是使用的现有库。参考：[我跳](https://jinzhangyu.github.io/2018/09/06/2018-09-06-OpenCV-Python%E6%95%99%E7%A8%8B-16-%E5%B9%B3%E6%BB%91%E5%9B%BE%E5%83%8F-3/)

![&#x56FE;1 GF&#x7B97;&#x6CD5;&#x6846;&#x67B6;](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/GF.png)

```python
# -*- coding: utf-8 -*-
"""
@First_author: 不用先生
@Second_author: Dragon Liu
Operating environment: Python 3.7.1
lib:  opencv-python
Date: 2020/3/16
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
    
    # 在(rad, rad)窗口的内对图像做均值滤波。
    P_mean = cv2.boxFilter(srcImg, -1, (rad, rad), normalize=True) # p的均值平滑
    I_mean = cv2.boxFilter(guidedImg,-1, (rad, rad), normalize=True) # I的均值平滑

    I_square_mean = cv2.boxFilter(np.multiply(guidedImg, guidedImg), -1, (rad, rad), normalize=True) #I*I的均值平滑
    I_mul_P_mean = cv2.boxFilter(np.multiply(srcImg, guidedImg), -1, (rad, rad), normalize=True)# I*p的均值平滑
    
    var_I = I_square_mean-np.multiply(I_mean,I_mean)# 方差
    cov_I_P = I_mul_P_mean-np.multiply(I_mean,P_mean)# 协方差
    
    a = cov_I_P/(var_I+eps)# 相关因子a
    b = P_mean-np.multiply(a,I_mean)# 相关因子b
    
    a_mean = cv2.boxFilter(a, -1, (rad, rad), normalize=True) # 对a进行均值平滑
    b_mean = cv2.boxFilter(b, -1, (rad, rad), normalize=True)  # 对b进行均值平滑
    
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

```python
# -*- coding: utf-8 -*-
"""
@First_author: Jin ZhangYu
@Second_author: Dragon Liu
Operating environment: Python 3.7.1
lib:  opencv-contrib-python
Date: 2020/3/16
"""
# 导入库
import argparse
import cv2
import matplotlib.pyplot as plt
import skimage
import numpy as np

# 构造参数解析器
# ap = argparse.ArgumentParser()
# ap.add_argument("-H:\project_work\Machine_Vision_Lab\thesis\Gaussian\code", "--02.png", required=True, help = "Path to the image")
# args = vars(ap.parse_args())

# 加载图像并显示
input_fn = '02.png'
# img = cv2.imread(args["image"],1)
img = cv2.imread(input_fn)
img = img[:,:,::-1]
guide = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)

# 进行导向滤波
dst1 = cv2.ximgproc.guidedFilter(
            guide=guide, src=img, radius=16, eps=50, dDepth=-1)
dst2 = cv2.ximgproc.guidedFilter(
            guide=guide, src=img, radius=16, eps=200, dDepth=-1)
dst3 = cv2.ximgproc.guidedFilter(
            guide=guide, src=img, radius=16, eps=1000, dDepth=-1)

# 绘制图片
images = [img,[dst1,dst2,dst3]]
titles =    [
                'Original',
                ['Guided Filter eps=50','Guided Filter eps=200','Guided Filter eps=1000']
            ]

# 绘制原图
plt.figure(figsize=(9,4))

plt.subplot(2, 3, 2),plt.imshow(images[0])
plt.title(titles[0], fontsize=10),plt.xticks([]), plt.yticks([])

plt.subplot(2, 3, 4),plt.imshow(images[1][0])
plt.title(titles[1][0], fontsize=10),plt.xticks([]), plt.yticks([])

plt.subplot(2, 3, 5),plt.imshow(images[1][1])
plt.title(titles[1][1], fontsize=10),plt.xticks([]), plt.yticks([])

plt.subplot(2, 3, 6),plt.imshow(images[1][2])
plt.title(titles[1][2], fontsize=10),plt.xticks([]), plt.yticks([])

# plt.savefig('1_out.png', transparent=True, dpi=300, pad_inches = 0)
plt.show()
```

#### 4. 代码2\(快速导向滤波\)

　　****通过下采样减少像素点，计算mean\_a & mean\_b后进行上采样恢复到原有的尺寸大小。假设缩放比例为s,那么缩小后像素点的个数为 $$\frac {N}{s^2}$$ ，那么时间复杂度变为 $$O(\frac {N}{s^2})$$ 。伪代码中：fmean代表均值平滑，fsubsample代表图像下采样即缩小图像，fupsample代表图片上采样即放大图像，s为缩小系数。参考：[我跳](https://blog.csdn.net/wsp_1138886114/article/details/84228939?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)

![&#x56FE;2 FGF&#x7B97;&#x6CD5;&#x6846;&#x67B6;](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/FGF.png)

```python
# -*- coding: utf-8 -*-
"""
@First_author: SongpingWangSongpingWangs
@Second_author: Dragon Liu
Operating environment: Python 3.7.1
lib:  opencv-python
Date: 2020/3/16
"""
import cv2
import numpy as np

def guideFilter(I, p, winSize, eps, s):
    # 输入图像的高、宽
    h, w = I.shape[:2]

    # 缩小图像
    size = (int(round(w * s)), int(round(h * s)))
    small_I = cv2.resize(I, size, interpolation=cv2.INTER_CUBIC)
    small_p = cv2.resize(I, size, interpolation=cv2.INTER_CUBIC)

    # 缩小滑动窗口
    X = winSize[0]
    small_winSize = (int(round(X * s)), int(round(X * s)))

    # I的均值平滑 p的均值平滑
    mean_small_I = cv2.blur(small_I, small_winSize)
    mean_small_p = cv2.blur(small_p, small_winSize)

    # I*I和I*p的均值平滑
    mean_small_II = cv2.blur(small_I * small_I, small_winSize)
    mean_small_Ip = cv2.blur(small_I * small_p, small_winSize)

    # 方差、协方差
    var_small_I = mean_small_II - mean_small_I * mean_small_I
    cov_small_Ip = mean_small_Ip - mean_small_I * mean_small_p

    small_a = cov_small_Ip / (var_small_I + eps)
    small_b = mean_small_p - small_a * mean_small_I

    # 对a、b进行均值平滑
    mean_small_a = cv2.blur(small_a, small_winSize)
    mean_small_b = cv2.blur(small_b, small_winSize)

    # 放大
    size1 = (w, h)
    mean_a = cv2.resize(mean_small_a, size1, interpolation=cv2.INTER_LINEAR)
    mean_b = cv2.resize(mean_small_b, size1, interpolation=cv2.INTER_LINEAR)

    q = mean_a * I + mean_b

    return q
    
if __name__ == '__main__':
    eps = 0.01
    winSize = (16,16)       #类似卷积核（数字越大，磨皮效果越好）
    image = cv2.imread(r'02.png', cv2.IMREAD_ANYCOLOR)
    image = cv2.resize(image,None,fx=0.8,fy=0.8,interpolation=cv2.INTER_CUBIC)
    I = image/255.0       #将图像归一化
    p =I
    s = 3 #步长
    guideFilter_img = guideFilter(I, p, winSize, eps,s)

    # 保存导向滤波结果
    guideFilter_img = guideFilter_img  * 255         #(0,1)->(0,255)
    guideFilter_img[guideFilter_img  > 255] = 255    #防止像素溢出
    guideFilter_img = np.round(guideFilter_img )
    guideFilter_img = guideFilter_img.astype(np.uint8)
    cv2.imshow("image",image)
    cv2.imshow("winSize_16", guideFilter_img )
    cv2.waitKey(0)
    cv2.destroyAllWindows()
```

### 0x07 高通滤波 -- 边缘检测/高反差保留

1. **定义**：
2. **代码**：使用的函数有：`cv2.Sobel()` , `cv2.Schar()` , `cv2.Laplacian()` Sobel, scharr其实是求一阶或者二阶导数。scharr是对Sobel的优化。 Laplacian是求二阶导数。cv2.Sobel\(\) 是一种带有方向过滤器。参考：[我跳](https://blog.csdn.net/wsp_1138886114/article/details/82872838?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)

```python
# -*- coding: utf-8 -*-
"""
@First_author: SongpingWang
@Second_author: Dragon Liu
Operating environment: Python 3.7.1
lib:  opencv-python
Date: 2020/3/16
"""

"""
dst = cv2.Sobel(src, ddepth, dx, dy[, dst[, ksize[, scale[, delta[, borderType]]]]])
src:    需要处理的图像；
ddepth: 图像的深度，-1表示采用的是与原图像相同的深度。 
        目标图像的深度必须大于等于原图像的深度；
dx和dy: 求导的阶数，0表示这个方向上没有求导，一般为0、1、2。

dst     不用解释了；
ksize： Sobel算子的大小，必须为1、3、5、7。  ksize=-1时，会用3x3的Scharr滤波器，
        它的效果要比3x3的Sobel滤波器要好 
scale： 是缩放导数的比例常数，默认没有伸缩系数；
delta： 是一个可选的增量，将会加到最终的dst中， 默认情况下没有额外的值加到dst中
borderType： 是判断图像边界的模式。这个参数默认值为cv2.BORDER_DEFAULT。

"""

import cv2

img=cv2.imread('02.png',cv2.IMREAD_COLOR)
x=cv2.Sobel(img,cv2.CV_16S,1,0)
y=cv2.Sobel(img,cv2.CV_16S,0,1)

absx=cv2.convertScaleAbs(x)
absy=cv2.convertScaleAbs(y)
dist=cv2.addWeighted(absx,0.5,absy,0.5,0)

cv2.imshow('original_img',img)
cv2.imshow('y',absy)
cv2.imshow('x',absx)
cv2.imshow('dsit',dist)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

### 0x08 窗口感知的高斯引导滤波

* **gr.m**

```python
function result = gr(px, py, qx, qy, dr)
% 高斯空间核函数
    result = exp( - ( (qx - px)^2 + (qy - py)^2 ) / (2 * dr^2) );
end
```

* **gzeta.m**

```python
function result = gzeta(guide_img, div, px, py, qx, qy, dzeta)
% 高斯频域核函数
    result = exp( - ( ( guide_img(px, py, div) - guide_img(qx, qy, div) )^2 )  / (2 * dzeta^2) );
end
```

* **GS.m**

```python
function output = GS(image, r, dr, px, py, div)
% 求解高斯空间域滤波，返回指定像素点(p)的输出
    Upsilon = 0;%τ，归一化系数
    output = 0;
    for i = -r : r % 以p为中心的窗口半径为2r+1的区域
        for j = -r : r
            Upsilon = Upsilon + gr(px, py, px + i, py + j, dr);
            output = output + gr(px, py, px + i, py + j, dr) * image(px + i,py + j,div);
        end
    end
    output = output / Upsilon ;
end
```

* **WGGF.m**

```python
function output = WGGF(guide_img, source, r, dzeta, px, py, div, lambda)
% 窗口感知的高斯引导滤波
%求解WGGF在每个像素点p的输出并返回
    Upsilon = 0;%τ，归一化系数
    output = 0;
    flag = 0;
    for i = -r : r
        for j = -r : r
            temp = abs( guide_img(px + i, py + 1, div) - guide_img(px, py, div) );
            if temp <= lambda 
                flag = flag + 1;
                Upsilon = Upsilon + gzeta(guide_img, div, px, py, px+i, py+j, dzeta);
                output = output + guide_img(px + i,py + j,div) * gzeta(guide_img, div, px, py, px+i, py+j, dzeta);
            end
        end
    end

    if flag == 1 %不满足窗口感知的要求，返回3*3窗口中的像素点中值
        output = medfilt2( source( (px - 1):(px + 1), (py - 1):(py + 1), j), [3,3] );
    else %满足条件
        output = output / Upsilon ;
    end
end
```

* **Main.m**

```python
%% 读取图片
source = im2double( imread('01.jpg') );
guide_img = source;

%% 求解高斯引导滤波
[m ,n, div] = size(source);
r = 5; %窗口半径
dr = 0.5; %空域带宽
for k = 1 : div
    for i = 1 : m
        for j = 1 : n
            if i <= r || i >= m - r || j <= r || j >= n - r %图片四周处理(原像素)
                continue;
            else
                guide_img(i,j,k) = GS(source, r, dr, i, j, k); %空间域滤波
            end
        end
    end
end

%% 求解WGGF
target = guide_img;
r = 5; %窗口半径
dzeta = 0.1; %频域带宽
lambda = 0.12; % λ为一选定的阈值 
for k = 1 : div
    for i = 1 : m
        for j = 1 : n
            if i <= r || i >= m - r || j <= r || j >= n - r%图片四周处理(引导像素)
                continue;
            else
                target(i, j, k) = WGGF(guide_img, source, r, dzeta, i, j, k, lambda); 
            end
        end
    end
end

%% 显示图形
figure;
subplot(1,2,1), imshow(source), title('Source image');
subplot(1,2,2), imshow(target), title('WGGF image');
```

* **WGGF.py\(Bug\)**

```python
#encoding:utf-8
"""
@author: Dragon Liu
Operating environment: Python 3.7.1
lib:  opencv-python
Date: 2020/3/22
BUG: 时间复杂度O(m*n*div*r*r)，不可行，另外存在img[]访问问题
"""
#导入库
import math
import cv2  
import numpy as np  
import matplotlib.pyplot as plt

# 高斯空间核函数
def gr(px, py, qx, qy, dr):

   nut = math.exp( - ( pow((qx - px), 2) + pow((qy - py), 2) ) ) #分子
   det = 2 * pow(dr, 2) #分母
   result =  nut / det  
   return result

# 高斯频域核函数
def gzeta(guide_img, div, px, py, qx, qy, dzeta):
	
   guide_img = guide_img 
   nut = math.exp( - ( pow( ( guide_img[px, py, div] - guide_img[qx, qy, div] ), 2 ) ) ) #分子
   det = 2 * pow(dzeta, 2)
   result =  nut / det
   return result

# 求解高斯空间域滤波，返回指定像素点(p)的输出
def GS(image, r, dr, px, py, div):

   Upsilon = 0 #τ，归一化系数
   output = 0
   for i in range(r, -(r+1), -1):# 以p为中心的窗口半径为2r+1的区域
      for j in range(r, -(r+1), -1):
         Upsilon = Upsilon + gr(px, py, px + i, py + j, dr)
         output = output + gr(px, py, px + i, py + j, dr) * image[px + i,py + j,div]
   
   output = output / Upsilon 
   return output

#求解指定窗口(3*3)的中值
def medbox(img, x, y, div, length, width):
   
   nums = []
   length = width = 3
   for i in range(math.floor(length/2), -math.floor(length/2)-1, -1):
      for j in range(math.floor(width/2), -math.floor(width/2)-1, -1):
         nums.append( img[x+i, y+j, div])

   return np.median(nums)

#窗口感知的高斯引导滤波
#求解WGGF在每个像素点p的输出并返回
def WGGF(guide_img,source,r,dzeta,px,py,div, lam):
   
   guide_img = guide_img 
   source = source  
   Upsilon = 0 #τ，归一化系数
   output = 0
   flag = 0
   for i in range(r, -(r+1), -1):# 以p为中心的窗口半径为2r+1的区域
      for j in range(r, -(r+1), -1):
         temp = abs( guide_img[px + i, py + 1, div] - guide_img[px, py, div] )
         if temp <= lam:
               flag = flag + 1
               Upsilon = Upsilon + gzeta(guide_img, div, px, py, px+i, py+j, dzeta)
               output = output + guide_img[px + i,py + j,div] * gzeta(guide_img, div, px, py, px+i, py+j, dzeta)

   if flag == 1 or Upsilon == 0: #不满足窗口感知的要求，返回3*3窗口中的像素点中值
      output = medbox( source, px, py, j, 3, 3 )
   else: #满足条件
      output = output / Upsilon 
   return output

# 主函数，测试
def main():
   #读取图片
   img = cv2.imread('02.png', 1)
   source = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
   source = source / 255.0
   guide_img = source
   
   print(1.666)
   #求解高斯引导滤波
   [m ,n, div] = np.shape(source)#查看矩阵或者数组的维数。
   r = 5 #窗口半径
   dr = 0.5 #空域带宽
   # 高斯滤波
   guide_img = cv2.GaussianBlur(source, (r,r), dr)
               
   
   print(2.666)
   #求解WGGF
   target = guide_img
   r = 5 #窗口半径
   dzeta = 0.1 #频域带宽
   lam = 0.12 #λ为一选定的阈值 
   num = 0
   for k in range(div):
      for i in range(m):
         for j in range(n):
               if i <= r or i >= m - r or j <= r or j >= n - r: #图片边界处理(引导像素)
                  continue
               else:
                  target[i, j, k] = WGGF(guide_img, source, r, dzeta, i, j, k, lam)
               num = num + 1
               print(num)
   print(3.666)
   #显示图形
   titles = ['Source Image', 'WGGF Image']  
   images = [source*255.0, target*255.0]  
   for i in range(2):  
      plt.subplot(1, 2, i+1), plt.imshow(images[i], 'gray')  
      plt.title(titles[i])  
      plt.xticks([]),plt.yticks([]) #禁止输出坐标轴 
   plt.show()  

    
if __name__ == '__main__':
    main()
```

