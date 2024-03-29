[TOC]

## 基础命令

### ss

ss -tanlp t:tcp下进程，a:所有sockets，n:显示端口号，l:监听方式，p:进程

### ls

ls -alh -d h:以human_readable的方式显示文件大小，d只显示dir

ls -alh -r r:反转查询结果

ls -alh -R R：以递归的方式

ls -alh -1  1:数字1表示每一行只显示一个文件

ls -al |wc -1 参看当前文件夹下文件及目录的数量

-rwxrwxrwx

第一个参数：-等价于f表示regular文件，普通文件

d文件，蓝色或绿色

c字符设备，深黄色

b块设备，浅黄色

l 软连接，蓝绿色

s socket文件，粉色

### stat

touch 文件名 三个时间都改变

stat redis.conf(文件名)

atime: 访问文件的时间

mtime:修改文件的时间

ctime:元数据改变的时间，比如修改了文件名字

### cd

cd - 回到上一次的操作路径

### basename dirname

basename  (esc.)   当前目录的最后一部分

dirname 除了最后一部分之前的路径部分

### alias

alias  ll  查看命令别名

### which whereis whatis

which alias查看命令在哪个目录下

whereis alias查看命令在哪个目录下,  还能显示手册位置

whatis alias查看命令的类型及具体介绍

### type

type ls 查看命令是外部还是内部命令

### echo(回显)

echo:默认后面有一个\n

echo /{a,b}/{c,d}   # /a/c /a/d /b/c /b/d

echo {a,b}\*{c,d}   #  a\*d b\*c\* b\*d

echo{a..z..2}

### cp

cp /etc/redis.conf{,.bak} ./  #复制到根目录

#### cp 文件

cp afile ./    afile在当前文件夹，不能在当前文件夹下相同文件之间进行拷贝

cp afile a/b/bfile  将afile中的内容拷贝到bfile中, bfile文件名字不改变，如果bfile不存在则新建一个bfile,并且将afile中内容拷过去

cp afile a/b/  如果b下面存在与afile同名的文件，会将这个文件内容替换掉

#### cp 目录

cp a b -r 当b文件夹不存在时，会将a目录下的内容拷贝到b目录下, 当b存在时，会将a作为一个整体目录放到b目录下,并且替换b中的内容。

cp a b -rf 当a中的有文件afile并且b中也有afile时，会提示时替代，加上-n则不会替代

### mv

mv afile dfile  不管dfile存在或者不存在，都会将a中的内容移动到dfile, 并且删除afile, 多级目录同样适用

mv a b  不需要写递归的方式，直接移动，如果存在b,则将a目录的内容连带a一起放到b下面，先copy再删除，如果b不存在，则直接将a的名字改为b。

mv afile.txt afile.txt 不能这么操作会提示samefile

mv afile.txt afile  直接改名字

### cat

cat *.txt  将txt文件连到一起

tac *.txt 将txt文件连到一起, 文件顺序不变，文件内容反转连接

cat afile > bfile  bfile存在或者不存在，都会将afile中的内容重定向到bfile中

cat afile >> bfile 追加



### yum

yum -y install tree  默认是yes

### tree

tree / -L 1 查看根目录下面的一层

tree -d 只显示目录

### rm

rm -r  a 递归的移除目录

### mkdir

mkdir -pv   如果没有父目录则新键一个父目录，并且显示详情

### tail

tail -f redis.conf  随着文件内容的增加输出后10行数据（-f = -follow），一般日志文件使用

tail -n100 redis.conf 输出文件后100行数据  

 ### ln

ln -s 目录或文件1  目录或文件2    -s一定要写这样才能看清楚从谁到谁的链接

建立连接时2一定要不存在，软连接建立完成时，使用stat查看状态时，stat -L, 如果原文件改变了，软连接则会跟进，如果不加-L，则原文件变了软连接状态不会跟进。

###  pwd

查看当前路径

### export 

export k1=v1 新建一个环境变量的同时，列出所有的环境变量

列出当前shell中的环境变量, 包括新建的环境变量(export k1=v1),  如果当前新开一个bash或者sh, 则子bash或者sh中也包含k1=v1的环境变量，对于其他的没有定义的，但是被某些程序已经定义好的环境变量，也可以被子进程继承(父进程中也含有这些变量)，但是父进程或者重新登陆一个新窗口，则看不到这个临时的环境变量

普通定义的变量：

k2=v2

参看刚才定义的环境变量和普通变量

set |grep ^k

取消刚才定义的变量或者环境变量

unset k1

unset k2

### sed

Stream Editor 行编辑器，一次处理一行内容，处理时会把当前处理的行存储在临时缓冲区，这个缓冲区也称模式空间（pattern space）。sed可以同时处理多个文件,但是vim 一般只处理一个文件



sed 参数1 参数2 参数3

参数1: [OPTION]... 

参数2: {script-only-if-no-other-script} 参数2必须给

参数3: [input-file]...



sed -n '2p' abc 取消默认打印的功能，并将abc文件的第二行打印

sed -n '2p'   后面不加文件，则回车后可以敲入文档，文档的第二行会打印两次，即sed支持标准输入



sed '' abc  默认含有一个p,打印一次

sed 'p' abc  在默认的基础上又加一个p，打印两次

sed -n '' abc 默认一次打印，但是又取消一次打印，所以不打印

sed -n 'p' abc 默认一次打印，又加了一次打印，一共打印两次，取消一次打印，所以最后打印一次



## 基础知识

### 家目录与根目录

root用户下面的家目录~

home下面的家目录~

root和home都在系统的根目录下/

### 查看帮助的几种方法

help 命令

命令 --help

命令 -h

man 命令

### 路径搜索过程

linux系统：hash-builtin-path   不会找当前路径，只会从path 中查找，找不到就找不到，如果想要查找当前路径需要在前面加一个点。

window系统：先搜素当前路径在搜素path路径，查看目录内容实用dir命令(隐藏与不隐藏都能查到)

### 通配符(wildcard)

ls -d s*  以s开头的目录，后面可以是任意个包括0个字符

ls -d s??  以s开头的目录，后面需要有2个字符

ls -d s?*  以s开头的目录，后面需要有2个以上字符

ls -d s* [0-9]  以s开头的目录，以数字结尾，中间可以有任意个字符

### 添加用户并设置密码

useadd jw

cat 123456 |grep passwd jw —stdin

echo python | passwd python —stdin 直接保存密码了

### 切换用户

su -l root

su -l python # 切换到跟目录

### 安装python编译依赖环境

```python
yum -y install gcc make patch gdbm-devel openssl-devel sqlite-devel zlib-devel bzip2-devel
```

### 安装git

```python
yum install git -y
```

### 登陆python用户后安装pyenv

```python
curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
```

### pip通用配置

$ mkdir ~/.pip

在~/.pip/pip.conf配置文件中填写：

```python
[global]
index-url = https://mirrors.aliyun.com/pypi/simple/

[install]
trusted-host = mirrors.aliyun.com
```

### 创建virtualenv虚拟环境

真实目录放在~/.pyenv/versions下面，以后只要使用这个虚拟环境，

包就会安装到对应的目录中而不是3.6.9。

```python
# 默认虚拟环境存放路径在
#/home/python/.pyenv/versions/3.6.9/envs/virtual1/lib/py# thon3.6/site-packages (18.1)
pyenv virtualenv 3.6.9 virtual1
```

### 在虚拟环境virtual1中安装需要的包

```python
# 进入到对应目录
cd projects/web1

# 激活虚拟环境,web文件夹下面可以没有virtual1，
# 文件夹
pyenv local virtual1

# pip安装软件
pip install ipython
pip install jupyter

# 切换到别的路径可以自动退出虚拟环境，只有进入
# 到当前目录，才会开启当前的虚拟环境，不需要额外的命令
```

### 在虚拟环境virtual2中配置与virtual1相同的环境

```python
# 在虚拟环境virtual1中
pip freeze > requirements

mkdir -p ~/projects/web2
cd ~/projects/web2
# 建立虚拟环境
pyenv virtualenv 3.6.9 virtual2
pyenv local virtual2

mv ../web1/requirments ./
pip install -r requirements

```

### vim使用

在命令模式下的粘贴和复制

3yy : 在命令行模式下，从鼠标所在的当前位置，复制3行包括鼠标

所在的一行(只能是3行，其他数字不起作用)。这种方式的复制只能在当前shell 中复制

通过右键的复制，既可以在当前shell中粘贴，也可以在mac上粘贴



在Mac与虚拟机之间互传文件





p ：小p, 从当前鼠标所在一行的下一行开始，向后粘贴

P ：大P，重当前鼠标所在一行的上一行开始，向前粘贴



光标移动

在命令行模式下：gg光标跳到开头那一行，G光标跳到末尾那一行

: set nu 在命令行模式下设置行号  : set nonu在命令行模式下取消行号



已经打开了文件，并且在命令行模式下定位光标

: 20 将光标定位到20行

20G  将光标定位到20行

2和enter  光标向下移动2格，如果当前行为第1行，则移动到第3行



打开文件之前定位光标，一般用在已经知道错误信息在第几行，然后在打开文件瞬间定位到这一行

vim +20  ~/.bashrc  

u 取消命令行模式下的操作

### 传文件

先安装lrzsz

yum install lrzsz

rz -be  从mac传到Linux，以二进制的方式，传完就断开

sz -be  linux本地文件名，传到mac一个默认的目录下

### finalshell

登陆时的坑：

不能以root身份登陆，只能以普通用户身份登陆，

可以登录后再切换到root用户

### 查看环境变量的方法

export

printenv

env

只查看环境变量等号右边的部分

env |cut -d= -f2  通过等号切割，只取等号右边的部分

cut:一般用在对的整整齐齐的时候，具体方法可以看手册

env |cut -d= -f2 |sort

cat abc| sort| uniq  先排序再去重复，uniq默认只能删除相邻的重复元素

### 全局环境变量

有关的几个文件夹

/etc/profile文件 /etc/bashrc文件 /etc/profile.d 文件夹

第一个文件中，存放的是全局环境变量的基础定义

第二个文件中，存放的是全局环境变量相关的函数和别名，也定义了会自动加载prefile.d文件夹下面所有的.sh文件的函数

### 局部环境变量