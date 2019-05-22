---
title: Hexo常用命令
date: 2019-05-22 14:46:14
tags:
  - hexo
  - 技术
categories: hexo
type: 'categories'
---

> 我的 Hexo 常用命令

<!--more-->

### 安装 Hexo

```javascript
// 安装命令
npm install -g hexo-cli
```

### Hexo 关联 github

```javascript
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: https://github.com/username/username.github.io
  branch: master
```

### 发布上传

```javascript
hexo clean
hexo generate
hexo deploy
```

### 创建本地博文服务

```javascript
// 启动博文站点
hexo server
```

访问 http://localhost:4000 就能打开博文了
Ctrl+C 关闭服务器
