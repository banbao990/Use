# Github

### 1.1 支持 Latex

+ `Google Chrome` 安装插件 [github-with-mathjax](https://chrome.google.com/webstore/detail/github-with-mathjax/ioemnmodlmafdkllaclgeombjnmnbima)
+ 下载之后用 `Typora` 打开(需要点时间...)



### 1.2 下载单个文件夹

+ 使用 `SVN`
+ 下载 [SVN](https://tortoisesvn.net/downloads.zh.html)
+ 步骤（此处使用版本为 ` 1.14.0(64bit)` ）
    + 在目标文件夹中右键打开 `SVN Checkout`
    + `URL of resposity:` 中输入需要下载的文件夹
        + 注意这里要修改路径：`  /tree/master/` 换成 `/trunk/ `
        + 举个例子
            + 原始文件夹：`https://github.com/banbao990/Java/tree/master/Game/2048`
            + 修改后文件夹：`https://github.com/banbao990/Java/truck/Game/2048`
    + `Checkout directory:` 下载到本地对应的文件夹



### 1.3 合作

+ 选中需要共同合作的仓库 repository
+ 选择 setting
+ 选择 manage acesss
+ 选择 Invite a collaborator
    + 邀请别人
+ 被邀请方会收到邮件邀请
    + 接收后会有 **push** 的权限
    +  You now have **push** access to the xxx/xxx repository