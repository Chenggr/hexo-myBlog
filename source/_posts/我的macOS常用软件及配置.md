---
title: 我的macOS常用软件及配置
date: 2019-05-22 17:13:08
tags:
  - 配置
  - 软件下载
---

> 记录我的某些常用软件及配置，方便以后查看。

<!--more-->

# 破解软件下载地址

<a  href ="https://xclient.info/">精品 MAC 应用分享</a>
<a  href ="https://www.macbl.com/">马可菠萝</a>

# 软件

- chrome & chrome 插件
  划词翻译
  web 前端助手（FeHelper）

- 可能需要用到的
  MacBooster 7（清理垃圾、内存）
  Dr. Unarchiver（解压）
  iStatistica（查看内存、网络、网速、等等）

---

- Sourcetree（git）
- SmartSVN（svn）
- 微信开发者工具
- Navicat Premium（数据库）
- Sublime Text3（编辑器）
- MAMP PRO（服务器）
- Postman（接口）
- Charles（抓包）
- Vscode（编译器）

---

# 配置

## vscode

```javascript
{
"editor.detectIndentation": false,
// 重新设定 tabsize
"editor.tabSize": 2,
// #每次保存的时候自动格式化
"editor.formatOnSave": true,
// #每次保存的时候将代码按 eslint 格式进行修复
"eslint.autoFixOnSave": true,
// 添加 vue 支持
"eslint.validate": [
"javascript",
"javascriptreact",
{
"language": "vue",
"autoFix": true
}
],
// #让 prettier 使用 eslint 的代码格式进行校验
"prettier.eslintIntegration": true,
// #去掉代码结尾的分号
"prettier.semi": false,
// #使用带引号替代双引号
"prettier.singleQuote": true,
// #让函数(名)和后面的括号之间加个空格
"javascript.format.insertSpaceBeforeFunctionParenthesis": true,
// #这个按用户自身习惯选择
"vetur.format.defaultFormatter.html": "js-beautify-html",
// #让 vue 中的 js 按编辑器自带的 ts 格式进行格式化
"vetur.format.defaultFormatter.js": "vscode-typescript",
"vetur.format.defaultFormatterOptions": {
"js-beautify-html": {
"wrap_attributes": "force-aligned"
// #vue 组件中 html 代码格式化样式
}
},
// 格式化 stylus, 需安装 Manta's Stylus Supremacy 插件
"stylusSupremacy.insertColons": false, // 是否插入冒号
"stylusSupremacy.insertSemicolons": false, // 是否插入分好
"stylusSupremacy.insertBraces": false, // 是否插入大括号
"stylusSupremacy.insertNewLineAroundImports": false, // import 之后是否换行
"stylusSupremacy.insertNewLineAroundBlocks": false, // 两个选择器中是否换行
"eslint.options": {
"plugins": ["html"]
},
"editor.fontSize": 13
}
```
