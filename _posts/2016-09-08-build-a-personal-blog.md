---
title: Build a Personal Blog
date: 2016-09-08 15:51:01
tags: hexo
toc: true
---

To build a personal blog with [Github Pages](https://pages.github.com) and [Hexo](https://hexo.io).

<!-- more -->

## Node

Download & Install [`Node.js`](https://nodejs.org/en)


## Git

- Download & Install [`Git`](https://git-scm.com/downloads/)
- Configuration

``` bash
git config --global user.name hekie
git config --global user.email 1250682474@qq.com
git config --global core.autocrlf false
```

- Generating SSH Public Key ([REF](https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key))

``` bash
ssh-keygen -t rsa -C "1250682474@qq.com"
```

- Adding SSH Key to GitHub Account ([REF](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/))  
**Path:** https://github.com/settings/ssh


## Hexo

- Install [`Hexo`](https://hexo.io/)

``` bash
# install
npm install hexo-cli -g
# initialize blog
hexo init hekie.github.io
cd hekie.github.io
npm install
hexo s
```

- Install [`hexo-deployer-git`](https://github.com/hexojs/hexo-deployer-git)

``` bash
$ npm install hexo-deployer-git --save
```

- Edit settings ([REF](https://hexo.io/docs/deployment.html#Git))

``` yaml
deploy:
  type: git
  repo: git@github.com:hekie/hekie.github.io.git
  branch: master
```
