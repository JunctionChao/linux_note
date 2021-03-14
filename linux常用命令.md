### Linux 常用命令

#### Linux查看系统信息基本命令

- 查看系统版本信息：lsb_release -a
- 查看内存信息：free -h
- 查看磁盘空间：df -h
- 查看CPU信息：cat /proc/cpuinfo
- 查看当前目录下所有文件，文件夹的大小：du -ah --max-depth=1

#### netstat（监控TCP/IP网络的命令）

- 常用命令：netstat -antp

  根据权限自行添加sudo

- 常见参数：

  ```text
  -a或--all：显示所有连线中的Socket； 
  -A<网络类型>或--<网络类型>：列出该网络类型连线中的相关地址； 
  -c或--continuous：持续列出网络状态，每隔固定时间，执行netstat命令； 
  -C或--cache：显示路由器配置的快取信息； 
-e或--extend：显示网络其他相关信息； 
  -F或--fib：显示FIB； 
  -g或--groups：显示多重广播功能群组组员名单； 
  -h或--help：在线帮助； 
  -i或--interfaces：显示网络界面信息表单； 
  -l或--listening：显示监控中的服务器的Socket； 
-M或--masquerade：显示伪装的网络连线； 
  -n或--numeric：拒绝显示别名，能显示数字的全部转化成数字，而不显示域名服务器； 
  -N或--netlink或--symbolic：显示网络硬件外围设备的符号连接名称； 
  -o或--timers：显示计时器； 
  -p或--programs：显示正在使用Socket的程序识别码和程序名称； 
  -r或--route：显示Routing Table； 
  -s或--statistice：显示网络工作信息统计表； 
  -t或--tcp：显示TCP传输协议的连线状况； 
  -u或--udp：显示UDP传输协议的连线状况； 
  -v或--verbose：显示指令执行过程； 
  -V或--version：显示版本信息； 
  -w或--raw：显示RAW传输协议的连线状况； 
  -x或--unix：此参数的效果和指定"-A unix"参数相同； 
  --ip或--inet：此参数的效果和指定"-A inet"参数相同。
  ```
  
- 举例说明：

  - 列出所有端口：netstat -a
    
    ```
    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State
    tcp        0      0 0.0.0.0:5900            0.0.0.0:*               LISTEN
    tcp        0      0 0.0.0.0:x11             0.0.0.0:*               LISTEN
    Active UNIX domain sockets (servers and established)
    Proto RefCnt Flags       Type       State         I-Node   Path
    unix  2      [ ACC ]     STREAM     LISTENING     17347    @/tmp/dbus-szg2jigh4q
    unix  2      [ ACC ]     STREAM     LISTENING     993      @/tmp/dbus-cXbudwWzHR
    unix  2      [ ACC ]     STREAM     LISTENING     983      /tmp/.X11-unix/X0
    unix  2      [ ACC ]     STREAM     LISTENING     21942    @/tmp/dbus-dCCwBT1sjU
    unix  2      [ ACC ]     SEQPACKET  LISTENING     15846    /run/WSL/12_interop
    unix  2      [ ACC ]     SEQPACKET  LISTENING     15853    /run/WSL/27_interop
    unix  2      [ ACC ]     STREAM     LISTENING     16216    /home/junction/.gnupg/S.gpg-agent
    unix  2      [ ACC ]     STREAM     LISTENING     16218    /home/junction/.gnupg/S.gpg-agent.extra
    unix  2      [ ACC ]     STREAM     LISTENING     16219    /home/junction/.gnupg/S.gpg-agent.browser
    unix  2      [ ACC ]     STREAM     LISTENING     16220    /home/junction/.gnupg/S.gpg-agent.ssh
    unix  3      [ ]         STREAM     CONNECTED     985      /tmp/.X11-unix/X0
    ```
    
    **Active Internet connections** 活动的Internet网络连接，其中"Recv-Q"和"Send-Q"指接收队列和发送队列。这些数字一般都应该是0。如果不是则表示软件包正在队列中堆积。这种情况只能在非常少的情况见到。
    
    **Active UNIX domain sockets** 活动的Unix域套接字(和网络套接字一样，但是只能用于本机通信，性能可以提高一倍)
    
  - 列出所有TCP端口号：netstat -at

  - 列出所有 udp 端口：netstat -au

  - 列出所有监听端口：netstat -l

  - 只列出所有监听tcp端口：netstat -lt

  - 只列出所有监听udp端口：netstat -lu

  - 只列出所有监听UNIX 端口：netstat -lx

  - 显示所有端口的统计信息：netstat -s

  - 显示TCP端口的统计信息：netstat -st      显示UDP统计信息 -su

  - 显示核心路由信息：netstat -r

    使用 netstat -rn 显示数字格式，不查询主机名称

  - 查看某个程序的运行端口：netstat -ap | gerp 程序名等关键词

    查看ssh的运行详情：netstat -anp | gerp ssh

    查找80端口占用的进程：netstat -anp | grep 80

    

  - netstat -antp

    ```
    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
    tcp        0      0 0.0.0.0:5900            0.0.0.0:*               LISTEN      1584/Xtightvnc
    tcp        0      0 0.0.0.0:6000            0.0.0.0:*               LISTEN      1584/Xtightvnc
    tcp        0      0 127.0.0.1:46416         127.0.0.1:5900          ESTABLISHED -
    tcp        0      0 127.0.0.1:5900          127.0.0.1:46416         ESTABLISHED 1584/Xtightvnc
    tcp        0      0 172.172.230.211:46326   172.172.100.3:80        TIME_WAIT   -            
    tcp        0      0 172.172.230.211:5401    172.172.100.3:443       TIME_WAIT   -     
    tcp        0      0 :::22                   :::*                    LISTEN      1904/sshd           
    tcp        0      0 ::1:631                 :::*                    LISTEN      1750/cupsd          
    tcp        0      0 :::11776                :::*                    LISTEN      1713/rpc.statd 
    ```

    **Local address**：连接的本地端地址详情，默认为netstat显示地址的本地主机名，端口的服务名。默认情况下，netstat会显示地址的本地主机名，端口的服务名。

    ​		127.0.0.1 表示只能本机访问，外面访问不了此端口；0.0.0.0 是对外开放端口，表示本机和外部电脑都可以访问，通过服务域名:ip可以访问的端口。

    ​		::: 这三个: 的前两个”::“，是“0:0:0:0:0:0:0:0”的缩写，相当于IPv6的“0.0.0.0”，第三个:是IP和端口的分隔符
    
    **Foreign Address**：与本机建立连接的外部地址和端口号，连接远端的地址和端口号。
    
    在上述例子中 127.0.0.1:46416 这一行表示本地的46416端口 与本地的5900端口建立了连接
    
    在上述例子中 0.0.0.0:5900  这一行表示本地5900端口正在监听，还没有和外部建立连接
    
    **State**：state列共有12中可能的状态，前面11种是按照TCP连接建立的三次握手和TCP连接断开的四次挥手过程来描述的

- reference：

  https://www.howtogeek.com/513003/how-to-use-netstat-on-linux/

  https://blog.csdn.net/m0_37556444/article/details/83000553
  
  https://www.cnblogs.com/ggjucheng/archive/2012/01/08/2316661.html
  
  https://www.linuxcool.com/

#### Linux 重定向

重定向可以分为输入重定向以及输出重定向这两种类型

- linux中重定向有3中数据流
  - 输入信息会从 `stdin` 中读取（标准输入，通常是键盘或鼠标）。
  - 输出信息会被输出到 `stdout` （标准输出，一个文本文件或者数据流）。
  - 错误信息会被输出到 `stderr`。

- 在 Linux 系统中，标准输入，标准输出以及标准错误都作为文件存在。 你可以在 `/dev` 目录下看到它们

  ```
  junction@DESKTOP-GKN9MD5:~$ ls /dev/std*
  /dev/stderr  /dev/stdin  /dev/stdout
  ```

- **重定向输出**

  - 在 Linux 系统中，使用 `>` 字符表示重定向输出。例如，将 `ls` 命令的输出重定向到一个文件中：`$ ls > list.txt`
  - 重定向还可以用于复制文件的内容，而且不限于复制文本文件，二进制文件也可以复制：`$ cat image.png > picture.png`
  - 如果想要将一个文件的内容复制到另一个文件的末尾，你只需将 `>` 字符换成 `>>` 字符串即可：`$ cat lxlinux >> alvin`

- **重定向输入** 

  重定向输入使用的是 `<` 字符

  - 输入重定向可以将输入信息重定向至命令中作为参数使用。该功能可能比较少用，但是，当命令需要一个参数列表时，而这些参数都存在一个文件中，然后你想快速地将它们从文件中复制粘贴到终端，这时这个功能就能派上用场了

  - 输入重定向的常见用法是Here-doc以及 Here-string 。将输入的文本块重定向至标准输入流，直至遇到特殊的文件结束标记符为止（文件结束标记符可以是任意的唯一的字符串，但大部分人都默认使用 `EOF`）

    ```
    junction@DESKTOP-GKN9MD5:~/cmd_test$ cat << eof
    > ali
    > lixe
    > eof
    ali
    lixe
    ```
    
    Here-doc 是 Bash 脚本编写者们将多行文本转储到文件或屏幕上的常用技巧。
    
    Here-string 与 Here-doc 相似，但是它只有一个字符串，或者几个被引号括起来的字符串：
    
    ```
    junction@DESKTOP-GKN9MD5:~/cmd_test$ cat <<< "alvin lxlinux.net"
    alvin lxlinux.net
    junction@DESKTOP-GKN9MD5:~/cmd_test$ cat <<< alvin
    alvin
    ```
  
- **重定向错误信息**

  错误信息默认会进入叫 `stderr` 的流，使用 `2>` 可以对其进行重定向,  `2>>`: 追加方式

  ```
  junction@DESKTOP-GKN9MD5:~/cmd_test$ ls /nope 2> error.log
  junction@DESKTOP-GKN9MD5:~/cmd_test$ cat error.log
  ls: cannot access '/nope': No such file or directory
  ```

- **重定向数据至 /dev/null**

  和标准输入、标准输出以及标准错误一样，在 Linux 文件系统中，空，也存在一个文件与之对应，它叫做 `null` ，放在 `/dev` 目录下

  `/dev/null` 并不保存数据，被写入 `/dev/null` 的数据最终都会丢失，就像被丢进虚空中一样。因此，你可以使用重定向将不需要的数据输送到 `/dev/null` 。

  例如，`find` 命令的输出往往很冗长，而且在搜索文件时还经常会报告权限冲突的错误，像这样：

  `find ~ -type f`   查找~目录下文件类型为f（普通文件）的文件

  ```
  $ find ~ -type f 
  /home/seth/actual.file 
  find: '/home/seth/foggy': Permission denied
  find: '/home/seth/groggy': Permission denied
  find: '/home/seth/soggy': Permission denied 
  /home/seth/zzz.file
  ```

  这时，你就可以将错误信息重定向到 `/dev/null` ，以过滤掉不必要的信息，像这样：

  ```
  $ find ~ -type f 2> /dev/null 
  /home/seth/actual.file 
  /home/seth/zzz.file
  ```

- example：

  - 将显示的数据，正确的输出到 list.txt 错误的数据输出到 list.err：`ls -al 1> list.txt 2> list.err`
  - 将显示的数据，不论正确或错误均输出到 list.txt 当中！错误与正确文件输出到同一个文件中，则必须以上面的方法来写！不能写成其它格式：`ls -al 1> list.txt 2> &1`

#### cat命令
cat命令用于查看文件内容，适合较小的纯文本文件

当文件内容较大时，文本内容会在屏幕上快速闪动（滚屏），用户往往看不清所显示的具体内容。因此对于较长文件内容可以按Ctrl+S键，停止滚屏；以及Ctrl+Q键可以恢复滚屏；而按Ctrl+C（中断）键则可以终止该命令的执行。或者对于大文件，干脆用more命令

- 常用参数

  - **-n 或 --number**：由 1 开始对所有输出的行数编号，包括空行。
  - **-b 或 --number-nonblank**：和 -n 相似，只不过对于空白行不编号。
  - **-s 或 --squeeze-blank**：当遇到有连续两行以上的空白行，就代换为一行的空白行。
  - **-v 或 --show-nonprinting**：使用 ^ 和 M- 符号，除了 LFD 和 TAB 之外。
  - **-E 或 --show-ends** : 在每行结束处显示 $。
  - **-T 或 --show-tabs**: 将 TAB 字符显示为 ^I。
  - **-A, --show-all**：等价于 -vET。
  - **-e：**等价于"-vE"选项；
  - **-t：**等价于"-vT"选项

- example：

  - 查看文件的内容，并添加行数编号后输出到另外一个文件中：`cat -n linuxcool.log > linuxprobe.log` 

  - 清空文件的内容（相当于把空数据写入文件）：`cat /dev/null > /root/filename.txt`

  - 持续写入文件内容，碰到EOF符后结束并保存：

    ```
    [root@linuxcool ~]# cat > filename.txt <<EOF
    > Hello, World 
    > Linux!
    > EOF
    ```

  - 把 textfile1 和 textfile2 的文档内容加上行号（空白行不加）之后将内容附加到 textfile3 文档里：

    `cat -b textfile1 textfile2 >> textfile3`

#### 清空文件的几种方式

- 重定向方法：

  ```
  [root@centos7 ~]# du -h test.txt 
  4.0K    test.txt
  [root@centos7 ~]# > test.txt 
  [root@centos7 ~]# du -h test.txt 
  0    test.txt
  ```

- 使用true命令重定向清空文件

  ```
  [root@centos7 ~]# du -h test.txt 
  4.0K    test.txt
  [root@centos7 ~]# true > test.txt 
  [root@centos7 ~]# du -h test.txt 
  0    test.txt
  ```

- 使用cat/cp/dd命令以及/dev/null设备来清空文件

  ```
  [root@centos7 ~]# du -h test.txt 
  4.0K    test.txt
  [root@centos7 ~]# cat /dev/null >  test.txt 
  [root@centos7 ~]# du -h test.txt 
  0    test.txt
  ###################################################
  [root@centos7 ~]# echo "Hello World" > test.txt 
  [root@centos7 ~]# du -h test.txt 
  4.0K    test.txt
  [root@centos7 ~]# cp /dev/null test.txt 
  cp：是否覆盖"test.txt"？ y
  [root@centos7 ~]# du -h test.txt 
  0    test.txt
  ##################################################
  [root@centos7 ~]# echo "Hello World" > test.txt 
  [root@centos7 ~]# du -h test.txt 
  4.0K    test.txt
  [root@centos7 ~]# dd if=/dev/null of=test.txt 
  记录了0+0 的读入
  记录了0+0 的写出
  0字节(0 B)已复制，0.000266781 秒，0.0 kB/秒
  [root@centos7 ~]# du -h test.txt 
  0    test.txt
  ```

- 使用echo命令清空文件

  ```
  [root@centos7 ~]# echo "Hello World" > test.txt 
  [root@centos7 ~]# du -h test.txt 
  4.0K    test.txt
  [root@centos7 ~]# echo -n "" > test.txt    =>要加上"-n"参数，-n表示不输出结尾的换行符，默认情况下会"\n"，也就是回车符
  [root@centos7 ~]# du -h test.txt  
  0    test.txt
  ```

- 使用truncate命令清空文件

  ```
  [root@centos7 ~]# du -h test.txt 
  4.0K    test.txt
  [root@centos7 ~]# truncate -s 0 test.txt   -s参数用来设定文件的大小，清空文件，就设定为0；
  [root@centos7 ~]# du -h test.txt 
  0    test.txt
  ```

#### more / less命令

- more命令，功能类似 cat ，cat命令是整个文件的内容从上到下显示在屏幕上。 more会以一页一页的显示方便使用者逐页阅读，而最基本的指令就是按空白键（space）就往下一页显示，按 b 键就会往回（back）一页显示，而且还有搜寻字串的功能 。more命令从前向后读取文件，因此在启动时就加载整个文件

  ```
  1、命令格式 
  more [-dlfpcsu] [-num] [+/pattern] [+linenum] [file ...] 
  2、命令功能 
  more命令和cat的功能一样都是查看文件里的内容，但有所不同的是more可以按页来查看文件的内容，还支持直接跳转行等功能。 
  3、常用参数列表 
   -num 一次显示的行数
   -d 在每屏的底部显示友好的提示信息 
   -l 忽略 Ctrl+l （换页符）。如果没有给出这个选项，则more命令在显示了一个包含有 Ctrl+l 字符的行后将暂停显示，并等待接收命令。 
   -f 计算行数时，以实际上的行数，而非自动换行过后的行数（有些单行字数太长的会被扩展为两行或两行以上） 
   -p 显示下一屏之前先清屏。
   -c 从顶部清屏然后显示。
   -s 文件中连续的空白行压缩成一个空白行显示。
   -u 不显示下划线
   +/pattern 在每个档案显示前搜寻该字串（pattern），然后从该字串前两行之后开始显示
   +num 从第num行开始显示
   4、常用操作命令
   Enter    向下n行，需要定义。默认为1行
   Ctrl+F   向下滚动一屏
   空格键    向下滚动一屏
   Ctrl+B   返回上一屏
   =        输出当前行的行号
   ：f      输出文件名和当前行的行号
   v        调用vi编辑器
   !命令    调用Shell，并执行命令 
   q        退出more
  ```

  - example:
  - 第五行开始显示 text.txt 文件中的内容：`more +5 text.txt`
  - 从 text.txt 文件中查找第一个出现"5"字符串的行，并从该处前两行开始显示输出：`more +/5 text.txt`

- less 命令也是对文件或其它输出进行分页显示的工具，应该说是linux正统查看文件内容的工具，功能极其强大。less 的用法比起 more 更加的有弹性。在 more 的时候，我们并没有办法向前面翻， 只能往后面看，但若使用了 less 时，就可以使用 [pageup] [pagedown] 等按键的功能来往前往后翻看文件，更容易用来查看一个文件的内容！除此之外，在 less 里头可以拥有更多的搜索功能，不止可以向下搜，也可以向上搜

  ```
  1．命令格式： 
  less [参数] 文件 
  2．命令功能： 
  less 与 more 类似，但使用 less 可以随意浏览文件，而 more 仅能向前移动，却不能向后移动，而且 less 在查看之前不会加载整个文件。 
  3．命令参数： 
   -b <缓冲区大小> 设置缓冲区的大小 
   -e  当文件显示结束后，自动离开
   -f  强迫打开特殊文件，例如外围设备代号、目录和二进制文件
   -g  只标志最后搜索的关键词
   -i  忽略搜索时的大小写
   -m  显示类似more命令的百分比 
   -N 显示每行的行号
   -o <文件名> 将less 输出的内容在指定文件中保存起来 
   -Q  不使用警告音 
   -s  显示连续空行为一行
   -S  行过长时间将超出部分舍弃 
   -x <数字> 将“tab”键显示为规定的数字空格 
   /字符串：向下搜索“字符串”的功能 
   ?字符串：向上搜索“字符串”的功能
   n：重复前一个搜索（与 / 或 ? 有关）
   N：反向重复前一个搜索（与 / 或 ? 有关） 
   b 向后翻一页
   d 向后翻半页
   h 显示帮助界面
   Q 退出less 命令
   u 向前滚动半页
   y 向前滚动一行
   空格键 滚动一页
   回车键 滚动一行
  ```

#### head / tail命令

- head	

  head命令以行为单位，取文件的内容,后面不接参数时默认打印前10行

  语法格式：head [参数] [文件]

  常用参数：

  -n	后面接数字，代表显示几行的意思
  -c	指定显示头部内容的字符数
  -v	总是显示文件名的头信息
  -q	不显示文件名的头信息

  - example：

    - 显示文件名信息，并显示文件前两行：

      ```
      [root@linuxcool ~]# head -v -n 2 test.txt 
      ==> test.txt <==
      hello world
      hello linuxcool
      ```

  
  - 显示文件前5个字符：
  
    ```
      [root@linuxcool ~]# head -c 5 test.txt 
    hello
      ```
  
- tail

  tail用于显示文件尾部的内容，默认在屏幕上显示指定文件的末尾10行。如果给定的文件不止一个，则在显示的每个文件前面加一个文件名标题。如果没有指定文件或者文件名为“-”，则读取标准输入

  语法格式：tail [参数]

  常用参数：


  --retry	即是在tail命令启动时，文件不可访问或者文件稍后变得不可访问，都始终尝试打开文件。使用此选项时需要与选项“——follow=name”连用

  -c<N>或——bytes=<N>	输出文件尾部的N（N为整数）个字节内容

  -f<name/descriptor>	--follow<nameldescript>：显示文件最新追加的内容

  -F	与选项“-follow=name”和“--retry”连用时功能相同

  -n<N>或——line=<N>	输出文件的尾部N（N位数字）行内容

  --pid=<进程号>	与“-f”选项连用，当指定的进程号的进程终止后，自动退出tail命令

  --help	显示指令的帮助信息

  --version	显示指令的版本信息

  - examples：

    - 显示文件file的最后10个字符：

      ```
      [root@linuxcool ~ ]  tail -c 10 file 
      ```

    - 一直变化的文件总是显示后10行：

      ```
      [root@linuxcool ~ ]  tail -f 10 file
      ```