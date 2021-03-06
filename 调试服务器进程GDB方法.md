GDB是GNU开源组织发布的一个强大的UNIX下的程序调试工具。
一般来说，GDB主要帮忙你完成下面四个方面的功能：

    1、启动你的程序，可以按照你的自定义的要求随心所欲的运行程序。
    2、可让被调试的程序在你所指定的调置的断点处停住。（断点可以是条件表达式）
    3、当程序被停住时，可以检查此时你的程序中所发生的事。
    4、动态的改变你程序的执行环境。
    
##一般程序文件调试过程
####1.编译文件
        gcc -g test.c -o test
-g用于生成调试信息，如果没有-g，你将看不见程序的函数名、变量名，所代替的全是运行时的内存地址。
####2.启动gdb调试
        gdb test
####3.显示源码
        l (list) n ---------------------------l+数字可用于显示n行源码
        l func     ---------------------------显示函数名为func的函数源码
        l -        ---------------------------显示当前行前面的源码
        set listsize -------------------------设置一次显示源码函数
        list  f，l ---------------------------显示从f行到l行之间源码
####4.设置断点
        b          ---------------------------在下一行设置断点
        b(break) n ---------------------------在第n行设置断点
        b  func    ---------------------------在函数func设置断点
        b  file：n ---------------------------在文件file第n行设置断点
        b  file:func -------------------------在文件file的函数func处设置断点
        b ... if(cont) -----------------------在cont成立时设置断
####5.运行程序
        r(run)
        step      ----------------------------单步执行，有函数调用则进入函数
        stepi     ----------------------------单步追踪一条机器指令，运行结束后会在打出程序代码的同时打出机器指令
        n(next)   ----------------------------单步追踪，有函数也不进入
        f(finish) ----------------------------运行直到函数完成返回，并打印函数返回堆栈地址和返回值
####7.继续执行
        c(continue)
####8.打印变量
       p(print) i  --------------------------打印变量i的值
       p *array@len -------------------------打印动态数组array的值，len是array的长度
       p/a i      ---------------------------以十六进制格式显示变量，c字符格式，f浮点数格式，x十六进制格式，t二进制格式，d十进制格式
       info args   --------------------------打印当前函数中的参数名及其值
       info locals --------------------------打印当前函数中所有局部变量及其值
       info catch ---------------------------打印当前函数中的异常处理信息
####9.查看函数堆栈
       bt(backtrace) ------------------------打印当前函数调用栈的所有信息
       bt  n       --------------------------只打印栈顶n层的栈信息
       bt -n       --------------------------只打印栈底n层的栈信息
       f(frame) n  --------------------------查看第n层栈信息
       f           --------------------------打印栈的层编号、当前函数名、函数参数值、函数所在文件及编号、函数执行到的语句
       up n        --------------------------向栈的上面移动n层
       down n      --------------------------向栈的下面移动n层
####10.搜索源码
       forward-search  str ------------------向前搜索
       reverse-search  str ------------------全部搜索str是一个正则表达式表示一个字符串的匹配模式
##服务器进程的调试方法
 GDB提供了两种方式来调试正在运行的进程：一种是在GDB命令行上指定进程的PID，另一种是在GDB中使用“attach”命令。
####启动方式：
       gdb -p PID  --------------------------启动调试进程号是PID的进程
       gdb --pid=PID
另外一种连接到其它进程的方法是先用file命令加载调试时所需的符号表，然后再通过“attach”命令进行连接
####连接方法
       file pwd    --------------------------加载路径为pwd的符号表
       attach PID  --------------------------连接进程号是PID的进程
####结束调试
在完成调试之后，不要忘记用detach命令断开连接，让被调试的进程可以继续正常运行。
           detach     ---------------------------结束调试