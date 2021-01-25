Node.js

[TOC]

---



## 1. 退出命令行模式

```js
process.exit()
```



## 2. 安装 node.js

+ 官网下载即可
+ http://nodejs.cn/download/



## 3.  修改安装包路径

```shell
npm config set prefix "D:/installed-application/nodejs/module_cache/npm_global"
npm config set cache "D:/installed-application/nodejs/module_cache/npm_cache"
```



## 4. 安装包

+ 以 *http-server* 为例
    + -g：全局安装

```bash
npm install http-server -g
```

+ 网络代理问题报错
    + 换用源

```shell
npm --registry https://registry.npm.taobao.org install http-server -g 
```

+ 永久换源

```shell
npm config set registry https://registry.npm.taobao.org
```

