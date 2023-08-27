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

