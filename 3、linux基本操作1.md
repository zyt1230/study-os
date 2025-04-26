# 一、用户
---

> + ubuntu可能刚开始在xshell上使用ssh连接vmvare不得行。
>     - 可以先更新apt：sudo apt upgrade
>     - 再安装ssh客户端：
>

（**root用户下是用来安装各种东西等等的，尽量不使用这个账户**）

```bash
useradd 用户名 //创建用户 
su 用户  //切换用户
useradd -d 路径 用户名 //创建用户在该路径下
passwd 用户名 //为用户增添密码 
userdel 用户名 //删除用户 
userdel -r 用户名 //删除用户包括它的目录 
id 用户名 //查询用户信息 [uid是用户id，gid是用户组id，groups是用户组名] 
who //查看创建的用户们，里面有root用户
who am i //查看当前用户信息
sudo usermod -aG sudo 用户名//用户改为sudor
```

+ **如果是Ubuntu环境，最好是在root下进行创建用户和删除用户操作。或者在命令前加sudo**
+ **sudo 可以让普通用户获得超级管理员权限，root权限**。
+ Ubuntu的用户创建后，再创建一个  **目录/home/你要创建的用户名**
+ 例如

```bash
useradd 用户名
su - 用户 //在Ubuntu里最好加 - 符号。否则有些命令可能无法用简写模式。比如：本来想用 ll 【在shell模式下使用 su - a也是错，要切换到bash模式】，使用后会报错，但是ls -l 又可以使用。
chsh -s /bin/bash 用户名 //在Ubuntu里切换用户名后是shell模式，如果不喜欢，可以切换到bash模式。这个命令是在root下进行。
exit //退出当前目录，一定用这个，否则就没有退出，你使用userdel 用户名 //删除这个用户，就会出现进程后台使用着这个用户。
当然可以用kill -9 进程号//进程号，它会提示，这个是强制删除这个进程。可能需要重新连接。
passwd 用户名//Ubuntu每创建一个用户就要在root下设置密码，否则root会随机分配给这个新用户一个密码，但是你又不知道密码

推荐使用【adduser 用户名】【deluser 用户名】
这个创建，会有bash。
```

+ 这里是使用Ubuntu操作  
![](https://i-blog.csdnimg.cn/direct/e131aa0b89f04e749e4280a0c7bea8a2.png)  
![](https://i-blog.csdnimg.cn/direct/8ad23850dd374607a1cb75bc303113fd.png)  
![](https://i-blog.csdnimg.cn/direct/6284ac76433046f8bc48f1b13d1f5d38.png)  
![](https://i-blog.csdnimg.cn/direct/6ef9f192aee14909ba155cb83926fee1.png)  
![](https://i-blog.csdnimg.cn/direct/aead7d7a67d84570978a409a395ed158.png)  
![](https://i-blog.csdnimg.cn/direct/7b9fda9ce5ce4f55a97262600520b93a.png)

# 二、用户组
---

+ 用户组类似于角色，系统可以对有共性(权限)的多个用户进行统一管理。
+ **Ubuntu必须在root下创建**。

```bash
groupadd 组名 //创建用户组 
groupdel 组名 //删除用户组 
useradd -g 用户 用户组名 //创建用户和用户组
groups //查看当前用户所属的组
groups 用户名 //查看特定用户的用户组
groupmod -n <新组名> <旧组名>//修改组名
cat /etc/passwd //查看所有的用户组和用户信息
```

+ cat /etc/passwd
    - 每行的含义：用户名：口令：用户标识号：组标识号：注释性描述：主目录：登录shell

# 三、linux关机
+ shutdown
    - shutdown -h now 表示立即关机
    - shutdown -h 1:表示一分钟后关机
    - shutdown -r now :立即重启
+ halt 就是直接使用，效果等同于关机
+ sync 把内存的数据同步到磁盘
+ reboot 就是重启系统
+ 注意细节： 1. 不管是重启系统还是关闭系统，首先要运行sync命令，把内存中的数据写入到磁盘中。 2. 目前的shutdown、reboot、halt命令在关机前**都进行了sync**。
+ 这些基本上用不到。理解就行了。

# 四、linux运行级别
---

7种：  
0：关机  
1：单用户（找回用户丢失的密码，可以使用单用户模式）  
2：多用户状态但没有网络服务（一般很少用）  
3：多用户状态但有网络服务（没有图形化界面，但是有网络，这种用的最多）  
4：系统未使用，保留给用户（很少用）  
5：图形界面  
6：系统重启

```bash
init 数字
```

+ 这个就是图形化界面  
![](https://i-blog.csdnimg.cn/direct/3fd1ccbd3fed48e2a8610110d74fb3d9.png)
+ 一般用`init 3`的人多

# ![](https://i-blog.csdnimg.cn/direct/6fde6e74553942d6bda3aa44de21d417.png) 五、帮助指令
---

#### 1、man
```bash
man 命令/函数  
//就能得到相关信息。这个用的最多
```

当我输入一个 `man useradd`后就出现了这个界面，可以按上下左右键移动，按`q`退出  
![](https://i-blog.csdnimg.cn/direct/bd2ae54c57094e5494bc3dfc372b996c.png)

#### 2、ls
```bash
ls -a //可以显示隐藏文件，linux的隐藏文件都以 . 开头  
ls -l //可以显示文件及其属性(字节的大小和创建的时间) 
ls -la //可以组合使用以上2种方法 
help 命令 //帮助查看命令信息,就记住man的使用，也行
```

# ![](https://i-blog.csdnimg.cn/direct/c50a16503f0c45a5af115bebf4bb33cc.png) 六、路径
---

```bash

pwd //绝对路径 
cd ~  //返回当前用户home目录下 
cd /  //返回root根目录 
cd ..  //返回上一级目录 
cd -   //返回上一条命令的目录
```

+ 绝对路径：从**根目录开始**的完整路径，唯一且明确
    - 例如

```bash
/usr/local/bin/python3
```

+ 相对路径：从**当前工作目录开始**的路径，灵活且简洁。
    - 例如

```bash
src/main.py
```

![](https://i-blog.csdnimg.cn/direct/786053d2987b43af8fd22cd05a4d7c89.png)

# 七、创建和删除目录文件
---

#### 1、创建目录
```bash

mkdir 目录名 //只能创建一个目录 
mkdir -p 第一个目录名/第二个目录名/.../第n个目录名  //可以创建多级目录
```

#### 2、删除空目录
```bash
rmdir 目录名 //删除目录 
rmdir -r  目录名 //删除多级目录【会询问是否删除】 
rmdir -rf 目录名 //可以取消询问的删除方法
```

#### 3、创建文件
```bash
touch 文件名 //创建文件
```

![](https://i-blog.csdnimg.cn/direct/739bb0de2191479cb4de13a630101a60.png)

#### 4、拷贝文件
```bash

cp 文件 路径 //把文件拷贝到该路径下 
cp -r 文件 路径 //递归拷贝整个文件及其它所在的目录到该路径下
```

#### 5、删除文件和有内容的目录
```bash
rm：移除文件或者目录  
-r：递归删除整个文件夹  
-f：强制删除不提示
```

#### 6、移动文件
```bash
mv：移动文件（剪切）或重命名
```

## 八、查看操作
---

#### 1、查看文件内容
```bash
cat 文件名 //可以显示内容
cat -n 文件名   //可以显示内容和行数
```

+ more:more指令是一个基于vi编辑器的文本过滤器，他以全屏的方式显示文本文件的内容，more 指令内置了若干快捷键。

```bash
more 文件名
```

![](https://i-blog.csdnimg.cn/direct/6f3e7a56626945f092da367ff2d616d7.png)

+ less :less指令用于来分屏查看文件内容，他的功能与more类似，但是比more更加强大，支持各种显示终 端。less指令在显示文件内容时，并不是一次将整个文件加载后才显示的，而是根据要加载的内容，对 显示大型文件具有高效率

```bash
less 文件名 //这个我用的多一些，more和less看你们喜欢哪个用哪个
```

![](https://i-blog.csdnimg.cn/direct/fefd65c1b3be4e45b6d95f4858d1f352.png)

+ echo：将内容输入到控制台
    - 输出环境变量 echo $PATH 【很少遇到，理解即可】
    - 输出主机名称 echo $HOSTNAME 【理解即可】
    - 输出内存到bash上 【**这个要知道**】  
![](https://i-blog.csdnimg.cn/direct/06c50ee92b3f4a30ba02449eb3d9f7d1.png)

![](https://i-blog.csdnimg.cn/direct/0597c2badaa945e7801a7036e6f767b8.png)

+ head
    - head -n 文件：显示文件的前5行内容
    - head 文件：默认显示前10行内容  
![](https://i-blog.csdnimg.cn/direct/8709e55715d9438d836e949616809612.png)
+ tail
    - tail 文件： 查看文件最后10行的内容
    - tail -n 5 文件： 查看文件最后5行的内容，5可以是任意数）
    - tail -f 文件： 实时监控文件发生的变化
+ ‘>’ 和 '>>【**用的比较多**】
    - '>'重定向（覆盖）
    - '>>'追加（填到最后）
+ 软连接（快捷键）
    - ln -s[源文件和目录][软连接名称] //创建软连接
        * 使用方法很简单，这个源文件或目录就是取了个别名，你调用别名就行了。例如：看内容，cat file
    - rm -f 名称 //删除软连接  
![](https://i-blog.csdnimg.cn/direct/f467465cb72b49fe971e5adf18bd82ba.png)
+ history:查看用户已经执行过的指令
    - history 10：查看当前用户的最近10条指令  
![](https://i-blog.csdnimg.cn/direct/400480ef7c474763aefd240e7bcf1acd.png)

#### 2、时间
+ 查看时间

```bash
date +%Y //哪一年 
date +%m //哪一月 
date +%d //哪一天 
date "+%Y-%m-%d %H:%M:%S" //年-月-日 时:分:秒
```

![](https://i-blog.csdnimg.cn/direct/3782cc2410ff4357b13e382388016349.png)

+ 设置（修改）linux时间【一般不用设置这个】

```bash
date -s "年-月-日 时:分:秒"
```

+ 日历

```bash
cal 年  //显示这一年的日历
```

![](https://i-blog.csdnimg.cn/direct/8b9f4d68a72c436c9595185f49fbfde6.png)

#### 3、搜索查找
+ find 搜索范围 / 目录（就是路径) 选项  
![](https://i-blog.csdnimg.cn/direct/e3f5c0613cc44616b6972618cf480272.png)

实例一：按照文件名称查询文件  
**使用相对路径**：  
![](https://i-blog.csdnimg.cn/direct/8064c5651a184b99a17e5af7563e00ed.png)

**使用绝对路径**  
![](https://i-blog.csdnimg.cn/direct/f864b19bc26f4853bff9880ace69c57b.png)

实例二：在/linuxgit目录下，查询root用户【Ubuntu使用了sudo创建目录和文件，就是root类型，centos是zyt用户】已经创建好的文件们 。

![](https://i-blog.csdnimg.cn/direct/23476aa488d14ffba13944f0703136f3.png)  
实例三：查找整个linux系统下，大于2k的文件 （**+n大于,-n小于，n等于**）**单位还有k，M，G，c** （c是字节，其他是kb，mb，gb）  
![](https://i-blog.csdnimg.cn/direct/97c180a6a6b744f48ab0d14e041ded04.png)

#### 4、locate快速定位
使用这个速度比较快。推荐使用。

```bash
locate 文件名

```

![](https://i-blog.csdnimg.cn/direct/983ba154b3b3476ba2bb85a6628d94cd.png)

#### 5、查看指令的目录位置
which 指令 【**注意不能用简写去查找，在根目录 / 下找**】  
![](https://i-blog.csdnimg.cn/direct/00ec4ed90f2c4a44bb2b968bdbeebef9.png)

#### 6、grep（重点）
```bash
grep 选项 查找内容 源文件  
```

grep过滤查找，管道符，”|“,表示前一个指令的处理结果输出传递给后面的指令处理。一般我们将 | 和 grep一起结合起来使用。

## ![](https://i-blog.csdnimg.cn/direct/922bf4af265e46f68492f75529aeca2f.png)  
![](https://i-blog.csdnimg.cn/direct/b677e1f8376c45c39e1b3cb9d392b50a.png)  
九、压缩和解压
---

#### 1、gzip/gunzip指令 gzip用于压缩文件 gunzip用于解压缩文件
```bash
gzip 文件名 目录  //把文件压缩到固定目录下
gunzip 文件名.gz 目录  
gzip 压缩文件（将文件压缩为\*.gz的文件，原文件被压缩后不存在。）
gunzip 文件.gz (解压缩文件命令)
```

#### 2、zip/unzip指令
```bash
zip \[选项\] XXX.zip 将要压缩的内容 （压缩文件和目录的命令）
-r :递归压缩，即压缩目录
-d :指定解压后文件存放方目录
unzip -d 目录 文件名 //把文件压缩到指出的目录下
```

#### 3、tar
tar指令是打包指令，最后打包后的文件是.tar.gz的文件。

```bash
tar \[选项\] XXX.tar.gz 打包的内容 （功能描述：打包目录，压缩后的文件格式.tar,gz）
```

## ![](https://i-blog.csdnimg.cn/direct/739ef9c01e2d44c3beafac55a228d74f.png)  
十、linux组管理和权限管理
---

#### 1、修改用户组和用户
在linux中每个用户都必须属于一个组，不能独立于组外，在linux中每个文件有所有者，所在组，其他 组的概念。下面我们用一幅图来解释用户、组、其他组的概念。

```bash
chown kelly c.c # 将当前文件c.c的所属用户变kelly 
chgrp 新用户组 c.c #将当前文件c.c的所属用户组变另一个 
usermod -g 新用户组 用户名 #把用户改成另一个组`
```

#### 2、linux权限
总共10位，我们使用0-9来描述。 第0-9位说明

+ 第0位确定文件类型(d,-,l,c,b)
    - l是软连接，相当于windows的快捷方式
    - d是目录，相当于windows的文件夹
    - c是字符设别，鼠标，键盘(/dev 目录里面查看)
    - b是块设备，比如说硬盘(/dev 目录里面查看)
    - 第1-3位确定所有者（该文件的所有者）拥有该文件的权限 --User
+ 第4-6位确定所属组，（同用户组的）又有该文件的权限 --Group
+ 第7-9位确定其他用户拥有改文件的权限 --Other
+ rwx作用到文件
    - r 代表可读 read 可以读取，
    - 查看 w 代表可写 write 可以修改，但是不代表可以删除改文件，删除一个文件的前提条件是对该 文件所在的目录有写权限，才能删除文件
    - x 代表可执行 execute 可被执行
+ rwx作用到目录
    - r 代表可读 可以读取 ls查看目录的内容
    - w 代表可写 对目录内进行创建+删除+重命名该目录
    - x 代表可执行 可以进入该目录

> 修改权限  
第一种方法： chmod u=rwx,g=rx,o=x #设置成了用户rwx权限，用户组是rx权限，其他人是x权限  
第二种方法：  
r=4,w=2,x=1 rwx=4+2+1=7 chmod u=rwx,g=rx,o=x 文件目录名 等价于 chmod 751 文件目录名
>

本文转自 [https://blog.csdn.net/2401_82911768/article/details/146446387?spm=1001.2014.3001.5501](https://blog.csdn.net/2401_82911768/article/details/146446387?spm=1001.2014.3001.5501)，如有侵权，请联系删除。

