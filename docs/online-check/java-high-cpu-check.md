## JAVA故障定位—CPU占用率高
一个应用的CPU占有率，除了是计算密集型应用外，通常原因是出现了死循环。
该文章介绍下如何定位发现和解决问题
<img src="https://cdn.jsdelivr.net/gh/shaofeng-c/CodeGuide@master/assets/img/Fj6XQA.png" width="75%">
（随便找的图 😄）
根据top命令，发现PID为xxxx的Java进程占用CPU高达200%，出现故障。

我们可以以下命令进一步确定故障的应用
```shell
    $ ps -aux | grep PID
````
但如何定位到具体的线程和代码呢？
```shell
    ps -mp PID -o THREAD,tid,time
````
<img src="https://cdn.jsdelivr.net/gh/shaofeng-c/CodeGuide@master/assets/img/OvJ9MU.png" width="75%">
找到CPU占有最高的线程20048（假设），将对应的线程id转换成16进制格式：
```shell
    printf "%x\n" TID
````
最好使用打印线程的堆栈信息：
```shell
    jstack PID | grep TID -A 60
````
找出出现问题的代码

> **最后，总结下排查CPU故障的方法和技巧有哪些：**
>
> 1. top命令：Linux命令。可以查看实时的CPU使用情况。也可以查看最近一段时间的CPU使用情况。
> 2. PS命令：Linux命令。强大的进程状态监控命令。可以查看进程以及进程中线程的当前CPU使用情况。属于当前状态的采样数据。
> 3. jstack：Java提供的命令。可以查看某个进程的当前线程栈运行情况。根据这个命令的输出可以定位某个进程的所有线程的当前运行状态、运行代码，以及是否死锁等等。
> 4. jstack：Linux命令。可以查看某个进程的当前线程栈运行情况。


