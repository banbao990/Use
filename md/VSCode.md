# VS Code

[TOC]

---



## 1. 取消 git

+ `Git enabled:false`



## 2. 修改代码格式

- **File** > **Preferences** > **Settings** > **Extensions** > **Scroll down and find "Edit in settings.json"**
- 添加

```json
"C_Cpp.clang_format_style": "{ BasedOnStyle: Google, IndentWidth: 4}"
```



## 3. 支持 js 自动补全

+ 下载 `typings`

```powershell
npm install -g typings
```

+ 添加配置文件 `jsconfig.json`

```json
{
    "exclude": ["node_modules"],
    "typeAcquisition": {
        "include": ["d3"]
    }
}
```

