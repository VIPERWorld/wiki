# 驱动学习

# 虚拟机
参考:
* http://www.if-not-true-then-false.com/2010/install-virtualbox-guest-additions-on-fedora-centos-red-hat-rhel/
* http://rationallyparanoid.com/articles/virtualbox-centos-6.2.html

[安装笔记](vbox)

# hello模块


# kprintf 打印到控制台而不是log文件 

参考:
* http://www.cnitblog.com/textbox/archive/2009/10/13/61785.html
* http://blog.sina.com.cn/s/blog_4ba5b45e0102e537.html

先 `/proc/sys/kernel/printk` 设置打印级别,

如果无效再根据发行版查看修改 `rsyslog.conf` 配置文件

