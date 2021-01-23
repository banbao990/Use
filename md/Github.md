# Github

[TOC]

---



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



### 1.4 Github Desktop 无法 push

+ Authentication failed 问题解决
+ 重新生成 *SSH Key*



#### (1) 检查是否已经生成

+ 打开 `git-bash`

```powershell
ls -al ~/.ssh
```

+ 若有显示目录，则可以直接使用已经生成的 *id_ras.pub* 中的内容
+ 可以直接跳到最后一步，或者重新生成



#### (2) 检查账号配置

```powershell
git config user.name
git config user.email
```

+ 如果没有配置，则进行配置

```powershell
git config --global user.name "banbao990"
git config --global user.email "xxx@xx.xxx"
```



#### (3) 生成新的 SSH Key

```powershell
ssh-keygen -t rsa -C "上面的邮箱"
```

+ -t：生成算法
+ -C：注释
+ 一路回车即可



#### (4) Github 添加 SSH Key

+ https://github.com/settings/keys
+ New SSH Keys
+ 复制文件 *id_rsa.pub* 的内容即可
+ Add SSh key
+ 重启 Github Desktop 即可
    + 还不行的话重新登陆下账号