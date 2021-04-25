#e大v4部署N1
```
docker run -dit \
   -v /jd/config:/jd/config \
   -v /jd/log:/jd/log \
   -v /jd/scripts:/jd/scripts \
   -v /jd/own:/jd/own \
   -p 5678:5678 \
   -e ENABLE_HANGUP=true \
   --net host \
   --name jd \
   --hostname jd \
   --restart always \
   nevinee/jd:v4
```

##多容器配置

#要想换库直接改最后一行
```
docker run -dit \
    -v /你想保存的目录/jd1/config:/jd/config `# 配置保存目录，冒号左边请修改为你想存放的路径`\
    -v /你想保存的目录/jd1/log:/jd/log `# 日志保存目录，冒号左边请修改为你想存放的路径` \
    -v /你想保存的目录/jd1/scripts:/jd/scripts  `# 脚本文件目录，映射脚本文件到安装路径` \
    -v /你想保存的目录/jd/own:/jd/own \
    -p 5679:5678 \
    -e ENABLE_HANGUP=true \
    -e ENABLE_WEB_PANEL=true \
    -e ENABLE_WEB_TTYD=true \
    --name jd1 \
    --hostname jd1 \
    --restart always \
    nevinee/jd:v4
```

##自动更新Docker容器（也就是更新京东文件）
```
docker run -d \
        --name watchtower \
        -v /var/run/docker.sock:/var/run/docker.sock \
        containrrr/watchtower
```

##创建后使用`docker logs -f jd`查看创建日志，直到出现容器启动成功…字样才代表启动成功（不是以此结束的请更新镜像），按Ctrl+C退出查看日志。

#v4更新命令
```
docker exec -it jd bash jup
```
##安装v4面板

#先进入容器

```
docker exec -it jd bash
```
```
wget -q https://ghproxy.com/https://raw.githubusercontent.com/tm309/abc/main/v4mb.sh -O v4mb.sh && chmod +x v4mb.sh && ./v4mb.sh
```
#重启后手动运行面板

```
docker exec -it jd bash jup
```
