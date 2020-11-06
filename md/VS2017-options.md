# VS2017

[TOC]

---

+ https://docs.microsoft.com/en-us/cpp/build/reference/c-cpp-building-reference?view=msvc-150



## 1. 一些参数的说明

### (1) LIBPATH

+ /LIBPATH (Additional Libpath)
+ Specifies a path that the linker will search before it searches the path specified in the LIB environment option. 
+  Use the /LIBPATH option to override the environment library path. The linker will first search in the path specified by this option, and then search in the path specified in the LIB environment variable. You can specify only one directory for each /LIBPATH option you enter. If you want to specify more than one directory, you must specify multiple /LIBPATH options. The linker will then search the specified directories in order. 



### (2) LIB

+ 对应环境变量 `LIB`
    + `LIB` is for the linker, helps it find import and static libraries.
    + `LIBPATH` is for the compiler, helps it find metadata files. Like type libraries, .NET assemblies, WinRT .winmd files.



## 2. OpenGL

```txt
INCLUDE
D:\Code\OpenGL-course\include

LIB
D:\Code\OpenGL-course\lib

链接器-输入
opengl32.lib
glew32.lib
glut32.lib
```

+ 设置环境变量 `PATH`
    + 添加 `D:\Code\OpenGL-course\dll`
+ 设置完成之后在对应目录放置文件即可

