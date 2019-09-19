# Docker 基础 
 
- Docker的基本组成
    - Docker Client
    - Docker Daemon
    - Docker Image
    - Docker Container
    - Docker Registry

- Docker依赖Linux内核特性
    - Namespaces命名空间
    - Control groups(cgroups) 控制组

## Docker使用

- 使用非root用户： (ubuntu下没有效果，登出后再登入也没有效果， 重启后就解决了)
    - $ sudo groupadd docker
    - $ sudo gpasswd -a ${USER_NAME} docker
    - $ sudo service docker restart

```
docker version
# 到仓库查找应用
docker search app_name
# 下载应用
docker pull app_name
```

- container 命令
```
# 运行container - 例：运行ubuntu 打出 'Hello world' 这种属于一次性的启动， 结束后自动停止容器
docker run ubuntu echo 'Hello world' 

# 持续启动交互的容器 - 启动了ubuntu 启动了bash 进入了交互模式(i-interactive, t-tty)
docker run -i -t ubuntu /bin/bash
Ctrl + P -> Ctrl + Q 能以守护形式运行容器

# 重新进入交互模式
docker attach 容器id

# 以守护形式运行容器 - 例： 运行一个shell命令 每个一秒 echo hello world
docker run --name dc1 -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done" 

# 查看容器日志
docker logs [-f] [-t] [--tail] 容器名
    -f --follows=true default=false
    -t --timestamps=true default=false
    --tail='all' 要加数字 表示显示尾部多少行

# 查看容器信息
docker top 容器名

# 在已有容器里启动新的进程
docker exec [-d] [-i] [-t] 容器名 [command] [arg]

# 停止容器
docker stop 容器名 -- 等待容器停止
docker kill 容器名 -- 强制停止

# 查看容器 (a-所有容器， l-最新容器)
docker ps [-a] [-l]

# 查看容器信息
docker inspect 容器名/容器id

# 启动容器时自定义名称
docker run --name=自定义名 -i -t ubuntu /bin/bash

# 重启停止的容器
docker start -i 容器名

# 删除容器-只能删除已停止的容器
docker rm 容器id
```