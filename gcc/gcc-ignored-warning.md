#各个层次的gcc警告

从上到下覆盖

##变量(代码)级:指定某个变量警告

```c
int a __attribute__ ((unused));
```

指定该变量为"未使用的".即使这个变量没有被使用,编译时也会忽略则个警告输出.

##文件级:在源代码文件中诊断(忽略/警告)

在一个c语言源文件中指定启用/忽略的警告

### 使用

在源代码中加入下面的代码

```c
#pragma GCC diagnostic [error|warning|ignored] "-W<警告选项>"
```

可能有些第版本的gcc不支持在个别函数内指定，仅支持整个文件的作用域

### 诊断-忽略:(关闭警告)

```c
#pragma  GCC diagnostic ignored  "-Wunused"
#pragma  GCC diagnostic ignored  "-Wunused-parameter"
```

### 诊断-警告:(开启警告)

```c
#pragma  GCC diagnostic warning  "-Wunused"
#pragma  GCC diagnostic warning  "-Wunused-parameter"
```

### 诊断-错误:(开启警告-升级为错误)

```c
#pragma  GCC diagnostic error  "-Wunused"
#pragma  GCC diagnostic error  "-Wunused-parameter"
```

### 一般实际用法:

在文件开头处关闭警告,在文件结尾出再开启警告,这样可以忽略该文件中的指定警告.

如果不知道什么选项.`-fdiagnostics-show-option`可以打印出什么警告.(gcc如果不行的话,clang应该可以)

##项目级:命令行/编译参数指定

警告:

```bash
gcc main.c -Wall
```

忽略:

```bash
#开启`all`警告,但是忽略 `-unused-parameter`警告
gcc mian.c -Wall -Wno-unused-parameter  
```

选项格式: `-W[no-]<警告选项>`  
如:
	-Wno-unused-parameter # no- 表示诊断时忽略这个警告

