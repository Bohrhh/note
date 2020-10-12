# 琐碎的
> 一些杂乱的点，需要之后整理出一个脉络

#### nvcc 编译选项
对 `-code`， `-arch`，`-gencode`的理解。首先要理解nvcc的两阶段编译，cuda代码首先被编译为一种面向虚拟架构(virtual architecture)的**ptx**代码，接着将**ptx**代码编译为实际架构(real architecture)中可执行的二进制文件。

在运行时，若二进制代码可直接运行在显卡上，则直接运行二进制代码；否则，若文件中包含虚拟架构代码，显卡驱动会尝试将合适的虚拟架构代码动态编译为二进制代码并执行。

二进制代码的兼容性，$X.y$的二进制代码能够运行在$X.z$的设备上，只要满足$z>=x$

ptx代码的兼容性，低版本的ptx代码总是能够本编译成高版本的二进制代码并在相应的设备上运行。

- `-arch` 就是nvcc用来指定在第一阶段使用什么虚拟架构，  
   使用方法:
   ```
   -arch compute_61
   ```
- `-code` 是nvcc用来指定将什么代码放入目标文件中，
   使用方法:
   ```
   -code sm_61      #将对应的二进制代码放入目标文件

   -code compute_75 #将对应的ptx代码放入目标文件
   ```
- `-gencode` 可以结合`arch`和`code`，让编译器生成面向多种gpu架构的代码，
   使用方法:
   ```
   -gencode arch=compute_61, code=sm_61                 # 将二进制代码放入目标文件
   -gencode arch=compute_72, code=sm_72                 # 将二进制代码放入目标文件
   -gencode arch=compute_75, code=\`compute_75, sm_75`\ # 将二进制代码和ptx代码放入目标文件
   ```
