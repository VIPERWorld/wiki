# find 简单使用

查找

    find -name april* 在当前目录下查找以april开始的文件

    find /tmp -name wa* -type l 在/tmp下查找名为wa开头且类型为符号链接的文件

执行

    find -mmin -60 -exec ls -l {} \;

    find -iname *.wav  -exec flac {} \; 转换所有wav到flac


详细

```bash
find path -option [ -print ] [ -exec -ok command ] {} \;
#-print 将查找到的文件输出到标准输出
#-exec command {} \; —–将查到的文件执行command操作,{} 和 \;之间有空格
#-ok 和-exec相同，只不过在操作前要询用户
```

# 参考
* [能否查找或显示指定多个后缀名的文件](http://bbs.chinaunix.net/thread-1924056-1-1.html)