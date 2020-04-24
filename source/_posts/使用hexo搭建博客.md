---
title: 使用hexo搭建博客
date: 2020-01-12 14:50:05
tags: [hexo, github]
---

那个男孩子不想拥有一个个人博客（还是免费的）

现在有很多第三方博客网站，掘金，简书，csdn等，今天就来搭建一个个人的博客网站，基于Github Page，国内可以通过码云，coding等网站托管，操作步骤大体相同。

<!-- more -->

## 目录

1. [环境要求](#环境要求)

2. [安装Hexo](#安装Hexo)

3. [Github设置](#Github设置)

4. [配置 SSH key](#配置-SSH-key)

5. [部署到Github](#部署到Github)

6. [写博客](#写博客)

7. [图床推荐](#图床推荐)

8. [接入腾讯公益404](#接入腾讯公益404)

***

## 环境要求

需要 node 和 git 环境

node中文网 [http://nodejs.cn/](#http://nodejs.cn/)

git教程和使用参考廖雪峰的教程 [git教程](#https://www.liaoxuefeng.com/wiki/896043488029600/896067008724000)

## 安装Hexo

Hexo官网 [https://hexo.io/zh-cn/](#https://hexo.io/zh-cn/)

1. 全局安装 hexo

    `npm install hexo-cli -g`

2. 创建 hexo 项目

    ```cmd
    hexo init blog
    cd blog
    npm i
    ```

3. 项目目录和运行

    创建后的项目目录

    ```txt
    ├── _config.yml # 网站的配置信息
    ├── package.json
    ├── scaffolds # 模版文件夹
    ├── source  # 资源文件夹
    |   ├── _drafts # 草稿文件夹
    |   └── _posts # 博客文章Markdowm
    └── themes  # 主题文件夹
    ```

    本地运行命令 `hexo s`

    浏览器打开` http://localhost:4000` 就可以看到效果

## Github设置

Github上新建一个项目

项目名必须为 `github用户名.github.io`

![ ](https://s1.ax1x.com/2020/04/24/JB9IUg.png)

创建完成后

在根目录添加一个index.html，随便编辑一些东西

然后打开 `http://你的用户名.github.io` 就可以看到你写的东西了

## 配置 SSH key

使用hexo自动部署需要使用SSH key

1. 查看是否生成过打开cmd输入

    `cd ~/.ssh` 没报错说明以前生成过直接使用 `cat ~/.ssh/id_rsa.pub` 命令就是可以查看本机上的 SSH key

2. 以前未生成过SSH key

    全局配置git账号

    ```cmd
    git config --global user.name "用户名"
    git config --global user.email "邮箱地址"
    ```

    开始生成 SSH key

    `ssh-keygen -t rsa -C '邮箱地址'`

    ![ ](https://s1.ax1x.com/2020/04/24/JBAlHx.jpg)

    返回 `Hi xxx! You've successfully authenticated, but GitHub does not provide shell access.` 说明添加SSH成功

3. 添加SSH key 到 Github

    ![ ](https://s1.ax1x.com/2020/04/24/JBZPud.png)

## 部署到Github

官方部署文档 [部署文档](https://hexo.io/zh-cn/docs/one-command-deployment)

1. 配置_config.yml 文件参数

    ```yml
    deploy:
      type: git
      repo:
        github: https://github.com/用户名/用户名.github.io
      branch: 分支名字
    ```

2. 要安装一个部署插件 `hexo-deployer-git`

    `npm install hexo-deployer-git --save`

3. 执行命令部署上传

    `hexo g -d`

4. 打开你的博客地址

## 写博客

官网写作文档 [https://hexo.io/zh-cn/docs/writing](https://hexo.io/zh-cn/docs/writing)

如果你不会 `markdown` 的书写，请先阅读 [菜鸟教程 | Markdown 教程](https://www.runoob.com/markdown/md-tutorial.html)

1. 新建文章

    `hexo new '文章标题'`

2. 文章目录

    新建的文章在 `/source/_posts` 中查看到

  本地运行查看

  ```cmd
  hexo g
  hexo s
  ```

  就可以看到你写的博客

  最后，部署项目

  ```cmd
  hexo clean
  hexo g -d
  ```

  运行 `hexo clean` 为了清除缓存文件和已生成的静态文件，尤其是更换主题后需要执行一次

## 图床推荐

上传到图床后可以直接到md文件中引用

(转载自知乎：<https://zhuanlan.zhihu.com/p/35270383?ivk_sa=1023345p>)

选几个我常用的来列举，上面链接里有更多的图床介绍

1. [七牛云](https://portal.qiniu.com)

    注册认证后有10G永久免费空间，每月10G国内和10G国外流量，速度相当快，七牛云是国内专业CDN服务商，插件支持比较多，有免费ssl证书，但https流量收费

    注意：七牛云30天后会回收测试域名，因此你必须要绑定自己的已备案的域名

2. [公益图床](http://sbimg.cn)

    长期保存需要注册使用，这个图床服务器在国内应该还用了cdn，总之速度非常快

3. [路过图床](https://imgchr.com)

    支持免注册上传图片，永久存储，支持HTTPS加密访问和调用图片，提供多种图片链接格式，成立于2011年

    限制：最大10M

4. [聚合图床](https://www.superbed.cn)

    将图片分发到多处备份，借助其本身的CDN加速功能，节省服务器流量，并且不用担心图片被删除，即便其中某几个图床上的图片被删除了，还有其他备份，保证万无一失，支持匿名和注册管理

## 接入腾讯公益404

公益404网站 [https://www.qq.com/404/](https://www.qq.com/404/)

在 `/source` 根目录下建立 `404.html`

接入公益404JS文件，修改跳转到自己的博客主页

## 结束语

到这一个基本框架的博客就搭建好了，想要自己想要的功能和主题可以阅读Hexo的官方文档来修改和定制。
