---
title: hexo-notes
description: Hexo部署及环境配置备忘
mathjax: true
date: 2023-06-22 19:35:23
updated: 2023-06-22 19:35:23
tags:
- 备忘
---

## 安装环境

安装 Git & Node.js

安装Hexo

`npm install -g hexo`

验证Hexo已安装

`hexo v` 

安装pandoc

## 配置Git

`git config --global {邮件地址}`

`ssh-keygen -t rsa -b 4096 -C {邮件地址}` ，设置密码

`eval "$(ssh-agent -s)"`

`ssh-add ~/.ssh/id_rsa`

在 github 里添加 key，其中 `cat ~/.ssh/id_rsa.pub` 查看公钥

`ssh -T git@github.com` 验证是否连接成功

`Hi {用户名}! You've successfully authenticated, but GitHub does not provide shell access.` 是正常提示

## 配置Hexo

如果 `hexo -g` `pandoc exited with code null`

```
npm un hexo-renderer-marked
npm i hexo-renderer-pandoc
```

进入 `_config.yml` ，将mathjax的false改为true

Hexo安装目录： `/node_modules/.bin`

`deploy.sh` 内容

```
hexo clean
hexo g
git add .
git commit -m "update"
git push
hexo deploy
```


