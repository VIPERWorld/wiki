# mini2440 uboot

使用buildroot编译uboot.

* [目录](customize-mini2440-softwave) 

## 清单

* uboot源代码
 * buildroot 自动下载通用的uboot(未包含mini2440的配置) 推荐进阶玩家
 * 为mini2440[定制的uboot](http://wiki.linuxmce.org/index.php/Mini2440),推荐新手,或者对搭建的环境进行测试时使用.
* usb下载软件
 * [dnw-linux](https://github.com/changbindu/dnw-linux) linux的dnw.进阶使用,或者前者不能使用时.可能遇到的问题见"故障排除"

1. `make menuconfig` 
2. Bootloaders 
3. U-Boot 
4. U-Boot board name `smdk2410` 硬件密切相关  
 在`output/build/uboot-2013.04/board`目录文件夹名称

## 在原有的vivi bootloader情况下安装uboot.

mini2440版本的uboot http://wiki.linuxmce.org/index.php/Mini2440

在linux通过usb下载uboot到mini2440开发板上的软件 https://github.com/changbindu/dnw-linux

1. mini2440 官方nor模式进入vivi bootloader.
2. a
3. host上执行 `dnw -a 33f80000 uboot.bin`  # 33f80000 这个数字由硬件决定
4. 开发板关机,切换到nand模式开机
5. minicom上任意键,停在uboot界面
6. 今后从nand flash启动就是都由uboot引导了.

可能是我的nand flash有问题,`saveenv`时只能停在擦出界面,所以在`/include/configs/mini2440.h`文件中修改了一些默认的参数,如主机和目标板的IP地址等.

http://wiki.linuxmce.org/index.php/Mini2440中提到的usb下载工具无效的情况下可以使用dnw按照以上步骤试试.如果wiki页面提到的方法有下,则推荐使用其方式.

## 在已经有uboot的情况下安装/更新 uboot

推荐 Tekkaman 的 http://u-boot-all-in-one.googlecode.com/files/mini2440%E4%B9%8BU-boot%E7%A7%BB%E6%A4%8D%E8%AF%A6%E7%BB%86%E6%89%8B%E5%86%8C-20100419.pdf 

## 故障排除

### dnw

1. 可能需要手动加载驱动 `insmod secbulk.ko`
2. `dnw.rules`文件陈旧可能不能实现非root用户操作,
 * 使用root用户(不推荐) 或
 * 修改/增加`/etc/udev/rules.d/dnw.rules`文件:
   ```
   SUBSYSTEMS=="usb", ATTRS{idVendor}=="5345", ATTRS{idProduct}=="1234", GROUP="users", MODE="0666"
   ```