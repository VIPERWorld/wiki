# pppd 笔记

> * http://www.apinpai.com/b53019/

一个ppp会话分为四个步骤:

1. 连接建立
2. 连接质量控制
3. 网络层协议配置
4. 连接终止；

linux下脚本拨号的过程:

1. 由pppd程序调用chat会话程序
2. 由pppd程序继续chat会话程序的工作，与服务器端的pppd程序进行握手，建立ppp连接
3. chat会话程序负责拨号，启动服务器端的pppd程序，验证身份，然后chat会话程序结束

启动脚本

```
pppd call <脚本名称>
pppd call tdscdma &
```
脚本内容
```bash
# cat tdscdma
nodetach
lock
/dev/ttyS4 # 串口设备文件 
115200 # 波特率
user "cmnet" #APN
crtscts
modem
hide-password
usepeerdns
noauth
noipdefault
novj
debug
novjccomp
noccp
defaultroute
ipcp-accept-local
ipcp-accept-remote
connect 'chat -s -v -f /etc/ppp/peers/chat-tdscdma-connect'  # 连接脚本
disconnect 'chat -s -v -f /etc/ppp/peers/chat-tdscdma-disconnect' #断线脚本
```

# 调试

参考一个例子 http://www.spinics.net/lists/linux-ppp/msg01283.html

追踪

```bash
root@mymachine:~# strace -e trace=open,close,ioctl pppd dump debug nodetach call gprs
```