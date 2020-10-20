# 设置

## 1，鼠标滚轮设置
1. sudo apt install imwheel：安装软件
2. sudo vim ~/.imwheelrc： 编辑
```
".*"
None, Up, Button4, 5 
None, Down, Button5, 5 
Control_L, Up, Control_L|Button4 
Control_L, Down, Control_L|Button5 
Shift_L, Up, Shift_L|Button4 
Shift_L, Down, Shift_L|Button5
```
3. imwheel: 启动
4. killall imwheel: 终止

## 2，设置开机启动
启动应用程序里添加命令 imwheel

## 3，使用useradd添加用户后默认sh为/bin/sh导致没有TAB自动补全
```
修改/etc/passwd  
yourUserName:x:1002:1003::/home/yourUserName:  
改为  
yourUserName:x:1002:1003:,,,:/home/yourUserName:/bin/bash  
```

## 4，设置 apt 镜像源
```
清华镜像： sed -i s@/archive.ubuntu.com/@/mirrors.tuna.tsinghua.edu.cn/@g /etc/apt/sources.list
阿里云镜像： sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list
```


## 5，设置用独立显卡来传输视频（服务器）
要在bios中
进入 Advanced选项
进入 PCIe/PCI/PnP Configuration
设置 VGA Priority 为 offboard


## 6，修改计算机名及用户名
#### **root权限下修改**
计算机名
vim /etc/hostname
vim /etc/hosts

用户名
vim /etc/shadow
vim /etc/passwd
vim /etc/group
mv /home/olduserame /home/newusername

## 8，开机自动挂载磁盘
ubuntu下disk软件设置


## 9， 更换 gcc (g++) 版本
sudo update-alternatives --config gcc

## 10， pip镜像源
- 永久修改  
linux：在用户主目录下新建.pip文件夹，进入.pip文件夹并创建pip.conf，编辑pip.conf。  
windows：进入%APPDATA%，新建pip文件夹，进入pip文件夹，创建pip.ini文件，编辑pip.ini
```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```

- 临时使用
```
pip install numpy -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## 11， python多环境配置
- 1 创建虚拟环境：`conda create -n venv_name python=3.8`
- 2 查看但前存在哪些虚拟环境：`conda env list` 或 `conda info -e`
- 3 检查更新当前conda：`conda update conda`
- 4 移除虚拟环境：`conda remove -n venv_name --all`
- 5 设置镜像源：`conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/`
- 6 激活虚拟环境：**Linux**，`conda activate venv_name`。 **Mac**，`source activate venv_name`
- 7 失活虚拟环境：**Linux**，`conda deactivate`。 **Mac**，`source deactivate`












