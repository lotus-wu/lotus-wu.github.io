# CentOS 7 安装Mysql

社区使用mariadb替代了mysql

```
yum install mariadb-server mariadb
systemctl start mariadb
systemctl enable mariadb
```

第一次设置下密码

```
mysqladmin -uroot passowrd "123456"	 
```

访问

```
mysql -uroot -p
```

