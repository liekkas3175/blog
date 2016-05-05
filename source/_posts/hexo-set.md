title: hexo搭建
date: 2015-08-31 20:51:53
tags: technology
---

hexo是一款基于Node.js的静态博客框架。

## 如何搭建hexo

**安装**
1、安装[git](http://www.git-scm.com/downloads "链接到git下载地址")
2、安装[nodejs](https://nodejs.org/ "链接到nodejs下载地址")

**安装hexo**
利用 npm 命令即可安装。
```bash
npm install -g hexo
npm install hexo-deployer-git --save
```

**创建hexo文件夹**
安装完成后，在你喜爱的文件夹下（如D:\hexo），Hexo 即会自动在目标文件夹建立网站所需要的所有文件。
```bash
hexo init
```

**安装依赖包**
```bash
npm install
```

**本地查看**
现在我们已经搭建起本地的hexo博客了，执行以下命令(在D:\hexo)，然后到浏览器输入localhost:4000看看。
```bash
hexo generate
hexo server
```
至此，本地博客已经搭建起来了，但是只是本地

## hexo部署到Github

**创建repository**
登录到[github](https://github.com/)，创建一个新的repository。比如我的Github账号是liekkas3175，那么我应该创建的repository名字应该是liekkas3175.github.io。

**部署**
编辑_config.yml(在H:\hexo下)。你在部署时，要把下面的liekkas3175都换成你的账号名。
```bash
deploy:
  type: git
  repository: https://github.com/liekkas3175/liekkas3175.github.io.git
  branch: master
```
执行下列指令即可完成部署。
```bash
hexo generate
hexo deploy
```
**注意**：有些新用户需要设置 ssh，否则上述命令会失败。[ssh](https://help.github.com/articles/generating-ssh-keys)的介绍和设置方法请看官方教程，并不复杂哟。

这样，我们的博客已经完全搭建起来了，在浏览器访问liekkas3175.github.io就能看到你的成就了！