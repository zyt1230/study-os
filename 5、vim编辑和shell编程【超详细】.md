## 一、vim
### 1、了解
Vim (Vi IMproved) 是一款功能强大的**文本编辑器**。

+ 正常模式：vim 文件，刚打开的样子
+ vim模式：输入文本的地方
+ 命令模式：输入 :wq等等的位置，可以对文本进行一些操作，比如：保存文本  
![](https://i-blog.csdnimg.cn/direct/638d8b1d450e4f4fae18979322a062d8.png)

### 2、使用方法
+ 创建

```plain
vim 文件名 //如果没有这个文件，它会自己在当前目录生成
```

+ 创建好后，它会自己进入编辑里面
    - 你会看到这样的界面  
![](https://i-blog.csdnimg.cn/direct/d31723c783a1404db36a938e5abfbda7.png)
+ 进行编辑

```plain
先按一下 i 或 a
然后输入文字
输入完后，就按 ESC键 。
```

![](https://i-blog.csdnimg.cn/direct/0872c78a78c94c1d8084629840de5e6e.png)  
![](https://i-blog.csdnimg.cn/direct/7b6bf801e29541de959d364e255bd1a7.png)

+ 保存或退出文件

```plain
:wq  保存并退出
:q!  强制退出
:q   不保存退出
注意：一定是在英语编辑模式下输入 : 符号
```

![](https://i-blog.csdnimg.cn/direct/73be0ecbf38d4e898ff48e73ee8939e2.png)

### 3、特殊操作
```plain
1. 拷贝当前行 (yy )，并粘贴（p）
2. 拷贝当前向下的2行(2yy ) 并粘贴（p）
3. 删除当前行(dd)或 删除当前向下的2行 (2dd)
4. 撤销上一操作 u
5. ctrl+r:反撤销
注意 ：是在**正常模式下进行**
```

![](https://i-blog.csdnimg.cn/direct/99b35162a7004264836214ca77968b4b.png)

+ yyp  
![](https://i-blog.csdnimg.cn/direct/c2fdab9f71eb4b47add13c163b43cf04.png)
+ dd  
![](https://i-blog.csdnimg.cn/direct/3b67a62f7b504d929fa2251fed7a9208.png)

```plain
设置行号 :set nu
取消行号 set nonu

注意：在命令模式下
```

![](https://i-blog.csdnimg.cn/direct/d0534414e0784da4853789736e071412.png)  
![](https://i-blog.csdnimg.cn/direct/c2dba85c76b1467abcda16045b6fa90e.png)

```plain
定位和修改操作

切换到正常模式
nG 表示跳到第n行
gg 将光标直接跳到首行位置
0 表示光标移动到 当前行的 行首位置
$ 表示光标移动到 当前行的 行尾位置

修改在命令模式下进行
 :s/string1/string2/g 表示将 当前行 所有的string1更换成string2
 :%s/string1/string2/g 表示将文本里的所有string1变string2
 :m,ns/string1/string2/g 表示[m,n]行闭区间内的所有string1更换成string2
 :/string 查找string
```

## 二、什么是shell编程？
### 1、了解
Shell编程是指利用**Shell脚本（Shell Script）****来****自动化执行一系列命令或任务**。`Shell是一种命令行解释器`，充当用**户与操作系统内核**（如Linux/Unix）之间**的桥梁**，而Shell脚本则是包含多个Shell命令的文本文件，可以**批量运行这些命令**。  
![](https://i-blog.csdnimg.cn/direct/d77e5730ba8f454394cebbb340291120.png)

---

1. **脚本文件**
    - 扩展名通常为`.sh`（如`test.sh`），文件开头需指定解释器（如`#!/bin/bash`）。
    - 通过`chmod +x 脚本名.sh`赋予可执行权限后，可直接运行（`./脚本名.sh`）。
2. **语法特点**
    - **变量**：存储数据（如`name="张三"`，使用时加`$`符号，如`echo $name`）。
    - **条件判断**：`if-else`、`case`语句（例如判断文件是否存在）。
    - **循环**：`for`、`while`循环（如遍历文件列表）。
    - **函数**：封装重复代码块。
    - **参数传递**：通过`$1`、`$2`获取脚本参数。
3. **示例脚本**

```bash
#!/bin/bash
echo "你好，世界！"  # 打印文本
today=$(date)       # 获取当前日期
echo "今天是：$today"
```



## 二、shell的编写执行方式
### 1、第一个shell程序
+ 创建 .sh 后缀的文件 ，并且在文件里写 #!/bin/bash 。运行最好用 ./文件名.sh 【**无法直接运行，添加可执行权限给用户**】。

```bash
注释用
# 
这个是单行

:<<!
这个是多行
!
注意：被注释的内容 不要和 注释在同一行
```

```plain
mkdir shellCode //创建目录shellCode
cd shellCode //切换到shellCode
vim hello.sh //编辑 hello.sh
//进入hello.sh文件里面进行编写
#!/bin/bash  //必须输入这个，才能运行
echo "hello world" //echo输出。
//然后运行文件
sh hello.sh  //第一种运行方式

//第二种方式
chmod u+x //给u可执行的权限
./hello.sh

```

![](https://i-blog.csdnimg.cn/direct/d947a660205b46bf9b101c4e273b4f3d.png)

![](https://i-blog.csdnimg.cn/direct/44c0bd2597f445179b9bb6a705a6e1c8.png)

### 2、shell变量
Linux 中 **Shell 的变量分为系统变量和用户自定义变量**。**

#### 2.1、系统变量
+ 系统变量**：`$HOME、$PWD、$SHELL、$USER 等等`，比如：echo $HOME 等等。我们可以使用set命令显示当前 Shell 中所有变量。  
![](https://i-blog.csdnimg.cn/direct/fa52efd83e1d401187397d5d87c7b617.png)

#### 2.2、用户变量
+ 用户变量
    - 我们在开发的过程中，可以**自定义变量**。
    - 定义过程：
        * ①定义变量：变量=值【注意等号两侧无空格】
        * ②撤销变量：unset 变量
        * ③声明静态变量（不能修改，类似于常量）：readonly 变量 【注意该变量不能unset】
+ 自定义的变量要**用 echo输出时 ，要加 $ 符号**。
+ 如下图  
![](https://i-blog.csdnimg.cn/direct/ea7d9c107fa7479db0a7a15716e86fae.png)



```plain
#!/bin/bash
A=100
echo $A 
#或echo A=$A 或echo "A=$A"
echo A=$A 
echo "A=$A"
#然后保存退出vim编辑器
#销毁变量A
unset A
echo "A=$A"
#设置静态变量
readonly B=2
#销毁静态变量
unset B
echo $B
 # 这时候，就会出现问题，它会提醒，静态变量是只能读不能修改的。

```

![](https://i-blog.csdnimg.cn/direct/2bb23af5490342d989e70158477b444c.png)  
![](https://i-blog.csdnimg.cn/direct/5c50f7a9f576452a93fe1918923345f0.png)

![](https://i-blog.csdnimg.cn/direct/7e3e71a822934cbe9cd0f879b9d04029.png)

---

+ 我们也可以把linux的命令结果赋予给变量

```plain
C=`date`
echo $C
```

![](https://i-blog.csdnimg.cn/direct/a042ebe47f244de9bde50fdad29d6f18.png)

---

+ linux命令还有一种声明的方式

```plain
D=$(date)
echo D=$D
```

![](https://i-blog.csdnimg.cn/direct/55bab1fd203943928bb5c2b307fe5d65.png)

#### 2.3、设置环境变量
+ 首先要知道设置的 文件是 `/etc/profile`
+ 基本语法
    - export 变量名=变量值
    - 将shell变量输出为环境变量/全局变量。那样多个脚本都可以使用 .sh 文件。  
![](https://i-blog.csdnimg.cn/direct/53d7bbc0bbee4a528f69917db29b2fc5.png)
+ source 配置文件：让修改后的配置文件立即失效
+ echo $变量名 :查询环境变量的值

#### 2.5、设置位置参数变量
+ 基本语法
    - ![image](https://cdn.nlark.com/yuque/__latex/7cb9a4366d218e94d8b8bac975f9525a.svg)0 代表命令本身，![image](https://cdn.nlark.com/yuque/__latex/860c5f78e3fe04ab5d189654c1c031f0.svg){10}
    - $ ∗ ：代表命令行中所有的参数， * ：代表命令行中所有的参数， ∗：代表命令行中所有的参数，*把所有的参数看成一个整体
    - $@：代表命令行中所有的参数，不过该命令是把每个参数区分对待
    - $#：代表命令行中所有参数的个数

```plain
#!/bin/bash
echo "p0=$0,p1=$1,p2=$2"
echo "$*"
echo "$@"
echo "$#"
```

![](https://i-blog.csdnimg.cn/direct/c4ffaa3fc3164604976b7ef71ba13fa3.png)

#### 2.6、预定义变量
+ 基本语法
    - $$：**当前进程的进程号**。
    - $!：**后台运行的最后一个进程的进程号**。
    - $?：**最后一次执行的命令的返回状态**。如果这个变量的值为 **0**，证明上一个命令**正确执行**；如果这个变量的值为**非 0**（具体是哪个数，由命令自己来决定），则证明**上一个命令执行不正确**。

```plain
#!/bin/bash
echo "当前进程号=$$"
echo "最后一个进程号=$!"
echo "上一个命令的返回状态=$?"
```

### 3、shell中的运算符
+ 3种写法

```plain
1、$((表达式))
2、$[表达式]
3、$(expr m 运算符 n)
注意：expr与运算符之间要有空格。只能有2个操作数，m和n必须是数字 ，数字和运算符之间必须有空格 。
```

#### 3.1、 第一种 $(())
```plain
#!/bin/bash

#输出表达式 3*(4+10)
TOTAL=$((3*(4+10)))
echo $TOTAL

```

![](https://i-blog.csdnimg.cn/direct/a7996cfd1ebb45089994b923f650c64d.png)

#### 3.2、 第二种【比较老了，可能用不了】
```plain
#!/bin/bash
#输出表达式 3*(4+10)
RESULT=$[3*(4+10)]
echo $RESULT
```

#### 3.3、 第三种 expr
```plain
#expr
TEMP=$(expr 10 + 10)
echo "TEMP=$TEMP"

```

![](https://i-blog.csdnimg.cn/direct/34b3bbc7a18145b49688df412b3b73c2.png)

> 注意：linux里 乘号是 \* ,**在expr里要用这个**
>

+ 传入参数

```plain
$(($n运算符$n))
#注意 $0是本身，不用这个
```

![](https://i-blog.csdnimg.cn/direct/5520444d4ac24e5980ade44f9e0a5fe3.png)  
![](https://i-blog.csdnimg.cn/direct/6b8a610111154f8db676f634c1d911a8.png)

### 4、shell的条件判断
#### 4.1、单个if
+ 基本语法

```plain
if [ condition ] 
then
    满足if语句执行的代码
fi 

```

> 注意：**condition前后要有空格**
>

#### 4.2、条件判断
+ 常用判读条件
    - **字符串比较**
        * 字符串相等"$  str1&quot; = “ $ str2”
        * 字符串为空-z “$str”
        * 字符串非空-n “$ str”
        * 字符串不等"$  str1&quot; != “ $ str2”
        * str1 小于 str2 (按字典序)“$  str1” &lt; “ $ str2”
        * str1 大于 str2 (按字典序)“$ str1” &gt; &quot;  $ str2"
    - **两个整数的比较**
        * 小于：-lt
        * 大于：-gt
        * 小于等于：-le
        * 大于等于：-ge
        * 不等于：-nt
        * 等于：-eq
    - **按照文件权限进行判断**
        * 有读的权限：-r
        * 有写的权限：-w
        * 有可执行的权限：-x
    - **按照文件的类型进行判断**
        * 文件存在且是常规文件：-f
        * 文件存在：-e
        * 文件存在且是目录：-d
    - **逻辑运算符**
        * AND：-a 【只有 `[[ condition ]]` 才能使用`&&`】
        * OR：-o 【只有`[[ condition ]]`才能使用 `||`】
        * NOT：!
    - **true和false**
        * true 是对
        * false是错
+ 案例1
    - abc 和 cbd 不相等

```plain
#!/bin/bash
if [ "abc"!="cbd" ]
then
        echo "两个字符串不相等"
fi
```

+ 案例2
    - 中国人大于18 岁是中国成年人

```plain
if [ $age -ge 18 -a "$country" = "CN" ]; then
    echo "中国成年人"
fi

# 使用 [[ ]] 的更清晰写法 , 这里有&&
if [[ $age -ge 18 && "$country" == "CN" ]]; then
    echo "中国成年人"
fi
```

+ 案例3
    - 查看 a.txt 文件存在 【`注意输入的是绝对路径`】

```plain
#!/bin/bash
if [ -f /home/a/shellCode/a.txt ]
then
        echo "a.txt存在"
fi


```

+ 案例4
    - a.txt 的权限是 -r

```plain
#!/bin/bash
if [ -r /home/a/shellCode/a.txt ]
then
        echo "a.txt的权限是write"
fi
```

+ 案例5
    - true的使用

```plain
#!/bin/bash
if [ true ]
then
        echo "true"
fi


```

#### 4.3、多if-else
+ 基本语法

```plain
if [ conditon ]
then 
    代码1
elif [ condition ]
then
   代码2
elif [ conditon ]
then
    代码3
else 
    默认
fi
```

+ 案例

```plain
#!/bin/bash
if [ $1 -lt $3  ]
then
        echo "1<3"

else
        echo "1>3"
fi

```

#### 4.4、case语句
+ 基本语法

```plain
case $变量名 in
    "值1")
    如果变量名的值等于 值1，就执行代码1
    ;;
    "值2"）
    代码2
    ;;
    *)
    如果以上都不满足就执行这个代码
    ;;
esac
```

+ 案例

```plain
#!/bin/bash
# 传参数
case $1 in
        "1")
        echo "一"
        ;;
        "2")
        echo "二"
        ;;
        *)
        echo "三"
        ;;
esac


```

![](https://i-blog.csdnimg.cn/direct/ccb1f38e998c4e108fe52db9b023fc65.png)  
![](https://i-blog.csdnimg.cn/direct/8f7b1f7be2084b48981362bd94ba3628.png)

### 5、循环语句
#### 5.1、for循环[2种方法][无$变量]
+ 基础语法1

```plain
for 变量 in "值1" "值2" "值3"....
do
    代码
done
```

+ 案例

```plain
#!/bin/bash
for i in "$@"
do
        echo "数字是：$i"
done

```

![](https://i-blog.csdnimg.cn/direct/b11301e1f22048bd918c42dfc8960072.png)

+ 基础语法2

```plain
for(( 初始值;循环控制条件;变量变化 ))
do
    代码
done
```

+ 案例

```plain
#!/bin/bash
for(( i=0;i<10;i++ ))
do
        echo "数字是：$i"
done
           
```

![](https://i-blog.csdnimg.cn/direct/5d2881edc79c466a942f6a4d42bc621f.png)

#### 5.2、while循环
+ 基础语法

```plain
while [ condition ]
do
   代码
done
```

+ 案例

```plain

#!/bin/bash
SUM=0
i=0
while [ $i -le $1 ]
do
        SUM=$(($SUM+$i));
        i=$(($i+1));
done
echo "数字之和是：$SUM"
```

![](https://i-blog.csdnimg.cn/direct/80d3288060574af3826b3498017d0969.png)

### 6、read获取输入
+ 基础语法

```plain
read 选项 参数
-p  指定读取值时的提示符
-t   指定读取值时等待的时间（秒），如果没有在指定的时间内输入，就不再等待了(放弃输入)
```

+ 案例1：使用-p

```plain
#!/bin/bash
read -p "请输入一个数字：" NUM1
echo "用户输入的值是$NUM1"
                          
```

+ 案例2：使用-t

```plain
#!/bin/bash
read -t 10 -p "请输入一个数字：" NUM1
echo "用户输入的值是$NUM1"
# 10秒内不输入 ，它就自己跳到下一个函数了                      
```

### 7、函数
#### 7.1、系统函数[遇到这种就网上查，这里只举2个例子]
+ 基础语法

```plain
basename  文件的完整路径    作用：获取文件名
dirname   文件的完整路径     作用：获取完整路径最前面部分
```

+ 案例1：使用basename

```plain
a@zyt-virtual-machine:~/shellCode$ pwd
/home/a/shellCode
a@zyt-virtual-machine:~/shellCode$ basename /home/a/shellCode/hello.sh
hello.sh
```

![](https://i-blog.csdnimg.cn/direct/cf33937cf7e049e0ba85c58046882ef8.png)

+ 案例2：使用dirname

```plain
a@zyt-virtual-machine:~/shellCode$ dirname /home/a/shellCode
/home/a

```

![](https://i-blog.csdnimg.cn/direct/6c3e317aa92c4f44ab968fe0452c8c86.png)

#### 7.2、自定义函数
+ 基础语法

```plain
function function_name {
    # 函数体
    commands
}
function_name [$参数1...$参数2] 调用这个函数
```

+ 案例：函数参数传递

```plain
greet() {
    echo "Hello, $1!"
}

greet "Alice"  # 输出: Hello, Alice!
greet "Bob"    # 输出: Hello, Bob!
```

+ 案例：返回值处理
    - 返回状态码（0-255）：

```plain
is_even() {
    if (( $1 % 2 == 0 )); then
        return 0  # 成功/真
    else
        return 1  # 失败/假
    fi
}

is_even 4
echo $?  # 输出返回状态码
```

+ 案例：返回数据（通过echo）

```plain
add() {
    local sum=$(( $1 + $2 ))
    echo $sum
}

result=$(add 3 5)  # 捕获输出
echo "3 + 5 = $result"
```

+ 案例：局部变量（推荐）

```plain
myfunc() {
    local var="局部变量"
    echo "函数内: $var"
}

myfunc
echo "函数外: $var"  # 输出为空
```

+ 案例：全局变量

```plain
global_var=""

modify_global() {
    global_var="修改后的值"
}

modify_global
echo $global_var  # 输出: 修改后的值
```

+ 案例：2数之和

```plain
#!/bin/bash
function getSum(){
        SUM=$(($n1+$n2))
        echo "两个数字之和是：$SUM"
}
read -p "请输入2个数字" n1 n2
getSum $n1 $n2

```

![](https://i-blog.csdnimg.cn/direct/433ad842fa9b490db8d55d454fd6cea0.png)

+ 案例：函数引用

```plain
say_hello() { echo "Hello!"; }
say_goodbye() { echo "Goodbye!"; }

# 通过变量选择函数
action="say_hello"
$action  # 输出: Hello!

action="say_goodbye"
$action  # 输出: Goodbye!
```

+ 案例：递归函数

```plain
factorial() {
    local n=$1
    if (( n <= 1 )); then
        echo 1
    else
        echo $(( n * $(factorial $((n-1))) ))
    fi
}

factorial 5  # 输出: 120
```

### 8、数组
#### 8.1、 初始化
```plain
# 方式1：空格分隔
colors=("red" "green" "blue")
arr=("$@")
# 方式2：逐个元素赋值
fruits[0]="apple"
fruits[1]="banana"
fruits[2]="orange"
```

#### 8.2、访问单个和全部
+ 单个

```plain
echo ${colors[0]}    # 输出第一个元素（索引从0开始）
echo ${colors[-1]}   # 输出最后一个元素
```

+ 全部

```plain
echo ${colors[@]}    # 展开为独立单词（推荐）
echo ${colors[*]}    # 所有元素作为单个单词（可能有问题）
```

本文转自 [https://blog.csdn.net/2401_82911768/article/details/146518671?sharetype=blogdetail&sharerId=146518671&sharerefer=PC&sharesource=2401_82911768&spm=1011.2480.3001.8118](https://blog.csdn.net/2401_82911768/article/details/146518671?sharetype=blogdetail&amp;sharerId=146518671&amp;sharerefer=PC&amp;sharesource=2401_82911768&amp;spm=1011.2480.3001.8118)，如有侵权，请联系删除。

