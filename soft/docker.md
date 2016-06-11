# host和container数据共享

[参考](https://www.digitalocean.com/community/tutorials/how-to-work-with-docker-data-volumes-on-ubuntu-14-04)

```
user@host: mkdir /tmp/m_in_host
user@host: sudo docker run -t -i -v /tmp/m_in_host:/tmp/m_in_container unikernel/mirage
```
`unikernel/mirage` 是image名称

在容器中查看

```
opam@container:/src$ ls /tmp/
m_in_container
```