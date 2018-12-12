# 负载均衡 HAProxy

##  下载镜像
```bash
docker pull vwarship/hello-world:latest
docker pull haproxy:latest
```

## 运行 hello-world 容器，生成两个实例。
```bash
docker run --rm -p 8001:80 --name APP1 --env NAME=APP1 vwarship/hello-world:latest
docker run --rm -p 8002:80 --name APP2 --env NAME=APP2 vwarship/hello-world:latest
```

## 编写 HAProxy 配置文件：[haproxy.cfg](haproxy.cfg)

## 运行 HAProxy 容器，负载均衡生效。
```bash
docker run --rm -d --link APP1:APP1 --link APP2:APP2 -p 8000:8000 -v ~/GitHub/wang-junjian/learn-docker/load-balancing/haproxy/haproxy.cfg:/usr/local/etc/haproxy/haproxy.cfg --name haproxy haproxy
```

## 查看
* [APP1](http://localhost:8001)
* [APP2](http://localhost:8002)
* [HAProxy](http://localhost:8000)
* [HAProxy Stats](http://localhost:8000/admin?stats)

## 参考资料
