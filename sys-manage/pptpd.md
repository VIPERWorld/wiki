# pptpd 服务器,安装配置


安装服务器教程

1. http://www.ebayram.net/howto-vpn-pptp-server-debian-ubuntu/
2. http://www.networkinghowtos.com/howto/configure-a-pptp-vpn-server-on-ubuntu-linux/
3. 详细(包括客户端设置) http://www.howtogeek.com/51237/setting-up-a-vpn-pptp-server-on-debian/
4. windowXP 不代替默认路由(连上vpn还可以通过本机访问互联网,而不是通过vpn访问互联网) http://service.tp-link.com.cn/detail_article_414.html

其他一些客户端设定 [[pptp]] 

路由.网络操作 [[ifconfig]]

```text
# 查看状态
sudo service pptpd status 
sudo service pptpd restart #重启
#服务器配置
sudo vim /etc/pptpd.conf
#服务器选项
sudo vim /etc/ppp/pptpd-options
# 这种加密的用户管理
sudo vim /etc/ppp/chap-secrets 

```

# 更多的IP

给客户端分配更多ip地址: 笨办法 http://serverfault.com/questions/512751/more-than-254-client-ips-in-pptp-pptpd

    remoteip 192.168.0.2-254,192.168.1.2-254

# 转发客户端之间

http://superuser.com/questions/516634/pptp-linux-clients-unreachable

http://www.net-gyver.com/?p=1317

使能转发 

    echo 1 > /proc/sys/net/ipv4/ip_forward

或者
    
    sysctl -w net.ipv4.ip_forward=1

IPtable

    iptalebs -A FORWARD -s 10.0.0.0/8 -d 10.0.0.0/8 -j ACCEPT