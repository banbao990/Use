# VSCode opencv 配置(未完成)

[TOC]

---

+ `win10`
+ `C/C++`



## 1. 准备工作

### 1.1 安装 opencv

#### 1.1.0 说明

+ 这里不能使用 [VS2017教程](opencv-VS2017.md) 中编译完成的文件，因为用的编译器是 `mingw`
    + 也就是说要自己进行编译 `opencv` 的源码
    + 如果你使用的是 `MSVC` 的话应该是可以直接使用之前下载的文件的
+ **没有完成编译，我使用的是别人已经编译完成的版本**
    + https://github.com/huihut/OpenCV-MinGW-Build



#### 1.1.1 下载 opencv+opencv_contrib 源码

+ https://opencv.org/releases/

+ https://github.com/opencv/opencv_contrib/releases

+ `Sources`

+ 解压到指定目录

    + 例如我这里

    ```txt
    D:\installed-application\opencv\opencv-src\opencv-4.4.0
    D:\installed-application\opencv\opencv_contrib-4.4.0
    ```



#### 1.1.2 下载 mingw

+ [教程](vscode-c-c++.md)



#### 1.1.3 通过 mingw-gui 生成 cmake 文件

##### (1) 设置路径

```txt
Where is the source code:
 	D:\installed-application\opencv\opencv-src\opencv-4.4.0
Where to build the binaries: 
	D:\installed-application\opencv\opencv-built-mingw
```



##### (2) 设置 Configue

```txt
Specify the generator for this project: 
	MinGW Makefiles
Specify native compilers

Next

Compilers C:
	D:/installed-application/mingw64/bin/gcc.exe
Compilers C++:
	D:/installed-application/mingw64/bin/g++.exe

Finish
```



##### (3) 然后进入一段漫长读条时间

+ 测试 + 联网下载



##### (4) 开始处理爆红的问题

+ **注意文件路径分隔符必须使用 `/`**
+ `opencv_contrib`
    + **search** > **extra**
    + `OPENCV_EXTRA_MODULES_PATH` 的 `value`  中选择 `opencv_contrib` 的 `module` 目录
+  **search** > **nonfree**
    + 勾选 `OPENCV_ENABLE_NONFREE`
+  **search** > **world**
    + 勾选 `BUILD_OPENCV_WORLD`
+ 勾选 `WITH_QT`，`WITH_OPENGL` ，不能勾选 `WITH_IPP` (默认不勾选)
+ 取消选中 `WITH_MSMF`

##### (5) 重新 Configue 即可

+ 我的 `configue` [输出](../material/opencv/configuration.txt)



##### (6) 支持和 cuda 一起编译

+ 但是没有尝试



#### 1.1.4 进行编译

+ 进入到 `D:\installed-application\opencv\opencv-built-mingw` 文件夹中
+ 打开 `cmd/powershell`
+ `mingw32-make`
    + 多线程编译 ` mingw32-make -j 8`
+ 出错记录

```txt
gcc: error: long: No such file or directory

(回到 1.1.3 mingw-gui, generate)
	OPENCV_ENABLE_ALLOCATOR_STATS: false
```

+ 弃坑了（搞不动）

```java
/**
 * ERROR
 */
```





### 1.2 vscode 安装插件 C/C++

+ 搜索插件 `c/c++` 下载安装即可
+ 配置 `c/c++` 查看[教程](vscode-c-c++.md)







## 2. 通过 json 配置文件



## 3. 通过 CMakeLists.txt



## 4. 参考资料

+ https://blog.csdn.net/huihut/article/details/81317102

