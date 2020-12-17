# Open GL

[TOC]

---

+ `VS2017` 配置
+ `WIN10`



## 0. 一个简单的配置

+ [简单配置](VS2017-options.md)



## 1. 下载库

### 1.1 下载 GLFW 库

+ https://www.glfw.org/download.html
+ 直接下载已经编译好的库即可
    + https://github.com/glfw/glfw/releases/download/3.3.2/glfw-3.3.2.bin.WIN32.zip
    + 这里使用的是 `WIN32` 版本
+ 我们为你将其解压至指定目录
    + 这里为 `D:\Code\OpenGL\glfw-3.3.2.bin.WIN32\`
    + 选择好需要的版本 `lib-vc2017`



### 1.2 下载 GLAD 库

+ https://glad.dav1d.de/
+ 我们大胆的尝试版本 `4.6`，吃个螃蟹
+ 选择

```txt
Language         ->   C/C++
Specification    ->   OpenGL
API/gl           ->   Version 4.6
Profile          ->   Core
Options          ->   Generate a loader

其他都选择默认
```

+ 下载生成的 ` glad.zip` 文件
    + 就是上面的几个文件夹的压缩包
    + 解压至指定目录
        + 这里为 `D:\Code\OpenGL\glad`



## 2. 配置 VS2017

+ 新建一个空项目

    + 例如我这里
        + 目录 `D:\Code\OpenGL\VS2017`
        + 项目名 `OpenGL`

+ 配置属性：项目 `->` 属性

    + 配置：**活动(Debug)**

    + 平台：`WIN32`

    + 配置属性 `->` `VC++` 目录

        + **包含目录**（头文件）添加上述两个库的 `include` 文件夹

        ```txt
        D:\Code\OpenGL\glad\include
        D:\Code\OpenGL\glfw-3.3.2.bin.WIN32\include
        ```

        + **库文件** 中添加

        ```txt
        D:\Code\OpenGL\glfw-3.3.2.bin.WIN32\lib-vc2017
        ```

    + 链接器 `->` 输入 `->` 附加依赖项

    ```txt
    opengl32.lib
    glfw3.lib
    ```

+ 配置完成后将 `glad` 包中的 `src` 中的 `glad.c` 复制到项目中的源文件中



## 3. 测试

+ 新建源文件测试
+ https://learnopengl.com/code_viewer_gh.php?code=src/1.getting_started/1.2.hello_window_clear/hello_window_clear.cpp



## 4. 参考资料

+ https://blog.csdn.net/qq_36696486/article/details/104155711
+ https://learnopengl.com/Getting-started/Creating-a-window
