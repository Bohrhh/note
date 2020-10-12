# 琐碎的
> 一些杂乱的点，需要之后整理出一个脉络

#### nvcc 编译选项
对 `-code`， `-arch`，`-gencode`的理解。
首先要理解nvcc的两阶段编译，cuda代码首先被编译为一种面向虚拟架构(virtual architecture)的ptx代码，接着将ptx代码编译为实际架构(real architecture)中可执行的二进制文件。
