# TVM

#### 环境搭建

- 1 主机编译

    ``` bash
    git clone --recursive https://github.com/apache/incubator-tvm tvm
    cd tvm/docker
    ./build.sh ci_gpu /bin/bash # 可以根据安装需要，编辑文件内容
    ./build.sh demo_gpu /bin/bash
    ```

- 2 设备(rk3399)

    安装运行时环境
    ``` bash
    git clone --recursive https://github.com/apache/incubator-tvm tvm
    cd tvm
    mkdir build
    cp cmake/config.cmake build
    cd build
    echo set\(USE_OPENCL ON\) >> config.cmake
    cmake ..
    make runtime -j4
    ```

    编辑 `~/.bashrc`
    ```
    export PYTHONPATH=$PYTHONPATH:~/tvm/python
    ```