# Operation System

# Lecture1 Linux Introduction

## 1.1 What Is an Operation System

![20210419114953](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210626162226.png)

- `API` ：提供给程序员编写软件的接口
- `AUI`：编写好的各种软件
- Operating System ：以有效、公平、有序的方式分配上层所需的资源。屏蔽了一些复杂硬件资源使用的接口，不用关心底层。 

## 1.2 Linux Operation System

<img src="https://i.loli.net/2021/03/02/rXSdOBJsVA8MGRE.png" alt="image-20210302161440320"  />

- hard drivers : 驱动程序，由操作系统打包，驱动硬件
- kernel：操作系统内核，执行文件管理，存储管理，进程管理，进程通信（管道、匿名管道、socket？），CPU调度
- System Call Interface：系统调用接口，规定了申请内存资源的调用方式
- Language libraries：库函数
- 两类 AUI
  - Command User Interface : CUI 
  - Graphical User Interface : GUI  

## 1.3 Free Software & Open source

- GPL(GNU Public License)
  - access source code
  - copy
  - modify
  - redistribute

- Other License
  - [BSD, Apache, LGPL, MIT](http://oss.org.cn/?action-viewnews-itemid-53184)

- Freeware & Shareware

![image-20210302164545780](https://i.loli.net/2021/03/02/nce6NBojTvq34Ca.png)

## 1.4 Variations in Linux

- Linux distribution: Redhat, Slackware, Debian, Mandrake, Suse, Redflag, Gentoo, Bluepoint,Ubuntu,Centos, Knoppix

Linux 发行版本 $\to$ 使用的内核相同，区别在于周围的东西不同（驱动程序、`Xwindow` 图形界面接口、`deb / rbm` 不同格式的安装包）

**[Which Distro Should I Choose?](https://www.linuxtrainingacademy.com/distros/)**

Redhat ( 收费 ) / Ubuntu

## 1.5 Linux System Standardization

- Portable Operation System Interface (POSIX)

- Single UNIX Specification (SUS)

- Linux Standard Base (LSB)

# Lecture 2 LINUX Shells

## 2.1 Putty

- translation 
- `SSH` 登录
- `SSH - Auth` $\to$ 文件登录：公钥文件（远程计算机），私钥文件（登录密码，认可用户身份）

## 2.2 Command Interpreter-shell

- Various Unix Shells: bash （Linux的默认shell）, `csh`, `sh`, `ksh`
- Choose shell
  - Set in the file: ` /etc/passwd`
  - Change default shell：`chsh`
  - Change current shell

- shell 的三个自启动文件   (Bash startup file)
  - `/etc/profile`: system environment 
    - 所有的 `system` 配置文件都保存在 `etc` 目录下以文本格式存放
    - `system` 启动时执行
  - `$HOME/. bash_profile`: execute once when logging on 
    - 带 `.` 表示的是隐藏文件
    - 每个用户登录时
    - `nano .bash_profile`
  - `$HOME/.bashrc`: execute each time fork a shell
    - 在 `bash` 启动时执行
    - 只针对 `bash`
    - `nano .bashrc`

作用：对系统进行配置，如环境变量

## 2.3 Environment variables

环境变量 ：在内存中，保持在操作系统中的变量，当程序需要某些信息时，从约定好的环境变量中读取值

- `CLASSPATH`

 `CLASSPATH = %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin`  指定到哪里去找 `java` 调用的库函数(缺省的库函数)

PS： `%JAVA_HOME%` （宏变量）：`java` 的安装目录

否则 需要通过 `java -cp ... 目录`  查找环境变量 

- `PATH` 

如，输入 `calc` 先在当前目录下找可执行文件，然后再在 `PATH` 环境变量下找可行性文件

### 2.3.1 Check Environment Path

在 Linux 中使用

- `echo $PATH(name)`  
- `env`

**注意：在 Linux 中不会优先在当前目录中找可执行程序，而是在环境变量中**

如果需要在

- 添加路径信息

```
./hello
```

- 把当前目录加到环境变量的后面

```
PATH=$PATH:.
```

其中 `.` 就是添加的目录

- 把当前目录加到环境变量的前面

```
PATH=.:$PATH
```

其中 `.` 就是添加的目录

### 2.3.2 Commands

- View environment variables
  - `echo`：view a single environment variables
  - `env, set`： view all environment variables

- Common environment variables
  - `–$PATH`：command searching path
  - `–$HOME`：user logging on directory
  - `–$PS1`：command prompt
    - `\h` first part of machine
    - `\s` shell name（i.e.` “bash”`） 
    - `\u` user name 
    - `\w` current work directory（i.e. `“/home/s1”`） 
    - `\$`  if not super user (root): `"$"`；if supper user:`"#" `
  - `–$LANG`: language （shell和用户交互的编码方式）

## 2.4 Linux Command

### 2.4.1 Command struct

`–command [[-]option(s)][option argument(s)] [command argument(s)]`

格式：命令 -选项 -选项参数 -命令参数

### 2.4.2 Command key

- Command auto complement : `TAB`
- 快速执行某个命令 `! ` + 命令的前缀
- 执行刚刚执行的命令：`!!`
- Hot key
  - `Ctrl + u` : delete characters to the begin
  - `Ctrl + k` : delete characters to the end    
  - `Ctrl + c` : cancel the command   
  - `Ctrl + a` : move the cursor to the begin
  - `Ctrl + e` : move the cursor to the end

- alias: create pseudonyms (nicknames) for commands
  - Create alias
    - `alias [[name]=string]`
  - Disable alias 
    - `unalias name`
- type 

### 2.4.3 Command execute order

1. alias

2. Build-in command

3. Execute file

### 2.4.4 Shell Metacharacters

shell 元字符

| Metacharacters | purpose                                                      | Example            |
| -------------- | ------------------------------------------------------------ | ------------------ |
| $              | Dereference  shell variable                                  | `  echo  $PATH  `  |
| “              | To  quote multiple  characters but allow substitution 对其中的元字符做特殊解释 | `  echo  “$PWD”  ` |
| ‘              | To  quote multiple  characters  不对其中的元字符做特殊解释   | `echo  ‘$PWD’  `   |
| *              | To  match zero or more characters  任意多个任意字符          | `rm  *.tmp  `      |
| ?              | To  substitute a wild card for exactly one characters   对应一个字符 | ` rm  ?.tmp `      |
| [ ]            | To  insert wild cards  填区间值                              | `rm  [1-3].tmp  `  |
| \|   |To  substitute a command  命令替换|`PATH=$PATH:pwd`|
| ~              | To  name home directory  快速访问到工作目录                  | `ls  ~/  `         |
| \              | To  escape a single character  转义符，转为普通字符，删除空格使用 | `rm  a\ b\ c  `    |

- `pwd` 表示当前所在目录

### 2.4.5 view system information

- `whoami(id)`：user identity
- `hostname`：host name
  - `hostname name` 修改机器名
- `uname`：OS information
  - `uname -a` 操作系统的所有信息
- `free`：Memory
  - `free -h`
- `date`：system date
  - `date +%y%m%d`
  - `date +%Y%m%d`
- view the files in the `/proc`

# Lecture 4 File System

## 4.1 Unix devices

在 Linux 中，设备也看作文件

| Device              | ID in Unix                     |
| ------------------- | ------------------------------ |
| SCSI/SATA Hard Disk | `/dev/sd[a-p]  `               |
| USB Disk            | `/dev/sd[a-p](same as SCSI)  ` |
| CDROM               | `/dev/cdrom`                   |
| Printer             | `/dev/lp[0-2]`                 |
| Mouse               | `/dev/mouse`                   |

e.g. 第一块 SATA 硬盘   `/dev/sda`  第二块 SATA 硬盘  `/dev/sdb` 第一块u盘  `/dev/sdc`

## 4.2 Hard Disk

在 Linux 中，使用目录来进行分区

![image-20210323155946112](https://i.loli.net/2021/03/23/cyQXqlKmMUOeB5g.png)

- `mounted on` 就类似于 Windows 中的盘符，对 Linux 下的文件系统进行分区，优先找映射过的分区

## 4.3 File System Mount

- 在安装 Linux 时，自动创建三个分区
  - `/` 根目录，存放大部分文件
  - `swap` 虚拟内存分区
  - ` /boot`  系统启动文件
- Linux 不关心文件的扩展名，文件能否运行取决于它所拥有的权限

## 4.4 Make the File System Work

Linux 最多生成 4 个分区，分区有两种类型

- 主分区
- 扩展分区：对于一个分区，可以设置一个分区为扩展分区，扩展分区中可以设置逻辑分区

### 4.4.1 Disk Partition（分区）: `parted`

### 4.4.2 Format the partition（格式化）: `mkfs`  

文件系统格式：`ext2，ext3，ext4，xfs，zfs`

现在最常用：`ext4`

``` 
mkfs -t ext4 /dev/sdb1
```

Mount the disk partition （挂载分区到目录上，使得分区可用）

- 使用 `mount` 创建分区

```
mount [-t vfstype]（可不写） [-o options] device dir
```

比如

```
mount /dev/sdb1 /mnt 
```

- 这样操作后 `/mnt` 就是新硬盘的分区，通过访问 `/mnt` 目录访问文件
- 注意：`sdb1` 中的 $1$ 一定要写，表示这个设备的第一个分区
- `mount` 命令可以查看当前的分区
- 在命令行下输入的挂载命令，只在当前有效，重新登录系统挂载信息消失
  - 将挂载文件写入 `/etc/fstab` 文件中，可以自动挂载
  - `/dev/sdb1 /mnt ext4 defaults（选项） 0（） 1（检查文件完整性）`

### 4.4.3 Uninstall Partition  （卸载分区）：`umount`

输入文件分区名或者挂载的目录均可以卸载分区

```
umount /dev/sdb1
```

或者

```
umount /mnt
```

## 4.5 Types of Files

### 4.5.1 Simple/ordinary file

- Linux 中，不关心文件的扩展名，一个文件是否可以执行，由权限决定

![image-20210323163709653](https://i.loli.net/2021/03/23/tzpn3HrQE4iRWxv.png)

### 4.5.2 Directory File 目录文件

- 目录文件记录了所在目录下的文件信息：文件名，索引节点号

![image-20210323163747621](https://i.loli.net/2021/03/23/pKRdTGen1c48C7N.png)

### 4.5.3 Link File 链接文件

保存路径信息，指向另一个文件，类似于快捷方式

### 4.5.4 Special (Device) File 设备文件

- Character Special Files 字符设备文件，以字符为单位传输数据
  - Correspond to character-oriented devices (e.g., Keyboard)
- Block Special Files 以块为单位传输数据
  - Correspond to block-oriented devices (e.g., a disk)

### 4.5.5 Named Pipe (FIFO) 命名管道文件

- 帮助进程通信

- 一个进程往文件中写数据，另一个进程读数据，当一个进程读取过管道文件的数据后，这些在管道的数据被销毁

### 4.5.6 Socket 插口文件

- 帮助网络间的进程通信

## 4.6 Linux directory

使用目录的形式组织文件

Linux 文件系统标准 `directory structure: FHS`

![image-20210323164606193](https://i.loli.net/2021/03/23/KktOAjDGW8m2JE4.png)

- `bin` ：常用命令
- `sbin` ：系统管理命令
- `boot`：保存启动文件
- `dev`：设备目录
- `ect` ：系统相关的配置文件，配置命令和脚本
- `home`：每个用户的工作目录
- `lib`：程序库
- `proc` ：虚拟目录，保存的是系统的运行信息
- `usr` ：类似于系统应用目录 类似于`windows ProgramFile`
- `var`：存放大小容易变化的文件，比如日志文件

## 4.7 Some commands about files

- Check the storage of system
  - `df`  分区使用情况(分区设备名，分区大小，已用，可用，已用%，挂载点)
    - ` df -h dev/sda1`
    - `du` 查看某个文件使用存储空间的情况

- Manipulate directory
  - `pwd`    ：显示当前目录
  - `cd`   ：返回上一级或者转到某一级目录
  - `mkdir`  
  - `rmdir`  
  - `ls`：列出当前目录下的文件
    - `ls -a` 列出隐藏目录下的文件
    - `ls -l` 列出包含当前目录下所有文件的详细信息

**详细信息的含义**

![image-20210330155200389](https://i.loli.net/2021/03/30/a1BIHuVTfxivlXS.png)

PS：`du`命令显示的是给文件分配的存储空间， `ls` 显示的文件的实际大小

- Manipulate files
  - `rm`：删除某个目录
  - `cp`：用于拷贝的命令（文件、目录）    
  - `mv`  ：文件、目录的移动，重命名
    - `mv dira dirc`
    - `mv dira \tmp`
  - `file`   
  - `touch`：创建空文件，修改日期为当前时间，如果文件已经存在，会修改文件的最后访问时间
- Check the file system
  - `fsck`

## 4.8 LVM

分区逻辑卷管理，可以跨硬盘创建虚拟分区，对于存储空间变化很大的分区十分有用

**缺点**

- 效率较低，不建议用于 `system` 分区

# Lecture 5 File Security

## 5.1 Protection based on Access Permission

- 使用 `id` 或者 `group` 查看用户处于哪个组

**Types of users**

- User (owner), group, others
- A user with multiple groups

**Types of Access Permissions**

- Read, write, and execute（文件能否执行取决于权限）

**Access Permissions for Directories**

- Read: list the files 
- Write: create or remove directories and files
- Execute: Directory search

## 5.2 Determining File Access Privileges

- 文件的九个权限位

![image-20210406161553825](https://i.loli.net/2021/04/06/cD2PiA4WzJOhkpE.png)

-  查看文件权限

```
s193157@GOJ:~$ ls -l /tmp/hello
-rwxrwxr-- 1 test stu 8920 Mar 30 08:59 /tmp/hello
```

> 第一个横杠表示是普通文件
>
> 后面表示是文件的权限

## 5.3 File owner information

- Find the user id
  -  `id user`
- Find the user group
  - `group user`
- Change the file owner
  - `chown`
  - `chgrp`

## 5.4 Changing File Access Privileges

- Changing File Access Privileges

```
chmod [options] symbolic-mode file-list
```

- 增加其他人的目录权限

```
chmod o+w dira/a
```

- 取消其他人和同组用户的读写执行权限

```
chmod -R(对目录里面所有子目录的文件递归执行) og-rwx dira/a
```

- 直接指定文件的访问权限

```
chmod -R u=rwx,g=rx,o= dira/a
或者
chmod -R 750 dira/a
chmod -R 7(111)5(101)0(000) dira/a
```



![image-20210406162214169](https://i.loli.net/2021/04/06/NoVfrYXGmWSzTP3.png)

**注意**

- 只读文件也可以被删除

## 5.5 Default file access privileges

通过掩码值控制文件的默认访问权限
$$
get=777-umask (目录)\\
get=666-umask(文件)
$$

- 每一位分别相减

- 重设 `umask +掩码值` （只对当前登陆有效）
  - 将命令放入 `shell` 启动文件中，可以对每次启动生效
- 不可执行的文件无法设置可执行位

## 5.6 Special Access Bits 特殊访问位

- The Set-User-ID (SUID) Bit
  - 如果为包含命令的可执行程序的文件设置了该位，则该文件在执行时将具有文件所有者的特权

```
chmod 4xxx file-list
chmod u+s file-list
```

- The Set-Group-ID (SGID) Bit
  - 在执行的时候，使文件的访问权限采用文件所有者所属组的组标识

```
chmod 2xxx file-list
chmod g+s file-list
```

- 黏着位 The Sticky Bit
  - 针对目录有效
  - 设定后，各个用户在同一目录下创建的文件就不会被他人删除或者修改

```
chmod 1xxx file-list
chmod +t file-list
```





# Lecture 6 File Processing

## 6.1 Viewing text files

### 6.1.1 Viewing complete files

- `cat`  : 显示空行的行号

- `nl`  ：空行被忽略

- `more/less` ：分页方式查看文本文件的所有内容

- `od`: 查看文本文件中的不可见字符（格式分析：默认以8进制显示文件）

  - `-c` 以转义字符

    ```
    s193157@GOJ:~$ od -c  /tmp/hello.cpp
    0000000   #   i   n   c   l   u   d   e       <   i   o   s   t   r   e
    0000020   a   m   >  \n   u   s   i   n   g       n   a   m   e   s   p
    0000040   a   c   e       s   t   d   ;  \n  \n   i   n   t       m   a
    0000060   i   n   (   )       {  \n  \t   c   o   u   t       <   <
    0000100   "   h   e   l   l   o   "       <   <       e   n   d   l   ;
    0000120  \n  \t   r   e   t   u   r   n       0   ;  \n   }  \n
    
    ```

  - `-h` 以十六进制显示

  ```
  s193157@GOJ:~$ od -h  /tmp/hello.cpp
  0000000 6923 636e 756c 6564 3c20 6f69 7473 6572
  0000020 6d61 0a3e 7375 6e69 2067 616e 656d 7073
  0000040 6361 2065 7473 3b64 0a0a 6e69 2074 616d
  0000060 6e69 2928 7b20 090a 6f63 7475 3c20 203c
  0000100 6822 6c65 6f6c 2022 3c3c 6520 646e 3b6c
  0000120 090a 6572 7574 6e72 3020 0a3b 0a7d
  0000136
  ```

### 6.1.2 Viewing the head or tail of a file

- `head `

```
s193157@GOJ:~$ head /etc/passwd  #默认显示前10行
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin

s193157@GOJ:~$ head -3 /etc/passwd  #显示前3行
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin


```

- `tail`

  - 实时的监控日志信息

  ```
  tail -f /tmp/sys.log
  ```

### 6.1.3 Determining file size

- `wc`

```
wc /tmp/student_records
5 20 92 /tmp/student_records
# 行数，单词数，字符数
wc -l /tmp/student_records
5 /tmp/student_records

wc -w /tmp/student_records
20 /tmp/student_records

wc -c /tmp/student_records
92 /tmp/student_records

# 查找系统中有多少用户
s193157@GOJ:/var/log$ wc -l /etc/passwd
476 /etc/passwd
# 一共476个用户
```

- `du`

  ```
  du /tmp/student_records
  4       /tmp/student_records #文件分配块
  ```

- `ls -l`

## 6.2 Comparing Files

### 6.2.1 Comparing two files

- `diff`

```
s193157@GOJ:/var/log$ diff /tmp/Fall_OH /tmp/Spring_OH
1c1 #change 改变
< Office Hours for Fall 2017
---
> Office Hours for Spring 2018
6a7 #append 增加
> 1:00 - 2:00 P.M.
9d9 #delte 删除
< 3:00 - 4:00 P.M.
12,13d11 
< 2:00 - 3:00 P.M.
< 4:00 - 4:30 P.M.
```

> 通过diff可以进行增量修改从而进行版本管理

### 6.2.2 Patch

- `patch` 文件是一个文件差异文件, 指明了两个文件的版本差异

```
# hello1 内容
s193157@GOJ:/var/log$ cat /tmp/hello1
Hello, world!
Welcome to the patch command.
# hello2 内容
s193157@GOJ:/var/log$ cat /tmp/hello2
Hello, world!
Welcome to the diff and patch commands.
Goodbye!

s193157@GOJ:~$ cp /tmp/hello1 .
s193157@GOJ:~$ cp /tmp/hello.patch .
s193157@GOJ:~$ ls
hello.patch  hello1


s193157@GOJ:~$ patch hello1 hello.patch
patching file hello1
# 根据patch文件修改内容应用到源文件,记录增量更新

s193157@GOJ:~$ cat hello1
Hello, world!
Welcome to the diff and patch commands.
Goodbye!
```

### 6.2.3 Removing repeated lines

只能去掉出现连续出现的重复行,但是并不会修改源文件的内容, 只是将输出结果到屏幕上

```
uniq [options][+N][input-file][output-file]
```

```
s193157@GOJ:~$ cat /tmp/sample
This is a test file for the uniq command.
It contains some repeated and some nonrepeated lines.
Some of the repeated lines are consecutive, like this.
Some of the repeated lines are consecutive, like this.
Some of the repeated lines are consecutive, like this.
And, some are not consecutive, like the following.
Some of the repeated lines are consecutive, like this.
The above line, therefore, will not be considered a repeated
line by the uniq command, but this will be considered repeated!
line by the uniq command, but this will be considered repeated!

s193157@GOJ:~$ uniq /tmp/sample
This is a test file for the uniq command.
It contains some repeated and some nonrepeated lines.
Some of the repeated lines are consecutive, like this.
And, some are not consecutive, like the following.
Some of the repeated lines are consecutive, like this.
The above line, therefore, will not be considered a repeated
line by the uniq command, but this will be considered repeated!

s193157@GOJ:~$ cat /tmp/sample
This is a test file for the uniq command.
It contains some repeated and some nonrepeated lines.
Some of the repeated lines are consecutive, like this.
Some of the repeated lines are consecutive, like this.
Some of the repeated lines are consecutive, like this.
And, some are not consecutive, like the following.
Some of the repeated lines are consecutive, like this.
The above line, therefore, will not be considered a repeated
line by the uniq command, but this will be considered repeated!
line by the uniq command, but this will be considered repeated!

#统计重复出现的次数
s193157@GOJ:~$ uniq -c /tmp/sample
      1 This is a test file for the uniq command.
      1 It contains some repeated and some nonrepeated lines.
      3 Some of the repeated lines are consecutive, like this.
      1 And, some are not consecutive, like the following.
      1 Some of the repeated lines are consecutive, like this.
      1 The above line, therefore, will not be considered a repeated
      2 line by the uniq command, but this will be considered repeated!
```

## 6.3 Compressing Files

- The `gzip` command
  - 压缩后源文件自动删除,解压后压缩文件删除,两个文件不会同时存在
  - 解压 `gizp -d filename` 或者  `gunzip`

```
gzip [options] [file-list]
```

- The `bzip2` command
  - 压缩比更高

```
bzip2 [options] [file-list]
```

## 6.4 Searching for Commands and Files

### 6.4.1 Find directory-list expression

- `-name pattern`

  ```
  #查找当前目录下以hello开头的文件
  s193157@GOJ:~$ find . -name 'hello*'
  ./hello1.gz
  ./hello.patch
  ```

- `-size +/-N`

  ```
  s193157@GOJ:~$ find /tmp  -size 0 #大小为0
  s193157@GOJ:~$ find /tmp  -size +2 #大小大于2
  s193157@GOJ:~$ find /tmp -name 'hello*' -o -size 0 
  # 以hello开头或者大小为0的文件
  # -o (or) -a and
  ```

- `–exec or -ok CMD`

```
#查看文件的详细信息
s193157@GOJ:~$ find . -name 'hello*' -exec ls -l {} \;
# -exec 添加额外的命令 -ok询问是否执行(添加了确认过程)
# {} 占位符
```

- `\( \)`

### 6.4.2 `whereis/which`

```
#列出对于的可执行文件在哪里
#根据PATH环境变量中的信息去查找
s193157@GOJ:~$ which rm
/bin/rm

# whereis 额外的列出了帮助文件
s193157@GOJ:~$ whereis rm
rm: /bin/rm /usr/share/man/man1/rm.1.gz
```

## 6.5 Sorting

- 字段分隔符默认是空格和定位符

```
sort： Ordering a set of items according to some criteria
-b  Ignore leading blanks
-f  Consider lowercases and uppercase letters to be equivalent
-t  field separator
-r  Sort in reverse order
-k  Specify a field as the sort key
-n  Compare according to string numerical value
Notice the LANG!

```

```
#第一关键字按字典序排序
s193157@GOJ:~$ sort /tmp/student_records
Amy Nash ECE 2.38
Jason Kim ECE 3.97
Jim DAVIS CS 12.71
Jonh Doe ECE 3.54
Pam Meyer CS 3.61

#按第四关键字排序(默认是字符串)
s193157@GOJ:~$ sort -k4 /tmp/student_records
Jim DAVIS CS 12.71
Amy Nash ECE 2.38
Jonh Doe ECE 3.54
Pam Meyer CS 3.61
Jason Kim ECE 3.97

#按第四关键字(数值)
s193157@GOJ:~$ sort -n -k4 /tmp/student_records
Amy Nash ECE 2.38
Jonh Doe ECE 3.54
Pam Meyer CS 3.61
Jason Kim ECE 3.97
Jim DAVIS CS 12.71

#按第四关键字逆序(数值)
s193157@GOJ:~$ sort -n -r -k4 /tmp/student_records
Jim DAVIS CS 12.71
Jason Kim ECE 3.97
Pam Meyer CS 3.61
Jonh Doe ECE 3.54
Amy Nash ECE 2.38

#按第四关键字,分隔符为(:)
s193157@GOJ:~$ sort -t: -k4 /etc/passwd
root:x:0:0:root:/root:/bin/bash
zq:x:1000:1000:zq,,,:/home/zq:/bin/bash
uuidd:x:100:101::/run/uuidd:/bin/false
syslog:x:101:104::/home/syslog:/bin/false
mysql:x:102:106:MySQL Server,,,:/nonexistent:/bin/false
messagebus:x:103:107::/var/run/dbus:/bin/false
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
postfix:x:104:111::/var/spool/postfix:/bin/false
```

## 6.6 Cutting and Pasting

### 6.6.1 Cut

- 截取文件

- `cut` 默认字段分割符只能是定位符 `-t`

```
s193157@GOJ:/tmp$ cut -f1-3 /tmp/student
-f filed
Jonh    Doe     ECE
Pam     Meyer   CS
Jim     DAVIS   CS
Jason   Kim     ECE
Amy     Nash    ECE
Jim     DAVIS   EECS
```

### 6.6.2 Pasting

- 拼接文件

```
s193157@GOJ:/tmp$ cut /tmp/a.txt
1 one
2 two
3 three
s193157@GOJ:/tmp$ cut /tmp/b.txt
1 yi
2 er
3 san
s193157@GOJ:/tmp$ paste /tmp/a.txt /tmp/b.txt
1 one   1 yi
2 two   2 er
3 three 3 san
```

## 6.7 正则表达式

- 用一个字符串描述满足某些特征的字符串集合
- shell 元字符
  - `*`：表示任意多个**任意字符**
  - `？`
  - `[]`

- 正则表达式 [正则表达式手册 (oschina.net)](https://tool.oschina.net/uploads/apidocs/jquery/regexp.html)

  ```
  x
  y
  z
  hello world
  this is a book
  this is xy and z and xyz
  ```

  - `|`：表示或者
  - `.`：表示匹配任意字符

  ```
  x
  y
  z
  hel* *rld
  this is a *ok
  this is xy and z and xyz
  ```

  - `^`：表示位于一行的开始

  ```
  ^h
  H
  
  y
  z
  Hello world
  this is a book
  this is xy and z and xyz
  ```

  - `$`：表示一行的结束

  ```
  x
  y
  z
  hello worlD
  this is a book
  this is xy and z and xyz
  ```

  - `\`：转义

  - `?` : `?`前的**一个字符**至多出现一次
- `*`：代表**一个字符**不出现或者出现任意多次

## 6.8 grep

- 找出包含查找单位的行
- 支持正则表达式
- `-w` 全字匹配
- `-i` 忽略大小写
- `-n` 列出行号
- `-c` 只返回匹配行数
- `-l` 只列出文件名
- `-v` 输出不匹配的行
- `egrep` 增强版，支持 `|`

```
s193157@GOJ:/tmp$ grep Kim /tmp/student
Jason   Kim     ECE     3.97

s193157@GOJ:/tmp$ grep CS /tmp/student
Pam     Meyer   CS      3.61
Jim     DAVIS   CS      12.71
Jim     DAVIS   EECS    12.71
s193157@GOJ:/tmp$ grep '\<CS' /tmp/student
Pam     Meyer   CS      3.61
Jim     DAVIS   CS      12.71

s193157@GOJ:/tmp$ grep -w CS /tmp/student
Pam     Meyer   CS      3.61
Jim     DAVIS   CS      12.71
```

## 6.9 Stream editor - Sed

流水线，非交互的编辑器

- 格式

```sh
sed '[address]command' filename(s)
```

- 注意

  - 不会修改源文件的内容，只是将修改后的内容输出到屏幕
  - 给定地址或者正则表达式后，根据地址修改，不给定地址，默认对每一行修改
  - `sed` 遵循最长匹配原则

- 选项

  - 示例文件

  ```
  jonh    Doe     ECE     3.54
  Pam     Meyer   CS      3.61
  Jim     DAVIS   CS      12.71
  Jason   Kim     ECE     3.97
  Amy     Nash    ECE     2.38
  Jim     DAVIS   EECS    12.71
  ```

  - 删除 `-d`

  ```
  删除第二行和第四行
  sed '2,4d' student	
  
  `-i` 改动源文件
  sed -i '2,4d' student	
  
  正则表达式删除
  sed '/\<CS/d' student
  ```

  - 替换 `'s/seg/string'`

  ```
  把CS替换成EECS
  sed 's/\<CS/EECS/' student
  
  对这行每一个匹配的都进行替换 g命令
  sed 's/[0-9\.]/*/g' student
  
  搜索包含某字符串的
  /要包含的字符串/s/要替换的/替换成的/
  ```

  - 打印 `-p`  ( `-n` 不默认输出缓冲区的内容)

  ```
  看中间的2-4行
  s193157@GOJ:/tmp$ sed '2,4p' student
  此时为
  jonh    Doe     ECE     3.54
  Pam     Meyer   CS      3.61
  Pam     Meyer   CS      3.61
  Jim     DAVIS   CS      12.71
  Jim     DAVIS   CS      12.71
  Jason   Kim     ECE     3.97
  Jason   Kim     ECE     3.97
  Amy     Nash    ECE     2.38
  Jim     DAVIS   EECS    12.71
  观察到2，4行输出了两次
  因为sed会默认输出缓冲区的内容
  -n 不默认输出缓冲区的内容
  s193157@GOJ:/tmp$ sed -n '2,4p' student
  此时为
  Pam     Meyer   CS      3.61
  Jim     DAVIS   CS      12.71
  Jason   Kim     ECE     3.97
  ```

  - 插入行 `-i`
  
  ```
  在特定行前面加一个注释
  s193157@GOJ:/tmp$ sed '/\<CS/i high_salary/' student
  jonh    Doe     ECE     3.54
  high_salary/
  Pam     Meyer   CS      3.61
  high_salary/
  Jim     DAVIS   CS      12.71
  Jason   Kim     ECE     3.97
  Amy     Nash    ECE     2.38
  Jim     DAVIS   EECS    12.71
  在后面加
  s193157@GOJ:/tmp$ sed '/\<CS/i high_salary/a' student
  jonh    Doe     ECE     3.54
  high_salary/a
  Pam     Meyer   CS      3.61
  high_salary/a
  Jim     DAVIS   CS      12.71
  Jason   Kim     ECE     3.97
  Amy     Nash    ECE     2.38
  Jim     DAVIS   EECS    12.71
  
  ```

  - `!` 取反
  
  ```
  s193157@GOJ:/tmp$ sed -n '/\<CS/!p' student
  jonh    Doe     ECE     3.54
  Jason   Kim     ECE     3.97
  Amy     Nash    ECE     2.38
  Jim     DAVIS   EECS    12.71
  ```
  
  - 全部匹配 `-g`
  - 禁用账号：使用 `sed` 更改 password 的最后一个字段
  - 转换换行符：使用 `sed` 将 `\r` 去掉
    - win `\r\n`
    - Linux `\n`

## 6.10 Awk

A programming language used for manipulating data and generating reports

- Form of awk command

```
awk ‘pattern’ filename
awk ‘{action}’ filename
awk ‘pattern {action}’ filename

不默认输出非匹配行
s193157@GOJ:/tmp$ awk '/Kim/' student //找出包含Kim的一行
s193157@GOJ:/tmp$ awk '{print $1,$2}' student //输出文件的第一个和第二个字段
// 默认的分隔符是空格或者定位符\t
// PS:cut默认的字段分割符是定位符 要用-d转换

//awk使用-F指定字段分隔符
s193157@GOJ:/tmp$ awk -F: '{print $1,$2}' /etc/passwd

//用空格和冒号同时做字段分隔符
s193157@GOJ:/tmp$ awk -F'[ :]'  '{print $2}' databook //'[ ]' 表示一个集合

//输出CS的行的第一个和第二个字段
s193157@GOJ:/tmp$ awk '/\<CS/{print $1,$2}' student

//如果需要查普通的逗号和$ 要加双引号
```

- Awk's pattern is similar to C expression

```
Relationship expression
s193157@GOJ:/tmp$ awk '$4>3.5{print $1,$2}' student
s193157@GOJ:/tmp$ awk '$3=="CS"' student //也可以进行字典序比较
s193157@GOJ:/tmp$ awk '$2~/^D/' student //输出lastname以大写D开头的 
//~为匹配运算符
//!~为不匹配
Conditional expression
s193157@GOJ:/tmp$ awk '$3=="CS"&&$4>4' student

Arithmetic expression
+,-,*,/,%,^(求幂次)
s193157@GOJ:/tmp$ awk '($2+$3+$4)/3>70{print $0,($2+$3+$4)/3}' score

Compound patterns

Range patterns


内置变量 
$0 //一整行
NR //行号
s193157@GOJ:~$ awk 'NR>=2&&NR<=4' /tmp/student
s193157@GOJ:/tmp$ awk '{print NR,$0}' hello.cpp //添加行号

```

# Lecture 7 Redirection and Piping

## 7.1 Input Redirection

![image-20210511162306007](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210511162306.png)

- 0号：标准输入文件
- 1号：标准输出文件
- 2号：标准错误输出文件

## 7.2 Output Redirection

- Use '>' or '>>' for output redirection
  - command > output-file   (overwrite)
  - command >> output-file  (append)

![image-20210511162627900](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210511162627.png)

```
重定向标准输入
s193157@GOJ:~$ ./add < a.in //重定向到文件a.in

重定向标准输出
s193157@GOJ:~$ ./add > a.out //重定向到文件a.out
s193157@GOJ:~$ ./add >> a.out //重定向到文件a.out增加
```

## 7.3 Redirecting Standard Error

![image-20210511162706644](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210511162706.png)

- 如果没有权限访问一个文件或者产生了错误信息，使用二号文件（标准错误输出文件）输出到屏幕

```
e.g 忽略错误信息
s193157@GOJ:~$ find /tmp -name '*.cpp' 2>result
通常会重定向到 /dev/null文件下 这个文件始终为空
s193157@GOJ:~$ find /tmp -name '*.cpp' 2>/dev/null
```

## 7.4 Redirecting stdin,stdout and stderr in One Command

- Redirecting stdin and stdout in One Command

```
Command < input-file > out-file
```

- Redirecting stdout and stderr in One Command

```
Command > out-file 2>err-file
Command > out-file 2>&1 
//同时重定向到标准输出和标准错误输出
Command >& out-file
```

- example

```
s193157@GOJ:~$ nano input.txt
s193157@GOJ:~$ cat input.txt
200 300
s193157@GOJ:~$ /tmp/add < input.txt > output.txt
s193157@GOJ:~$ cat output.txt
500
```

## 7.5 UNIX Pipes (‘|’)

### 7.5.1 `|`

Used to connect the stdout of one command to the stdin of another command `who | wc`

![image-20210511164502367](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210511164502.png)

![image-20210511164511385](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210511164511.png)

- 结合多个简单命令，构成一个复杂功能
- `KISS` 原则
  - `K`：keep
  - `I`：It
  - `S`：Simple
  - `S`：Stupid

```
统计登陆到系统的人数
s193157@GOJ:~$ who | wc -l
50

s193157@GOJ:~$ who | awk '/^s19/{print $0}' | awk '/\(192.168/{print $0}'
s192872  pts/1        2021-05-11 15:24 (192.168.207.215)
s192982  pts/9        2021-05-11 15:31 (192.168.207.131)
s192985  pts/14       2021-05-11 15:34 (192.168.207.132)
s193157  pts/15       2021-05-11 15:34 (192.168.207.215)
s192875  pts/17       2021-05-11 15:36 (192.168.207.122)
s193036  pts/18       2021-05-11 15:36 (192.168.207.102)
s193101  pts/22       2021-05-11 15:39 (192.168.207.148)
s192860  pts/23       2021-05-11 15:39 (192.168.207.134)
s193071  pts/30       2021-05-11 16:58 (192.168.207.215)
s192952  pts/32       2021-05-11 16:17 (192.168.207.215)
s192965  pts/33       2021-05-11 16:18 (192.168.207.215)
s192894  pts/36       2021-05-11 16:30 (192.168.207.153)
s193080  pts/37       2021-05-11 16:30 (192.168.207.7)
s193083  pts/38       2021-05-11 16:30 (192.168.207.133)
s192913  pts/39       2021-05-11 16:30 (192.168.207.121)
s193073  pts/40       2021-05-11 16:30 (192.168.207.176)
s192972  pts/42       2021-05-11 16:34 (192.168.207.97)
s192999  pts/43       2021-05-11 16:44 (192.168.207.105)
s192866  pts/46       2021-05-11 16:32 (192.168.207.125)
s192887  pts/47       2021-05-11 16:39 (192.168.207.120)
s192864  pts/51       2021-05-11 16:33 (192.168.207.98)
s192862  pts/53       2021-05-11 16:54 (192.168.207.128)
s193031  pts/54       2021-05-11 16:35 (192.168.207.113)
s193213  pts/6        2021-05-11 16:47 (192.168.207.135)
s193198  pts/57       2021-05-11 16:48 (192.168.207.136)
s193157@GOJ:~$ ^C
s193157@GOJ:~$ who | awk '/^s19/{print $0}'
s192872  pts/1        2021-05-11 15:24 (192.168.207.215)
s192876  pts/8        2021-05-11 15:31 (10.173.40.31)
s192982  pts/9        2021-05-11 15:31 (192.168.207.131)
s193121  pts/10       2021-05-11 15:31 (10.173.42.111)
s192903  pts/13       2021-05-11 15:32 (10.173.42.112)
s192985  pts/14       2021-05-11 15:34 (192.168.207.132)
s193157  pts/15       2021-05-11 15:34 (192.168.207.215)
s193176  pts/16       2021-05-11 15:34 (10.173.42.140)
s192875  pts/17       2021-05-11 15:36 (192.168.207.122)
s193036  pts/18       2021-05-11 15:36 (192.168.207.102)
s192867  pts/19       2021-05-11 15:36 (10.173.41.26)
s193179  pts/20       2021-05-11 15:38 (10.173.42.181)
s192901  pts/21       2021-05-11 15:38 (10.173.42.194)
s193101  pts/22       2021-05-11 15:39 (192.168.207.148)
s192860  pts/23       2021-05-11 15:39 (192.168.207.134)
s192988  pts/24       2021-05-11 15:40 (10.173.42.235)
s193080  pts/25       2021-05-11 15:57 (10.173.42.223)
s192882  pts/26       2021-05-11 15:40 (10.173.42.29)
s193126  pts/27       2021-05-11 15:41 (10.173.42.226)
s193021  pts/28       2021-05-11 15:41 (10.173.42.230)
s193217  pts/29       2021-05-11 15:43 (10.173.43.144)
s193071  pts/30       2021-05-11 16:58 (192.168.207.215)
s192984  pts/31       2021-05-11 16:06 (10.173.43.8)
s192952  pts/32       2021-05-11 16:17 (192.168.207.215)
s192965  pts/33       2021-05-11 16:18 (192.168.207.215)
s193164  pts/34       2021-05-11 16:27 (10.173.40.137)
s192988  pts/35       2021-05-11 16:54 (10.173.42.235)
s192894  pts/36       2021-05-11 16:30 (192.168.207.153)
s193080  pts/37       2021-05-11 16:30 (192.168.207.7)
s193083  pts/38       2021-05-11 16:30 (192.168.207.133)
s192913  pts/39       2021-05-11 16:30 (192.168.207.121)
s193073  pts/40       2021-05-11 16:30 (192.168.207.176)
s192972  pts/42       2021-05-11 16:34 (192.168.207.97)
s193042  pts/41       2021-05-11 16:30 (10.173.43.110)
s192999  pts/43       2021-05-11 16:44 (192.168.207.105)
s192988  pts/44       2021-05-11 16:31 (10.173.42.235)
s193021  pts/45       2021-05-11 16:34 (10.173.42.230)
s192866  pts/46       2021-05-11 16:32 (192.168.207.125)
s192887  pts/47       2021-05-11 16:39 (192.168.207.120)
s193021  pts/49       2021-05-11 16:38 (10.173.42.230)
s192864  pts/51       2021-05-11 16:33 (192.168.207.98)
s193123  pts/52       2021-05-11 16:39 (10.173.42.110)
s192862  pts/53       2021-05-11 16:54 (192.168.207.128)
s193031  pts/54       2021-05-11 16:35 (192.168.207.113)
s192988  pts/55       2021-05-11 16:43 (10.173.42.235)
s192900  pts/56       2021-05-11 16:43 (10.173.41.213)
s192871  pts/59       2021-05-11 16:55 (10.173.42.121)
s193213  pts/6        2021-05-11 16:47 (192.168.207.135)
s193198  pts/57       2021-05-11 16:48 (192.168.207.136)
s193143  pts/58       2021-05-11 16:52 (10.173.41.231)

s193157@GOJ:~$ who | awk '/^s19/{print $0}' | awk '/\(192.168/{print $0}'
s192872  pts/1        2021-05-11 15:24 (192.168.207.215)
s192982  pts/9        2021-05-11 15:31 (192.168.207.131)
s192985  pts/14       2021-05-11 15:34 (192.168.207.132)
s193157  pts/15       2021-05-11 15:34 (192.168.207.215)
s192875  pts/17       2021-05-11 15:36 (192.168.207.122)
s193036  pts/18       2021-05-11 15:36 (192.168.207.102)
s193101  pts/22       2021-05-11 15:39 (192.168.207.148)
s192860  pts/23       2021-05-11 15:39 (192.168.207.134)
s193071  pts/30       2021-05-11 16:58 (192.168.207.215)
s192952  pts/32       2021-05-11 16:17 (192.168.207.215)
s192965  pts/33       2021-05-11 16:18 (192.168.207.215)
s192894  pts/36       2021-05-11 16:30 (192.168.207.153)
s193080  pts/37       2021-05-11 16:30 (192.168.207.7)
s193083  pts/38       2021-05-11 16:30 (192.168.207.133)
s192913  pts/39       2021-05-11 16:30 (192.168.207.121)
s193073  pts/40       2021-05-11 16:30 (192.168.207.176)
s192972  pts/42       2021-05-11 16:34 (192.168.207.97)
s192999  pts/43       2021-05-11 16:44 (192.168.207.105)
s192866  pts/46       2021-05-11 16:32 (192.168.207.125)
s192887  pts/47       2021-05-11 16:39 (192.168.207.120)
s192864  pts/51       2021-05-11 16:33 (192.168.207.98)
s192862  pts/53       2021-05-11 16:54 (192.168.207.128)
s193031  pts/54       2021-05-11 16:35 (192.168.207.113)
s193213  pts/6        2021-05-11 16:47 (192.168.207.135)
s193198  pts/57       2021-05-11 16:48 (192.168.207.136)

排序 q
s193157@GOJ:~$ who | awk '/^s19/{print $0}' | awk '/\(192.168/{print $1}' | sort | uniq | wc -l
21
```

- 对命令输出的分页查看

```
ls –l | more
```

- 去除所有重复出现的重复行 （不一定连续出现）

```
s193157@GOJ:~$ sort /tmp/uniq.txt | uniq
a
b
c
s193157@GOJ:~$ sort /tmp/uniq.txt -u
```

- 在 `/tmp` 目录下找到占用空间最大的五个文件

```
s193157@GOJ:~$ du /tmp/*  2>/dev/null | sort -nr | head -5
9040    /tmp/jieba.cache
24      /tmp/grade.csv
24      /tmp/a
20      /tmp/bf8f84e4-b15d-47ef-be3c-858cd0c2b46e
20      /tmp/5d517a3f-8b35-4000-a09c-91aeb99a7661

```

- 查看 `/var` 下的占用大小

```
s193157@GOJ:~$ df /var | awk -F'[ %]' 'NR==2{print $7}'
```

### 7.5.2 tee

- 既希望保存一个输出，又希望把信息传给下一个管道

```
s193157@GOJ:~$ who | tee result
```

## 7.6 FIFOs

- 管道利用内存共享的方式实现进程间的通信
- 命名管道（FIFOs）通过文件实现进程间的通信
  - 读文件相当于消费，读之后数据就没有了

- 建立管道文件

```
mkfifo[option] file-list
```

# Lecture 8 File Sharing

## 8.1 File Sharing Usage

- 给文件定义链接

```
alias awk='gawk' # 定义别名,但是每个用户都要定义一遍

# 通过层层链接找到可执行文件
# 以'l'开头就是链接文件
s193157@GOJ:~$ which awk
/usr/bin/awk
s193157@GOJ:~$ ls -l /usr/bin/awk
lrwxrwxrwx 1 root root 21 12月 21  2018 /usr/bin/awk -> /etc/alternatives/awk
s193157@GOJ:~$ ls -l /etc/alternatives/awk
lrwxrwxrwx 1 root root 13 12月 21  2018 /etc/alternatives/awk -> /usr/bin/gawk
s193157@GOJ:~$ ls -l /usr/bin/gawk
-rwxr-xr-x 1 root root 658072 2月  11  2018 /usr/bin/gawk

# 更改符号链接
s193157@GOJ:~$ ln -sf /usr/bin/python2.7 /usr/bin/python
```

## 8.2 File Sharing via Links

### 8.2.1 Hard Links

```
ln [options] existing-file new-file
ln [options] existing-file-list directory
```

- Commonly used options:
  - `-f`  Force creation of link  	
  - `-n`  Don't create the link if 'new-file' exists  	
  - `-s`  Create a symbolic link to 'existing-file' and name it 'new-file'

```
# 创建硬链接文件
s193157@GOJ:~$ ln -f /tmp/chapter3 chapter3.hard
# 文件如下
-rw-rw-rw- 16 zq      zq     6 5月  25 15:57 chapter3.hard
```

- 通过访问相同的索引结点号，访问的数据块相同，所以得到的文件相同

```
s193157@GOJ:~$ ls -i /tmp/chapter3
1969230 /tmp/chapter3
s193157@GOJ:~$ ls -i chapter3.hard
1969230 chapter3.hard
# 发现索引结点号相同
s193157@GOJ:~$ ls -li /tmp/chapter3
1969230 -rw-rw-rw- 29 zq zq 6 5月  25 16:00 /tmp/chapter3
# 有29个同学创建了硬链接文件
```

![image-20210525161229258](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210525161229.png)

![image-20210525161236455](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210525161236.png)

#### Characteristics of Hard Links 

- No hard links across file systems 不可跨文件系统
- Can‘t create hard links to directories 不能对目录创建硬链接文件
- 不会额外分配存储空间
- 一次硬盘读取
- 在文件删除后依然可以访问文件
  - 在删除一个索引结点的时候先检查 `Link Count` 如果 `Link Count` 大于 0 ，这个索引结点不会被删除

### 8.2.2 Soft / Symbolic Links

```
s193157@GOJ:~$ ls -li chapter3.soft
12321140 lrwxrwxrwx 1 s193157 stu 13 5月  25 16:11 chapter3.soft -> /tmp/chapter3
s193157@GOJ:~$ ls -li /tmp/chapter3
1969230 -rw-rw-rw- 31 zq zq 8 5月  25 16:11 /tmp/chapter3
```

- 通过分配空间的索引节点，同时在硬盘上分配存储空间，存储指向的文件信息

![image-20210525161331602](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210525161331.png)

#### Characteristics of Soft Links 

- 可以跨文件系统访问，可链接目录
- 软链接文件在源文件删除后无法访问文件
- 一次访问要访问两次硬盘，效率相对低一些

# Lecture 9 Processes

## 9.1 Introduction

- A process is a program in execution
- A process is created every time you run an external command and is removed after the command finishes its execution

## 9.2 Running Multiple Processes Simultaneously

- Processor Scheduler

  - The operating system code that implements the CPU scheduling algorithm （进程调度算法，给进程分配时间片）

- Dispatcher

  - The OS code that takes the CPU away from the current process and hands it over to the newly scheduled process 

- Process’s Priority value is computed by Nice value and CPU usage

  - 如果一个进程使用的CPU时间越多，优先级越低

- `Nice` value is a integer between -20 and 19 （用户控制的静态优先级值，动态值为系统自动计算）

  - ```
    nice –n nice_value command
    ```

### 9.2.1 `ps`  查看终端的进程

```
s193157@GOJ:~$ ps
  PID TTY          TIME CMD
 7449 pts/16   00:00:00 bash
14618 pts/16   00:00:00 ps

PID 进程ID
TTY 进程和哪个终端相关联
TIME 进程使用的CPU时间(真正给进程分配的CPU时间,如为0则不到一秒钟)
CMD 进程名

# 列出进程更为详细的信息
s193157@GOJ:~$ ps -l
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1963  7449  7448  0  80   0 -  6991 wait   pts/16   00:00:00 bash
0 R  1963 14821  7449  0  80   0 -  8119 -      pts/16   00:00:00 ps

第一列:0是普通用户的进程, 1是管理员和系统进程
第二列:当前进程的状态 R(运行) S(阻塞)
UID :创建者ID
PPID:父进程ID
C:使用CPU时间
PRI:优先级值 越低,优先级越高 
NI:初始优先级值
ADDR:地址
SZ:占用内存的大小
WCHAN:进程状态

# 给进程降低优先级
s193157@GOJ:~$ nice -n 10 ps -l
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1963  7449  7448  0  80   0 -  6991 wait   pts/16   00:00:00 bash
0 R  1963 14838  7449  0  90  10 -  8119 -      pts/16   00:00:00 ps
# 普通用户只能给进程降低优先级,不能提高优先级,保证系统的关键进程得到资源
s193157@GOJ:~$ nice -n -10 ps -l
nice: 无法设置优先级: 权限不够
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1963  7449  7448  0  80   0 -  6991 wait   pts/16   00:00:00 bash
0 R  1963 14878  7449  0  80   0 -  8119 -      pts/16   00:00:00 ps
s193157@GOJ:~$ ps -e
# 显示当前系统中所有的进程
```

### 9.2.2 `top` 动态查看系统中的进程

### 9.2.3 `pstree` 查看进程树

## 9.3 Unix Process States

A UNIX process can be in one of many states , as it moves from one state to another , eventually finishing its execution(normally or abnormally) and getting out of the system

![image-20210525163939652](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210525163939.png)

- Swapped：存储到硬盘中
- Zombie：进程结束后，无法自己释放 PCB ，当子进程退出的时候，由父进程释放子进程的资源（给父进程发出信号）

## 9.4 Execution of shell Commands

A shell command can be external or internal

- An **internal (built-in) command（内部命令）** is one whose code is part of the shell process
  - `bg, cd,continue, echo, exec`
- An **external command（外部命令）** is one whose code is in a file; contents of the file can be binary code or shell script
  - `grep,more ,cat, mkdir, rmdir, ls`
- `type` ：查看命令类型

```
s193157@GOJ:~$ type echo
echo 是 shell 内建
s193157@GOJ:~$ type rmdir
rmdir 是 /bin/rmdir 
```

A UNIX process can create another process by using the fork system call, which creates an exact main memory map of the original process

- The forking process is known as the parent process
- The created (forked) process is called the child process 

![image-20210525165545862](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210525165545.png)

当执行 `ps` 命令后，`bash` 是 `ps` 的父进程（因为 `ps` 的 PPID 等于 `bash` 的 PID）

```
s193157@GOJ:~$ ps -l
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1963  7449  7448  0  80   0 -  6991 wait   pts/16   00:00:00 bash
0 R  1963 15337  7449  0  80   0 -  8119 -      pts/16   00:00:00 ps
s193157@GOJ:~$ ps
  PID TTY          TIME CMD
16131 pts/29   00:00:00 bash
17462 pts/29   00:00:00 ps

```

- 执行二进制文件

![image-20210525170136448](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210525170136.png)

- 执行脚本文件：需要一个子进程

![image-20210525170153222](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/20210525170153.png)

## 9.5 Process switch

- Foreground and Background Process
- Run a process in the background
  - Append an ampersand(&) to the command line
- suspended Foreground process：`CTRL+Z`
- kill Foreground process：`CTRL+C`
- Display all jobs status：`jobs`
  - Background $\to$ Foreground
    - `fg [%jobnum]`
  - suspended $\to$ Background
    - `bg [%jobnum]`

```
s193157@GOJ:~$ jobs
[1]+  已停止               /tmp/count > /dev/null
[2]-  运行中               /tmp/count > /dev/null &
# 有加号的是刚刚停止的
# 直接用 fg 切换刚刚停止的任务到前台
# fg %2 切换2号到前台
```

## 9.6 UNIX Daemons

- 提供系统服务，精灵进程（守护进程）
- 进程名称以 `d` 结尾

## 9.7 Sequential and Parallel Execution of Commands

- `cmd1;cmd2;…;cmdN`
  - Purpose:	Execute the `‘cmd1’, ‘cmd2’, ‘cmd3’,…,’cmdN’` commands sequentially

- `cmd1& cmd2&…cmdN&`
  - Purpose: Execute commands `‘cmd1’,cmd2’,…’cmdN’` in parallel as separate processes

- UNIX allows you to group commands and execute them as one process by separating commands using semicolons and enclosing them in parenthesis. This is called **command grouping**.
  - `(cmd1;cmd2;…cmdN)`
  - Purpose: Execute commands  `‘cmd1’,’cmd2’…,’cmdN’`  **sequentially but as one process**

## 9.8 Abnormal Termination of Commands and Processes

- Can terminate a foreground process by `<Ctrl-C>`
- Can terminate a background process:
  - Use the kill command
  - By first bringing the process into foreground by using the `fg` command and then pressing `<Ctrl-C>`

- A process can take one of three actions upon receiving a signal
  - Accept the default action as determined by the UNIX kernel （默认方式处理）
  - Ignore the signal
  - Intercept the signal and take a user-defined action（使用自己的方式处理）

**内部信号和外部信号**

- A signal caused by an event internal to a process is known as an **internal signal** or **trap**.
  - 指针异常、除数为 $0$
- A signal caused by an event external to a process is called an **external signal**

- `kill [-signal_number] proc-list`
- `Kill –l`
  Purpose: Send the signal for `‘signal_number’`  to processes whose PIDs or `jobIDs` are specified in the `‘poc-list’`; `jobIDs` must start with `%`.The command `kill –l` return a list of all signals and their names (on some systems, numbers are not displayed)
- Commonly used `signal_numbers`:

```
1			Hangup
2			Interrupt(<Ctrl-C>)
3			Quit(<Ctrl-\>)
9			Sure kill(所有进程都不能忽略这个信号量)
15			Software signal (default signal number)	
```

- 每个用户只能给自己的进程发送信号量，超级用户可以给所有进程发送信号量

- 杀死所有进程 `killall`

```shell
s193157@GOJ:~$ killall count
[2]   已终止               /tmp/count > /dev/null
[3]   已终止               /tmp/count > /dev/null
[4]   已终止               /tmp/count > /dev/null
[5]   已终止               /tmp/count > /dev/null
[6]   已终止               /tmp/count > /dev/null
[7]   已终止               /tmp/count > /dev/null
[8]   已终止               /tmp/count > /dev/null
[9]   已终止               /tmp/count > /dev/null
[10]   已终止               /tmp/count > /dev/null
[11]   已终止               /tmp/count > /dev/null
[12]-  已终止               /tmp/count > /dev/null
[13]+  已终止               /tmp/count > /dev/null

s193157@GOJ:~$ /tmp/neverdie &
[1] 23975
s193157@GOJ:~$ /tmp/neverdie &
[2] 23976
s193157@GOJ:~$ /tmp/neverdie &
[3] 23977
s193157@GOJ:~$ killall neverdie
I won't Die!!!
I won't Die!!!
I won't Die!!!
s193157@GOJ:~$ killall -9 neverdie # 使用9选项终止
[1]   已杀死               /tmp/neverdie
[2]-  已杀死               /tmp/neverdie
[3]+  已杀死               /tmp/neverdie
```

- `nohup commands [args]` 忽略挂起信号量
  - Purpose: Run ‘command and ignore the hang-up signal

## 9.9 Scheduling a Process To Execute Later

- 计划任务：数据备份

| Create  | **at** **time** | **crontab** **-e** |
| ------- | --------------- | ------------------ |
| List    | `at  -l`        | `crontab -l`       |
| Details | `at  -c jobnum` |                    |
| Remove  | `at  -d jobnum` | `crontab -r`       |
| Edit    |                 | `crontab -e`       |

- One-time jobs use `at` ：一次性任务

```
s193157@GOJ:~$ at 23:59 # 在这个时间创建计划任务
warning: commands will be executed using /bin/sh
at> backup
at> /tmp/count
at> <EOT> # Ctrl+D
job 15 at Tue Jun  1 23:59:00 2021

s193157@GOJ:~$ at -l # 查看自己计划任务
15      Tue Jun  1 23:59:00 2021 a s193157

s193157@GOJ:~$ at -c 15 # 查看计划任务具体内容
#!/bin/sh
# atrun uid=1963 gid=1689
# mail s193157 0
.....
backup
/tmp/count

s193157@GOJ:~$ at -d 15 # 删除计划任务

```

- recurring jobs use `crontab` ：周期执行任务

```shell
s193157@GOJ:~$ crontab -e
no crontab for s193157 - using an empty one

Select an editor.  To change later, run 'select-editor'.
  1. /bin/nano        <---- easiest
  2. /usr/bin/vim.basic
  3. /usr/bin/vim.tiny
  4. /bin/ed

Choose 1-4 [1]: 1

# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
```

## 9.10 File Package 文件压缩

- 打包文件

```
s193157@GOJ:/tmp$ tar -zcvf f.tar.gz /tmp/f
tar: 从成员名中删除开头的“/”
/tmp/f/
/tmp/f/f2
/tmp/f/f1
```

- 查看压缩文件的文件结构

```
s193157@GOJ:/tmp$ tar -ztvf f.tar.gz
drwxrwxr-x zq/zq             0 2021-06-08 08:51 tmp/f/
-rw-rw-r-- zq/zq             6 2021-06-08 08:50 tmp/f/f2
-rw-rw-r-- zq/zq             6 2021-06-08 08:50 tmp/f/f1
```

- 解压压缩文件

```
s193157@GOJ:/tmp$ tar -zxvf f.tar.gz
```

# Lecture 10 Bourne Shell Programming

## 10.1 Running a Bourne Shell Script

Ways of running a Bourne Shell

- Make the script file executable by adding the execute permission to the existing access permissions for the file
  - 给文件一个执行权限

```
chmod u+x script_file
```

- Run the `/bin/sh` command with the script file as its parameter
  - 让它在子进程 shell 里面运行

```
/bin/bash script_file
```

- Run the source or `.`  command with the script file as its parameter
  - 在当前 shell 中执行

```
/bin/source script_file
```

- Force the current shell to execute a script in the Bourne shell, regardless of your current shell
  - 当语法shell的当前运行的shell不一致的时候，添加命令使用另外的程序对它解释执行

```
#!/bin/bash //当在解释这个文件的时候，当在创建这个子进程对脚本解释执行的时候，替换文件的语法shell对脚本解释执行
```

## 10.2 Shell Variables

- 通过等号赋值
  - 等号两端不能有空格
- 通过 `$` 访问

```
s193157@GOJ:/tmp$ name='tom'
s193157@GOJ:/tmp$ echo $name
tom
s193157@GOJ:/tmp$ a=$name
s193157@GOJ:/tmp$ echo $a
tom
```

- 子进程可以继承父进程的环境变量
  - 使用 `env` 查看环境变量
  - 当创建子进程的时候，子进程将所有环境变量**复制**一份
  - 子进程如果修改了环境变量的值，不会影响的父进程
  - 让脚本在当前shell执行
  - ！`PATH`：去哪些目录去找可执行文件

- 使用 `export` 创建环境变量

```
s193157@GOJ:/tmp$ export name
```

## 10.3 Read-only Shell Variables

- `$0` ：可执行的脚本的文件的文件名
- `$1-9`：可执行文件的参数
- `$*/$@`：显示所有的参数
  - 区别：用`""` 引起来的时候
    - `$*`：表示 `"a b c"`
    - `$@`：表示 `"a" "b" "c"`

- `$#`：代表参数的个数

- `$$`：代表当前执行脚本的进程 `id`

- `$?`：上一条命令的返回状态
  - 可以使用 `$?` 判断语句的执行是否成功

- `$!`：刚刚切换到后台的变量

- 默认变量是字符串

```
s193157@GOJ:/tmp$ a=1
s193157@GOJ:/tmp$ a=$a+1
s193157@GOJ:/tmp$ echo $a
1+1
```

- 以数值进行运算

```
s193157@GOJ:/tmp$ declare -i a
s193157@GOJ:/tmp$ a=4
s193157@GOJ:/tmp$ a=$a+1
s193157@GOJ:/tmp$ echo $a
5
```

## 10.4 Command Substitution

```
s193157@GOJ:~$ num=`who | wc -l`
s193157@GOJ:~$ num=$(who | wc -l)
```

## 10.5 Resetting Variables

	unset [name-list]

**Purpose**  Reset or remove the variable or function corresponding to the names in ‘name-list’, where ‘name-list’ is a list of names separated by spaces

## 10.6 Creating Read-Only Defined Variables

	readonly [name-list]

**Purpose**  Prevent assignment of new values to the variables in ‘name-list’

```
s193157@GOJ:~$ name='tom'
s193157@GOJ:~$ name='jack'
s193157@GOJ:~$ readonly name
s193157@GOJ:~$ name='tom'
-bash: name: 只读变量
```

## 10.7 Reading from Standard Input

```
read variable-list
```

 **Purpose** Read one line from standard input and assign words in the line to variables in ‘name-list’

```
nano hello.sh

read -p 'Please input two names:' name1 name2
echo "Hello, $name1"
echo "Hello, $name2"
```

- read 在输入赋值的时候，如果是最后一个变量，将没有赋值的字符串直接赋值给最后一个变量

## 10.8 Special Characters for the echo Command

- 转义字符只有加上 `-e` 才可以识别转义字符

```
s193157@GOJ:~$ echo -e "tom\tjack"
tom     jack
```

- echo语句不换行使用 `-n` 语句

## 10.9 Operators for the `test` Command

![image-20210615155127196](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/image-20210615155127196.png)

![image-20210615155226999](https://cdn.jsdelivr.net/gh/QiuHong-1202/FigureBed/2021/image-20210615155226999.png)

