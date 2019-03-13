# Docker 命令

## 搜索镜像（Docker Hub）
``` bash
$ docker search busybox
NAME                        DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
busybox                     Busybox base image.                             1381                [OK]                
progrium/busybox                                                            68                                      [OK]
hypriot/rpi-busybox-httpd   Raspberry Pi compatible Docker Image with a …   44                                      
radial/busyboxplus          Full-chain, Internet enabled, busybox made f…   20                                      [OK]
hypriot/armhf-busybox       Busybox base image for ARM.                     9                                       
```

## 显示镜像
```bash
$ docker images

REPOSITORY                  TAG                 IMAGE ID            CREATED             SIZE
nginx                       latest              dbfc48660aeb        5 days ago          109MB
python                      3.6-slim            74e41a603f31        11 days ago         138MB
busybox                     latest              59788edf1f3e        2 weeks ago         1.15MB
```

## 删除镜像
```bash
$ docker rmi busybox:latest

Untagged: busybox:latest
Deleted: sha256:59788edf1f3e78cd0ebe6ce1446e9d10788225db3dedcfd1a59f764bad2b2690
Deleted: sha256:8a788232037eaf17794408ff3df6b922a1aedf9ef8de36afdae3ed0b0381907b
```

## 拉取镜像
```bash
$ docker pull busybox:latest

latest: Pulling from library/busybox
90e01955edcd: Pull complete 
Digest: sha256:2a03a6059f21e150ae84b0973863609494aad70f0a80eaeb64bddd8d92465812
Status: Downloaded newer image for busybox:latest
```

## 导出镜像
```bash
$ docker save -o busybox.tar busybox:latest
```

## 导入镜像
```bash
$ docker load -i busybox.tar 
```

## 构建镜像
```bash
$ docker build -t test .
```

## 查看镜像的层
```bash
$ docker history busybox:latest
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
59788edf1f3e        5 months ago        /bin/sh -c #(nop)  CMD ["sh"]                   0B                  
<missing>           5 months ago        /bin/sh -c #(nop) ADD file:63eebd629a5f7558c…   1.15MB              
```
  > docker history 的输出中的 \<missing\> 行指示那些层在其他系统上构建并且已经不可用了，可以忽略这些。

## 运行容器
```bash
$ docker run --name test busybox:latest echo Hello World
Hello World
```

## 显示容器（-a 隐藏的容器也显示，不加-a只显示运行的容器）
```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS                      PORTS               NAMES
eefda2f06583        busybox:latest      "echo Hello World"   12 seconds ago      Exited (0) 11 seconds ago                       test
```

## 删除容器
```bash
$ docker rm test
test
```

## 容器运行完自动删除
```bash 
$ docker run --rm --name auto-exit-test busybox:latest echo Hello World
Hello World
```

## 删除当前所有容器
```bash
$ docker rm -vf $(docker ps -a -q)
```

## 删除当前状态为退出的所有容器
* 方法1
```bash
$ docker container prune

WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
```

* 方法2
```bash
$ docker rm $(docker ps -q -f status=exited)
```

## 启动容器
```bash
$ docker start test
```

## 暂停容器
```bash
$ docker stop test
```

## 查看容器日志
```bash
$ docker logs test
```

## 查看容器更改
```bash
$ docker-training wjj$ docker run -it --name test busybox:latest
/ # touch log.txt

$ docker diff test
A /log.txt
C /root
A /root/.ash_history
```

## 在后台运行一个容器
```bash
$ docker run --detach --name test busybox:latest sleep 10000
```

## 在容器中运行的进程
```bash
$ docker exec test ps

PID   USER     TIME  COMMAND
    1 root      0:00 sleep 10000
    8 root      0:00 ps
```

## 查看容器的环境变量
```bash
$ docker exec test env

PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=1b350cb662c0
HOME=/root
```

## 设置环境变量
```bash
$ docker run --rm -p 8001:80 --name APP1 --env NAME=APP1 vwarship/hello-world:latest
```

## 自动重启容器，使用回退策略
```bash
$ docker run -d --name backoff-detector --restart always busybox:latest date

$ docker logs backoff-detector

Sun Oct 21 10:39:47 UTC 2018
Sun Oct 21 10:39:48 UTC 2018
Sun Oct 21 10:39:50 UTC 2018
Sun Oct 21 10:39:51 UTC 2018
Sun Oct 21 10:39:53 UTC 2018
Sun Oct 21 10:39:55 UTC 2018
Sun Oct 21 10:39:59 UTC 2018
Sun Oct 21 10:40:06 UTC 2018
Sun Oct 21 10:40:19 UTC 2018
Sun Oct 21 10:40:45 UTC 2018
```

## 参考资料
* [如何批量删除Docker中已经停止的容器](https://www.linuxidc.com/Linux/2018-02/150708.htm)
