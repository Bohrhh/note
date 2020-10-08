# 基本命令

内置变量

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
 cmake_minimum_required(VERSION 3.1)
 
 # 项目信息
 project(hello)

 # 指定生成目标
 add_executable(hello main.cpp)
```

#### 2. 源文件和头文件分开

- 目录结构
```
├── include/
│   ├── hello.h
│
├── src/
│   ├── main.cpp
│   ├── hello.cpp
│
├── CMakeLists.txt
```

- CMakeLists.txt
```CMakeLists.txt
 cmake_minimum_required (VERSION 3.1)
 
 project(hello)

 add_executable(hello src/main.cpp src/hello.cpp)

 target_include_directories(
    hello
    PRIVATE 
    ${PROJECT_SOURCE_DIR}/include
)
```


#### 3. 静态库|动态库编译

- 目录结构
```
├── include/
│   ├── hello.h
│
├── src/
│   ├── main.cpp
│   ├── hello.cpp
│
├── CMakeLists.txt
```

- CMakeLists.txt
```CMakeLists.txt
 cmake_minimum_required (VERSION 3.1)
 
 project(hello)

 ############################################################
 # Create a library
 ############################################################
 add_library(
     hello_library
     STATIC # 动态库用 SHARED
     src/hello.cpp
 )

 target_include_directories(
     hello_library
     PUBLIC 
     ${PROJECT_SOURCE_DIR}/include
 )

 ############################################################
 # Create an executable
 ############################################################

 add_executable(hello src/main.cpp)

 target_link_libraries(
    hello
    PRIVATE 
    hello_library
 )
```


#### 3. 安装

- 目录结构
```
├── include/
│   ├── hello.h
│
├── src/
│   ├── main.cpp
│   ├── hello.cpp
│
├── CMakeLists.txt
```

- CMakeLists.txt
```CMakeLists.txt
 cmake_minimum_required (VERSION 3.1)
 
 project(hello)

 ############################################################
 # Create a library
 ############################################################
 add_library(
     hello_library
     STATIC # 动态库用 SHARED
     src/hello.cpp
 )

 target_include_directories(
     hello_library
     PUBLIC 
     ${PROJECT_SOURCE_DIR}/include
 )

 ############################################################
 # Create an executable
 ############################################################

 add_executable(hello src/main.cpp)

 target_link_libraries(
    hello
    PRIVATE 
    hello_library
 )

 ############################################################
 # Install, 默认情况下会安装在 /usr/local 下对应的目录
 # 也可以由 -DCMAKE_INSTALL_PREFIX=/install/dir 指定
 # 也可以在CMakeLists.txt中改变CMAKE_INSTALL_PREFIX的默认值
 ############################################################

 #if( CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT )
 #  message(STATUS "Setting default CMAKE_INSTALL_PREFIX path to ${CMAKE_BINARY_DIR}/install")
 #  set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/install" CACHE STRING "The path to use for make install" FORCE)
 #endif()

 # Binaries
 install (
     TARGETS hello
     DESTINATION bin)

 # Library
 install (
     TARGETS hello_library
     LIBRARY DESTINATION lib)

 # Header files
 install(
     DIRECTORY ${PROJECT_SOURCE_DIR}/include/ 
     DESTINATION include)
```

- 卸载

在执行 `make install` 命令之后会生成 *install_manifest.txt* 文件，该文件记录了安装文件的目录
执行 `sudo xargs rm < install_manifest.txt` 可删除安装的文件


#### 4. 编译选项
