<div align="center">
gcc/ g++
</div> 

# gcc/ g++

## 编译器安装
- 安装gcc/g++
  ```bash
  # 通过以下命令安装编译器
  sudo apt install build-essential
  ```
- 安装成功确认
  ```bash
  # 以下命令确认每个软件是否安装成功
  # 如果成功，则显示版本号
  gcc --version
  g++ --version
  ```
## **前言**：

1. GCC 编译器支持编译 Go、Objective-C，Objective-C ++，Fortran，Ada，D 和 BRIG（HSAIL）等程序；
2. Linux 开发C/C++ 一定要熟悉 GCC
3. **VSCode是通过调用GCC编译器来实现C/C++的编译工作的；**

实际使用中：
- 使用 gcc 指令编译 C 代码
- 使用 g++指令编译 C++ 代码

## 1. 编译过程

1. 预处理-Pre-Processing	//.i文件
   ```bash
    # -E 选项指示编译器仅对输入文件进行预处理
    g++  -E  test.cpp  -o  test.i    //.i文件
   ```
   
2. 编译-Compiling	// .s文件
   ```bash
   # -S 编译选项告诉 g++ 在为 C++ 代码产生了汇编语言文件后停止编译
   #  g++ 产生的汇编语言文件的缺省扩展名是 .s
   g++  -S  test.i  -o   test.s
   ```
   
3. 汇编-Assembling	// .o文件
   ```bash
   # -c 选项告诉 g++ 仅把源代码编译为机器语言的目标代码
   # 缺省时 g++ 建立的目标代码文件有一个 .o 的扩展名。
   g++  -c  test.s  -o  test.o
   ```

4. 链接-Linking	// bin文件
   ```bash
   # -o 编译选项来为将产生的可执行文件用指定的文件名
   g++  test.o  -o  test
   ```
