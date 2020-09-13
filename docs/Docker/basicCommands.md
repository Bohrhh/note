# 基本命令

## 操作

- 查看镜像： docker images  
- 运行镜像： docker run -it images_id /bin/bash  
- 安全退出容器： [ctrl + P][ctrl + Q]  
- 查看正在运行的镜像： docker ps  
- 关闭容器（限时60秒）： docker stop -t=60 容器ID或容器名  
- 杀死容器： docker kill 容器ID或容器名  
- 进入一个你正在运行的容器并打开新终端： docker exec -it container_id /bin/bash  
- 重新进入容器：docker attach container_id  
- 保存更改： docker commit -m="has update" -a="author" e218edb10161 new_image_name  
- 删除镜像： docker rmi ed9c93747fe1(imageId)  
- 搜索镜像： docker search name  
- 拉取镜像： docker pull name  
- 导出镜像：docker save imageID -o path/to/your/save.tar  
- 加载镜像：docker load -i path/to/your/save.tar  
- 重命名镜像：docker tag 镜像ID REPOSITORY:TAG  
- 查看docker空间占用：docker system df  
- 清理docker空间占用：docker system prune  
- 创建用户组：sudo groupadd docker  
- 添加用户：sudo usermod  -aG docker 用户名  
- 重启docker：sudo systemctl restart docker  
- 查看所有容器：docker ps -a  
- 重启容器：docker restart 容器ID  

## 设置

### 1. docker镜像中画图

```
# install tk first
apt install tcl-dev tk-dev python3-tk

xhost +
docker run -it \
           -v $HOME:$HOME \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -w $PWD \
           -e "DISPLAY=${DISPLAY}" \
           --gpus all \
           onnx2trt-7.0:python \
           /bin/bash
```

### 2. docker 镜像中多线程

```
docker run -it \
           -v $HOME:$HOME \
           -w $PWD \
           --ipc=host \
           --cpuset-cpus="0-15" \
           --gpus all \
           ubutnu-16.04:cuda-10.1 \
           /bin/bash
```

### 3. docker x86_64, aarch64交叉编译

```
docker run --rm --privileged multiarch/qemu-user-static:register --reset
```

### 4. docker 设备挂载

```
docker run -it \
           -v $HOME:$HOME \
           --device /dev/video0:/dev/video0 \
           hello \
           /bin/bash
```