---
title: "【Tip】使用脚本完成 Hexo 的部署与源文件管理"
date: 2021-01-02 01:00:00
tags:
- 使用技巧
- Hexo
categories:
- [使用技巧]
- [Hexo]
---

我看到不少文章介绍如何使用 Travis CI 等持续集成工具实现 Hexo 的自动部署, 包括 Hexo 的官方文档. 但我认为同样的功能使用一个简单的 Shell 脚本即可实现, 没有必要引入新的工具, 这也有悖于奥卡姆剃刀原理. 我将在这篇文章中总结自己部署 Hexo 并管理源文件的方法.

<!-- more -->

这篇文章不是 Hexo, git, GitHub 或者 Shell Script 的使用教程, 假定读者已经熟悉这些工具的使用.

假设我们的个人博客网址是 `username.github.io`, 对应的仓库 SSH 地址为 `git@github.com:username/username.github.io.git`, 我们使用同一个仓库完成 Hexo 的部署和源文件管理, 其中部署部分与官方文档没有区别, 我们主要实现使用同一个仓库进行源文件管理的功能.

首先需要在本地仓库创建一个新分支并切换到这个分支:

```sh
git checkout -b hexo
```

我们将源文件提交到这个分支上, `master` 分支仍然用于部署 Hexo. 然后按照正常流程添加远程仓库:

```sh
git remote add origin git@github.com:username/username.github.io.git
```

编写部署脚本:

```sh
#deploy.sh

# Upload source codes.
git add .
git commit -m "Upload source codes."
git push origin hexo

# Deploy the blog.
hexo clean
hexo generate
hexo deploy
```

注意始终在新建的 `hexo` 分支上进行写作, 提交到远程仓库时也是提交到远端的 `hexo` 分支上, `master` 分支始终是用来部署 Hexo 的. 这个部署脚本非常简单, 只实现了最基本的功能, 有兴趣的读者完全可以进一步修改和定制.

这样, 我们在完成写作之后, 只需要在命令行中输入

```sh
sh deploy.sh
```

即可自动完成 Hexo 的部署和源文件管理. 需要在不同的设备间迁移个人博客时, 只需要拉取 `username.github.io` 仓库的 `hexo` 分支并执行 `npm install`.