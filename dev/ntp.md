# The Network Time Protocol 移植

版本: 4.2.6p5	2011/12/24 稳定版

# 参考

1. 官网: http://www.ntp.org/
2. 交叉编译可能的一些错误 http://bbs.21ic.com/blog-134715-99647.html
3. ntpd 和 ntpdate 区别(慢慢调整和跳变的区别) http://scoke.blog.51cto.com/769125/491419
4. 配置文件 `/etc/ntp.conf`
5. 国内一些ntp服务器 http://www.douban.com/note/171309770/
6. `/etc/TZ` 一些示例时区 http://zzgthk.iteye.com/blog/1935876

# 配置
```
./configure \
--host=arm-linux \
CC=arm-linux-gcc \
--prefix='/home/zodiac1111/Downloads/ntp-4.2.6p5/_install' 
```

* prefix 必须绝对路径
# 安装

```
make && make install
```

# 配置文件