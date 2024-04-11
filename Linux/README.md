<div align="center">
📖 Linux
</div> 
<br>

<div align="center">
简体中文
&emsp;&emsp; | &emsp;&emsp;
English
</div> 
<br>

# Linux

**什么是linux系统？**

- Linux是**开源**的操作系统

**多用户多任务：**

- 单用户：一个用户，在登录计算机（操作系统），只能允许**同时**登录一个用户；
- 单任务：一个任务，允许用户**同时**进行的操作任务数量；
- 多用户：多个用户，在登录计算机（操作系统），允许**同时**登录多个用户进行操作；
- 多任务：多个任务，允许用户**同时**进行多个操作任务；

**Windows**属于：单用户、多任务。

**Linux**属于：多用户、多任务。

**Linux一切皆文件**

对于文件的操作的都有哪些种类？

- **创建文件、编辑文件、保存文件、关闭文件、重命名文件、删除文件、恢复文件。**

## **1. 目录结构**

**目录结构：**

- **Bin:** 全称binary，含义是二进制。该目录中存储的都是一些二进制文件，文件都是可以被运行的。
- **Dev：该目录中主要存放的是外接设备，例如盘、其他的光盘等。在其中的外接设备是不能直接被使用的，需要挂载（类似window**下**的分配盘符）。**
- **Etc：** 该目录主要存储一些配置文件。
- **Home：**表示“家”，表示**除了root用户以外**其他用户的家目录，类似于windows下的User/用户目录。
- **Proc：** 全称process，表示进程，该目录中存储的是Linux运行时候的进程。
- **Root：** 该目录是root用户自己的家目录。
- **Sbin：** 全称super binary，该目录也是存储一些可以被执行的二进制文件，但是必须得有super权限的用户才能执行。
- **Tmp：** 表示“临时”的，当系统运行时候产生的临时文件会在这个目录存着。
- **Usr：** 存放的是用户自己安装的软件。类似于windows下的program files。
- **Var：** 存放的程序/系统的日志文件的目录。
- **Mnt：** 当外接设备需要挂载的时候，就需要挂载到mnt目录下。

## **2. 指令与选项**

- **指令含义：**
  - **Linux的指令**是指在Linux**终端（命令行）**中输入的内容。
- **指令格式：**
    - 完整指令的**标准格式**：**命令**（空格） [**选项**]（空格） [**操作对象**]
    - 选项和操作对象都可以没有，也可以是多个
    ```bash
    # 指令示例：以下两条指令等价
    ls -l -a -h /home ./
    ls -lah /home ./
    ```
## **3. 指令示例：以下两条指令等价**

- **pwd** - **Print current working directory**
  - **作用：**打印当前终端所在的目录
  - **用法： pwd**
  ```bash
  # 打印当前目录
  pwd
  ```
  
- **ls - List directory contents**
  - **作用：**列出当前工作目录下的所有文件/文件夹的名称
      
  - **用法1：ls**
    **含义：**列出当前工作目录下的文件/文件夹的名称
    ```bash
    ls
    ```
      
  - **用法2：ls [路径]**
    
    **含义：** 列出指定**路径**下的所有文件/文件夹的名称
    - 绝对路径：相对**根目录**的路径；
    - 相对路径：相对**当前目录**的路径；
    ```bash
    # ls 相对路径
    ls ./   #【表示当前目录下】
    ls ../  #【上一级目录下】
    # ls 绝对路径
    ls /home
    ```

  - **用法3：ls [选项] [路径]**
    
    **含义：** 在列出指定路径下的文件/文件夹的名称，并以指定的格式进行显示。
    ```bash
    # ls 选项 路径
    ls -lah /home
    # 选项解释：
      -l：表示list，表示以详细列表的形式进行展示
      -a：表示显示所有的文件/文件夹（包含了隐藏文件/文件夹）
      -h：表示以可读性较高的形式显示
    # ls -l 中 “-”表示改行对应的文档类型为文件，“d”表示文档类型为文件夹。
    # 在Linux中隐藏文档一般都是以“.”开头
    ```
- **cd - change directory**
  - **作用：**切换当前的工作目录
  - **用法1：cd ； cd ~**
    ```bash
    # 以下两条命令等价，示直接进入当前用户的家目录下【很常用】
    cd
    cd ~
    ```
    
  - 用法2：cd [相对路径]
    ```bash
    # 进入到上级目录下
    cd ..
    # 进入到上级目录中的local目录下
    cd ../local
    ```
  
  - 用法3：cd [绝对路径]
    ```bash
    # 进入到/usr/local目录下
    cd /usr/local
    ```

- **mkdir - make directories**
  - **作用：**创建目录
  - **用法1：mkdir 路径**
    ```bash
    # 在当前路径下创建出目录“myfolder”
    mkdir myfolder
    ```

  - **用法2：mkdir -p 路径**
      **含义：**一次性创建多层不存在的目录
    ```bash
    # 创建 ~/a/b/c 目录
    mkdir -p ~/a/b/c
    ```
  - **用法3：mkdir 路径1 [路径2] [路径3]**
    
    **含义：** 一次性创建多个目录
    ```bash
    # 在当前目录分别创建a、b、c三个文件夹
    mkdir a b c
    ```

- **touch - change file timestamps**
    - **作用：**创建新文件
      ```bash
      --------------------------------------------------------------------------
      # 									【为什么创建新文件是touch】
      # 1. touch的作用本来不是创建文件，而是将指定文件的修改时间设置为当前时间。
      就是假装“碰”（touch）了一下这个文件，假装文件被“修改”了，于是文件的修改时间就是被设置为当前时间。
      # 2. 这带来了一个副作用，就是当touch一个不存在的文件的时候，它会创建这个文件。
      然后，由于touch已经可以完成创建文件的功能了，就不再需要一个单独的create了。
      --------------------------------------------------------------------------
      ```
    - 用法1：touch [路径]
      ```bash
      # 在当前目录下创建linux.txt文件
      touch linux.txt
      
      # 在上级目录下创建linux文件
      touch ../linux
      
      # 在/home/bing/目录下创建myfile文件
      touch /home/bing/myfile
      ```
    
    - 用法2：touch [路径1] [路径2]
      ```bash
      # 在当前目录下创建file file.txt 两个文件
      touch file file.txt
      ```

- **rm - remove files or directories**
    - **作用：**删除文件/目录
    - **用法1：rm [选项] 需要移除的文件路径**
      ```bash
      # 删除当前路径下的myfile文件
      rm myfile
      # 删除/usr路径下的myfile文件
      rm /usr/myfile
      ```
    - 用法2：rm [选项] 需要移除的目录
      ```bash
      # 删除当前路径下的abc文件
      rm -rf myfolder
      # 删除/usr路径下的abc文件
      rm -rf /usr/myfolder
      -r: recursive
      -f: force
      ```
      
- **cp - copy files and directories**
    - **作用：**复制文件/文件夹到指定的位置
    - **用法1：cp [被复制的文件路径] [文件被复制到的路径]**
      ```bash
      # cp命令来复制一个文件
      cp /home/bing/myfile ./
      ```
      
    - **用法2：cp -r [被复制的文件夹路径] [文件夹被复制到的路径]***
        
        **含义：**-r 表示递归复制，复制文件夹的时候需要加 -r
        ```bash
        # 复制/home/bing/myfolder文件夹到根目录/下
        cp -r /home/bing/myfolder /
        ```

- **mv - move (rename) files**
    - **作用：**移动文件到新的位置，或者重命名文件
    - **用法：mv [需要移动的文件路径] [需要保存的位置路径]**
      ```bash
      # 移动当前目录下myfile文件到根目录/下
      mv myfile /myfile
      
      # 移动当前目录下myfolder文件夹到根目录/下
      mv myfolder /myfolder
      
      # 移动当前目录下myfile到根目录/下，并重命名为myfile007
      mv myfile myfile007
      ```

- **man - an interface to the system reference manuals**
    - **作用：**包含了Linux中全部命令手册
    - **用法：man [命令]**
    - **含义：**查看命令使用手册，按 q 退出
      ```bash
      # 查看ls命令的手册
      man ls
      # 查看cd命令的手册
      man cd
      # 查看man命令的手册
      man man
      ```

- **reboot - reboot the machine**
    - **作用：**重启linux系统
    - **用法：reboot**
      ```bash
      # 立即重启
      reboot
      ```

- **shutdown - power-off the machine**
    - **作用：**关机
    - **用法：shut -h [时间]**
      ```bash
      # 立即关机
      shutdown -h now
      ```
### **4. 文件编辑**

- **Vim [file]**
    - 所有的 Linux系统都会内建 Vi/Vim编辑器，其他的编辑器则不一定会存在
    - Vim是所有Unix及Linux系统下标准的编辑器
    - **Vim 具有程序开发的能力，也可以用来对文件进行简单的编辑**
    
    **Vim具有“编辑器之神”的称号**，学会Vim便可在Linux的世界里**畅行无阻**，**尤其是在终端中**。
  
    🤜[**Vim cheatsheet**](https://devhints.io/vim)🤛
    
    
- **gedit [file]**
    - Linux 下的一个纯文本编辑器
    - 可以根据不同的语言高亮显现关键字和标识符。
- **nano [file]**
    - nano 是一个小巧的文本编辑器
    - 它比vi/vim要简单得多，比较适合Linux初学者使用。
    - 某些Linux发行版的默认编辑器就是nano。

<a id="Bibliography"></a>
# Bibliography:
- [基于VSCode和CMake实现的C/C++开发-Linux篇](https://xbing.notion.site/xiaobing-9bab00c7243c46d3a02b08aa54921a52?p=c330a94669a84c2480a59ba708fd4ece&pm=c)
- [Vim cheatsheet](https://devhints.io/vim)
