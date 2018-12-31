---
title: GitHub Pages + Hexo + Travis CI 自动化构建静态博客
date: 2019-01-01 00:45:15
tags:
---
### 系统环境
```
Windows10
WorkSpace D:\Projects
```
### 安装 Node.js
http://nodejs.org/
### 安装 Git
http://git-scm.com/
### 安装 Hexo
  Win + R 键入 cmd 打开命令提示符，输入以下指令开始安装。
  ``` bash
  $ npm install -g hexo-cli
  ```
### 创建网站
  使用 Hexo 在 D:\Projects\blog 下创建网站。
  创建网站
  ``` bash
  $ D:
  $ cd Projects
  $ hexo init blog
  $ cd blog
  $ npm install
  ```
  测试网站
  ``` bash
  $ hexo deploy
  $ hexo server
  ```
### 注册 Github
### 创建仓库
  新建仓库，命名为 username.github.io，使用 README.md 初始化仓库。
### 克隆仓库
  将目录克隆到工作空间(WorkSpace = D:\Projects)下。
  ``` bash
  $ git clone https://github.com/username/username.github.io.git
  ```
### 新建 source 分支
  ``` bash
  $ git branch source
  ```
### 拷贝网站
  将 blog 目录下的所有文件拷贝过来。
  ``` bash
  $ xcopy blog username.github.io /e
  ```
### 创建 CI 脚本
  新建 .travis.yml 文件，复制以下代码，替换用户名。
  {% gist 7ae7fc06fd721b6f25a5d100938fdeb0 %}
### 推送 source 分支
### Travis CI
  打开 Travis CI，使用 Github 账号登录，并激活仓库。
  https://travis-ci.org/
### 创建 GitHub Token
  打开 Github Settings -> Developer settings -> Personal access tokens,
  创建名为 “Travis CI” 的 Token，复制。
  安全起见，不要给 delete_repo 的权限。
### Add Environment Variable
  回到 Travis CI，进入仓库 Settings -> Environment Variables
  Name 项填 GH_TOKEN
  Value 项填入刚才复制的 GitHub Token
  点击 Add

至此，便完成了基于 GitHub Pages，Travis CI 自动化构建的静态 Hexo 博客的搭建。

### 更新博客
1.拉取 username.github.io 仓库的 source 分支。
2.使用 MarkDown 编写博客。
3.提交推送。Travis CI 会在 source 分支每次更新后，触发网站的重新部署。
