# kindle相关

# 参考
* kindle 亚马逊 源代码 http://www.amazon.com/gp/help/customer/display.html?nodeId=200203720
* 越狱 http://www.mobileread.com/forums/showthread.php?t=198446
* [越狱应用等wiki](http://wiki.mobileread.com/wiki/Kindle_Touch_Hacking#USB_Networking) 
* 各版本原始固件 http://ixtab.tk/kindle-touch-updates.php
* usbnet登录/WiFi/ssh http://www.mobileread.com/forums/showthread.php?t=186645
* 自定义屏保 [[kindle-screensaver]]
* 让Kindle支持扫描版PDF重排,中文/pdf扫描版重排/epub,
  * 插件:[Koreader](https://github.com/koreader/koreader)
  * [让Kindle支持扫描版PDF重排(博客说明)](http://vislab.bjmu.edu.cn/blog/hwangxin/2012/10/read-scanned-pdfs-with-kindlepdfviewer/)
 * 下载 https://github.com/koreader/koreader/wiki/Download
 * mobileread http://www.mobileread.com/forums/showthread.php?t=209276
* usbnet 查询本机IP :`;711`
* 注册您的kindle时出错

其他一些指令:
```text
;dm - Dump messages to /documents
;dh - Dump cvm heap
;dt - Dump cvm stack
;shpm - set device to shipping mode
;urst - Reset user partition, deletes content of hidden System folder, Audible folder, Documents and tts folder. 
        Before using do a complete backup of your device
;debugOn - verbose logging
;debugPaint - log painting functions
;debugOff - non-verbose logging
;debugPref - pref level logging
;dP - alias of ;debugPref
;311 - change carrier settings
;411 - server information
;611 - wan information
;711 - wifi information
;fc-cache - updates fontconfig's cache, then restart the framework
;setTime - sets kindle time to unix clock
;st - alias of ;setTime (format: yyyy-mm-dd HH:MM – e.g.: ;st 2012-07-22 17:59)
~ds - Never show screen saver   (then you cannot lock the kindle till next reboot. 
                                 Rebooting the Kindle will restore the screen saver lock
                                 and, hopefully, everything goes fine!)
```