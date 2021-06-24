# 软件安装

## docker
```
# 卸载旧版
sudo apt-get remove docker docker-engine docker.io containerd runc

# 安装
sudo apt-get update
# 依赖
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
# 添加 Docker 的官方 GPG 密钥
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
# 验证现在是否拥有带有指纹的密钥
sudo apt-key fingerprint 0EBFCD88
# 使用以下指令设置稳定版仓库
sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"
# 安装
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## docker-compose
```
# 下载：
# 从 https://github.com/docker/compose/releases
# 选择对应版本，如 docker-compose-Linux-x86_64 

sudo mv docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

## nvidia driver
[驱动下载地址](https://www.nvidia.com/Download/index.aspx)
```
sudo service lightdm stop
sudo chmod a+x NVIDIA-Linux-x86_64-440.31.run
sudo sh ./NVIDIA-Linux-x86_64-440.31.run --no-opengl-files
sudo service lightdm start
```

## opencv
[opencv 源码下载地址](https://opencv.org/releases/)
```
# 依赖
# 可能会遇到 Unable to locate package libjasper-dev
# 需要安装 add-apt-repository: 
# sudo apt-get install software-properties-common
# sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
# sudo apt-get update

sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev

# 安装
cd opencv-3.4.3/
mkdir build && cd build
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..
make -j7
sudo make install

```


## 搜狗输入法
- [软件下载页面](https://pinyin.sogou.com/linux/)  
- [安装指南](https://pinyin.sogou.com/linux/help.php)  
安装完之后，终端执行 `fcitx-configtool`，添加输入法如下图所示，最后注销重新登录即可。
<div style="text-align: center;">
    <img src=Linux/_images/sogou.png width=100%/>
</div>