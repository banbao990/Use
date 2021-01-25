# Github 静态托管网页搭建

[TOC]

---



## 0. 一些说明

+ 基于 Hexo 进行搭建
    + https://hexo.io/zh-cn/
+ 需要的组件
    + *Git*
    + *node.js*
+ 我的版本信息

|  部件   |             版本             |
| :-----: | :--------------------------: |
| node.js |           v14.15.4           |
|   npm   |           6.14.10            |
|   Git   | git version 2.24.1.windows.2 |



## 1. 安装 Hexo

```shell
npm install -g hexo-cli
```

+ 如果下载不下来的话可以换源

```shell
npm --registry https://registry.npm.taobao.org install hexo-cli -g
```

+ 需要将 hexo 所在的目录添加到环境变量
+ 使用如下命令查看 `prefix` 即为安装目录

```shell
npm config ls
```



## 2. 开始我们的快乐

+ 如果命令太慢的话可以直接对 npm 换源

```shell
npm config set registry https://registry.npm.taobao.org
```

+ 新建一个空白文件夹
    + 之后的命令行操作均在该文件夹目录下进行

```shell
hexo init
npm install
```

+ 生成页面与预览

```shell
hexo g
hexo s
```

+ 指定端口打开预览

```shell
hexo server -p 5000
```



## 3. 部署 Hexo 到 GitHub Pages

+ 安装 *hexo-deployer-git*
    + 这里是安装在局部

```shell
npm install hexo-deployer-git --save
```

+  修改配置文件 *_config.yml* 的 *Deployment* 部分

```yaml
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: ""
```

```yaml
# Deployment
# Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repository: git@github.com:banbao991/banbao991.github.io.git
  branch: main
```

+ 将 "banbao991" 修改文你自己的用户名即可
+ 上传

```shell
hexo d
```



## 4. 其他

### 4.1 新建文件

```shell
hexo new "New.File"
```

+ 然后进入文件夹 *source/_posts* 编辑即可



### 4.2 修改主题

+ 例如 *NexT*

```shell
git clone https://github.com/next-theme/hexo-theme-next.git themes/nexT
```

+ 修改配置文件 *_config.yml* 的 *Extensions* 部分

```yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: landscape
```

```yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: nexT
```

+ 支持 *Latex*

    + 修改 *nexT* 的主题的配置文件 *_config.yml*

    ```yaml
    math:
      # Default (false) will load mathjax / katex script on demand.
      # That is it only render those page which has `mathjax: true` in front-matter.
      # If you set it to true, it will load mathjax / katex srcipt EVERY PAGE.
      every_page: false
    
      mathjax:
        enable: false
        # Available values: none | ams | all
        tags: none
    
      katex:
        enable: false
        # See: https://github.com/KaTeX/KaTeX/tree/master/contrib/copy-tex
        copy_tex: false
    ```

    ```yaml
    math:
      every_page: false
    
      mathjax:
        enable: true
        tags: none
    
      katex:
        enable: true
        copy_tex: false
    ```

    + 然后在需要进行渲染的 *markdown* 文件开头加上 *mathjax: true*



### 4.3 nexT 主题细节

#### (1) 网页配置文件

+  *_config.yml*

##### [1] 主题

```yaml
# Schemes
# scheme: Muse
# scheme: Mist
# scheme: Pisces
scheme: Gemini
```



#### (2) nexT 主题配置文件

+  *themes/nexT/_config.yml*

##### [1] 菜单

```yaml
# 格式: 目录 || 图标

menu:
  home: / || fa fa-home
  # about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  # schedule: /schedule/ || fa fa-calendar
  # sitemap: /sitemap.xml || fa fa-sitemap
  # commonweal: /404/ || fa fa-heartbeat
```



##### [2] 目录

```yaml
toc:
  enable: true
  number: false  
  # 给标题添加标号
  wrap: false
  expand_all: false
  max_depth: 6
```



##### [3] 侧边栏

```yaml
# 头像
avatar:
  url: /images/avatar.jpg
  rounded: true
  rotated: false
```



##### [4] 顶部头像

```yaml
favicon:
  small: /images/favicon-16x16-next.jpg
  medium: /images/favicon-32x32-next.jpg
  apple_touch_icon: /images/apple-touch-icon-next.jpg
  safari_pinned_tab: /images/logo.svg
  # android_manifest: /manifest.json
```



##### [5] 访问次数

+ 出现数字不对是本地的问题，在线就没事

```yaml
busuanzi_count:
  enable: false
  total_visitors: true
  total_visitors_icon: fa fa-user
  total_views: true
  total_views_icon: fa fa-eye
  post_views: true
  post_views_icon: far fa-eye
```



### 4.4 添加分类模块

```bash
hexo new page tags
```

+ 此时会在 *source/tags* 文件夹下生成一个 *index.md* 文件
+ 打开这个文件，顶部加上一句

```markdown
type: "tags"
```

+ 按照 *(2)->[1]* 设置显示 *tags* 标签即可
+ 添加 *categories* 模块

```markdown
type: "categories"
```



### 4.5 插入图片

```shell
 npm install hexo-asset-image --save
```

+ 根目录的配置文件

```yaml
post_asset_folder: true
```

+ 之后新建 md 文件的时候便会同时新建一个为同名文件夹，用于保存引用的图片
+ 但是存在一个问题，**图片路径不一致**
+ 解决方案如下
+ 打开文件 node_modules/hexo-asset-image/index.js
+ 修改如下

```js
if(/.*\/index\.html$/.test(link)) {
    appendLink = 'index/';
    var endPos = link.lastIndexOf('/');
}
else {
    var endPos = link.lastIndexOf('.');
}
```

```js
if(/.*\/index\.html$/.test(link)) {
    appendLink = 'index/';
    var endPos = link.lastIndexOf('.');
}
else {
    var endPos = link.lastIndexOf('/');
}
```

### 4.6 github 挂载和本地不一致

```she
hexo clean
hexo d -g
```

+ 注意头像文件等的保存



## 5. 参考资料

+ https://zhuanlan.zhihu.com/p/60578464
+ https://hexo.io/zh-cn/docs/
+ https://www.cnblogs.com/thanksblog/p/12900165.html
+ http://theme-next.iissnan.com/getting-started.html
+ https://www.jianshu.com/p/3a05351a37dc