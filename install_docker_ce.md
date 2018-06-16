# 安装 Docker CE

## 查看 Linux 内核

```bash
uname -a
Linux centos7 3.10.0-862.3.2.el7.x86_64 #1 SMP Mon May 21 23:36:36 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```

## 安装仓库

```bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum-config-manager --enable docker-ce-edge
sudo yum-config-manager --enable docker-ce-test
```

## 安装 DOCKER CE

```bash
sudo yum install docker-ce
```

## 启动 Docker

```bash
sudo systemctl start docker
```

## 验证 Docker

```bash
sudo docker run hello-world
```

## 卸载 DOCKER CE

```bash
sudo yum remove docker-ce
sudo rm -rf /var/lib/docker
```

## FAQ
* 错误信息：

```bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
已加载插件：fastestmirror, langpacks
/var/run/yum.pid 已被锁定，PID 为 3480 的另一个程序正在运行。
Another app is currently holding the yum lock; waiting for it to exit...
另一个应用程序是：PackageKit
内存：264 M RSS （834 MB VSZ）
已启动： Sat Jun 16 22:56:13 2018 - 50:12之前
状态  ：睡眠中，进程ID：3480
Another app is currently holding the yum lock; waiting for it to exit...
另一个应用程序是：PackageKit
内存：264 M RSS （834 MB VSZ）
已启动： Sat Jun 16 22:56:13 2018 - 50:14之前
状态  ：睡眠中，进程ID：3480
Another app is currently holding the yum lock; waiting for it to exit...
另一个应用程序是：PackageKit
内存：264 M RSS （834 MB VSZ）
已启动： Sat Jun 16 22:56:13 2018 - 50:16之前
状态  ：睡眠中，进程ID：3480
```

* 解决方法：

```bash
sudo rm -r /var/run/yum.pid
```

## 参考资料

* [Get Docker CE for CentOS](https://docs.docker.com/install/linux/docker-ce/centos/)
