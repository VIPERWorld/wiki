# 打印错误可警告

> http://my.oschina.net/mingtingling/blog/118588

g纠结了半天，才发现问题的症结:原来的PHP 关闭了错误的显示。

下面讲解如何开启错误提示步骤：

1. 打开`php.ini`文件  
以我的ubuntu10.10为例，这个文件在： `/etc/php5/apache2` 目录下。

2. 搜索并修改下行，把Off值改成On
```
display_errors = Off
```

3. 搜索下行
```
error_reporting = E_ALL & ~E_NOTICE
```
或者搜索：
```
error_reporting = E_ALL & ~E_DEPRECATED
```
修改为
```
error_reporting = E_ALL | E_STRICT
```

4. 修改Apache的`httpd.conf`或者`apace2.conf`(debian)，
以我的 Ubuntu 为例， 这个文件在：`/etc/apache2/`  目录下，这是一个空白文件。
添加以下两行：
```
php_flag display_errors        on
php_value error_reporting       2039
```
5. 重启Apache，就OK了。
重启命令
```
sudo /etc/init.d/apache2 restart
```

# mysql 数据库警告

```
Warning: mysql_free_result() expects parameter 1 to be resource, boolean given in 
```
只有select等语句需要释放资源,如添加和更新操作是不需要释放支援的. 其是一个布尔型的返回值

> http://stackoverflow.com/questions/14527864/mysql-free-result-expects-parameter-1-to-be-resource

> mysql_query() only returns a resource for SELECT, SHOW, EXPLAIN, and DESCRIBE queries.