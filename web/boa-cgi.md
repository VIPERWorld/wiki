# boa cgi 笔记

# cgi 502错误

故障表现

```
[02/Jan/2007:22:00:38 +0000] cgi_header: unable to find LFLF
```
```
<HTML><HEAD><TITLE>502 Bad Gateway</TITLE></HEAD>
<BODY><H1>502 Bad Gateway</H1>
The CGI was not CGI/1.1 compliant.
</BODY></HTML>
```

故障排除

确认cgi可以执行: 在target上执行cgi程序,比如 1.cgi
