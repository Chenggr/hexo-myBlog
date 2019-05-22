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

### 创建本地博文服务

```javascript
// 启动博文站点
hexo server
```

访问 http://localhost:4000 就能打开博文了
Ctrl+C 关闭服务器

### 使用 Hexo 创建和发布文章

```javascript
// 进入 hexo-blog 根目录
// 创建文章命令：
hexo new "文章标题"
```

### 发布上传

```javascript
hexo clean
hexo generate
hexo deploy
```

### 完成后部署

您可执行下列的其中一个命令，让 Hexo 在生成完毕后自动部署网站，两个命令的作用是相同的。

```javascript
hexo generate --deploy
hexo deploy --generate
```

#### 简写

上面两个命令可以简写为:

```javascript
hexo g -d
hexo d -g
```
