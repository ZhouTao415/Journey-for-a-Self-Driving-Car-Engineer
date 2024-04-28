<div align="center">
CMake
</div> 

# CMake

## 编译器安装
- 安装 CMake
  ```bash
  sudo apt install cmake
  ```
- 安装成功确认
  ```bash
  # 确认是否安装成功
  # 如果成功，则显示版本号
  cmake --version
  ```

**前言**：

- **CMake**是一个**跨平台**的安装**编译工具**，可以用**简单**的语句来描述**所有平台**的安装(编译过程)。
- CMake可以说已经成为**大部分C++开源项目标配**

## **1 Cross-platform development**

Let’s assume you have some cross-platform project with C++ code shared along different platforms/IDEs. Say you use `Visual Studio` on Windows, `Xcode` on OSX and `Makefile` for Linux:

What you will do if you want to add new `bar.cpp` source file? You have to add it to every tool you use:

To keep the environment consistent you have to do the similar update several times. And the most important thing is that you have to do it **manually** (arrow marked with a red color on the diagram in this case). Of course such approach is error prone and not flexible.

CMake solve this design flaw by adding extra step to development process. You can describe your project in `CMakeLists.txt` file and use [CMake](https://cgold.readthedocs.io/en/latest/glossary/CMake.html#id1) to generate tools you currently interested in using cross-platform [CMake](https://cgold.readthedocs.io/en/latest/glossary/CMake.html#id1) code:

Same action - adding new `bar.cpp` file, will be done in **one step** now:

Note that the bottom part of the diagram **was not changed**. I.e. you still can keep using your favorite tools like `Visual Studio/msbuild`, `Xcode/xcodebuild` and `Makefile/make`!

## ** 2 语法特性介绍 **
- 基本语法格式：指令(参数 1 参数 2...)
  - 参数使用括弧括起
  - 参数之间使用空格或分号分开
- 指令是大小写无关的，参数和变量是大小写相关的
```Makefile
set(HELLO hello.cpp) 
add_executable(hello main.cpp hello.cpp)
ADD_EXECUTABLE(hello main.cpp ${HELLO})
```
- 变量使用${}方式取值，但是在 IF 控制语句中是直接使用变量名
```Makefile
${HELLO} / IF(HELLO)
```
## **3 重要指令和CMake常用变量**

### **6.3.1 重要指令**

- **cmake_minimum_required** **指定CMake的最小版本要求**
  - 语法： **cmake_minimum_required(VERSION versionNumber [FATAL_ERROR])**
  ```Makefile
  # CMake最小版本要求为2.8.3
  cmake_minimum_required(VERSION 2.8.3)
  ```
  
- **project 定义工程名称，并可指定工程支持的语言**
  - 语法： project(projectname [CXX] [C] [Java])
  ```Makefile
  # 指定工程名为HELLOWORLD
  project(HELLOWORLD)
  ```
​
- **set 显式的定义变量**
  - 语法：set(VAR [VALUE] [CACHE TYPE DOCSTRING [FORCE]])
  ```Makefile
  # 定义SRC变量，其值为sayhello.cpp hello.cpp
  set(SRC sayhello.cpp hello.cpp)

- **include_directories 向工程添加多个特定的头文件搜索路径 --->相当于指定g++编译器的-I参数**
  - 语法： include_directories([AFTER|BEFORE] [SYSTEM] dir1 dir2 ...)
  ```Makefile
  # 将/usr/include/myincludefolder 和 ./include 添加到头文件搜索路径
  include_directories(/usr/include/myincludefolder ./include)

- **link_directories 向工程添加多个特定的库文件搜索路径 --->相当于指定g++编译器的-L参数**
  - 语法： link_directories(dir1 dir2 ...)
  ```Makefile
  # 将/usr/lib/mylibfolder 和 ./lib 添加到库文件搜索路径
  link_directories(/usr/lib/mylibfolder ./lib)
  
- **add_library 生成库文件**
  - 语法： add_library(libname [SHARED|STATIC|MODULE] [EXCLUDE_FROM_ALL] source1 source2 ... sourceN)
  ```Makefile
  # 通过变量 SRC 生成 libhello.so 共享库
  add_library(hello SHARED ${SRC})

- **add_compile_options 添加编译参数**
  - 语法：add_compile_options(<option> ...)
  ```Makefile
  # 添加编译参数 -Wall -std=c++11 -O2
  add_compile_options(-Wall -std=c++11 -O2)

- **add_executable 生成可执行文件**
  - 语法：add_executable(exename source1 source2 ... sourceN)
  ```Makefile
  # 编译main.cpp生成可执行文件main
  add_executable(main main.cpp)

- **target_link_libraries 为 target 添加需要链接的共享库 -->相同于指定g++编译器-l参数**
  - 语法： target_link_libraries(target library1<debug | optimized> library2...)
  ```Makefile
  # 将hello动态库文件链接到可执行文件main
  target_link_libraries(main hello)

- **add_subdirectory 向当前工程添加存放源文件的子目录，并可以指定中间二进制和目标二进制存放的位置**
  - 语法： add_subdirectory(source_dir [binary_dir] [EXCLUDE_FROM_ALL])
  ```Makefile
  # 添加src子目录，src中需有一个CMakeLists.txt
  add_subdirectory(src)
  
- **aux_source_directory 发现一个目录下所有的源代码文件并将列表存储在一个变量中，这个指令临时被用来自动构建源文件列表**
  - 语法： aux_source_directory(dir VARIABLE)
  ```Makefile
  # 定义SRC变量，其值为当前目录下所有的源代码文件
  aux_source_directory(. SRC)
  # 编译SRC变量所代表的源代码文件，生成main可执行文件
  add_executable(main ${SRC})
