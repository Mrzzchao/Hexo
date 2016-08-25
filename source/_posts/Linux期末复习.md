---
title: Linux期末复习
date: 2016-05-28 17:24:02
categories: Linux
tags: Linux
---
# 前言
一晃眼，期末再次来临，各种考试也接踵而至。考试是一学期的浪荡再加3天苦读，相信这是很多大学生的4年状态。而考完后，这些挤压在脑壳中的字符就像被格式化一般，最后一无所有。所以为了在Linux这门课上留下点什么，在此记录。（参照老邝PPT所给考点归纳，貌似依旧应试）

# 正文

## Linux、类unix基本常识
### 什么是linux
是一个类 UNIX 内核的可以自由发布的实现版本，是一个操作系统的底层核心。可以获得内核源代码，编译并安装，然后获得并安装许多其他自由发布的软件，从而创建一个完整的 Linux，通常称为 Linux 系统

### Linux的特性
开放性、多用户、多任务、良好的用户界面、设备独立性、丰富的网络功能、可靠的系统安全、良好的可移植性。

### GNU、GPL概念
**GNU**

* 1983 年 Richard Stallman(自由软件业的精神教父) 创办 GNU(GNU’s not Unix)计划
* 旨在发展一個类-Unix 且为 自由软件 的完整操作系統

<!-- more -->
**GPL**

* GNU GPL（GNU General Public License，通用公共许可证）是一个广泛被使用的自由软件许可证，最初由理查德·斯托曼为GNU计划而撰写
* 在GPL中有一个关键的概念就是Copyleft。GPL规定，再发行权的授予需要许可证接受人公开软件的源代码及所有修改，而且复制件、修改版本都必须以GPL为许可证。这些要求就是Copyleft，它的基础就是作品在法律上版权所有
* Copyleft（是copyright的反话，就是防止有人给自由软件的使用加上限制）

### Linux的版本
**Linux操作系统（kernel+ultiliteies**）：专家才会用
**Linux发行版（Distribution**）：整合更多配套软件，普通用户也能用

* 内核版本号：由Linus等人制定和维护，全球统一
* 发行版本号：由各个发行公司或者组织自行制定，不同公司的发行版本号之间无可比性
* 内核版本号格式：x.y.zz-www，x为主版本号，y为次版本号，zz为次次版本号，www发行号

* 稳定版本：偶数 — 2.6.12
* 最新内核：奇数 — 3.4.1

### Linux各个目录的意义
以目录的方式来组织和管理系统中的所有文件
以根目录“/”为起点，所有其他的目录都由根目录派生而来  

![此处输入图片的描述][1]

![此处输入图片的描述][2]

![此处输入图片的描述][3]

**/bin**
这一目录中存放了供所有用户使用的完成基本维护任务的命令。其中bin是binary的缩写，表示二进制文件，通常为可执行文件。一些常用的系统命令，如cp、ls等保存在该目录中。

**/boot**
这里存放的是启动Linux时使用的一些核心文件。如操作系统内核、引导程序Grub等。

**/dev**
在此目录中包含所有的系统设备文件。从此目录可以访问各种系统设备。如CD-ROM，磁盘驱动器，调制解调器和内存等。在该目录中还包含有各种实用功能，如用于创建设备文件的MAKEDEV。

**/etc**
该目录中包含系统和应用软件的配置文件。

**/etc/passwd**
该目录中包含了系统中的用户描述信息，每行记录一个用户的信息。

**/home**
存储普通用户的个人文件。每个用户的主目录均在/home下以自己的用户名命名。

**/lib**
这个目录里存放着系统最基本的共享链接库和内核模块。共享链接库在功能上类似于Windows里的.dll文件。

**/lib64**
64位系统有这个文件夹，64位程序的库。

**/lost+found**
这并不是Linux目录结构的组成部分，而是ext3文件系统用于保存丢失文件的地方。不恰当的关机操作和磁盘错误均会导致文件丢失，这意味着这些被标注为“在使用”，但却并未列于磁盘上的数据结构上。正常情况下，引导进程会运行fsck程序，该程序能发现这些文件。除了“/”分区上的这个目录外，在每个分区上均有一个lost+found目录。

**/media**
可移动设备的挂载点，当前的操作系统通常会把U盘等设备自动挂载到该文件夹下。

**/mnt**
临时用于挂载文件系统的地方。一般情况下这个目录是空的，而在我们将要挂载分区时在这个目录下建立目录，再将我们将要访问的设备挂载在这个目录上，这样我们就可访问文件了。（注意在GNOME中，只有挂载到/media的文件夹才会显示在“计算机”中，挂载到/mnt不会做为特殊设备显示，详见自动挂载分区）

**/opt**
多数第三方软件默认安装到此位置，如Adobe Reader、google-earth等。并不是每个系统都会创建这个目录。

**/proc**
它是存在于内存中的虚拟文件系统。里面保存了内核和进程的状态信息。多为文本文件，可以直接查看。如/proc/cpuinfo保存了有关CPU的信息。

**/root**
这是根用户的主目录。与保留给个人用户的/home下的目录很相似，该目录中还包含仅与根用户有关的条目。

**/sbin**
供超级用户使用的可执行文件，里面多是系统管理命令，如fsck, reboot, shutdown, ifconfig等。

**/tmp**
该目录用以保存临时文件。该目录具有Sticky特殊权限，所有用户都可以在这个目录中创建、编辑文件。但只有文件拥有者才能删除文件。为了加快临时文件的访问速度，有的实现把/tmp放在内存中。

**/usr**
静态的用户级应用程序等，见下。

* /usr/bin
多数日常应用程序存放的位置。如果/usr被放在单独的分区中，Linux的单用户模式不能访问/usr/bin，所以对系统至关重要的程序不应放在此文件夹中。

* /usr/include
存放C/C++头文件的目录

* /usr/lib
系统的库文件

* /usr/local
新装的系统中这个文件夹是空的，可以用于存放个人安装的软件。安装了本地软件的/usr/local里的目录结构与/usr相似

* /usr/sbin
在单用户模式中不用的系统管理程序，如apache2等。

* /usr/share
与架构无关的数据。多数软件安装在此。

* /usr/X11R6
该目录用于保存运行X-Window所需的所有文件。该目录中还包含用于运行GUI要的配置文件和二进制文件。

* /usr/src
源代码

**/var**
动态的程序数据等，见下文。

* /var/cache
应用程序的缓存文件

* /var/lib
应用程序的信息、数据。如数据库的数据等都存放在此文件夹。

* /var/local
/usr/local中程序的信息、数据

* /var/lock
锁文件

* /var/log
日志文件

* /var/opt

* /opt中程序的信息、数据

* /var/run
正在执行着的程序的信息，如PID文件应存放于此

* /var/spool
存放程序的假脱机数据（即spool data）

* /var/tmp
临时文件

## 系统运行的各种级别及切换方法（*）
### Linux系统的运行级别（Run Level）
**0**：关机级别。
**1**：单用户运行级别，运行rc.sysinit和rc1.d目录下的脚本。
**2**：多用户，但系统不会启动NFS，字符模式，在有些linux系统中，级别2为默认模式，具有网络功能，如ubuntu.debian。
**3**：多用户，字符模式，系统启动具有网络功能，Red Hat常用运行级别。
**4**：用户自定义级别。 
**5**：图形界面模式，Red Hat常用运行级别。 
**6**：重启级别。

### 更改系统运行级别
* 在字符终端界面上以root用户身份执行命令init n或telinit n，n为级别号。

* 在字符终端界面上执行命令startx启动图形化环境。

* 更改/etc/inittab文件中“id: 5:  initdefault”项目，把数字5改为其他数字，表示Linux默认采用某级别启动。

## 系統关机
### 关机
* shutdown –h now
* halt
* poweroff
* init 0
### 重新启动
* shutdown –r now
* reboot
* init 6

## Shell（*）
### 什么是shell
* Shell是一个作为用户与linux系统间接口的程序，它允许用户向操作系统输入需要执行的命令

### 常用的shell有哪些
* ash：是贝尔实验室开发的shell，bsh是对ash的符号链接。
* bash：是GNU的Bourne Again  shell，是GNU操作系统上默认的shell。sh以及bash2都是对它的符号链接。
* tcsh：是Berkeley UNIX C shell。csh是对它的符号链接。
* ksh：Korn Shell的语法与Bourne Shell相同，同时具备了C * Shell的易用特点。

### Shell处于linux系统的哪个模块
* Shell 作为应用程序，部署在 Linux 内核周围。

### 如何指定用户使用某个shell(/etc/passwd)
* chsh –s /bin/bash 将 bash 设置为默认 shell
* 或者 vi /etc/passwd 设置对应账号的默认 shell

## Vi文本编辑器
### VI的几种工作模式：命令模式、插入模式、末行模式，如何切换（*）
![此处输入图片的描述][4]


### 如何保存、退出、设置行号
* 保存文件 :w
* 保存并退出 :wq 或者:x 或者 ZZ(**没有冒号**)
* 退出文件 :q
* 强制退出 :q!
* 设置行号 :set nu
* 取消显示行号 :set nonu
* 取消光标所在行:nu

## Linux文件（*）


### 文件属性，如何修改，如何计算
**文件属性**
![此处输入图片的描述][5]


**如何修改**
> chmod命令
作用：改变指定目录或文件的权限。
语法：chmod [选项] mode文件名或目录
该命令语法中mode代表权限设定字串，格式如下：
[ugoa...][+-=][rwxX]...][,...]  

**如何计算**
> rwx 可读可写可执行。 r=4,w=2,x=1, - =0;
每一组的权限值各个位相加，例如 *-rwxrwx---* 计算得770

### 有多少种文件类型，如何辨别

* 正规文件( regular file )
第一个属性为 [ - ]
纯文字文件(ascii)
二进制文件(binary)　

* 目录 (directory)：
第一个属性为 [ d ]

* 链接文件 (link)：
第一个属性为 [ l ]

* 设备文件 (device)：
区块 (block) 设备文件，第一个属性为 [ b ]；
字符 (character) 设备文件，第一个属性为 [ c ]。

* 管道文件
第一个属性为 [ p ]

* Socket文件
第一个属性为 [ s ]

### 硬链接、软链接
**命令格式**
```shell
ln [选项] <source> <dest>
```
硬链接（hard link）：给文件一个副本（别名），同时建立两者之间的连接关系，修改其中一个，与其连接的文件同时被修改，如果删除其中一个，其余的文件不受影响。磁盘上只有一份数据。硬链接是存在同一个文件系统中。

软链接（symbolic link）：软链接的方式则是产生一个特殊的文件，该文件的内容是指向另一个文件的位置。它只是一个快捷方式，删除了源文件，这个连接文件就没用了。软链接可以跨越不同的文件系统。

* 软链接
```shell
ln -s sourceFileName desFileName
```

* 硬链接
```shell
ln sourceFileName desFileName
```

## 系统管理
### 挂载的概念
如果要使用 USB 存储设备、光盘或软盘等存储设备，必须将这些设备中的“小”目录树像嫁接一样挂载（ mount）到 Linux 系统的“大”目录树中。

### 文件系统类型
ext、 ext2、 ext3、 ext4、 HPFS、 iso9660、 VFAT、 MINIX、 MSDOS、 NTFS

### 虚拟文件系统结构（*）
**VFS**
Linux系统可以支持多种文件系统，为此，必须使用一种统一的接口，这就是虚拟文件系统(VFS)。通过VFS将不同文件系统的实现细节隐藏起来，因而从外部看上去，所有的文件系统都是一样的。
![此处输入图片的描述][6]

### 磁盘在linux下的标识
**前面两个字母表示分区所在设备的类型**

* hd: IDE硬盘
* sd: SCSI硬盘（U盘）

**第三个字母表示分区在哪个设备上**

* hda: 第一块IDE硬盘
* sda: 第一块SCSI硬盘
* sdb: 第二块SCSI硬盘

**数字表示分区的次序**

* hda1: 第一块IDE硬盘的第一个分区
* sda1: 第一块SCSI硬盘的第一个分区

每一个硬盘最多可以有4个主分区， 因此*1-4*的作用表示硬盘的主分区。逻辑分区是从数字5开始的，每多一个分区，数字加1即可。

### 如何挂载U盘
```shell
fdisk –l   // 查看挂载的U盘是什么标示
cd /mnt    
mkdir usb  // 在mnt目录下创建挂载点usb目录
mount –o iocharset=cp936 /dev/sdb1 /mnt/usb // 如有中文文件名乱码，执行该命令 -o
```

### 系统初始化过程分析（*）
![此处输入图片的描述][7]


### 进程管理
* **进程、父进程、子进程、程序概念**
> Linux 系统上所有运行的东西都可以称之为一个进程。每个用户任务、每个系统管理任务，都可以称之为进程。进程是一个程序的运行。
程序只是一个静态的指令集合，不占系统的运行资源；而进程是一个随时都可能发生变化的、动态的、使用系统运行资源的程序。一个程序可以启动多个进程。
父进程和子进程是管理和被管理的关系。当父进程终止时，子进程也随之终止。但子进程终止，父进程并不一定终止。

* **At的使用**
> 在shell提示符下输入”at 时间”，然后按回车键。这时在下一行shell会等待用户继续输入要执行的命令。每一行输入一个命令，所有命令都输入完毕后按Ctrl+d键结束。
将各个命令写入shell脚本中，然后使用下面格式设置在指定时间执行shell脚本中的命令：
at 时间 –f 脚本文件

* **Cron的使用（*）**
> cron 命令在系统启动时由一个 shell 脚本自动启动，进入后台。
cron 启动后搜索/var/spool/cron 目录，寻找以/etc/passwd 文件中的用户名命名的
crontab 文件，被找到的这种文件将载入内存。
如果没有 crontab 文件，就转入“休眠”状态，释放系统资源。
cron 每分钟“醒”过来一次，查看当前是否有需要运行的命令。
如果发现某个用户设置了 crontab 文件，它将以该用户的身份去运行文件中指定的命
令。命令执行结束后，任何输出都将作为邮件发送给 crontab 的所有者，或者/etc/crontab
文件中 MAILTO 环境变量中指定的用户。

crontab 文件固定的格式：
> f1 f2 f3 f4 f5 program

f1:表示分钟，00-59
f2:表示小时，00-24
f3:表示一个月的第几天，01-31
f4:表示月份，01-12
f5:表示一周的第几天，0-6
program: 表示要执行的程序
```
f1为*：表示每分钟要执行program
f1为a-b：表示从a-b分钟要执行program
f1为*/n：表示每n分钟要执行program
f1为a,b,c,...：表示第a,b,c,..要执行program
```


* **Grep命令的使用,-v,-w,^d,^-**
>　grep（global search regular expression(RE) and print out the line，全面搜索正则表达式并把行打印出来）是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。

        -v 反转查找。
        -w 只显示全字符合的列。
        ^：匹配正则表达式的开始行
        -d<进行动作> 当指定要查找的是目录而非文件时，必须使用这项参数，否则grep命令将回报信息并停止动作


* **Awk命令的使用,awk ‘{print $2}’**

## 网络管理
### 如何配置机器的ip，如何查看（ifconfig用法）
* 使用终端命令ifconfig方便地查看系统目前所有活跃的网络接口的详细信息
例如：
```shell
ifconfig     // 查看所有接口信息（包括接口对应IP）
ifconfig eth0  // 查看指定接口信息（包括接口对应IP）
```

* 设置机器的接口IP
```shell
ifconfig <设备名> <IP地址> netmask <掩码>
// 例如
ifconfig eth0 192.168.15.11 netmask 255.255.255.0
fconfig eth1 21.156.299.13 netmask 255.255.255.0
ifconfig eth0:0 192.168.17.21 netmask 255.255.255.0
```
### 网络相关配置文件有哪些，有何作用
![此处输入图片的描述][8]


### ftp服务配置、启动、停止
> [root@localhost log]#setsebool -P ftpd_disable_trans on
[root@localhost log]#setsebool -P ftp_home_dir on
service vsftpd [start|stop|restart] 或者 /etc/rc.d/init.d/vsftpd [start|stop|restart]

### telnet 服务配置、启动、停止
完全由xinet控制

### Xinetd 服务配置、启动、停止
**配置文件**
> /etc/xinetd.conf：控制xinetd程序运行的配置文件。其中，提供了所有服务的缺省配置。
/etc/xinetd.d/*：该目录包括所有由xinetd程序启动的服务的配置文件，每个服务都有自己单独的配置文件，配置文件名与服务名一致。

**重启服务**
```shell
service xinetd restart
```

### 守护进程概念原理（*）
> 在 Client/Server 模式下。服务器监听（ Listen）在一个特定的端口上等待客户连接。连接成功后服务器和客户端通过端口进行数据通信。守护进程的工作就是打开一个端口，并且等待（ Listen）进入连接。如果客户端产生一个连接请求，守护进程就创建（ Fork）一个子服务器响应这个连接，而主服务器继续监听其他的服务请求。

### 网络服务独立模式与xinetd模式区别（*）
![此处输入图片的描述][9]
![此处输入图片的描述][10]


> xinetd 能够同时监听多个指定的端口，在接受用户请求时，他能够根据用户请求的端口不同，启动不同的网络服务进程来处理这些用户请求。

## Shell编程（*）
### 变量：自定义的变量、环境变量
* **自定义的变量**
变量＝值 （注意：等号两侧不能有空格）
* **环境变量**
![此处输入图片的描述][11]


### 程序结构：条件判断、循环结构、函数
* **条件**
>常见的条件：
变量属性；
文件属性；
命令执行结果；
多种条件的逻辑组合；

    > 判断结果的一般定义：
    真：0
    假：1

    > 格式：
    test condition
    [ condition ]

* **循环结构**
> for循环
while循环与until循环

* **函数**
定义：
![此处输入图片的描述][12]
引用：
![此处输入图片的描述][13]


### 如何执行
> /bin/sh filename
或给该文件属性添加执行权限 chmod +x filename，然后直接执行 ./ filename

### 文件属性的判断、字符串属性和整数关系的判断
* **文件**
![此处输入图片的描述][14]
* **字符串**
![此处输入图片的描述][15]
* **整数**
![此处输入图片的描述][16]


### 函数使用、shift
![此处输入图片的描述][17]


## XWindow
### Xwindow概念
X Window 系统是一种以位图方式显示的软件窗口系统。

### X Window 的组成
X Window 系统由三个基本元素组成： X Server、 X Client 和二者通信的通道。

### 原理（ *）
* C/S模式应用程序
> X Server 为S，X Client 为C
X Client只是单纯地执行程序、计算，它只能使用XServer提供的服务进行输入输出
X Server是一个管理显示的进程，必须运行在一个有图形显示能力的主机上

* X Protocol（ X 协议）
> X Protocol是X Client和X Server进行通信的一套协定
支持的网络协议有TCP/IP、DECnet等
可以认为X Protocol就是X Client和X Server交互的一种语言
X Protocol只是一种协议，并不是一个软件，该协议需要具体的软件来实现

    > X Client调用xlib，利用相应的通信功能向X Server发出请求
    X Server完成任务之后，同样调用xlib把结果显示指点的设备上去


### 有哪些XWindow
GNOME 和 KDE

## 基于Linux的C编程
### Gcc概念：各个选项的意义（*）
* **名称：**
> GNU project C and C++ Compiler
GNU Compiler Collection

* **使用格式**
```bash
$ gcc  [ 选项 ]   <文件名>
```

* **各个选项的意义**
![此处输入图片的描述][18]
![此处输入图片的描述][19]
![此处输入图片的描述][20]


### 各个阶段的编译及生成的文件，各种后缀名（ *）
* **编译过程**
> 预处理（Preprocessing）：将源文件的宏进行展开
编译（Compilation）：将源程序编译成汇编程序
汇编（Assembly）：将汇编文件编译成机器码
链接（Linking ）：将目标文件和外部符号进行链接，生成可执行文件

* **生成的文件后缀**
>（1）.c为后缀的文件，是C语言源代码文件。
（2）.h为后缀的文件，是头文件。
（3）.C，.cc、.cpp、.cp或.cxx为后缀的文件，是C++源代码文件。
（4）.h为后缀的文件，是程序所包含的头文件。
（5）.i为后缀的文件，是已经预处理过的C源代码文件。
（6）.ii为后缀的文件，是已经预处理过的C++源代码文件。
（7）.m为后缀的文件，是Objective-C源代码文件。
（8）.o为后缀的文件，是编译后的目标文件。
（9）.s为后缀的文件，是汇编语言源代码文件。
（10）.S为后缀的文件，是经过预编译的汇编语言源代码文件。

### Makefile（*）
![此处输入图片的描述][21]
> 1	hello:hello.o say_hello.o
2          gcc hello.o say_hello.o -o hello
3	say_hello.o:say_hello.c say_hello.h
4          gcc -c say_hello.c -o say_hello.o
5	hello.o:hello.c say_hello.h
6          gcc -c hello.c -o hello.o



## Linux 系统
### Linux 的系统体系结构（ *）
![此处输入图片的描述][22]

### **Linux的内核组成部分**
![此处输入图片的描述][23]


  [1]: http://7xrul1.com1.z0.glb.clouddn.com/ln1.png
  [2]: http://7xrul1.com1.z0.glb.clouddn.com/ln3.png
  [3]: http://7xrul1.com1.z0.glb.clouddn.com/ln4.png
  [4]: http://7xrul1.com1.z0.glb.clouddn.com/ln2.png
  [5]: http://7xrul1.com1.z0.glb.clouddn.com/ln5.png
  [6]: http://7xrul1.com1.z0.glb.clouddn.com/ln6.png
  [7]: http://7xrul1.com1.z0.glb.clouddn.com/ln7.png
  [8]: http://7xrul1.com1.z0.glb.clouddn.com/ln8.png
  [9]: http://7xrul1.com1.z0.glb.clouddn.com/ln9.png
  [10]: http://7xrul1.com1.z0.glb.clouddn.com/ln10.png
  [11]: http://7xrul1.com1.z0.glb.clouddn.com/ln11.png
  [12]: http://7xrul1.com1.z0.glb.clouddn.com/ln12.png
  [13]: http://7xrul1.com1.z0.glb.clouddn.com/ln13.png
  [14]: http://7xrul1.com1.z0.glb.clouddn.com/ln14.png
  [15]: http://7xrul1.com1.z0.glb.clouddn.com/ln15.png
  [16]: http://7xrul1.com1.z0.glb.clouddn.com/ln16.png
  [17]: http://7xrul1.com1.z0.glb.clouddn.com/ln17.png
  [18]: http://7xrul1.com1.z0.glb.clouddn.com/ln18.png
  [19]: http://7xrul1.com1.z0.glb.clouddn.com/ln19.png
  [20]: http://7xrul1.com1.z0.glb.clouddn.com/ln20.png
  [21]: http://7xrul1.com1.z0.glb.clouddn.com/ln21.png
  [22]: http://7xrul1.com1.z0.glb.clouddn.com/ln21.jpg
  [23]: http://7xrul1.com1.z0.glb.clouddn.com/ln22.jpg


# 原稿链接
## [Mrzzchao作业部落](https://www.zybuluo.com/Mrzzchao/note/389390)
