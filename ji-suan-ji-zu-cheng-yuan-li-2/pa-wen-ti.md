# PA问题

## PA0问题

### 0x01 Linux and Linux?

* 相同点：四者都是Linux的发行版本，都使用Linux内核；
* 不同点：**从发行系列角度**，Debian和Ubuntu属于一个系列， CentOS和Red Hat属于一个系列；**从性质角度**，linux大体分为由商业公司维护的商业版本与由开源社区维护的免费发行版本，商业版本以Redhat为代表，开源社区版本则以Debian为代表；**从用户或者用途角度**， CentOS 、Red Hat 、Debian通常用于服务器领域，内核版本通常使用Linux2.6版本，运行十分稳定，而Ubuntu通常用于桌面领域，内核版本通常比较新，一般跟Linux内核同步更新；**从安装包管理方式角度**， CentOS和Red Hat使用yum/rpm进行安装包管理，Debian和Ubuntu 使用apt/dpkg的管理方式，但使用配置上大同小异。

### 0x02 Can't memory be larger?

问题1：内存大小不能无限大，一方面32位系统最大只能支持4GB内存，另一方面取决于物理机内存。

问题2： CPU不能直接访问硬盘的数据，只能通过把硬盘的数据先放到内存里， 然后再从内存里访问硬盘的数据。计算机操作系统会给内存每1个字节分配1个内存地址，在32位操作系统中, 内存的地址就是32位的2进制数，所以32位的地址范围是0x00000000 ~ 0xFFFFFFFF。地址个数：2^32 = 4 \* 1024\(G\) \* 1024\(M\) \* 1024\(K\) = 4294967296 ,而每1个地址对应1个1个字节， 容量就是1byte， 所以2^32个地址就总共能对应应**4GB** 的内存容量。简言之，CPU寻址范围决定最大支持内存。

### 0x03 Why Windows is quite 'fat'?

　　Windows有GUI，而我们安装的Debian是CLI，没有图形化界面，所以安装Windows需要更多的磁盘空间和内存，因此Debian非常‘slim’，Windows相当'fat'。

### 0x04 Why executing the 'poweroff' command requires superuser privilege?

　　当Linux被用作服务器或类似服务器时，很多用户通过SSH进入Linux机器，其中一个具有SSH访问权限的人将其关闭，其他远程登录的用户也被迫关机，如果其他用户在做十分重要的事情，那么损失很大，此外，远程登录的用户将无法重新打开它。

### 0x05 What happened?

 　　`make`命令执行后，读入所有的Makefile，目标文件与所有的`.c`文件创建依赖关系，目标文件生成，对应的整个项目被编译。

### 0x06 How will you do?

 　　最重要的是设计好CPU，编写程序，使控制器能够控制运算器进行数据加工、从内存取送数据；存储器能够保存信息；然后再编写驱动程序能够驱动I/O等外部设备。

