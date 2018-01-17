# shadowsocks安装

> [https://github.com/shadowsocks/shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev)

### 1、追加软件源

### 2.然后更新源并安装

### 3.配置 shadowsocks 文件

### 4、shadowsocks服务命令

### 5. Server ss二维码

### 6.查看端口使用情况

### 7.配置多用户模式

---

---

---

### 1、追加软件源

> debian 9

1.查看系统版本

```
root@SparkServer:~# lsb_release -a
No LSB modules are available.
Distributor ID:    Debian
Description:    Debian GNU/Linux 9.2 (stretch)
Release:    9.2
Codename:    stretch
```

```
echo "deb http://shadowsocks.org/debian stretch main" >> /etc/apt/sources.list
```

---

### 2.然后更新源并安装

```
apt-get update
apt install shadowsocks-libev

```

---

### 3.配置 shadowsocks 文件

```
root@SparkServer:/etc# cat /etc/shadowsocks-libev/config.json
{
    "server":"104.238.114.125",
    "server_port":8191,
    "local_port":1080,
    "password":"111111",
    "timeout":60,
    "method":"aes-256-cfb"
}
```

---

### 4、shadowsocks服务命令

```
# Edit the configuration file
sudo vim /etc/shadowsocks-libev/config.json

# Edit the default configuration for debian
sudo vim /etc/default/shadowsocks-libev

# Start the service
sudo /etc/init.d/shadowsocks-libev start    # for sysvinit
sudo /etc/init.d/shadowsocks-libev status
sudo /etc/init.d/shadowsocks-libev stop
sudo systemctl start shadowsocks-libev      # for systemd
```

---

### 5.Server ss二维码

> 安装连接教程:

---

### 6.查看端口使用情况

```
#netstat －antu
```

* 效果:
  ```
  :/etc/shadowsocks-libev# netstat －antu
  Active Internet connections (w/o servers)
  Proto Recv-Q Send-Q Local Address           Foreign Address         State      
  tcp        0      0 104.238.114.125.v:51322 pl-in-f188.1e100.n:5228 ESTABLISHED
  tcp        0    300 104.238.114.125.vul:ssh 218.19.138.29:20704     ESTABLISHED
  tcp        0      0 104.238.114.125.vu:8388 113.90.74.58:62990      ESTABLISHED
  tcp        0      0 104.238.114.125.vu:8388 113.90.74.58:62982      ESTABLISHED
  tcp        0      0 104.238.114.125.vu:8388 113.90.74.58:62970      TIME_WAIT  
  tcp        0      0 104.238.114.125.vu:8388 113.90.74.58:62988      ESTABLISHED
  tcp        0      0 104.238.114.125.v:47416 sea15s01-in-f14.1:https TIME_WAIT  
  tcp        0      0 104.238.114.125.v:47422 sea15s01-in-f14.1:https ESTABLISHED
  tcp        0      0 104.238.114.125.vu:8388 113.90.74.58:62993      ESTABLISHED
  tcp        0      0 104.238.114.125.vu:8388 113.90.74.58:62975      TIME_WAIT  
  tcp        0      0 104.238.114.125.vu:8388 113.90.74.58:62977      ESTABLISHED
  tcp        0      0 104.238.114.125.v:41574 sea15s01-in-f138.:https ESTABLISHED
  tcp        0      0 104.238.114.125.v:47426 sea15s01-in-f14.1:https ESTABLISHED
  tcp        0      0 104.238.114.125.v:47424 sea15s01-in-f14.1:https ESTABLISHED
  ```

---

### 7.配置多用户模式

* 1.配置教程1: [https://github.com/shadowsocks/shadowsocks-libev/issues/5](https://github.com/shadowsocks/shadowsocks-libev/issues/5)
* 2.教程2：[https://vico-song.blogspot.com/2016/12/shadowsocks-libev.html](https://vico-song.blogspot.com/2016/12/shadowsocks-libev.html)

* 2.查看版本号

```
root@SparkServer:/etc/shadowsocks-libev# ss-server -v

shadowsocks-libev 2.6.3 with mbed TLS 2.4.2

  maintained by Max Lv <max.c.lv@gmail.com> and Linus Yang <laokongzi@gmail.com>

  usage:

    ss-server
```

* 3.复制一个 config.json 文件，并修改为想要的设置

  ```
  root@SparkServer:/etc/shadowsocks-libev# cat config1.json
  {
    "server":"104.238.114.125",
    "server_port":8119,
    "local_port":1080,
    "password":"111111",
    "timeout":60,
    "method":"aes-256-cfb"
  }
  ```

* 4.然后用 ss-server 配置,配置完就重启.

  ```
  ss-server -c config1.json -f pid1
  ```

  > 如果有多个用户,就继续下面的配置\(记得要有 configX.json 文件\)

```
ss-server -c config2.json -f pid2
ss-server -c config3.json -f pid3
```

* 5.就可以看到端口已经被监听，客户端也可以科学上网了.
  ```
  #:/etc/shadowsocks-libev# netstat -tlnp
  Active Internet connections (only servers)
  Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
  tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      536/sshd            
  tcp        0      0 104.238.114.125:8388    0.0.0.0:*               LISTEN      27009/ss-server     
  tcp        0      0 104.238.114.125:8389    0.0.0.0:*               LISTEN      26987/ss-server     
  tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      689/mysqld          
  tcp6       0      0 :::80                   :::*                    LISTEN      11293/apache2       
  tcp6       0      0 :::21                   :::*                    LISTEN      559/vsftpd          
  tcp6       0      0 :::22                   :::*                    LISTEN      536/sshd
  ```



