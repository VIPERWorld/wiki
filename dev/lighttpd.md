# lighttpd 笔记

参考

1. http://www.cyberciti.biz/faq/howto-lighttpd-add-pcre-support/
2. http://www.ridgesolutions.ie/index.php/2013/06/05/build-cross-compile-lighttpd-for-arm-linux-with-pcre/

# 编译

## pcre

首先需要pcre

主要参考1

```
wget -c ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.34.zip # 下载
```
```
unzip pcre-8.34.zip #解压
```
```
cd pcre-8.34/
```
```
./configure --host=arm-linux CC=arm-linux-gcc AR=arm-linux-ar STRIP=arm-linux-strip RANLIB=arm-linux-ranlib --prefix='/home/zodiac1111/Downloads/lighttpd-1.4.33/install'
```

## lighttpd

```
./configure --host=arm-linux CC=arm-linux-gcc AR=arm-linux-ar STRIP=arm-linux-strip RANLIB=arm-linux-ranlib \
 --prefix='/home/zodiac1111/Downloads/lighttpd-1.4.33/install' \
PCRECONFIG='/home/zodiac1111/Downloads/lighttpd-1.4.33/install/bin/pcre-config' \
PCRE_LIB='/home/zodiac1111/Downloads/lighttpd-1.4.33/install/lib/libpcre.a' \
CFLAGS="$CFLAGS -DHAVE_PCRE_H=1 -DHAVE_LIBPCRE=1 -I/home/zodiac1111/Downloads/lighttpd-1.4.33/install/include"
```

```
make && make install
```

# 使用

复制 `lighttpd`和`libpcre.so`文件到指定目录,并做好符号连接