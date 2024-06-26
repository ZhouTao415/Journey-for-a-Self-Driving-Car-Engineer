<div align="center">
VSCode
</div> 

# VSCode

### **1. 界面介绍**

1. 侧边栏
2. 菜单栏
3. 编辑区
4. 状态栏

### **2. 插件安装**

以下三款插件是在Linux下开发C/C++的三款必备插件~

- C/C++
- CMake
- CMake Tools

### **3. 快捷键**

**高频使用快捷键：**

| 功能 | 快捷键 | 功能 | 快捷键 |
| --- | --- | --- | --- |
| 转到文件 / 其他常用操作 | Ctrl + P | 关闭当前文件 | Ctrl + W |
| 打开命令面板 | Ctrl + Shift + P | 当前行上移/下移 | Alt + Up/Down |
| 打开终端 | Ctrl +` | 变量统一重命名 | F2 |
| 关闭侧边栏 | Ctrl + B | 转到定义处 | F12 |
| 复制文本 | Ctrl+C | 粘贴文本 | Ctrl+V |
| 保存文件 | Ctrl+S | 撤销操作 | Ctrl+Z |

---

**在 `Ctrl+P` 窗口下还可以:**

- 直接输入文件名，跳转到文件
- `?` 列出当前可执行的动作
- `!` 显示 `Errors`或 `Warnings`，也可以 `Ctrl+Shift+M`
- `:` 跳转到行数，也可以 `Ctrl+G` 直接进入
- `@` 跳转到 `symbol`（搜索变量或者函数），也可以 `Ctrl+Shift+O` 直接进入
- `@` 根据分类跳转 `symbol`，查找属性或函数，也可以 `Ctrl+Shift+O` 后输入:进入
- `#` 根据名字查找 `symbol`，也可以 `Ctrl+T`

**快捷键：编辑器与窗口管理**

1. 打开一个新窗口： `Ctrl+Shift+N`
2. 关闭窗口： `Ctrl+Shift+W`
3. 同时打开多个编辑器（查看多个文件）
4. 新建文件 `Ctrl+N`
5. 文件之间切换 `Ctrl+Tab`
6. 切出一个新的编辑器（最多 `3` 个） `Ctrl+\`，也可以按住 `Ctrl` 鼠标点击 `Explorer` 里的文件名
7. 左中右 `3` 个编辑器的快捷键 `Ctrl+1` `Ctrl+2` `Ctrl+3`
8. `3` 个编辑器之间循环切换 `Ctrl+`
9. 编辑器换位置， `Ctrl+k`然后按 `Left`或 `Right`

**↓ 代码编辑相关的快捷键 ↓**

**快捷键：格式调整**

1. 代码行缩进 `Ctrl+[` 、 `Ctrl+]`
2. `Ctrl+C` 、 `Ctrl+V` 复制或剪切当前行/当前选中内容
3. 代码格式化： `Shift+Alt+F`，或 `Ctrl+Shift+P` 后输入 `format code`
4. 上下移动一行： `Alt+Up` 或 `Alt+Down`
5. 向上向下复制一行： `Shift+Alt+Up` 或 `Shift+Alt+Down`
6. 在当前行下边插入一行 `Ctrl+Enter`
7. 在当前行上方插入一行 `Ctrl+Shift+Enter`

**快捷键：光标相关**

1. 移动到行首： `Home`
2. 移动到行尾： `End`
3. 移动到文件结尾： `Ctrl+End`
4. 移动到文件开头： `Ctrl+Home`
5. 移动到定义处： `F12`
6. 定义处缩略图：只看一眼而不跳转过去 `Alt+F12`
7. 移动到后半个括号： `Ctrl+Shift+]`
8. 选择从光标到行尾： `Shift+End`
9. 选择从行首到光标处： `Shift+Home`
10. 删除光标右侧的所有字： `Ctrl+Delete`
11. 扩展/缩小选取范围： `Shift+Alt+Left` 和 `Shift+Alt+Right`
12. 多行编辑(列编辑)：`Alt+Shift+鼠标左键`，`Ctrl+Alt+Down/Up`
13. 同时选中所有匹配： `Ctrl+Shift+L`
14. `Ctrl+D` 下一个匹配的也被选中 (在 sublime 中是删除当前行，后面自定义快键键中，设置与 `Ctrl+Shift+K` 互换了)
15. 回退上一个光标操作： `Ctrl+U`

**快捷键：重构代码**

1. 找到所有的引用： `Shift+F12`
2. 同时修改本文件中所有匹配的： `Ctrl+F12`
3. 重命名：比如要修改一个方法名，可以选中后按 `F2`，输入新的名字，回车，会发现所有的文件都修改了
4. 跳转到下一个 `Error` 或 `Warning`：当有多个错误时可以按 `F8` 逐个跳转
5. 查看 `diff`： 在 `explorer` 里选择文件右键 `Set file to compare`，然后需要对比的文件上右键选择 `Compare with file_name_you_chose`

**快捷键：查找替换**

1. 查找 `Ctrl+F`
2. 查找替换 `Ctrl+H`
3. 整个文件夹中查找 `Ctrl+Shift+F`

**快捷键：显示相关**

1. 全屏：`F11`
2. zoomIn/zoomOut：`Ctrl +/-`
3. 侧边栏显/隐：`Ctrl+B`
4. 显示资源管理器 `Ctrl+Shift+E`
5. 显示搜索 `Ctrl+Shift+F`
6. 显示 Git `Ctrl+Shift+G`
7. 显示 Debug `Ctrl+Shift+D`
8. 显示 Output `Ctrl+Shift+U`

### **4. [实战] 2个小项目**

通过手写2个小项目，呈现出基本的C++工程建立的过程，并编译运行这两个小项目

- **项目1：Hello world**
- **项目2：Swap with class**

### **4.1. 高频使用技巧**

- 左右分屏
- 固定打开的文件
- 格式化代码
- Rename Symbol
- 显示minimap
- 侧边栏查看OUTLINE
- 全屏
- 关闭多个打开的文件

### **4.2. 代码编写**

### **4.3. 编译并运行**


