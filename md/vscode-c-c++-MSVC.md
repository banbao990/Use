# VS Code 配置 C/C++ 编译环境

[TOC]

---



## 1. 安装 visual studio 2017

+ 官网下载安装即可



## 2. VS Code 配置(基于 vs2017/ MVSC)

+ 为了防止变量冲突，在环境变量 `PATH` 去掉 `mingw` 的路径
+ 如果已经安装了 `Visual Studio`，也可以直接配置

+ https://code.visualstudio.com/docs/cpp/config-msvc

+ 配置编译执行环境(添加 `tasks.json` )
    
    +   **Terminal** > **Configure Default Build Task** > **cl.exe**
    
    ```json
    {
        "version": "2.0.0",
        "tasks": [
            {
                "type": "shell",
                "label": "cl.exe build active file",
                "command": "cl.exe",
                "args": [
                    "/Zi",
                    "/EHsc",
                    "/Fe:",
                    "${fileDirname}\\${fileBasenameNoExtension}.exe",
                    "${file}"
                ],
                "problemMatcher": ["$msCompile"],
                "group": {
                    "kind": "build",
                    "isDefault": true
                }
            }
        ]
    }
    ```
    
+ 配置 `Debug` (添加 `launch.json` )
    
    +   **Run** > **Add Configuration...** > **C++ (Windows)**
    
    ```json
    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "cl.exe build and debug active file",
                "type": "cppvsdbg",
                "request": "launch",
                "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
                "args": [],
                "stopAtEntry": false,
                "cwd": "${workspaceFolder}",
                "environment": [],
                "externalConsole": false,
                "preLaunchTask": "cl.exe build active file"
            }
        ]
    }
    
    ```

+ 一些官网建议
    + You can modify your `tasks.json` to build multiple C++ files by using an argument like `"${workspaceFolder}\\*.cpp"` instead of `${file}`. This will build all `.cpp` files in your current folder. You can also modify the output filename by replacing `"${fileDirname}\\${fileBasenameNoExtension}.exe"` with a hard-coded filename (for example `"${workspaceFolder}\\myProgram.exe"`).





## 3. 参考资料

+ https://stackoverflow.com/questions/46455927/mingw-w64-installer-the-file-has-been-downloaded-incorrectly
+ https://code.visualstudio.com/docs/languages/cpp
+ https://code.visualstudio.com/docs/cpp/config-mingw