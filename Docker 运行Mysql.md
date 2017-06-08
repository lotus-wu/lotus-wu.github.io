# Docker 运行Mysql

## 系统

CentOS 7

## 获取镜像

```
sudo docker pull mysql
sudo docker images
```

## 运行一个mysql镜像

```
sudo docker run --name first-mysql -v /data/var/mysql/:/var/lib/mysql -p 3306:3306 -e MYSQL\_ROOT\_PASSWORD=123456 -d mysql
```

上述命令各个参数含义：

```
run            运行一个容器
--name         后面是这个镜像的名称
-p 3306:3306   表示在这个容器中使用3306端口(第二个)映射到本机的端口号也为3306(第一个)
-d             表示使用守护进程运行，即服务挂在后台
```

查看当前运行的容器状态：

```
sudo docker ps

CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES5b6bf6f629bf 

mysql "docker-entrypoint.sh" 32 hours ago Up 5 hours 0.0.0.0:3306->3306/tcp first-mysql
```

想要访问mysql数据库，我的机器上需要装一个mysql-client。

```
sudo yum install mysql
```

下面我们使用mysql命令访问服务器，密码如刚才所示为123456,192.168.95.4为我这台机器的ip, 3306为刚才所示的占用本物理机的端口（不是在docker内部的端口）

```
mysql -h192.168.95.4 -P3306 -uroot -p123456
```



## 有时候遇到NAT iptable错误

重启dokcer

```
sudo systemctl restart docker
```

## 问题

无法直接使用mysql -uroot -p进行访问（待解决）

## 参考资料

1. http://www.jianshu.com/p/c24e3e5f5b58