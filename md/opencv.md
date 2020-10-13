# OpenCV 配置(Win10)

[TOC]

---



## 1 说明

+ `win10`
+ `c++/c`
+ `vs2017`



## 2 安装 opencv(win10)

+ 官网下载解压
    + 例如这里解压到 `D:\installed-application\opencv`
        + 记作 `OPENCV_HOME`（不需要直接设置这个变量，这里只是方便说明）
        + 后面替换即可
    + https://opencv.org/releases/
    + 安装版本 `opencv-4.4.0-vc14_vc15.exe`
+ 配置环境变量
    + 需要配置的路径
    + `D:\installed-application\opencv\opencv\build\x64\vc15\bin`
        + `%OPENCV_HOME%\opencv\build\x64\vc15\bin`
            + `vc14` 兼容 `vs2015,2017`
            + `vc15` 兼容 `vs2017,2019`



## 3 配置环境

+ 环境：`vs2017`



### 3.1 配置项目目录

+ 新建空项目
    + `opencvPractice`
+ 视图  `->`  属性管理页
+ 右键 `Debug|x64`  `->`  添加新项目属性表
    + `OpenCV440DebugX64.props`



### 3.2 配置 include 目录

+ 双击属性页刚刚创建的`opencvPractice`
    + 属性页  `->`  `Debug|x64`  `->`  `OpenCV440DebugX64.props`
+ 配置属性  `->`  `VC++` 目录  `->`  包含目录
+ **添加**（编辑）

```txt
D:\installed-application\opencv\opencv\build\include
D:\installed-application\opencv\opencv\build\include\opencv2
```



### 3.3 配置静态库

+ 静态库作用
    + 把编译好的一些执行程序段复制到我们生成的程序里
    + 静态库可以保证我们的程序移植到没有安装OpenCV的机器上能够顺利运行 
+ 双击属性页 `opencvPractice`
+ 配置属性  `->`  `VC++` 目录  `->`  库目录
+ **添加**（编辑）

```txt
D:\installed-application\opencv\opencv\build\x64\vc15\lib
```

+ 配置属性  `->`  链接器  `->`  输入  `->`  附加的依赖项
+ **添加**（编辑）
    + 具体版本号查看路径 `D:\installed-application\opencv\opencv\build\x64\vc15\lib`
    + `d` ：`debug` 使用

```txt
opencv_world440d.lib
opencv_world440.lib
```



### 3.4 同样也可以设置一个 Release 版

+ 双击属性页刚刚创建的`opencvPractice`
    + 属性页  `->`  `Release|x64`  `->`  `OpenCV440ReleaseX64.props`



## 4 测试 opencv

+ https://docs.opencv.org/4.4.0/db/deb/tutorial_display_image.html

```cpp
#include <opencv2/core.hpp>
#include <opencv2/imgcodecs.hpp>
#include <opencv2/highgui.hpp>
#include <iostream>

int main() {
    // sample
    std::string image_path = cv::samples::findFile("starry_night.jpg");
    cv::Mat img = cv::imread(image_path, cv::IMREAD_COLOR);
    if (img.empty()) {
        std::cout << "Could not read the image: " << image_path << std::endl;
        return 1;
    }
    imshow("Display window", img);
    // Wait for a keystroke in the window
    int k = cv::waitKey(0); 
    if (k == 's') {
        imwrite("starry_night.png", img);
    }
    return 0;
}
```



## 5. 其他说明

+ 重新建立 `opencv` 的项目时可以直接添加上面已经完成的配置

+ 配置文件一般在项目路径附近

    + 例如我的项目文件路径 

    ```txt
    D:\Code\C_plus_plus\opencv\opencvPractice
    ```

    + 刚刚配置好的配置文件路径

    ```txt
    D:\Code\C_plus_plus\opencv\opencvPractice\opencvPractice\OpenCV440DebugX64.props
    D:\Code\C_plus_plus\opencv\opencvPractice\opencvPractice\OpenCV440ReleaseX64.props
    ```

+ 新建空项目之后，在属性管理器的 `Debug|x64` 中右键 **添加现有属性表**，找到上述配置文件即可

    + `Release|X64` 同理

+ 我的配置文件

    + [OpenCV440DebugX64.props](../material/opencv/OpenCV440DebugX64.props)
    + [OpenCV440ReleaseX64.props](../material/opencv/OpenCV440ReleaseX64.props)



## 6. 参考资料

+ https://www.cnblogs.com/cxyxm/p/12382990.html
+ https://www.jianshu.com/p/1942f2bbee80