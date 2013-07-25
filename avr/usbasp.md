# usbasp 笔记

在Linux(Fedora 18 i686)下,使用山寨usbasp硬件,ATmage8单片机最小系统和avrdude下载软件实现avr程序下载.

# 硬件

山寨硬件来源 [淘宝](http://item.taobao.com/item.htm?spm=0.0.0.0.brf3fj&id=4207291768)

分析发现改下载器基本基于 [这个](http://www.fischl.de/usbasp/). 

`lsusb`信息:
```
Bus 003 Device 017: ID 16c0:05dc Van Ooijen Technische Informatica shared ID for use with libusb
```

`dmesg`信息:
```
[64836.140363] usb 3-2: USB disconnect, device number 18
[64838.871009] usb 3-2: new low-speed USB device number 19 using xhci_hcd
[64838.888095] usb 3-2: New USB device found, idVendor=16c0, idProduct=05dc
[64838.888099] usb 3-2: New USB device strings: Mfr=1, Product=2, SerialNumber=0
[64838.888102] usb 3-2: Product: USBasp
[64838.888104] usb 3-2: Manufacturer: www.fischl.de
```

按照官方(原版)说明:

>On Linux and MacOS X **no** kernel driver is needed.

不需要驱动,很好.在本人的fedora18上也测试通过.

# 软件

> [AVRDUDE](http://www.nongnu.org/avrdude/) is an utility to download/upload/manipulate the ROM and EEPROM contents of AVR microcontrollers using the in-system programming technique (ISP).

支持多种下载器硬件(上面这种也支持).中文介绍: http://blog.21ic.com/user1/69/archives/2005/1551.html .

# 测试

## 需要root权限

没有权限,需要root

```
$ avrdude -cusbasp -pm8 -F
avrdude: Warning: cannot open USB device: Permission denied
avrdude: error: could not find USB device "USBasp" with vid=0x16c0 pid=0x5dc

avrdude done.  Thank you.
```

## 下载器硬件测试

仅连接下载器,不连接开发板,测试

```
# avrdude -cusbasp -pm8 -F

avrdude: warning: cannot set sck period. please check for usbasp firmware update. 
avrdude: error: programm enable: target doesn't answer. 1 
avrdude: initialization failed, rc=-1
avrdude: AVR device initialized and ready to accept instructions
avrdude: Device signature = 0x000000
avrdude: Yikes!  Invalid device signature.
avrdude: Expected signature for ATMEGA8 is 1E 93 07

avrdude done.  Thank you.
```

* `-cusbasp` 指定usbasp下载器类型
* `-pm8` 指定单片机类型,这里什么类型不重要,因为根本没有连接单片机,这一步仅测试下载器
* `-F` 强制执行,因为没有连接单片机,所以会显示错误,所以强制执行.

这时会看到代表数据的红色led闪烁一下.基本表示软硬件连接成功.

# 连上单片机测试

这个时候连上mega8单片机最小系统.再次执行
```
avrdude -cusbasp -pm8 
```
得到的显示:

```
avrdude: warning: cannot set sck period. please check for usbasp firmware update.
avrdude: AVR device initialized and ready to accept instructions

Reading | ################################################## | 100% 0.00s

avrdude: Device signature = 0x1e9307

avrdude: safemode: Fuses OK

avrdude done.  Thank you.
avrdude: warning: cannot set sck period. please check for usbasp firmware update.
avrdude: AVR device initialized and ready to accept instructions

Reading | ################################################## | 100% 0.00s

avrdude: Device signature = 0x1e9307

avrdude: safemode: Fuses OK

avrdude done.  Thank you.
```
恩,正确识别的单片机 :D