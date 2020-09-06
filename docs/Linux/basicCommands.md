# 基本命令

## apt
> 作用：软件包管理
```
常用命令
1. apt install 软件名
2. apt update
3. apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 4ABE1AC7557BEFF9： 解决由于没有公钥，无法验证下列签名的问题
4. /var/lib/apt/lists/ 这里面是apt的缓存
5. apt-cache search eigen：查找软件包
```

## cat 
> 作用：查看文本文件信息
```
常用命令
1. cat /proc/version：查看linux内核版本信息(宿主机)
2. cat /etc/issue：查看linux镜像版本(docker image)
```

## chown
> 作用：更改文件夹权限
```
常用命令
1. sudo chown 用户名 文件夹名/ -R
```

## cp
> 作用：拷贝文件
```
常用命令
1. cp 源文件 目标文件/目标文件夹
2. cp -r 源文件夹 目标文件/目标文件夹
```

## ctrl+alt+t
> 作用：快捷键开启多个终端

## ctrl+shift+t
> 作用：快捷键一个终端里开启多个小终端

## df
> 作用：查看磁盘占用情况
```
常用命令
1. df -h：查看磁盘占用情况
```

## dmidecode
> 作用：查看内存信息
```
常用命令
1. dmidecode | grep -A16 "Memory Device" | grep "Speed"：内存条频率
2. dmidecode | grep -P -A 5 "Memory\s+Device" | grep Size | grep -v Range：内存大小
```

## du 
作用：查看文件大小
```
常用命令
1. du -sh: 查看当前文件夹大小 
2. du -h -d 1: 查看各个文件夹大小
```

## echo
> 作用：清理缓存
```
常用命令
echo 1 > /proc/sys/vm/drop_caches
echo 2 > /proc/sys/vm/drop_caches
echo 3 > /proc/sys/vm/drop_caches
```

## env
> 作用：查看所有环境变量

## fdisk
> 作用：查看磁盘情况
```
常用命令
1. sudo fdisk -l
```

## find
> 作用：查找文件
```
常用命令
1. find -name "*raw*"：查找名字包含raw的文件
```

## ln 
> 作用：设置软链接
```
常用命令
1. ln -s originFile targetFile
```

## locate
> 作用：定位文件
```
安装 sudo apt install mlocate
更新 sudo updatedb
常用命令
1. locate filename
```

## ls
> 作用：显示文件
```
 常用命令
1. ls：显示当前文件夹下的文件
2. ls -a：显示当前文件夹下的所有文件，包括隐藏文件
3. ls -lR | grep "-" | wc -l： 查看文件夹中文件的数目，包含子目录
```

## lscpu
> 作用：查看CPU信息

## mkdir
> 作用：新建文件夹
```
常用命令
1. mkdir dirName：新建文件夹
```

## mount
> 作用：挂载磁盘
```
常用命令
1. sudo mount /dev/sdb1 /mnt：将磁盘/dev/sdb1 挂载到 /mnt
2. sudo umount /mnt：取消挂载
```

## mv
> 作用：移动文件
```
常用命令
1. mv originFile< originDir > targetFile< targetDir >：将文件或文件夹移动到某地。
```

## nvidia-smi
> 作用：查看英伟达的GPU使用率
```
常用命令
如果想每隔一段时间刷新则需要命令
watch -n 1 nvidia-smi
```

## passwd
> 作用：更改密码

## pip
> 作用：安装python的依赖包
```
常用命令
1.pip install numpy -i https://pypi.douban.com/simple：从指定镜像安装依赖包
```

## pwd
> 作用：print working directory

## rm
> 作用：移除某个文件
```
常用命令
1. rm file：删除文件
2. rm -r dir：删除文件夹
```

## scp
> 作用：上传文件到远程服务器
```
常用命令
1. scp -r localDir username@remoteAddress:remoterDir：将本地文件夹传送到远程服务器的某个目录。
2. scp localFile username@remoteAddress:remoterDir：将本地文件传送到远程服务器。
3. scp -r username@remoteAddress:remoteDir localDir：将远程服务器的文件夹传送到本地。
4. scp username@remoteAddress:remoteFile localDir：将远程服务器的文件传送到本地。
```

## screen
> 作用：在用ssh远程服务器的时候，若关闭远程窗口，那么你的程序就会被杀死，所以需要使用screen命令开启一个窗口，运行脚本然后安全退出，这样在关闭远程的后，你的脚本仍在运行。
```
常用命令
1. screen -S sockname：新建一个窗口
2. screen -ls：查看正在后台运行的窗口
3. screen -r < sockname>：进入某个已打开的窗口
4. CTRL+a 松开后按d：退出当前sock
5. CTRL+a 松开后按k：杀死当前sock
```

## ssh
> 作用：远程某台服务器
```
常用命令
1. ssh <user_name>@address：然后会提示输入密码
```

## tar 
> 作用：压缩和解压
```
-c：压缩
-x：解压
-v：显示过程
-z：有gzip属性的
-j：有bz2属性的
-f: 指定压缩后的文件名
常用命令
1. tar -zcvf dir.tar.gz  dir：压缩 dir 文件夹
2. tar -xvf file.tar.gz：解压 .tar.gz 文件
3. tar -xjf images.tar.bz2：解压 .tar.bz2 文件
4. tar zcvf - largefile | split -b 500m：分卷压缩，每个文件不大于500m
5. cat x* | tar xzvf - ：将x*的文件还原分卷压缩前的
```

## touch
> 作用：新建文件
```
常用命令
1. touch fileName：新建文本文件
```

## ulimit
> 作用：显示系统资源限制
```
常用命令
1. ulimit -a: 显示系统全部的资源限制
```

## unzip
> 作用：解压文件
```
常用命令
1. unzip -d /target/directory test.zip
```

## which
> 作用：查找命令所在目录
```
常用命令
1. which 命令
```

## wget 
> 作用：下载命令
```
常用命令
1. wget -c https://...
```









