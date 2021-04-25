# mitsuba0.6 配置

## 下载源代码

```shell
git clone --recursive https://github.com/mitsuba-renderer/mitsuba.git
```



## 开始编译

+ 使用 `mitsuba-msvc2017.sln`
    + 最终使用了命令行编译
    + 可能需要配置一些 `msvc` 的环境变量





### 运行 python 文件报错

+ `print` 语法问题
    + 原来使用的版本是 `py2`
+ 利用 anaconda 创建一个 2.7 的环境

```shell
conda create -n py27 python=2.7
```



### 未安装 scons

+ 利用提供的 scons 2.5.1
    + https://github.com/mitsuba-renderer/dependencies_win64

```shell
activate py27
python setup.py install
```



### UnicodeDecodeError

+ UnicodeDecodeError: 'ascii' codec can't decode byte 0xc9 in position 9: ordinal not in range(128):
+ `scons` 在编译时候会检查所有的环境变量（不仅仅是 path），如果环境变量中含有非 ascii 码的字符就会报错退出
+ 暂时的解决方案是把环境变量中的中文部分做一个修改（或者临时备份，到时候再改回去）



### configuration

+ 把 build 文件夹下的 `config-win64-msvc2017.py` 复制成 `config.py`



### required build dependency

+ 下载链接：https://github.com/mitsuba-renderer/dependencies_win64
+ 解压到 `mitsuba` 文件夹下，重命名为 `dependencies`



### Qt

+ 到此位置应该能够运行 `mitsuba.exe` 了，但是还是不能运行 `misgui.exe`
+ 可以从 `dependencies\include\QtCore` 中看到 Qt 的版本是 `5.9.1` ，去官网下载对应版本
+ https://download.qt.io/archive/qt/5.9/5.9.1/
+ 安装的时候除了默认选项之外，我把所有的 `VS2017` 相关的都加上了
+ 安装完之后把安装目录下的 `platforms/qwindows.dll` 复制到 `dist/platforms/qwindows.dll`
    + 可以在安装目录下搜索 `qwindows.dll`
+ 由于版本问题，需要用 `Qt` 安装目录下的同名文件覆盖 `mtsgui.exe` 同目录下的如下文件

```txt
Qt5Core.dll
Qt5Gui.dll
Qt5Network.dll
Qt5OpenGL.dll
Qt5Widgets.dll
Qt5Xml.dll
Qt5XmlPatterns.dll
```



### 大功告成



## 安装过程中踩的坑

### (1) 安装 scons(不能这么安装, 版本太高)

+ <span style="color:red;font-weight:bold">不能这么安装, 版本太高</span>
    + 4.1

```shell
python -m pip install scons
```

+ 注意需要把 `python` 安装的 `Scripts` 添加到环境变量 `PATH` 中
+ 例如

```txt
d:\installed application\python\scripts\
```



### (2) scons 2.5.1 只支持 python2.x

+ 修改 python 为 3.x 失败

#### 之前的修改方式

+ 利用正则表达式修改为 `py3` 语法
    + notepad++
    + 注意原来的 L175 是多行的，需要手动改一下

```txt
print([^\n\r]*)
->
print\(\1\)
```



### (3) 一个问题

+ 如果通过 `mitsuba-msvc2017.sln` 安装的话，需要临时修改环境变量
    + scons 安装在了环境 py27 下
    + 于是 VS2017 调用的应该也是这个环境，而不是我们之前的环境
    + 暂时的解决方案是把环境变量暂时设置为 py27 的环境

```txt
d:\installed application\python\scripts\
D:\installed application\python
```

```txt
D:\installed-application\Anaconda3\envs\py27\Scripts
D:\installed-application\Anaconda3\envs\py27
```



## 参考资料

+ https://github.com/mitsuba-renderer/mitsuba/issues/
+ https://github.com/mitsuba-renderer/mitsuba/issues/52#issuecomment-356929115
+ https://github.com/mitsuba-renderer/mitsuba/issues/143