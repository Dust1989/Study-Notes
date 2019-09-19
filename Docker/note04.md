# Docker 守护进程 - [参考](https://docs.docker.com/engine/reference/commandline/cli/)

- 查看守护进程
```
ps -ef|grep docker
sudo status docker (没用，没找到命令)
```

- 开启，关闭，重启
```
sudo service docker start
sudo service docker stop
sudo service docker restart
```