 

一、linux调度
---------

### 1、[crontab](https://so.csdn.net/so/search?q=crontab&spm=1001.2101.3001.7020) \[选项\]

#### 1.1、了解

定时任务调度:指每隔指定的时间，执行特定的命令或程序。  
基本语法：crontab \[选项\]  
常用选项：

*   e： 编辑定时任务
*   l：查询定时任务
*   r：删除当前用户的所有定时任务 例如：

```bash
crontab -e //然后输入调度内容在vim编译器里 
*/1 * * * * ls -l /etc/ > /tmp/etc.txt
```

#### 1.2、crontab的vim文件格式

```bash
* * * * * 要执行的命令
│ │ │ │ │
│ │ │ │ └── 星期几 (0-7, 0和7均代表周日)
│ │ │ └──── 月份 (1-12)
│ │ └────── 日 (1-31)
│ └──────── 小时 (0-23)
└────────── 分钟 (0-59)
```

> 注意：星期是0和7都为星期天。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/16f77c8be82b4977becb9a84db2aabbb.png)

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/8d853f199f1c40bea350bdce8d042ff6.png)

### 2、at \[选项\] \[时间\]

1.  at命令是一次性定时执行任务计划，at的守护线程atd以后台的模式运行，**检查作业队列来运行**。
2.  默认情况下，**atd守护线程每60秒检查作业队列**，有作业时会检查作业运行时间，如果时间与当前 时间匹配，则运行此作业。
3.  **at命令是一次性定制的计划任务**，执行完一个任务后就不再执行此任务了。
4.  在使用at命令的时候，**一定要保证atd进程的启动**，可以用相关指令来查看 `ps -ef | grep atd` 。

*   at \[选项\] \[时间\]

```bash
at [时间]  进入交互模式
at -l  查看任务id
at -r [任务id]  删除该任务
at -c [任务id]  查看任务id内容
at -v [任务id]  查看任务id的时间
```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/7ba69bc2811a4bfeb65e2162301fcf1f.png)

*   **时间格式**：  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/bf03b998f9d64b529f12edbbf63555a0.png)
    
*   例子
    

```bash
at now + 5 minutes
# 进入交互式输入（输入命令后按 Ctrl+D）
echo "Hello from at job" > ~/at_test.txt
<EOT>  # 按 Ctrl+D 结束
at -l #查看任务ID号
```

二、磁盘分区
------

### 1、基础知识点

> **linux 会把一切都抽象成文件**。  
> 把设备等等分成一个子目录或文件等等，但是都由root管理，构成树结构。  
> ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/afbe72e7fe4948b48ebe78a33c987670.png)
> 
> *   swap：交换分区
> *   boot：启动分区
> *   home：用户主目录
> *   挂载就是把他们形成映射关系（简单理解：可以对应起来）。
> *   挂载点就是对应的目录

查看分区信息：`lsblk` 在linux里面，硬盘有2种类型：

*   **IDE**硬盘 hdx~
    *   hd：标识硬盘类型， IDE类型
    *   x：不同硬盘的分区（a基本盘，b基本从属盘，c辅助盘，d辅助从属盘）
    *   ~ 磁盘分区 1 2 3 4 5
*   **SCSI**硬盘 sdx~
    *   sd：表示是SCSI硬盘
    *   x：代表是第几块硬盘（a：第一块 b：第二块 c：第3块硬盘 d：第4块硬盘）
    *   ~ 磁盘分区  
        ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c8beaf6bf09b4a1ba79a9c2f752c7fe2.png)

NAME ：**驱动器标识**  
FSTYPE ：文件系统类型  
LABLE ：文件系统 LABLE  
UUID ：**分区唯一标识符，格式化磁盘后，会给分区分配一个32位的唯一的字符串**  
MOUNTPOINT ：挂载点

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/548721057ed649a2822a84b7fdfb45af.png)

### 2、查看磁盘列表与分区

#### 2.1、查看列表、挂载和分区的普通方法

*   **ubuntu会有sudo** 。

```cpp

# 查看硬盘及分区详细信息（含型号、容量等）
sudo fdisk -l

# 或使用现代替代工具
sudo parted -l

#lsblk查看磁盘类型和挂载情况
lsblk
# lsblk -f 查看磁盘设备挂载情况
lsblk -f
```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/bfefbc4d5ee94a3da0722875dc56f3c4.png)  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/8e01727f4d1e488ca0a143569dff1b72.png)

### 3、新增硬盘

*   vmvare里先启动你的centos或Ubuntu `启动`，然后可以点击`虚拟机`,后再点击`设置` ， 选择`硬件` 添加`硬盘` ，选择`磁盘类型` ，点击`创建新虚拟机磁盘`,设置大小，点击 `将虚拟机磁盘拆分成多个文件` 。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/2e7a59f351544949a01ba77e78d09a69.png)

*   **打开虚拟机，会有一个设置**。  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/78fdb9341fa24b8196bc1171b32bd772.png)  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c6860aeb84bd431e9b37abfe42224798.png)  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/4b55adedfb24442d955a6564674506a5.png)  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/dce9c3f2ce594d1ab0497357db800e8d.png)  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a51af72c5a484997a33e77e727da79f3.png)

### 4、给新增的硬盘分区

#### 4.1、fdisk

fdisk 磁盘目录  
例如创建了sdb，他在dev目录里

```bash
sudo fdisk /dev/sdb   # 操作指定磁盘

```

*   交互命令
*   m： 显示命令列表
*   n： 新建分区（选择主/扩展分区）
*   p： 查看当前分区表
*   d： 删除分区
*   w： 保存并退出

```bash
[root@kongchao03 ~]# fdisk /dev/sdb
欢迎使用 fdisk (util-linux 2.23.2)。
 
更改将停留在内存中，直到您决定将更改写入磁盘。
使用写入命令前请三思。
 
Device does not contain a recognized partition table
使用磁盘标识符 0xdf03b737 创建新的 DOS 磁盘标签。
 
命令(输入 m 获取帮助)：m            
命令操作
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition
   g   create a new empty GPT partition table
   G   create an IRIX (SGI) partition table
   l   list known partition types
   m   print this menu
   n   add a new partition
   o   create a new empty DOS partition table
   p   print the partition table
   q   quit without saving changes
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit
   x   extra functionality (experts only)
命令(输入 m 获取帮助)：n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
分区号 (1-4，默认 1)：1
起始 扇区 (2048-2097151，默认为 2048)：
将使用默认值 2048
Last 扇区, +扇区 or +size{K,M,G} (2048-2097151，默认为 2097151)：
将使用默认值 2097151
分区 1 已设置为 Linux 类型，大小设为 1023 MiB
命令(输入 m 获取帮助)：w
The partition table has been altered!
Calling ioctl() to re-read partition table.
正在同步磁盘。

```

### 5、格式化磁盘分区：为分区创建文件系统，准备存储数据。mkfs -t

```bash
mkfs -t ext4 /dev/sdb1 # 格式化
lsblk -f#查看分区详细信息
```

*   **其中ext4是分区类型**

### 6、挂载分区：将分区连接到操作系统的目录树，使其内容可以被访问。

#### 6.1、mount方法【短暂挂载】

*   挂载语法：mount 设备名称 挂载目录 （挂载目录是任意的）
*   取消挂载：unmont 设备名或挂载点
    *   比如 unmont /dev/sdb1

```bash
cd /  #切换到根目录
mkdir newdir # 创建一个目录
mount /dev/sdb1 /newdisk/  #把sdb1与新目录进行挂载 
lsblk -f  #在MOUNTPOINT（挂载点）看是否成功
```

#### 6.2、永久挂载

*   永久挂载就是可以自动挂载。
*   vim打开 `/etc/fstab`
    *   写入`/dev/sdb1 /newdir exit4 defaults` 就行。`/dev/sdb1`也可以换成`UUID`。
*   退出来后进行 `mount -a` 即可

### 7、磁盘情况查询

```bash
df -h #查看整个磁盘的占用情况 
df -h [目录] #查询指定目录的磁盘占用情况
```

### 8、磁盘操作实用指令

*   统计opt文件夹下的文件个数

`ls -l /opt | grep "^-" |wc -l`

*   统计opt文件夹下的目录的个数

`ls -l /opt | grep "^d" | wc -l # "^d" 以文件目录开头 wc -l 统 计个数`

*   统计/opt文件下的**文件**的个数，包括**子文件夹**下的

`ls -lR /opt | grep "^-" | wc -l # R 代表递归`

*   统计/opt文件夹下的**目录**的个数，包括子文件夹下的

`ls -lR /opt | grep "^d" | wc -l`

*   以树状结构显示目录结构（如果没有tree，则使用 centos用yum install tree 安装，Ubuntu用apt代替install，并在root用户下安装）

`yum install tree #安装tree tree 目录`

三、网络
----

### 1、linux网络配置的指令

*   ip addr 在linux查看ip地址\[**ip和addr之间有空格**\]
*   ifconﬁg 在linux查看ip地址
*   ping 是否ping通指定的ip地址
*   ipconﬁg 在**windows**操作系统里面查看网络的ip地址

### 2、linux网络环境配置（固定ip的方式）

首先查看 ip是否是变化的。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/17ae02bf6c5b44e29b85e11f1dd7f864.png)  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/980191a861e94ab2af2af0fc8032ebe4.png)  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/0cacd9ef31c3475388ed12a75a40da01.png)

那么进行固定。

*   第一步 编辑我们linux的网卡文件 这个网卡文件在/etc/sysconﬁg/network-scripts/ifcfg-ens33 打开这个文件，进行编辑
*   编辑网卡文件
*   sudo vi /etc/sysconfig/network-scripts/ifcfg-ens33 打开 `编辑`\->`虚拟网络编译器`\->`更改设置`\->`VMnet8`\->`DHCP设置`\->`查看ip地址的范围`\->在ifcfg-ens33 添加IPADDR=“这里写的是ip地址范围内的随便一个”->`添加子网掩码、网关到ifcfg-ens33`(网关在vmnet8的nat设置里)->`最后加DNS1、DNS2`

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/4598886ed2654196b1216accb814ca3e.png)  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/fa8aae690b2c4ba0a908cac02187a0e3.png)

```bash
IPADDR=
NETMARSK=255.255.255.0
GETWAY=
DNS1=
DNS2=

```

### 3、设置主机名和host映射

```bash
查看主机名称方法
①hostname
②cat /etc/hostname
修改主机名
hostname new-hostname


```

也可以修改/etc/hostname指定主机名名称。注意，修改完成之后，需要重启[linux系统](https://so.csdn.net/so/search?q=linux%E7%B3%BB%E7%BB%9F&spm=1001.2101.3001.7020)才能生效。

在 Linux 中，`/etc/hosts` 文件用于将主机名映射到 IP 地址。这对于本地网络中的主机名解析非常有用。  
思考：我们可以通过ping linux的ip地址能ping通linux。那么我们可不可以通过ping linux的主机名 来ping通linux呢，答案是**不可以的**。  
`下面图片是windows的cmd里面操作，按win+r键，再输入cmd就打开了` 找到 `找到 C:\Windows\System32\drivers\etc：`下面的hosts文件，进行相关的编辑：  
输入一个ip和一个主机名。例如：

`192.168.10.130 xq100 # ip地址是linux的ip地址`

如何在linux里面通过本机的主机名来ping通主机呢？我们需要编辑/etc/hosts文件：

`192.168.10.1 DESKTOP-EKI0P48 # ip是vmnet8的ip地址 后面的是windows的主机名称`

四、linux服务管理
-----------

service(本质)就是进程，但是是运行在后台的，通常都会监听某个端口，等待其他程序的请求，比如说 （mysql3306，sshd222，redis6379)，因为我们又称为**守护进程**，在Linux中是重要的知识点。

### 1、service管理指令

```bash
service 服务名 [start|stop,reload,status]
```

*   **在CentOs7.0后，很多服务不再使用Service，而是systemctl**

```cpp
systemctl [start|stop|restart|reload|status|enable|disable] 服务名
```

*   service 指令管理的服务在`/etc/init.d`查看  
    例如：我们可以简单使用一下，比如查看network服务的状态：
    
*   要知道更多系统服务，可以使用setup命令 输入后选择 `系统服务`
    

选择系统服务，回车，我们可以看到系统服务的详细信息：

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/220810801112467eba82dad3813fa9e4.png)

注意：

1.  \[\*\] 代表这些系统服务会随着开机自启动而启动
2.  如果我们想去掉星号或者加上星号，上下按键切换到对应的服务`按空格键`即可。
3.  使用Tab键选择OK或Cancel.

### 2、systemctl服务管理指令

systemctl 指令管理的服务在`/usr/lib/systemd/system`中查看。

*   服务启动/停止/重启/重载/查看状态： systemctl \[start | stop | restart | status\] 服务名
*   查看所有服务的自启动状态

*   防火墙例子

```bash
[root@xq100 system]# systemctl list-unit-files | grep firewall #得到服务名 firewalld.service enabled    
[root@xq100 system]# systemctl status firewalld.service # 查看防火墙状态  
[root@xq100 system]# systemctl stop firewalld.service # 停止防火墙状态  
[root@xq100 system]# systemctl restart firewalld.service # 重启防火墙
```

*   服务的状态如下：
    *   masked 此服务禁止自启动
    *   static 该服务无法自启动，只能作为其他文件的依赖
    *   enabled 已配置为自启动
    *   disabled 未配置为自启动
*   查看某一服务是否自启动

```bash
[root@xq100 system]# systemctl is-enabled firewalld.service # 知道完整服务名 enabled
```

*   设置服务自启动 (服务运行级别 3、5)

```bash
[root@xq100 system]# systemctl enable firewalld.service
```

*   设置服务禁用自启动 (服务运行级别 3、5)

```bash
[root@xq100 system]# systemctl disable firewalld.service
```

五、日志
----

### 1、了解

*   日志可以理解成：记录了每天发生的事情。
*   一般在`var/log`下  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/f4d9cf0273d94c2aa40f30a9fac49c2c.png)

### 2、日志服务类型、级别

*   第一个\* :日志类型  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/868f984a39da49f7b420608ef01f6afd.png)
*   第2个\* ：日志级别  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/be03db3c549147c29ae524dae9158a30.png)

> **注意**：从上到下，日志级别从低到高，记录的信息也越来越少。

由日志服务rsyslogd记录的日志文件，日志文件的格式包含以下4列：

1.  事件产生的时间
2.  产生事件的服务器(主机名)
3.  产生事件的服务名和程序名
4.  事件的具体信息

### 3、自定义日志

*   rsyslogd服务是处理日志的核心服务，为了防止日志服务出现问题，请确保下面两项：
*   第1个：
    *   rsyslogd服务处在启动状态

```cpp
sudo ps -aux | grep "rsyslog" | grep -v "grep"

```

*   第2个：
    *   rsyslogd服务可以自启动（处在enabled状态）

```bash
systemctl is-enabled rsyslog

```

*   **然后修改自定义日志文件的步骤**
*   第1步：
    *   修改配置日志文件 `/etc/rsyslog.conf`

```bash
 sudo vim /etc/rsyslog.conf
```

*   第2步：
    *   增加一个新日志文件 xq.log

```bash
# add xq.log文件
*.*  /var/log/xq.log  #*就是什么类型都有，*什么级别都可以
```

*   第3步：
    *   重新启动reboot

```bash
reboot
```

*   第4步：
    *   查看日志

```bash
cat /var/log/xq.log

```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/56e2ac0acae84a42912c2619828934cc.png)

### 4、自定义日志轮替原则

*   是指把一些不需要的旧文件，按一定规则进行删除。
*   需要`/etc/logrotate.conf`这个配置文件进行管理。
*   打开 `logrotate.conf` ，我们可以看见 ,一些默认的参数。

```bash
vim /etc/logrotate.conf
```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/1a5487b11fa345a19445a90ac1cc859e.png)

> *   weekly：表示每周轮替一次
> *   rotate 4：表示同一个日志文件最多保存四个版本 多了会删除
> *   create：产生轮替之后生成一个新的空白的文件放在其后
> *   dateext：日志轮替文件名字的命名方式
>     *   如果配置文件中有dateext参数：日志会用日期作为日志文件的后缀，例如“message20220801”。
>     *   如果没用dateext：日志需要进行改名，当第一次日志轮替时，当前的“secure”改名为“secure.1”，然后新建“secure”日志用来保存新的日志。第二次日志轮替时，当前的  
>         “secure.1”会自动更名为“secure.2”，“secure”更名为“secure.1”，新建“secure”以保存新的日志。以此类推。
>     *   **include/etc/logrotate.d：可以将自定义的日志轮替规则写到这个文件里去**。

*   例如：  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/57acef7c885640a3bab3997949b8eb5e.png)

```bash
日志文件地址{
	参数
}

```

*   daily：轮替周期 每天
*   weekly：轮替周期 每周
*   monthly：轮替周期 每月
*   rotate \[num\]：保存日志文件的个数
*   compress：轮替时对旧日志进行压缩
*   create mode owner group：建立新日志的同时指定权限 所有者 所属组
*   mail address：日志轮替时输出内容通过邮件发送到指定的邮件地址
*   missingok：如果日志不存在则忽略日志的警告信息
*   notifempty：如果日志为空文件则不进行日志轮替
*   minsize \[size\]：日志轮替的最小值 即超过该大小才会轮替 否则到达轮替周期也不会轮替
*   size \[size\]：日志达到指定大小进行轮替 而不是按照轮替的时间周期
*   dateext：使用日期作为日志轮替文件的后缀
*   sharedscripts：在此关键字之后的脚本只执行一次
*   prerotate/endscripts：在日志轮替之前执行脚本命令
*   postrotate/endscripts：在日志轮替之后执行脚本命令

> 例子：自定义xq.log文件  
> ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c4f67554730b416881417ca8552e8cf4.png)  
> ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c56c6f35c32848f88aebeeda00f34555.png)

### 5、linux中的内存日志

*   在linux中，有一部分日志信息是**没有写到日志文件**里面去的，而是**写在内存中的**。这些日志的特点是日  
    志信息都在**随时发生变化**。比如linux内核的日志信息。**内存日志还有一个特点是linux系统在重新启动的时候，内存日志就会被清空**。
    
*   journalctl查看所有的内存日志
    
*   journalctl -n 3查看最新3条
    
*   journalctl -p err查看报错日志
    
*   journalctl -o verbose日志详细内容
    
*   journalctl --since 15:00 --until 15:10查看区间时间内的日志 可加日期

本文转自 <https://blog.csdn.net/2401_82911768/article/details/147119356?spm=1001.2014.3001.5501>，如有侵权，请联系删除。