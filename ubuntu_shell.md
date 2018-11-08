# Ubuntu Shell

## 运行 Ubuntu 进入 Shell
``` bash
$ docker run -it --name sh ubuntu /bin/sh
```

## 退出 Shell，停止容器运行。
Ctrl + D
``` bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
ec4b791fb324        ubuntu              "/bin/sh"           8 minutes ago       Exited (0) 3 seconds ago                       sh
```

## 退出 Shell，容器正常运行。
Ctrl + P, Ctrl + Q

``` bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
b330b6e30253        ubuntu              "/bin/sh"           27 seconds ago      Up 26 seconds                           sh
```
