#SSH配置

查看状态:netstat -antulp | grep ssh
启动：/etc/init.d/ssh start 


###1.添加 ssh key(公钥免密登陆)。
* 1.ssh 免密登陆教程: http://www.jianshu.com/p/f5a142cf3936

ssh root@104.238.114.125



###2.用scp 上传和下载文件.
* 1.把文件上传到 /tmp,然后再把文件到需要的文件里面
```
(MBP)scp /Users/tianzeng/.ssh/id_rsa.pub git@10.100.1.217:/tmp
(服务器)mv /tmp/id_rsa.pub /home/git/.ssh/authorized_keys
```

* 2.文件下载
```
(服务器)$ scp root@45.32.24.179:/tmp/aa.test /Users/tianzeng/Desktop
```








