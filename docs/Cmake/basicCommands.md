# 基本命令

#### 1. 单个源文件

- 目录结构
```
├── main.cpp
│
├── CMakeLists.txt
```

- CMakeLists.txt  
```CMakeLists.txt
 # CMake 最低版本号要求
 cmake_minimum_required (VERSION 2.8)
 
 # 项目信息
 project (hello)

 # 指定生成目标
 add_executable(hello main.cpp)
```

#### 2. 同一目录多个源文件

- 目录结构
```
├── main.cpp
│
├── functions.cpp
├── functions.h
│
├── CMakeLists.txt
```

- 当源文件数目少时  
```CMakeLists.txt
 cmake_minimum_required (VERSION 2.8)
 
 project (hello)

 add_executable(hello main.cpp functions.cpp)
```

- 当源文件数目多时，不方便一个一个添加进CMakeLists,这时可以使用  
`aux_source_directory(<dir> <variable>)` 
```CMakeLists.txt
 cmake_minimum_required (VERSION 2.8)
 
 project (hello)

 # 查找当前目录下的所有源文件
 # 并将名称保存到 DIR_SRCS 变量
 aux_source_directory(. DIR_SRCS)
 
 add_executable(hello ${DIR_SRCS})
```

#### 3. 多个目录多个源文件

- 目录结构
```
├── main.cpp
│
├── math/
│   ├── functions.cpp
│   ├── functions.h
│   ├── CMakeLists.txt
│
├── CMakeLists.txt
```

- math 子目录 CMakeLists.txt
```CMakeLists.txt
 # 查找当前目录下的所有源文件
 # 并将名称保存到 DIR_LIB_SRCS 变量
 aux_source_directory(. DIR_LIB_SRCS)

 # 生成链接库
 add_library (mathfunction ${DIR_LIB_SRCS})
```

- 主目录 CMakeLists.txt
```CMakeLists.txt
 cmake_minimum_required (VERSION 2.8)

 project (Demo3)

 # 查找当前目录下的所有源文件
 # 并将名称保存到 DIR_SRCS 变量
 aux_source_directory(. DIR_SRCS)

 # 添加 math 子目录
 add_subdirectory(math)

 # 指定生成目标 
 add_executable(Demo main.cc)

 # 添加链接库
 target_link_libraries(Demo mathfunction)
```