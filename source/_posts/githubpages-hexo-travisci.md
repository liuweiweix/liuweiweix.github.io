---
title: GitHub Pages/Hexo/Travis CI 搭建自动化构建静态博客
---

系统环境
Windows10
WorkSpace D:\Projects

1.安装 Node.js http://nodejs.org/
2.安装 Git http://git-scm.com/
3.安装 Hexo
  3.1 Win + R 键入 cmd 打开命令提示符
  3.2 $ npm install -g hexo-cli 开始安装
4.使用 Hexo 在 D:\Projects\blog 下创建网站
  4.1 创建网站
  $ D:
  $ cd Projects
  $ hexo init blog
  $ cd blog
  $ npm install
  4.2 测试网站
  $ hexo deploy
  $ hexo server
5.注册 Github
6.新建仓库，命名为 username.github.io，使用 README.md 初始化仓库
7.将目录克隆到工作空间(WorkSpace = D:\Projects)下
  $ git clone https://github.com/username/username.github.io.git
8.新建分支 source
  $ git branch source
9.将步骤 4 所创建网站根目录下的所有文件拷贝过来
  $ xcopy blog username.github.io /e
10.新建 .travis.yml 复制下文链接的内容，替换用户名
  https://gist.github.com/liuweiweix/7ae7fc06fd721b6f25a5d100938fdeb0
11.将 source 分支的修改推送到远端
12.打开 Travis CI，使用 Github 账号登录，并激活仓库
  https://travis-ci.org/
13.打开 Github Settings -> Developer settings -> Personal access tokens,
  创建名为 “Travis CI” 的 Token，复制 Token
  安全起见，不要给 delete_repo 的授权
14.回到 Travis CI，进入仓库 Settings -> Environment Variables
  Name  GH_TOKEN
  Value 填入刚才复制的 Token

至此，便完成了基于 GitHub Pages，Travis CI 自动化构建的静态 Hexo 博客的搭建。

更新博客：
1.拉取 username.github.io 仓库的 source 分支。
2.使用 MarkDown 编写博客内容保存到 source/_posts。
3.提交推送。Travis CI 会在 source 分支每次更新后，触发网站的重新部署。
