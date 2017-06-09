# CentOS 7 安装与初始化

## 更换源

> 参考：http://mirrors.163.com/.help/centos.html

首先备份/etc/yum.repos.d/CentOS-Base.repo

```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

下载对应版本repo文件, 放入/etc/yum.repos.d/(操作前请做好相应备份)

```
wget http://mirrors.163.com/.help/CentOS7-Base-163.repo
mv CentOS7-Base-163.repo /etc/yum.repos.d/
```

运行以下命令生成缓存

```
yum clean all
yum makecache
```

## 安装sshd

安装

```
yum install openssh-server
```

启动

```
systemctl start sshd
```

设置开机启动

```
systemctl enable sshd
```

## 调整iptables

安装iptables	

```
yum install iptables-services
```

修改配置文件

```
vi /etc/sysconfig/iptables
```

添加想开放的端口（如80)

```
-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
```

重启防火墙使配置文件生效 

```
systemctl restart iptables.service
```

设置iptables防火墙为开机启动项 

```
systemctl enable iptables.service
```

## 根据应用需要关闭SELINUX

如果某些应用和SELINUX冲突，需要关闭之

```
　vi /etc/selinux/config 
　#注释以下配置 
　SELINUX=enforcing 
　SELINUXTYPE=targeted 
　 
　#增加以下配置 
　SELINUX=disabled 
　 
　#使配置立即生效 
　setenforce 0
```

## 根据需要卸载firewalld

systemctl start firewalld

systemctl stop firewalld

yum remove firewalld

iptables好像更好用吧？卸载这个