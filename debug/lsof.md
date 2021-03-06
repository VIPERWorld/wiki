# lsof socket文件查看

> 引源:
> * http://blog.csdn.net/kozazyh/article/details/5495532
> *  linux lsof详解 http://blog.csdn.net/guoguo1980/article/details/2324454
> * 每天一个linux命令(51):lsof命令 http://www.cnblogs.com/peida/archive/2013/02/26/2932972.html
> * 使用 lsof 查找打开的文件:http://www.ibm.com/developerworks/cn/aix/library/au-lsof.html
> * `man 8 lsof` , `lsof(8)` **推荐,详细**
> * man page http://www.netadmintools.com/html/lsof.man.html


lsof - list open files

# 实际例子
一个在webbox上运行的实际例子,如下:
```
# lsof -c netcomm
COMMAND PID USER   FD   TYPE DEVICE SIZE/OFF   NODE NAME
netcomm 826 root  cwd    DIR   0,15      712     71 /data/bin
netcomm 826 root  rtd    DIR   0,12     1184      1 /
netcomm 826 root  txt    REG   0,15   226568  13313 /data/bin/netcomm
netcomm 826 root  DEL    REG    0,4               0 /SYSV000003e8
netcomm 826 root  mem    REG   0,12    21252   1302 /lib/ld-uClibc-0.9.31.so
netcomm 826 root  DEL    REG    0,4           65538 /SYSV000003e9
netcomm 826 root  mem    REG   0,12    96832 146307 /lib/libmxml.so.1
netcomm 826 root  DEL    REG    0,4           98307 /SYSV0000044c
netcomm 826 root  mem    REG   0,12   384052   1504 /lib/libuClibc-0.9.31.so
netcomm 826 root  DEL    REG    0,4          131076 /SYSV0000044d
netcomm 826 root  DEL    REG    0,4          163845 /SYSV0000044e
netcomm 826 root  mem    REG   0,12    63488   1303 /lib/libpthread-0.9.31.so
netcomm 826 root  DEL    REG    0,4          196614 /SYSV0000044f
netcomm 826 root    0r   CHR    1,3      0t0   1053 /dev/null
netcomm 826 root    1w   CHR    1,3      0t0   1053 /dev/null
netcomm 826 root    2w   CHR    1,3      0t0   1053 /dev/null
netcomm 826 root    3w   REG   0,15        1  13177 /data/logs/netcomm.log
netcomm 829 root  cwd    DIR   0,15      712     71 /data/bin
netcomm 829 root  rtd    DIR   0,12     1184      1 /
netcomm 829 root  txt    REG   0,15   226568  13313 /data/bin/netcomm
netcomm 829 root  DEL    REG    0,4               0 /SYSV000003e8
netcomm 829 root  mem    REG   0,12    21252   1302 /lib/ld-uClibc-0.9.31.so
netcomm 829 root  DEL    REG    0,4           65538 /SYSV000003e9
netcomm 829 root  mem    REG   0,12    96832 146307 /lib/libmxml.so.1
netcomm 829 root  DEL    REG    0,4           98307 /SYSV0000044c
netcomm 829 root  mem    REG   0,12   384052   1504 /lib/libuClibc-0.9.31.so
netcomm 829 root  DEL    REG    0,4          131076 /SYSV0000044d
netcomm 829 root  DEL    REG    0,4          163845 /SYSV0000044e
netcomm 829 root  mem    REG   0,12    63488   1303 /lib/libpthread-0.9.31.so
netcomm 829 root  DEL    REG    0,4          196614 /SYSV0000044f
netcomm 829 root    0r   CHR    1,3      0t0   1053 /dev/null
netcomm 829 root    1w   CHR    1,3      0t0   1053 /dev/null
netcomm 829 root    2w   CHR    1,3      0t0   1053 /dev/null
netcomm 829 root    3w   REG   0,15        1  13177 /data/logs/netcomm.log
netcomm 829 root    4u  IPv4   3523      0t0    TCP localhost:48436->115.28.134.81:www (ESTABLISHED)
```
## 内容分析

* COMMAND:netcomm 程序名称
* PID 进程号
* USER 运行该进程的用户
* FD 文件描述符
  * cwd current working directory 值表示应用程序的当前工作目录，这是该应用程序启动的目录，除非它本身对这个目录进行更改。
  * txt program text (code and data) 类型的文件是程序代码，如应用程序二进制文件本身或共享库，如上列表中显示的 /sbin/init 程序。其次数值表示应用程序的文件描述符，这是打开该文件时返回的一个整数。如上的最后一行文件/dev/initctl，其文件描述符为 10。u 表示该文件被打开并处于读取/写入模式，而不是只读(r)或只写 (w) 模式。同时还有大写 的W 表示该应用程序具有对整个文件的写锁。该文件描述符用于确保每次只能打开一个应用程序实例。初始打开每个应用程序时，都具有三个文件描述符，从 0 到 2，分别表示标准输入、输出和错误流。所以大多数应用程序所打开的文件的 FD 都是从 3 开始。
  * rtd root directory  
  * mem memory-mapped file
* Type 文件类型，如DIR、REG等
  * REG:文件
  * DIR:目录分别称为 
  * CHR:字符设备
  * BLK:块设备
  * UNIX:UNIX 域套接字
  * FIFO:先进先出 (FIFO)队列
  * IPv4:网际协议 (IP) 套接字
* DEVICE：指定磁盘的名称
* SIZE：文件的大小
* NODE：索引节点（文件在磁盘上的标识）
* NAME：打开文件的确切名称

FD的后面有1u表示：  
* r for read access.  
* w for write access.  
* u for read and write access.  

# lsof命令是什么？

可以列出被进程所打开的文件的信息。被打开的文件可以是

1. 普通的文件
2. 目录  
3. 网络文件系统的文件，
4. 字符设备文件  
5. (函数)共享库  
6. 管道，命名管道 
7. 符号链接
8. 底层的socket字流，网络socket，unix域名socket
9. 在linux里面，大部分的东西都是被当做文件的…..还有其他很多

# 怎样使用lsof

这里主要用案例的形式来介绍lsof 命令的使用

## 列出所有打开的文件:

    lsof

备注: 如果不加任何参数，就会打开所有被打开的文件，建议加上一下参数来具体定位

##  查看谁正在使用某个文件

    lsof   /filepath/file

## 递归查看某个目录的文件信息

    lsof +D /filepath/filepath2/

备注: 使用了+D，对应目录下的所有子目录和文件都会被列出

## 比使用+D选项，遍历查看某个目录的所有文件信息 的方法

    lsof | grep ‘/filepath/filepath2/’

## 列出某个用户打开的文件信息

    lsof  -u username

备注: -u 选项，u其实是user的缩写

## 列出某个程序所打开的文件信息

    lsof -c mysql

备注: -c 选项将会列出所有以mysql开头的程序的文件，其实你也可以写成 lsof | grep mysql, 但是第一种方法明显比第二种方法要少打几个字符了

## 列出多个程序多打开的文件信息

    lsof -c mysql -c apache

## 列出某个用户以及某个程序所打开的文件信息

    lsof -u test -c mysql

## 列出除了某个用户外的被打开的文件信息

    lsof   -u ^root

备注：^这个符号在用户名之前，将会把是root用户打开的进程不让显示

## 通过某个进程号显示该进行打开的文件

    lsof -p 1

## 列出多个进程号对应的文件信息

    lsof -p 123,456,789

## 列出除了某个进程号，其他进程号所打开的文件信息

    lsof -p ^1

## 列出所有的网络连接

    lsof -i

## 列出所有tcp 网络连接信息

    lsof  -i tcp

## 列出所有udp网络连接信息

    lsof  -i udp

## 列出谁在使用某个端口

    lsof -i :3306

## 列出谁在使用某个特定的udp端口

    lsof -i udp:55

特定的tcp端口

    lsof -i tcp:80

## 列出某个用户的所有活跃的网络端口

    lsof  -a -u test -i

## 列出所有网络文件系统

    lsof -N

## 域名socket文件

    lsof -u

## 某个用户组所打开的文件信息

    lsof -g 5555

## 根据文件描述列出对应的文件信息

    lsof -d description(like 2)

## 根据文件描述范围列出文件信息

    lsof -d 2-3