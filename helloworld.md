# helloworld

## app.py
```py
from flask import Flask
import socket
import os

app = Flask(__name__)

@app.route('/')
def hello():
    html = "<h3>Hello {name}!</h3>" \
           "<b>Hostname:</b> {hostname}<br/>"           
    return html.format(name=os.getenv("NAME", "world"), hostname=socket.gethostname())
    
if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## requirements.txt
```
Flask
```

## Dockerfile
```
# 使用官方提供的 Python 开发镜像作为基础镜像
FROM python:3.6-slim

# 将工作目录切换为 /app
WORKDIR /app

# 将当前目录下的所有内容复制到 /app 下
ADD . /app

# 使用 pip 命令安装这个应用所需要的依赖
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# 允许外界访问容器的 80 端口
EXPOSE 80

# 设置环境变量
ENV NAME vwarship

# 设置容器进程为：python app.py，即：这个 Python 应用的启动命令
CMD ["python", "app.py"]
```

## 编译镜像
```bash
$ docker build -t helloworld .
```

## 查看镜像
```bash
$ docker images

REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
helloworld            latest              4fcaa1b2e820        3 minutes ago       148MB
python                3.6-slim            74e41a603f31        4 days ago          138MB
```

## 运行容器
```bash
$ docker run -p 4000:80 helloworld

$ curl http://localhost:4000/
<h3>Hello vwarship!</h3><b>Hostname:</b> 04ee24b61b94<br/>
```

## 查看容器
```bash
$ docker ps

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                  NAMES
04ee24b61b94        helloworld          "python app.py"     2 minutes ago       Up 2 minutes        0.0.0.0:4000->80/tcp   stoic_kepler
```

## 给镜像起一个名字
```bash
$ docker tag helloworld vwarship/helloworld:v1
```

## 上传镜像到 Docker Hub
```bash
$ docker push vwarship/helloworld:v1
```