# VS Code(python 配置)

[TOC]

---



## 1. 说明

+ 基于 `Anaconda` 具体环境配置
+ `powershell` 无法使用 `activate env_name` 功能
    + `cmd` (不需要打开 `conda` 的某个环境)
        + ` conda install -n root -c pscondaenvs pscondaenvs `
    + 管理员身份打开 `powershell`
        + ` Set-ExecutionPolicy RemoteSigned `
        + `Y`



## 2. Anaconda

### 2.1 官网下载

### 2.2 配置新环境

+ 版本、名字自己选择
    + `cv_env`
    + `3.7`

```powershell
conda create -n cv_env python=3.7 --yes --no-default-packages
```

+ 进入环境

```powershell
activate cv_env
```

+ 退出环境

```powershell
conda deactivate
```



## 3. VS Code

+ 安装插件
    + `Anaconda Extension Pack`
    + `YAML`
    + `Python`
+  `file` > `preferences` > `setting`
+ 搜索 `python.python Path` 
+ 修改为具体的环境中的 `python` 路径，例如

```txt
D:/installed-application/Anaconda3/envs/cv_env/python.exe
```

+ 配置文件
+ `tasks.json`

```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "py37",
            "type": "shell",
            "command": "D:/installed-application/Anaconda3/envs/cv_env/python.exe ${file}",
            "problemMatcher": [],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

+ `settings.json`

```json
{
    "python.pythonPath": "D:/installed-application/Anaconda3/envs/cv_env/python.exe",
    "python.terminal.activateEnvironment": false
}

```

+ `launch.json`

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: cv44py37",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "pythonPath": "${command:python.interpreterPath}"
        }
    ]
}
```



## 4. opencv

### 4.1 下载 opencv

+ 官网下载 `opencv`

    + https://opencv.org/releases/

+ 我下载的版本

    + https://sourceforge.net/projects/opencvlibrary/files/4.5.0/opencv-4.5.0-vc14_vc15.exe/download

+ 解压到指定文件夹

    + 添加环境变量（解压文件夹中的对应版本呢）

    ```txt
    D:\installed-application\opencv\opencv\build\x64\vc15\bin
    ```

+ 将 `opencv` 加入到 `Anaconda` 环境中(复制)

```txt
D:\installed-application\opencv\opencv\build\python\cv2\python-3.7\cv2.cp37-win_amd64.pyd

=>

D:\installed-application\Anaconda3\envs\cv_env\Lib\site-packages
```

+ 依赖库缺少下啥就行
    + 执行不下去了就要下了

```powershell
activate cv_env
conda install numpy
conda install scipy
```

+ 安装完成后可以试一试

```python
import cv2 as cv
print(cv.__version__) # 4.4.0 => OK
```





## 5. 参考资料

+ https://blog.csdn.net/shiren8538/article/details/80926213
+ https://www.cnblogs.com/bjxqmy/p/12971005.html#ready
