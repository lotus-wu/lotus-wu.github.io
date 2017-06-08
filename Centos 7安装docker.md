# Centos 7安装docker

## 参考资料

[官网链接](https://store.docker.com/editions/community/docker-ce-server-centos?tab=description)

[Docer-compose资料](http://blog.csdn.net/yulei_qq/article/details/52984334)



## 操作步骤

### 1. Set up the repository

Set up the Docker CE repository on CentOS:

```
sudo yum install -y yum-utils

sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

sudo yum makecache fast
```

### 2. Get Docker CE

Install the latest version of Docker CE on CentOS:

```
sudo yum -y install docker-ce
```

Start Docker:

```
sudo systemctl start docker
```

使doker开机启动

```
systemctl enable docker
```



### 3. Test your Docker CE installation

Test your installation:

```
sudo docker run hello-world
```
## 4.Install docker-compose

安装python-pip

```
 yum -y install epel-release
 yum install python-pip
```

对安装好的pip进行升级 

```
 pip install --upgrade pip
```

安装docker-compose

```
pip install docker-compose
```

