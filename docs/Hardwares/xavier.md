# nvidia xavier 环境配置

#### 系统烧写
1. sdkmanager 下载所需系统镜像
2. 手动方式烧写
    需要自己动手使xavier进入recovery模式：  
    a、用原装usb先将host与xavier连接，还要注意是连接电源灯旁边的插口；  
    b、确保连接电源并保持xavier为关闭状态；  
    c、按住中间的按键（Force Recovery）不松手；  
    d、按住左边的电源（Power）不松手；  
    e、过一两秒，同时松手  
3. 按提示一步一步走，xavier需要连接显示器，不然会错过填写系统用户名密码。  
   装机期间xavier需要联网。

#### apt 镜像源

1. 编辑 /etc/apt/sources.list

```
deb https://mirror.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic main restricted
deb https://mirror.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-updates main restricted
deb https://mirror.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic universe
deb https://mirror.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-updates universe
deb https://mirror.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic multiverse
deb https://mirror.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-updates multiverse
deb https://mirror.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-backports main restricted universe multiverse
deb https://mirror.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-security main restricted
deb https://mirror.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-security universe
deb https://mirror.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic-security multiverse
```

#### 开机自启动
1. 编辑 /etc/rc.local

```bash
#!/bin/bash -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

# run when device startup

sleep 10

# set to fasted mode
sudo nvpmodel -m 0 &

# open fan
sudo /usr/bin/jetson_clocks --fan &

# after save , do : `sudo chmod u+x rc.local`

exit 0

```

2. 赋予权限

```bash
sudo chmod u+x rc.local
```


#### 终端配置
1. 编辑 .bashrc，在末尾添加

```
export PATH=/usr/local/cuda-10.2/bin:$HOME/.local/bin:$PATH
```

#### python
```bash
sudo apt update
sudo apt install -y libpython3-dev python3-pip

# 更新pip并更改pip镜像源
pip3 install pip -U -i https://pypi.tuna.tsinghua.edu.cn/simple
source ~/.bashrc
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

# 安装其他
pip install ipython

# 安装jtop
cd ~/.local/bin
sudo ./pip install jetson-stats
sudo reboot
```

#### 常用库文件的安装
1. apt install

```bash
sudo apt install \
    libgflags-dev \
    libprotobuf-dev protobuf-compiler \
    v4l-utils \ # for video capture
    libopenblas-dev # for torch

```

2. cmake

```bash
wget https://github.com/Kitware/CMake/releases/download/v3.16.2/cmake-3.16.2.tar.gz
tar -xzf cmake-3.16.2.tar.gz
cd  cmake-3.16.2/
mkdir build && cd build
cmake  -DCMAKE_USE_OPENSSL=OFF ..
make -j$(nproc)
sudo make install
```

3. yaml

```bash
git clone https://github.com/jbeder/yaml-cpp.git
cd yaml-cpp
mkdir build && cd build
cmake .. -DYAML_BUILD_SHARED_LIBS=ON
make -j$(nproc)
sudo make install
```

4. tensorrt_plugin

```bash
git clone http://115.239.209.130:1111/zhilu/dl/quantization/tensorrt_plugin.git
cd tensorrt_plugin
mkdir build && cd build
cmake ..
make -j$(nproc)
sudo make install
```

5. dbow2

```bash
wget https://github.com/dorian3d/DBoW2/archive/master.zip
unzip master.zip
cd DBoW2-master
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX=/usr/local/ ..
make -j$(nproc)
sudo make install
```

6. spdlog

```bash
wget https://github.com/gabime/spdlog/archive/v1.8.0.tar.gz
tar -xzf v1.8.0.tar.gz
cd spdlog-1.8.0
mkdir build && cd build
cmake -DSPDLOG_BUILD_SHARED=1 ..
make -j$(nproc)
sudo make install
```

7. fmt

```bash
wget https://github.com/fmtlib/fmt/releases/download/7.0.3/fmt-7.0.3.zip
unzip fmt-7.0.3.zip
cd fmt-7.0.3
mkdir build && cd build
cmake -DBUILD_SHARED_LIBS=TRUE ..
make -j$(nproc)
sudo make install
```

8. torch

```bash
#从 https://elinux.org/Jetson_Zoo 下载对应版本的 pip wheel
pip install torch-1.6.0-cp36-cp36m-linux_aarch64.whl
```