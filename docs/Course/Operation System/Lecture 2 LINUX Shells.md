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
| \|             | To  substitute a command  命令替换                           | `PATH=$PATH:pwd`   |
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