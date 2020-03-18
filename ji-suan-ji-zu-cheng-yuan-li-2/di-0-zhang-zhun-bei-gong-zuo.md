# 第0章 准备工作

## git使用

### 0x01 学习文档

* 官方文档：[我跳](https://git-scm.com/)
* 菜鸟教程：[我跳](https://www.runoob.com/git/git-tutorial.html)

### 0x02 工作流程

![&#x56FE;1 git&#x5DE5;&#x4F5C;&#x6D41;&#x7A0B;](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-03-18_22-47-07.jpg)

* git、github、gitlab工作流程：[阮大牛讲解](http://www.ruanyifeng.com/blog/2015/12/git-workflow.html)

### 0x03 常用命令

#### **1. Git 配置**

```bash
git config --global user.name "dragon" 
git config --global user.email test@dragon.com
git config --global core.editor vim#设置默认编辑器
git config --list #查看配置信息
git config user.name#直接查阅某个环境变量的设定
```

* --global 所有的项目都会默认使用这里配置的用户信息；在某个特定的项目中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在当前项目的 .git/config 文件里。

#### 2. 初始化仓库

```bash
git init
git init newrepo
```

*  执行完成 **git init** 命令后，Git 仓库会生成一个 .git 目录，该目录包含了资源的所有元数据，其他的项目目录保持不变。
* 命令1执行完后会在当前目录生成一个 .git 目录，命令2，会在 newrepo 目录下会出现一个名为 .git 的目录，所有 Git 需要的数据和资源都存放在这个目录中。

#### 3. git add

```bash
git add *.c
git add README
git commit -m '初始化项目版本'
```

* 如果当前目录下有几个文件想要纳入版本控制，需要先用 git add 命令告诉 Git 开始对这些文件进行跟踪，然后提交;
* 以上命令将目录下以 .c 结尾及 README 文件提交到仓库中。
*  **git add .** 命令来添加当前项目的所有文件
* git add 命令可将该文件添加到缓存

#### 4. git clone

```bash
git clone <repo>
git clone <repo> <directory> #克隆到指定的目录
git clone git://github.com/schacon/grit.git
git clone git://github.com/schacon/grit.git mygrit
git clone git@github.com:fsliurujie/test.git   #--SSH协议
git clone git://github.com/fsliurujie/test.git  #--GIT协议
git clone https://github.com/fsliurujie/test.git #--HTTPS协议
```

* 命令3执行后当前目录下创建一个名为grit的目录，其中包含一个 .git 的目录，用于保存下载下来的所有版本记录
* 命令4自己定义要新建的项目目录名称
* git clone 时，可以所用不同的协议，包括 ssh, git, https 等，其中最常用的是 ssh，因为速度较快，还可以配置公钥免输入密码。













