# Docker 跑Gitlab

## 参考资料

[大神链接](https://github.com/sameersbn/docker-gitlab)



### 使用docker-compose快速启动Gitlab

```
wget https://raw.githubusercontent.com/sameersbn/docker-gitlab/master/docker-compose.yml
docker-compose up
```

### 或者手动三步走运行GitLab容器

#### 1、运行一个PostgreSQL容器

```
docker run --name gitlab-postgresql -d \
--env 'DB_NAME=gitlabhq_production' \
--env 'DB_USER=gitlab' --env 'DB_PASS=password' \
--volume /srv/docker/gitlab/postgresql:/var/lib/postgresql \
sameersbn/postgresql:9.4-2
```

#### 2、运行一个Redis容器

```
docker run --name gitlab-redis -d \
--volume /srv/docker/gitlab/redis:/var/lib/redis \
sameersbn/redis:latest
```

#### 3、运行GitLab容器

```
docker run --name gitlab -d \
--link gitlab-postgresql:postgresql --link gitlab-redis:redisio \
--publish 10022:22 --publish 10080:80 \
--env 'GITLAB_PORT=10080' --env 'GITLAB_SSH_PORT=10022' \
--volume /srv/docker/gitlab/gitlab:/home/git/data \
sameersbn/gitlab:7.13.1
```

**注意：GitLab应用的启动需要几分钟。**