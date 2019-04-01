# 安装 Docker CE

## 查看 Linux 内核

```bash
uname -a
Linux centos7 3.10.0-862.3.2.el7.x86_64 #1 SMP Mon May 21 23:36:36 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```

## 在线安装 DOCKER CE

### Ubuntu18
* 更新apt包索引
```bash
sudo apt-get update
```

* 安装包以允许apt通过HTTPS使用存储库
```bash
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

* 添加Docker的官方GPG密钥
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

* 使用以下命令设置稳定存储库
```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

* 更新apt包索引
```bash
sudo apt-get update
```

* 安装最新版本的Docker CE和containerd
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### CentOS7
* 安装仓库
```bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum-config-manager --enable docker-ce-edge
sudo yum-config-manager --enable docker-ce-test
```

* 安装 DOCKER CE
```bash
sudo yum install docker-ce
```

* 启动 Docker
```bash
sudo systemctl start docker
```

* 卸载 DOCKER CE
```bash
sudo yum remove docker-ce
sudo rm -rf /var/lib/docker
```

### 验证 Docker
```bash
sudo docker run hello-world
```

## 离线安装 DOCKER CE

### Ubuntu18
* 安装 gcc
```bash
apt-get download binutils binutils-common binutils-x86-64-linux-gnu cpp cpp-7 gcc-7 gcc-7-base libasan4 libatomic1 libbinutils libc-dev-bin libc6-dev libcc1-0 libcilkrts5 libgcc-7-dev libgomp1 libisl19 libitm1 liblsan0 libmpc3 libmpfr6 libmpx2 libquadmath0 libtsan0 libubsan0 linux-libc-dev manpages manpages-dev
apt-get download  gcc

dpkg -i *.deb

gcc --version
```

* 安装 make
```bash
apt-get download make

dpkg -i *.deb

make --version
```

* [下载安装包](https://download.docker.com/linux/ubuntu/dists/)（containerd.io, docker-ce-cli, docker-ce）
```bash
wget https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/containerd.io_1.2.2-3_amd64.deb
wget https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce-cli_18.09.2~3-0~ubuntu-bionic_amd64.deb
wget https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce_18.09.2~3-0~ubuntu-bionic_amd64.deb
```

* 安装
```bash
dpkg -i *.deb
```

### CentOS7
* CentOS镜像
```txt
重庆大学镜像：http://b.mirrors.lanunion.org/CentOS/
中国科学技术大学镜像：http://centos.ustc.edu.cn/centos/
上海交通大学镜像：http://ftp.sjtu.edu.cn/centos/
华中科技大学镜像：http://mirrors.hust.edu.cn/centos/
北京理工大学镜像：http://mirror.bit.edu.cn/centos/
西北农林科技大学镜像：http://mirrors.nwsuaf.edu.cn/centos/
大连东软信息学院镜像：http://mirrors.neusoft.edu.cn/centos/
网易镜像：http://mirrors.163.com/centos/
清华大学镜像：https://mirrors.tuna.tsinghua.edu.cn/centos/
```

* 安装 gcc
```bash
curl -O https://mirrors.tuna.tsinghua.edu.cn/centos/7.6.1810/os/x86_64/Packages/mpfr-3.1.1-4.el7.x86_64.rpm
curl -O https://mirrors.tuna.tsinghua.edu.cn/centos/7.6.1810/os/x86_64/Packages/libmpc-1.0.1-3.el7.x86_64.rpm
curl -O https://mirrors.tuna.tsinghua.edu.cn/centos/7.6.1810/os/x86_64/Packages/kernel-headers-3.10.0-957.el7.x86_64.rpm
curl -O https://mirrors.tuna.tsinghua.edu.cn/centos/7.6.1810/os/x86_64/Packages/glibc-headers-2.17-260.el7.x86_64.rpm
curl -O https://mirrors.tuna.tsinghua.edu.cn/centos/7.6.1810/os/x86_64/Packages/glibc-devel-2.17-260.el7.x86_64.rpm
curl -O https://mirrors.tuna.tsinghua.edu.cn/centos/7.6.1810/os/x86_64/Packages/cpp-4.8.5-36.el7.x86_64.rpm
curl -O https://mirrors.tuna.tsinghua.edu.cn/centos/7.6.1810/os/x86_64/Packages/libgomp-4.8.5-36.el7.x86_64.rpm
curl -O https://mirrors.tuna.tsinghua.edu.cn/centos/7.6.1810/os/x86_64/Packages/gcc-4.8.5-36.el7.x86_64.rpm

rpm -ivh mpfr-3.1.1-4.el7.x86_64.rpm 
rpm -ivh libmpc-1.0.1-3.el7.x86_64.rpm 
rpm -ivh kernel-headers-3.10.0-957.el7.x86_64.rpm 
rpm -ivh glibc-headers-2.17-260.el7.x86_64.rpm 
rpm -ivh glibc-devel-2.17-260.el7.x86_64.rpm 
rpm -ivh cpp-4.8.5-36.el7.x86_64.rpm 
rpm -ivh libgomp-4.8.5-36.el7.x86_64.rpm 
rpm -ivh gcc-4.8.5-36.el7.x86_64.rpm 

gcc --version
```

* 安装 make
```bash
curl -O https://mirrors.tuna.tsinghua.edu.cn/centos/7.6.1810/os/x86_64/Packages/make-3.82-23.el7.x86_64.rpm

rpm -ivh make-3.82-23.el7.x86_64.rpm

make --version
```

* 安装 Docker CE
```bash
curl -O https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.2-3.3.el7.x86_64.rpm
curl -O https://download.docker.com/linux/centos/7/x86_64/stable/Packages/docker-ce-selinux-17.03.3.ce-1.el7.noarch.rpm
curl -O https://download.docker.com/linux/centos/7/x86_64/stable/Packages/docker-ce-cli-18.09.2-3.el7.x86_64.rpm
curl -O https://download.docker.com/linux/centos/7/x86_64/stable/Packages/docker-ce-18.09.2-3.el7.x86_64.rpm

rpm -ivh containerd.io-1.2.2-3.3.el7.x86_64.rpm
rpm -ivh docker-ce-selinux-17.03.3.ce-1.el7.noarch.rpm
rpm -ivh docker-ce-cli-18.09.2-3.el7.x86_64.rpm
rpm -ivh docker-ce-18.09.2-3.el7.x86_64.rpm
```

## [安装 Docker Compose](https://docs.docker.com/compose/install/)
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
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
* [Get Docker CE for Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
* [CentOS离线安装GCC编译环境](https://www.bbsmax.com/A/ke5jV9g95r/)
* [Linux离线安装GCC](https://cloverat.github.io/2018/03/23/linux/[linux]离线安装GCC/)
