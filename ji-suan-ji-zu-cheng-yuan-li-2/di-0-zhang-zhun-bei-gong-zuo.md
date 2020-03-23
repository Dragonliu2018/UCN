# 第0章 准备工作

## git使用

### 0x01 学习文档

* 官方文档：[我跳](https://git-scm.com/)
* 菜鸟教程：[我跳](https://www.runoob.com/git/git-tutorial.html)

### 0x02 工作流程

![&#x56FE;1 git&#x5DE5;&#x4F5C;&#x6D41;&#x7A0B;](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-03-18_22-47-07.jpg)

* git、github、gitlab工作流程：[阮大牛讲解](http://www.ruanyifeng.com/blog/2015/12/git-workflow.html)

### 0x03 Git 工作区、暂存区和版本库

![&#x56FE;2 Git &#x5DE5;&#x4F5C;&#x533A;&#x3001;&#x6682;&#x5B58;&#x533A;&#x548C;&#x7248;&#x672C;&#x5E93;](https://cdn.jsdelivr.net/gh/Dragonliu2018/FigureBed@master/img/Snipaste_2020-03-19_18-27-19.jpg)

* **工作区：**就是你在电脑里能看到的目录。
* **暂存区：**英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
* **版本库：**工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

### 0x04 创建与基本操作

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

#### 5. git status \(-s\) 

* 显示你上次提交更新后的更改或者写入缓存的改动\(获得简短的结果输出\)；
* 输出信息中：??：未添加到缓存；A：已加入到缓存；AM：这个文件在我们将它添加到缓存之后又有改动

#### 6. git diff

* git diff 来查看执行 git status 的结果的详细信息。
* 尚未缓存的改动：**git diff**    
* 查看已缓存的改动： **git diff --cached**
* 查看已缓存的与未缓存的所有改动：**git diff HEAD**
* 显示摘要而非整个 diff：**git diff --stat**

#### 7. git commit

* 将缓存区内容添加到仓库中
* -m 选项以在命令行中提供提交注释。
* -a 选项跳过git add 提交缓存的流程

#### 8. git reset HEAD &lt;file&gt;

* 取消已缓存的内容

#### 9. git rm &lt;file&gt;

```bash
git rm <file>
git rm -f <file>
git rm --cached <file>
git rm –r * #删除该目录下的所有文件和子目录
```

### 

* 移除某个文件\(从已跟踪文件清单中移除，然后提交\)
* 如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f
* 把文件从暂存区域移除，但仍然希望保留在当前工作目录中，换句话说，仅是从跟踪清单中删除，使用 --cached 

#### 10. git mv

* 移动或重命名一个文件、目录、软连接
* git mv &lt;source file&gt; &lt;new file&gt;

### 0x05 Git 分支管理

```bash
git branch (branchname) #创建分支
git checkout (branchname) #切换分支
git checkout -b (branchname)#创建新分支并立即切换到该分支下
git merge <change_site>#合并某分支到master
git branch # 列出本地分支
git branch -d (branchname) #删除分支
```

### 0x06 Git 查看提交历史

```bash
git log #列出历史提交记录
git log --oneline #查看历史记录的简洁的版本
git log --graph #查看历史中什么时候出现了分支、合并
git log --reverse #逆向显示所有日志
git log --author=<name>#查找指定用户的提交日志
git log --oneline --before={3.weeks.ago} --after={2010-04-18}#指定时间段
git log --decorate #可查看git标签
```

### 0x07 Git 标签

```bash
git tag -a v1.0 #创建带注解的标签
git tag -a v0.9 85fc7e7#追加标签
git tag #查看标签
git tag -a <tagname> -m "runoob.com标签"#指定标签信息命令
git tag -d <tagname> #删除标签
```

### 0x08 Git 远程仓库\(Github\)

```bash
git remote add [shortname] [url] #添加远程仓库
ssh-keygen -t rsa -C "youremail@example.com" #生成 SSH Key
ssh -T git@github.com #验证ssh配置是否成功
git remote #查看当前配置有哪些远程仓库
git remote -v #每个别名的实际链接地址
git fetch [alias] #查看是否有更新数据，从远程仓库下载新分支与数据
git merge [alias]/[branch] #从远端仓库提取数据并尝试合并到当前分支
git push [alias] [branch] #推送你的新分支与数据到某个远端仓库
git remote rm [别名] #删除远程仓库
```

## C语言基础知识

### 0x01 struct 与 union

1. 在存储多个成员信息时，编译器会自动给struct第个成员分配存储空间，struct 可以存储多个成员信息，而Union每个成员会用同一个存储空间，只能存储最后一个成员的信息。
2. 都是由多个不同的数据类型成员组成，但在任何同一时刻，Union只存放了一个被先选中的成员，而结构体的所有成员都存在。
3. 对于Union的不同成员赋值，将会对其他成员重写，原来成员的值就不存在了，而对于struct 的不同成员赋值 是互不影响的。
4. 注：在很多地方需要对结构体的成员变量进行修改。只是部分成员变量，那么就不能用联合体Union，因为Union的所有成员变量占一个内存。eg：在链表中对个别数值域进行赋值就必须用struct.



