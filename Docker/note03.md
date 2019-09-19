# 镜像的操作

> 使用国内镜像(DaoCloud-镜像https://www.daocloud.io/mirror)
```
- 使用--registry-mirror选项
  - 修改： /etc/default/docker
  - 添加：DOCKER_OPTS=“--registry-mirror=http://MIRROR-ADDR”
```

- 列出镜像
```
docker images [OPTSIONS] [REPOSITORY]
    -a --all=false
    -f --filter=[]
    --no-trunc=false
    -q --quiet=false  ---只会返回一个缩略的id
```
- 查看镜像
```
docker inspect container|image -- 可以查看容器和镜像
docker inspect REPOSITORY(仓库名)|TAG(标签名)/镜像id
```

- 删除镜像
```
docker rmi [OPTIONS] IMAGE
    -f --force=false  ----强制删除
    --no-prune=false  ----保留没有标签的镜像的父镜像
```

- 获取和推送
```
# 查找
docker serach [OPTIONS] TERM
    --automated=false Only show automated builds
    --no-trunc=false Don't truncate output
    --s --stars=0 Only displays with at least x stars

# 拉取
docker pull [OPTIONS] NAME [:TAG]
    -a --all-tags=false Download all tagged images in the repository

# 上传镜像(需要docker hub 的账号和密码)
docker push REPOSITORY_NAME
```

- 构建镜像
```
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
    -a --author=""
    -m --message=""
    -p --pause=true Pause container during commit
docker build [OPTION] PATH|URL| -(通过Dockerfile)
    --force-rm=false
    --no-cache=false
    --pull=false
    -q --quiet=false
    --rm=true
    -t --tag=""
```
