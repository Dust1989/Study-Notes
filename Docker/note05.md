# Dockerfile 指令

> 例子
```
#First Dockerfile
FROM ubuntu:14.04
MAINTAINER dust "destiny2013@yeah.net"
RUN apt-get update
RUN apt-get install -y nginx
EXPOSE 80
```

- FROM
- MAINTAINER
- RUN -- 构建时运行的命令
- EXPOSE
- CMD -- 运行时运行的命令 - 会被run的命令覆盖
  ```
  CMD ["executable", "param1", "param2"](exec模式)
  CMD command param1 param2(shell模式)
  # 启动容器 -- 如下的命令会启动bash 而覆盖了CMD 里本来设置的命令
  docker run -p 80 -d --name ep_test01 dust1989/df_test1 /bin/bash
  ```
- ENTERYPOINT -- 运行时运行的命令 - 不会被run的命令覆盖
  ```
  ENTERYPOINT ["executable", "param1", "param2"](exec模式)
  ENTERYPOINT command param1 param2(shell模式)
  # 启动容器 -- 如下的命令bash将不会启动
  docker run -p 80 -d --name ep_test01 dust1989/df_test1 /bin/bash
  ```
- ADD -- 复制本地文件到容器目录里--和COPY的区别是能解压tar等文件--？没弄明白具体操作
  ```
  
  ```
- COPY
  ```
  COPY index.html /usr/share/nginx/html/
  ```
- VOLUME
- WORKDIR -- 指定工作目录，CMD/ENTERYPOINT 会在当前目录下运行
  ```
  WORKDIR /path/to/workdir
  ```
- ENV
- USER
- ONBUILD -- 镜像触发器- 初次构建的镜像不会执行，以这个镜像所构建的镜像就会运行这个命令(FROM 初次镜像)


## 使用Dockerfile build 构建镜像
```
# 在创建Dockerfile的目录里运行 -t 指定仓库和tag名， . 表示在Dockerfile的路径在当前目录
docker build -t="dust1989/df_test00" . 
```

> Dockerfile 构建过程
- 从基础镜像运行一个容器 (FROM ...)
- 执行一条指令， 对容器作出修改
- 执行类似docker commit的操作， 提交一个新的镜像层
- 再基于刚提交的镜像运行一个新容器
- 执行Dockerfile中的下一条指令，直至所有指令执行完毕

- 查看镜像构建的过程
  ```
  docker history [image]
  ```

- 不使用缓存构建
  ```
  docker build -t="dust1989/df_test00" --no-cache . 
  ```
