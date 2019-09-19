# 实例：创建静态网站 - 端口的映射

- 端口映射
  - -P --publish-all=true default=false  (容器所有端口进行映射)
    ```
    docker run -P -i -t ubuntu /bin/bash
    ```
  - -p --publish=[] (为指定端口进行映射)
    - containerPort (指定了容器的port， 母机的ip和port随意分配)
      ```
      docker run -p 80 -i -t ubuntu /bin/bash
      ```
    - hostPort:containerPort (指定母机和容器的port一一对应)
      ```
      docker run -p 8080:80 -i -t ubuntu /bin/bash
      ```
    - ip:ocntainerPort 
      ```
      docker run -p 0.0.0.0:80 -i -t ubuntu /bin/bash
      ```
    - ip:hostPort:containerPort
      ```
      docker run -p 0.0.0.0:8080:80 -i -t ubuntu /bin/bash
      ```


## 实例步骤
- 创建映射80端口的交互式容器
```
docker run -p 80 --name web -i -t ubuntu /bin/bash
```
- 安装Nginx
```
apt-get update
apt-get install -y nginx
apt-get install -y vim
```
- 创建静态页面
```
cd /var/www/html
vim index.html
```
- 修改Nginx配置文件
```
cd /etc/nginx/sites-enabled
# 修改 default文件里的 root 为 /var/www/html
```
- 运行Nginx
```
$ nginx
# 停止运行web后重启
docker start -i web
# 重启nginx
docker exec web nginx
```
- 访问网站
```
docker ps -- 查看容器的端口
curl http://127.0.0.1:port
docker inspect web -- 查看容器的ip
```