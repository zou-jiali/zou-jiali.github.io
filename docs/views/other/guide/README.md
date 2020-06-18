---
title: 适合初学的利用VuePress 搭建博客网站流程
date: 2020-06-18
tags:
 - VuePress
 - Blog
categories:
 - other
---

## 简介

本篇文章记录了作为技术新手的我，一步步摸索制作blog的过程。

首先，拥有一个个人博客有什么好处？

- 能够在找工作时，为简历增彩，取得更多的面试机会
- 能够总结记录生活、工作，整理知识体系
- 能够被别人看到，提升自己的时候同时也在帮助其他需要的人

在了解到个人博客的好处后，有没有更想学习下去的冲动呢?接下来，就需要我们准备下载软件（个人推荐，编辑器可任选其一）：

**编辑器选择** 

- **Typora** （网址是 <https://typora.io/>）
  它是闭源的商业软件，在 Beta 阶段都将是免费的。它的特点是所见即所得，且在功能上没有限制，功能强大丰富，甚至可以用来作图（<http://support.typora.io/Draw-Diagrams-With-Markdown/>）。它支持简体中文界面语言，在帮助菜单里面（Help | Markdown Reference）还带有 Markdown 的语法参考的英文文档。
- **Studio Code**（网址是 <https://code.visualstudio.com/>）
  它是微软为软件开发人员推出的代码编辑器，功能强大复杂，可作为多种语言的集成开发环境。开源免费，跨平台。如果您是开发人员，可以考虑它，既可以用来开发程序，又可以编写文档。

其他

下载安装 [Node.js](https://nodejs.org/) 和 [Yarn](https://yarnpkg.com/latest.msi)。

## VuePress 

VuePress （网址是 <https://vuepress.vuejs.org/>）是一个使用 Vue.js 的静态网站生成工具，来自知名的前端框架 Vue.js 的作者尤雨溪（Evan You）。VuePress 的目的是供软件开发商用于制作在线的用户手册文档，即作为工具软件，用来生成静态网站，便于发布到互联网上。

## 开始搭建博客网站

### 1. 安装 VuePress

注意：VuePress 需要 [Node.js](https://nodejs.org/en/) >= 8.6

![image-20200618001100493](C:\Users\HP\AppData\Roaming\Typora\typora-user-images\image-20200618001100493.png)

我的主力电脑安装的是 Windows 10 专业版64位操作系统，Git 的环境略过，仅就安装 VuePress 的环境做一简要叙述。

1. 下载安装 [Node.js](https://nodejs.org/) 和 [Yarn](https://yarnpkg.com/latest.msi)。例如，在本文写作的时候，下载安装的是`node-v12.16.2-x64.msi`和`yarn-1.22.4.msi`。
   
   >  **注意：** yarn 的二进制可执行程序，位于`%LOCALAPPDATA%\Yarn\bin`，应当被添加到 **当前用户** 的 PATH 环境变量中。
   
2. 参照 VuePress 的官方文档，[安装 VuePress](https://vuepress.vuejs.org/zh/) ：
   
   ```shell
   # Install vuepress.
   yarn global add vuepress
   
   # Upgrade.
   #yarn global upgrade vuepress
   ```
   
   新打开一个命令行窗口，检查一下版本：
   
   ```shell
   vuepress --version
   ```
   
3. 【可选】按照 VuePress 的文档说明，试试建立一个网站，体验一下效果。
   
   ```shell
   # 新建一个 markdown 文件
   echo # Hello VuePress! > README.md
   
   # 开始写作，用浏览器打开看效果
   vuepress dev
   
   # 构建生成静态文件（输出到 .vuepress\dist 文件夹中）
   vuepress build
   ```



### 2. 搭建 Blog 平台

官方提到了一些博客主题：

* [VuePress - 博客主题](https://vuepress.vuejs.org/zh/theme/blog-theme.html)
* [@vuepress/plugin-blog - Writing a blog theme](https://vuepress-plugin-blog.ulivz.com/guide/getting-started.html#writing-a-blog-theme)

这些看起来都太简陋。

另有2个主题，之前在 VuePress 官方网页里出现过的，现在已经被移除。个人猜想其原因可能是，这两个主题没有完全在官方插件上做扩展，而是做了过多的底层定制和修改，在未来官方博客插件升级时，有可能不兼容。

* [vuepress-theme-modern-blog](https://github.com/z3by/vuepress-theme-modern-blog)，[演示](https://vp-modern.z3by.com/) 。此主题有点过于华丽。
* [vuepress-theme-reco](https://vuepress-theme-reco.recoluan.com/)，[演示 - 午后南杂](https://www.recoluan.com/)。此主题简洁优雅。

个人偏好，我选择了`vuepress-theme-reco`主题，下面是搭建步骤。



按官方文档的[说明](https://vuepress-theme-reco.recoluan.com/)，使用 yarn 来安装：

```shell
# Install the theme.
yarn global add @vuepress-reco/theme-cli
# Upgrade.
#yarn global upgrade @vuepress-reco/theme-cli

# 初始化（需要回答一些问题，最后一个选择： blog）
theme-cli init my-blog

# 安装
cd my-blog
yarn install
```



这将生成一个博客网站模板“my-blog”，其中“docs”文件夹里面是主要的源文件，包括配置和博客文章的 Markdown 文件。我们可以在此基础上，进行修改和定制。

```shell
# 打开本地服务
# Or: vuepress dev docs
yarn dev

# 编译生成静态网页
yarn build
```

打开本地服务后，VuePress 的开发环境可通过浏览器访问 http://localhost:8080/。在`docs\.vuepress\config.js`中设定，编译生成的静态网页将位于“public”文件夹中。



在生成的模板上，我随即更新了 `package.json` 中的依赖，使用最新的版本。最新的版本号可以在这里找到：

- VuePress: [CHANGELOG.md](https://github.com/vuejs/vuepress/blob/master/CHANGELOG.md)
- vuepress-theme-reco: [CHANGELOG.md](https://github.com/vuepress-reco/vuepress-theme-reco/blob/develop/CHANGELOG.md)

```json
{
  "devDependencies": {
    "vuepress": "1.4.1",
    "vuepress-theme-reco": "1.2.2"
  },
}
```

然后升级本地的依赖包：

```shell
yarn install
yarn upgrade
```



博客文章即 Markdown 文档。例如，其他类（other）的文章之一：《利用 VuePress 搭建博客网站》，放在 `docs\views\other\guide\`文件夹中。此文章的文件命名为 `README.md`，它将作为`http://localhost:8080/views/other/guide/`的首页。关于图片文件的引用，有一个小技巧。

1. 在 `docs\.vuepress\public\views\` 和 `docs\views\` 中建立同样的目录结构。其中前者是 VuePress 要求存放图片文件的地方，后者是 Markdown 博客文章 Markdown 文件的存放地方。
2. 为了让 Typora 编辑器打开 Markdown 文件时能够显示图片，同时又能让图片文件位于 VuePress 所要求的文件夹，我们需要在 Markdown 文件所在的文件夹中，建立一个目录连接（Directory Junction），让它指向 VuePress 要求的文件夹中（那里存放着图片文件）。

举个例子， `docs\.vuepress\public\views\other\guide\asset\` 中，存放了几张图片文件。在 Markdown 文件`README.md` 所处的文件夹 `docs\views\other\guide\`中，我们建立了一个 `asset` 目录链接，它以相对路径的方式指向了`docs\.vuepress\public\views\other\guide\asset\`。

```shell
REM We would like to create a directory junction "asset" from:
REM docs\views\other\guide\
REM to: 
REM docs\.vuepress\public\views\other\guide\asset\

REM First, check if the relative path is correct:
CD /D docs\views\other\guide\
DIR ..\..\..\.vuepress\public\views\other\guide\asset

REM Then, run the command to create the directory junction:
MKLINK /J asset ..\..\..\.vuepress\public\views\other\guide\asset
```

另外，为了避免将目录链接里面的文件重复加入到 Git 的版本控制，我们需要在 `.gitignore` 中，添加一条设置，忽略建立的目录链接。例如：

```
# ignore directory junctions.
/docs/views/other/guide/asset/
```



打开本地服务，一边用 Typora 编辑 Markdown 文章，一边用浏览器（http://localhost:8080）看效果。每次保存 Markdown 文件，浏览器的结果会自动更新（不需要手动刷新），非常方便快捷。

```shell
# 打开本地服务
# Or: vuepress dev docs
yarn dev
```

本地开发满意后，在 GitHub （也可以是 GitLab等类似的版本控制托管服务）中建立一个代码库，将本地代码提交到代码库中。



### 3. 发布到 Netlify

发布到 [Netlify.com](https://www.netlify.com)，只需要简单几步：

1. 注册 Netlify 的账号并登录，需要提供一个电子邮件。
2. 新建一个项目，在设置里面填入 GitHub 代码库的链接，填写构建的命令和输出文件夹。
   ![](asset/netlify_build_settings.png)
   按“Deploy site”按钮，耐心等候5分钟左右时间，让构建流程正常结束。
3. 构建成功后，设置定制的域名。
   ![](asset/netlify_custom_domains.png)
   例如这里，我设置了定制的域名“bobyuan”，于是可以这样访问此博客网站：
   <https://bobyuan.netlify.com/>
   
4. 【可选】每次提交到 GitHub，Netlify 将自动构建并发布网站。为了了解构建状态，在首页（README.md）中添加一个“status badge”。
   ![](asset/netlify_status_badge.png)


## 小结

本文简明扼要地给出了基于 VuePress 搭建个人博客网站的全过程，有些技术细节没有提及，读者应该也是技术人员，相信您有能力自行探索或调整。希望本文对您有所帮助。

