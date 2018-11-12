# 创建 JDK-MCR 镜像

## Dockerfile
```
FROM openjdk:latest

MAINTAINER Wang Junjian

RUN apt-get update && \
apt-get install -y curl wget unzip xorg

# Install MATLAB runtime
RUN \
mkdir /mcr-install && cd /mcr-install && \
wget -nv http://ssd.mathworks.com/supportfiles/downloads/R2018b/deployment_files/R2018b/installers/glnxa64/MCR_R2018b_glnxa64_installer.zip && \
unzip MCR_R2018b_glnxa64_installer.zip && \
./install -mode silent -agreeToLicense yes && \
rm -Rf /mcr-install

ENV LD_LIBRARY_PATH /usr/local/MATLAB/MATLAB_Runtime/v95/runtime/glnxa64:/usr/local/MATLAB/MATLAB_Runtime/v95/bin/glnxa64:/usr/local/MATLAB/MATLAB_Runtime/v95/sys/os/glnxa64:/usr/local/MATLAB/MATLAB_Runtime/v95/extern/bin/glnxa64
```

## 编译镜像
```bash
$ docker build -t jdk-mcr .
```

## 运行容器
```bash
$ docker run -it --name mcr jdk-mcr /bin/sh
```

## 给镜像起一个名字
```bash
$ docker tag jdk-mcr vwarship/jdk-mcr:latest
```

## 上传镜像到 Docker Hub
```bash
$ docker push vwarship/jdk-mcr:latest
```
