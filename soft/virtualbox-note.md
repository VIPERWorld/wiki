# Virtualbox 相关笔记

# 安装增强功能(共享目录等)

为Virtualbox中的虚拟机(CentOS)安装增强功能(共享目录等)

安装失败,查看日志

需要当前 kernel 源代码

安装以下三个包 (kernel-headers, kernel-devel, gcc):

    [root@Linux ]# yum install kernel-headers kernel-devel gcc

Your system will install the packages above if they aren't installed already, plus the package   dependencies. Next confirm the version of your current kernel release 验证是否一致 :

    [root@Linux ]# uname -r
    2.6.32-220.2.1.el6.i686

Check /usr/src/kernels/ to confirm that a directory for the version of your current kernel release exists (this directory should exist after the installation of the packages above):

    [root@Linux ]# ls /usr/src/kernels/
    2.6.32-220.2.1.el6.i686

参考:
* http://rationallyparanoid.com/articles/virtualbox-centos-6.2.html

# 向虚拟机发送`<Ctrl+Alt+Fn>`

使用 `<HOST+Fn>` 替代.默认HOST为右Ctrl.

参考:
* http://blog.tordeu.com/?p=322
* http://ubuntuforums.org/showthread.php?t=723819

