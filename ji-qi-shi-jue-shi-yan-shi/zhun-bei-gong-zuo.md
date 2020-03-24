# 准备工作

## 0x01 labelme软件标注显著度图（二值图像）

1. 安装Anaconda：[我跳](https://blog.csdn.net/ITLearnHall/article/details/81708148)
2. labelme安装及使用：[我跳](https://www.bilibili.com/video/av50300496?p=1)
3. **实现labelme批量json\_to\_dataset：**[**我跳**](https://blog.csdn.net/yql_617540298/article/details/81110685)\*\*\*\*

{% hint style="warning" %}
**注意**  
问题1：3. 中按照步骤会报错：`AttributeError: module 'labelme.utils' has no attribute 'draw_label'`解决1：降低labelme版，`pip install labelme==3.16.2`
{% endhint %}

## 0x02 Latex使用

1. 安装配置Latex，其中“Tex Live Installer”一般要安装3个小时左右\(毕竟3966个文件\)；安装讲解视频：[我跳](https://www.bilibili.com/video/av90629350?from=search&seid=9672896493142246187)
2. Latex使用：[我跳](https://wenku.baidu.com/view/15ac929251e2524de518964bcf84b9d528ea2cab.html)

## 0x03 Matlab

1. 官方文档：内有入门视频和进阶视频，[链接](https://ww2.mathworks.cn/help/index.html?s_tid=CRUX_lftnav)
2. 无须编程基础的教程：[1-6讲](https://www.bilibili.com/video/av7081367?p=1)，[7-讲](https://www.bilibili.com/video/av9810059/)

## 0x04 PS

#### **1. 图像纹理**：

* [PS中添加纹理图案](https://jingyan.baidu.com/article/7c6fb4283f057580642c90e7.html)   
* [图层添加纹理](https://www.bilibili.com/video/av84432956) 
* [批量操作](https://m.copyan.com/dc/ps%E6%80%8E%E4%B9%88%E6%89%B9%E9%87%8F%E5%A4%84%E7%90%86/)

#### 2. 问题解决

* \*\*\*\*[**解决Photoshop暂存盘已满**](https://jingyan.baidu.com/article/95c9d20d66921aec4f75617c.html)\*\*\*\*

### **0x05 脚本**

* **批量修改文件名**

```python
import os
path=input('请输入文件路径(结尾加上/)：')       

#获取该目录下所有文件，存入列表中
fileList=os.listdir(path)

num = 0 #下标
id = 1400 #照片自定义序号
for i in fileList:
    
    #设置旧文件名（就是路径+文件名）
    oldname=path+ os.sep + fileList[num]   # os.sep添加系统分隔符
    
    #设置新文件名
    newname=path + os.sep +'img_'+str(id+1) + '_06' +'.jpg'
    
    os.rename(oldname,newname)   #用os模块中的rename方法对文件改名
    print(oldname,'======>',newname)
    
    num += 1
    id += 1
```

* **批量抓取网站照片**

```python
"""
    功能：批量下载网站图片
    时间：2019-5-18 16:14:01
    作者：倚窗听雨
    second_author: Dragonliu
"""
import urllib.request
import re
import os
 
headers = {
    "User-Agent":"yjs_id=0c19bb42793fd5c3c8c228f50173ca19; Hm_lvt_14b14198b6e26157b7eba06b390ab763=1529398363; __cfduid=de4421757fb00c0120063c1dbd0308e511558166501; ctrl_time=1; Hm_lvt_526caf4e20c21f06a4e9209712d6a20e=1558166930; zkhanecookieclassrecord=%2C66%2C; PHPSESSID=6bee044771973aba4aa5b989f1a3722d; zkhanmlusername=qq_%B7%E7%BE%ED%B2%D0%D4%C6186; zkhanmluserid=1380421; zkhanmlgroupid=1; zkhanmlrnd=4g6arf9678I6URIitCJ2; zkhanmlauth=1b4f3205834ec05575588adc84c0eb52; zkhandownid24031=1; Hm_lpvt_526caf4e20c21f06a4e9209712d6a20e=1558167143; security_session_verify=eb4cb5687c224e77089c64935fa16df8",
}
 
ur = "http://pic.netbian.com"
url_list = []
num = 1551 #图片序号
 
#获取各类型图片url
def picture(url):
    res = urllib.request.Request(url,data=None,headers=headers)
    html = urllib.request.urlopen(res).read().decode('GB18030')#这里如果gb2312报错，就改成GB18030
    # GB2312，GBK，GB18030，是兼容的，包含的字符个数：GB2312 < GBK < GB18030
 
    pic = re.findall(r'<div class="classify clearfix.+</div>',html)
    start = 0
    text = pic[0]
    for i in re.findall(r'<a ',pic[0]):
        a = re.search(r'<a ',text)
        end_a = re.search(r'</a>',text)
 
        href = url+text[a.start():end_a.end()].split('"')[1]
        title = text[a.start():end_a.end()].split('"')[3]
        d = {'href':href,'title':title}
        url_list.append(d)
 
        text = text[end_a.end():]
 
#获取图片链接
def get_pic(url):
    res = urllib.request.Request(url,headers=headers)
    html = urllib.request.urlopen(res).read().decode('gbk')
 
    page = re.search(r'class="slh".+[\s].+',html).group().split('</a')[0].split('>')[-1]
    print('共',page,'页')
    start_page = int(input('下载起始页：'))
    end_page = int(input('下载到哪页：'))
    total = 0
    for p in range(start_page,end_page+1):
        if p ==1:
            url2 = url + 'index'+'.html'
        else:
            url2 = url + 'index_'+str(p)+'.html'
        print('\n',url2)
        res2 = urllib.request.Request(url2, headers=headers)
        html2 = urllib.request.urlopen(res2).read().decode('gbk')
 
        texts =re.findall(r'<ul class="clearfix".+[\s]*.+',html2)
        t = texts[0]
        print('准备下载第',p,'页图片......')
 
        #获取当前页的图片并下载
        for i in re.findall(r'<li>',t):
            start_li = re.search(r'<li>',t)
            end_li = re.search(r'</li>',t)
 
            href = ur+t[start_li.start():end_li.end()].split('"')[1]
            name = t[start_li.start():end_li.end()].split('b>')[-2][:-2]
 
            total += download(href,name)
            # total += download(href, num)
            t = t[end_li.end():]
    print('\n下载完成，共下载{}张图片'.format(total))
#下载图片
def download(url, name):
    global num #全局变量
    res = urllib.request.Request(url, headers=headers)
    html = urllib.request.urlopen(res).read().decode('gbk')
    down_url = re.search(r'<a href="" id="img">.+',html).group()
    down_url = ur + re.split('"',down_url)[5]
    try:
        data = urllib.request.urlopen(down_url,timeout=10).read()
    except Exception as e:
        print(e,'跳过此图片：'+name+'.jpg')
        return 0
    t = -1
 
    #img目录不存在自动创建
    if not os.path.exists('img'):
        os.makedirs('img')
    #该文件不存在时才下载（存储位置可自行修改，现在存在当前目录的img目录下）
    
    if not os.path.exists('img\\'+'img_'+str(num)+'.jpg'):
        with open('img\\' + 'img_' + str(num)+'.jpg','wb')as f:
            f.write(data)
        print('img_' + str(num)+'.jpg'+"\t\t下载成功")
        t = 1
        num = num + 1
        if num == 1601:
            os._exit(0)
    else:
        print('img_' + str(num) + '.jpg' + "\t\t已存在")
        t = 0
    return t
 
#主程序
def main():
    picture("http://pic.netbian.com")
    print('4k图片网欢迎您'.center(20,'*'))
 
    for i,v in enumerate(url_list):
        print("{}、{}".format(i+1,v['title']))
    while True:
        try:
            t = int(input('要下载的图片类型（序号）：'))
            if t not in range(1,13):
                raise IndexError
            break
        except ValueError:
            print('请输入正确的序号！')
        except IndexError:
            print('请输入正确的序号！')
    get_pic(url_list[t-1]['href'])
 
 
if __name__ == '__main__':
    main()
```

