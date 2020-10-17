# VSCode opencv 配置

[TOC]

---

+ `win10`
+ `C/C++`



## 1. 安装 opencv

+ [VS2017](opencv-VS2017.md)



## 2. 通过 json 文件配置

+ 配置 `c_cpp_properties.json`
+ `ctrl+shift+P` > `C/C++ configurations` > `Edit Configurations (JSON) `
+ 修改

```json
"includePath": [
    "${workspaceFolder}/**",
    "D:/installed-application/opencv/opencv/build/include",
    "D:/installed-application/opencv/opencv/build/include/opencv2"
],
```

+ 在环境变量 `INCLUDE` 中添加路径

```txt
D:/installed-application/opencv/opencv/build/include
D:/installed-application/opencv/opencv/build/include/opencv2
```

+ 在环境变量 `LIB` 中添加路径

```json
D:\installed-application\opencv\opencv\build\x64\vc15\lib
```

+ 修改 `tasks.json`

```json
"args": [
    "/Zi",
    "/EHsc",
    "/Fe:",
    "${fileDirname}\\${fileBasenameNoExtension}.exe",
    "${file}",
    "opencv_world440.lib"
],
```

+ 最终我的配置文件
    + [tasks.json](../material/opencv/vscode/tasks.json)
    + [launch.json](../material/opencv/vscode/launch.json)
    + [c_cpp_properties.json](../material/opencv/vscode/c_cpp_properties.json)



## 3. 没有解决的问题

+ 发布到没有安装 `opencv` 的机子上运行



## 4. 参考资料

+ https://blog.csdn.net/weixin_41115751/article/details/89880333
+ https://blog.csdn.net/weixin_41115751/article/details/89817123