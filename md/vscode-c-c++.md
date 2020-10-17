# VS Code 配置 C/C++ 编译环境

[TOC]

---



## 1. 安装 mingw-w64

+ 直接通过下载 http://www.mingw-w64.org/doku.php/download 会出问题

    + 安装时会报错

    ```txt
    the file has been downloaded incorrectly
    ```

+ 直接在下载对应的文件（预编译的版本）
  
    + https://sourceforge.net/projects/mingw-w64/files/mingw-w64/
    
+ 版本选择

```txt
64位:x86_64, 32位:i686

开发Windows程序:win32, Linux/Unix/Mac OS 等其他操作系统下的程序:posix
(现在还不是太清楚区别)

异常处理模型, seh性能比较好, 不支持32位, sjlj稳定性好, 支持32+64位(dwarf性能比较好, 不支持64位)
```

+ 将文件解压至指定目录

```txt
D:\installed-application\mingw64
```

+ 配置环境变量

```txt
D:\installed-application\mingw64\bin
```



## 2. VS Code 配置(基于 mingw)

+ 如果已经安装了 `Visual Studio`，也可以直接配置
    + https://code.visualstudio.com/docs/cpp/config-msvc
+ 这里基于 `mingw`
    + https://code.visualstudio.com/docs/cpp/config-mingw
+ 配置环境无特殊要求直接默认即可
    + 配置编译执行环境(添加 `tasks.json` )
        +   **Terminal** > **Configure Default Build Task** > **g++.exe**
    + 配置 `Debug` (添加 `launch.json` )
        +   **Run** > **Add Configuration...**  > **C++ (GDB/LLDB)**. 
+ 一些官网建议
    + You can modify your `tasks.json` to build multiple C++ files by using an argument like `"${workspaceFolder}\\*.cpp"` instead of `${file}`. This will build all `.cpp` files in your current folder. You can also modify the output filename by replacing `"${fileDirname}\\${fileBasenameNoExtension}.exe"` with a hard-coded filename (for example `"${workspaceFolder}\\myProgram.exe"`).





## 3. 参考资料

+ https://stackoverflow.com/questions/46455927/mingw-w64-installer-the-file-has-been-downloaded-incorrectly
+ https://code.visualstudio.com/docs/languages/cpp
+ https://code.visualstudio.com/docs/cpp/config-mingw