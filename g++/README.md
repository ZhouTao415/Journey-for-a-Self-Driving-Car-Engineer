<div align="center">
gcc/ g++
</div> 

# gcc/ g++

## 📑 Contents
* [编译器安装](#编译器安装)
* [前言](#前言)
* [1. 编译过程](#编译过程)
* [2. g++重要编译参数](#g++重要编译参数)
* [3. [实战]g++命令行编译](#g++命令行编译)
  * [3.1 直接编译](#直接编译) 
  * [3.2 生成库文件并编译](#生成库文件并编译)
  * [3.3 运行可执行文件](#运行可执行文件)
  
  
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

<a id="编译过程"></a>
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

<a id="g++重要编译参数"></a>
## 2. g++重要编译参数

- **-g**	编译带调试信息的可执行文件
  ```bash
  # -g 选项告诉 GCC 产生能被 GNU 调试器GDB使用的调试信息，以调试程序。
  
  # 产生带调试信息的可执行文件test
  g++ -g test.cpp
  ```
- **-O[n]**	优化源代码
  ```bash
  ## 所谓优化，例如省略掉代码中从未使用过的变量、直接将常量表达式用结果值代替等等，
     这些操作会缩减目标文件所包含的代码量，提高最终生成的可执行文件的运行效率。
 
  # -O 选项告诉 g++ 对源代码进行基本优化。这些优化在大多数情况下都会使程序执行的更快。
    -O2 选项告诉 g++ 产生尽可能小和尽可能快的代码。 如-O2，-O3，-On（n 常为0–3）
  # -O 同时减小代码的长度和执行时间，其效果等价于-O1
  # -O0 表示不做优化
  # -O1 为默认优化
  # -O2 除了完成-O1的优化之外，还进行一些额外的调整工作，如指令调整等。
  # -O3 则包括循环展开和其他一些与处理特性相关的优化工作。
  # 选项将使编译的速度比使用 -O 时慢， 但通常产生的代码执行速度会更快。
   
   # 使用 -O2优化源代码，并输出可执行文件
   g++ -O2 test.cpp
   ```
- **l 和 -L**	指定库文件 | 指定库文件路径
  ```bash
  # -l参数(小写)就是用来指定程序要链接的库，-l参数紧接着就是库名
  # 在/lib和/usr/lib和/usr/local/lib里的库直接用-l参数就能链接
  
  # 链接glog库
  g++ -lglog test.cpp
   
  # 如果库文件没放在上面三个目录里，需要使用-L参数(大写)指定库文件所在目录
  # -L参数跟着的是库文件所在的目录名
   
  # 链接mytest库，libmytest.so在/home/bing/mytestlibfolder目录下
  g++ -L/home/bing/mytestlibfolder -lmytest test.cpp
  ```
- **I**	指定头文件搜索目录
  ```bash
  # -I
  # /usr/include目录一般是不用指定的，gcc知道去那里找，
    但是如果头文件不在/usr/icnclude里我们就要用-I参数指定了，比如头文件放在/myinclude目录里，
    那编译命令行就要加上-I/myinclude 参数了，
    如果不加你会得到一个”xxxx.h: No such file or directory”的错误。
    -I参数可以用相对路径，比如头文件在当前 目录，可以用-I.来指定。
    上面我们提到的–cflags参数就是用来生成-I参数的。
   
  g++ -I/myinclude test.cpp
  ```
- **Wall**	打印警告信息
  ```bash
  # 打印出gcc提供的警告信息
  g++ -Wall test.cpp
​  ```

- **w**	关闭警告信息
  ```bash
  # 关闭所有警告信息
  g++ -w test.cpp
  ​```
- **std=c++11**	设置编译标准
  ```bash
  # 使用 c++11 标准编译 test.cpp
  g++ -std=c++11 test.cpp
  ```​
- **o**	指定输出文件名
  ```bash
  # 指定即将产生的文件名
  
  # 指定输出可执行文件名为test
  g++ test.cpp -o test
  ​```
- **D**	定义宏
  ```bash
  # 在使用gcc/g++编译的时候定义宏
  
  # 常用场景：
  # -DDEBUG 定义DEBUG宏，可能文件中有DEBUG宏部分的相关信息，用个DDEBUG来选择开启或关闭DEBUG
  ```
- 示例代码：
  ```bash
  // -Dname 定义宏name,默认定义内容为字符串“1”

  #include <stdio.h>
  
  int main()
  {
      #ifdef DEBUG
      	printf("DEBUG LOG\n");
      #endif
      	printf("in\n");
  }
  
  // 1. 在编译的时候，使用gcc -DDEBUG main.cpp
  // 2. 第七行代码可以被执行
  ```
  注：使用 **man gcc**命令可以查看gcc英文使用手册

<a id="g++命令行编译"></a>
## 3. [实战]g++命令行编译

**案例：** 最初目录结构: 2 directories, 3 files
```bash
# 最初目录结构
.
├── include
│   └── Swap.h
├── main.cpp
└── src
    └── Swap.cpp

2 directories, 3 files
```

<a id="直接编译"></a>
### 3.1 直接编译
- 最简单的编译，并运行
  ```bash
  # 将 main.cpp src/Swap.cpp 编译为可执行文件
  g++ main.cpp src/Swap.cpp -Iinclude
  # 运行a.out
  ./a.out
  ```
- 增加参数编译，并运行
  ```bash
  # 将 main.cpp src/Swap.cpp 编译为可执行文件 附带一堆参数
  g++ main.cpp src/Swap.cpp -Iinclude -std=c++11 -O2 -Wall -o b.out
  # 运行 b.out
  ./b.out
  ```

<a id="生成库文件并编译"></a>
### 3.2 生成库文件并编译
- 链接静态库生成可执行文件①:
  ```bash
  ## 进入src目录下
  $cd src
  
  # 汇编，生成Swap.o文件
  g++ Swap.cpp -c -I../include
  # 生成静态库libSwap.a
  ar rs libSwap.a Swap.o
  
  ## 回到上级目录
  $cd ..
  
  # 链接，生成可执行文件:staticmain
  g++ main.cpp -Iinclude -Lsrc -lSwap -o staticmain
  ```
- 链接动态库生成可执行文件②：
  ```bash
  ## 进入src目录下
  $cd src
  
  # 生成动态库libSwap.so
  g++ Swap.cpp -I../include -fPIC -shared -o libSwap.so
  ## 上面命令等价于以下两条命令
  # gcc Swap.cpp -I../include -c -fPIC
  # gcc -shared -o libSwap.so Swap.o
  
  ## 回到上级目录
  $cd ..
  
  # 链接，生成可执行文件:sharemain
  g++ main.cpp -Iinclude -Lsrc -lSwap -o sharemain
  ```
- **编译完成后的目录结构**  
  最终目录结构：2 directories, 8 files
  ```bash
  # 最终目录结构
  .
  ├── include
  │   └── Swap.h
  
  ├── main.cpp
  ├── sharemain
  ├── src
  │   ├── libSwap.a
  │   ├── libSwap.so
  │   ├── Swap.cpp
  │   └── Swap.o
  └── staticmain
  
  2 directories, 8 files
  ```
<a id="运行可执行文件"></a>
### 3.3 运行可执行文件
- 运行可执行文件①:
  ```bash
  # 运行可执行文件
  ./staticmain
  ```
  
- 运行可执行文件②:
  ```bash
  # 运行可执行文件
  LD_LIBRARY_PATH=src ./sharemain
  ```
<a id="Bibliography"></a>
# Bibliography:
- [基于VSCode和CMake实现的C/C++开发-Linux篇](https://xbing.notion.site/xiaobing-9bab00c7243c46d3a02b08aa54921a52?p=c330a94669a84c2480a59ba708fd4ece&pm=c)
