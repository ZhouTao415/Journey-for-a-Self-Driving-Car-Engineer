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

### **1 Cross-platform development**

Let’s assume you have some cross-platform project with C++ code shared along different platforms/IDEs. Say you use `Visual Studio` on Windows, `Xcode` on OSX and `Makefile` for Linux:

What you will do if you want to add new `bar.cpp` source file? You have to add it to every tool you use:

To keep the environment consistent you have to do the similar update several times. And the most important thing is that you have to do it **manually** (arrow marked with a red color on the diagram in this case). Of course such approach is error prone and not flexible.

CMake solve this design flaw by adding extra step to development process. You can describe your project in `CMakeLists.txt` file and use [CMake](https://cgold.readthedocs.io/en/latest/glossary/CMake.html#id1) to generate tools you currently interested in using cross-platform [CMake](https://cgold.readthedocs.io/en/latest/glossary/CMake.html#id1) code:

Same action - adding new `bar.cpp` file, will be done in **one step** now:

Note that the bottom part of the diagram **was not changed**. I.e. you still can keep using your favorite tools like `Visual Studio/msbuild`, `Xcode/xcodebuild` and `Makefile/make`!

2 语法特性介绍
基本语法格式：指令(参数 1 参数 2...)
参数使用括弧括起
参数之间使用空格或分号分开
指令是大小写无关的，参数和变量是大小写相关的
```Makefile
set(HELLO hello.cpp)
add_executable(hello main.cpp hello.cpp)
ADD_EXECUTABLE(hello main.cpp ${HELLO})
```
