# 使用 VitePress 构建自己的学习站点

## 1.安装VitePress（前提先安装npm）

```
npm install vitepress@latest
```

### 1.1对package进行如图配置并运行项目

```markdown
{
  "name": "vitepress-project",
  "private": true,
  "type": "module",
  "scripts": {
    "dev": "vitepress dev docs",
    "build": "vitepress build docs",
    "serve": "vitepress serve docs",
    "docs:dev": "vitepress dev docs",
    "docs:build": "vitepress build docs",
    "docs:serve": "vitepress serve docs"
  },
  "devDependencies": {
    "vitepress": "1.0.0-alpha.28",
    "vue": "3.2.44"
  },
  "pnpm": {
    "peerDependencyRules": {
      "ignoreMissing": [
        "@algolia/client-search"
      ]
    }
  },
  "dependencies": {
    "vitepress-theme-demoblock": "^3.0.7"
  }
}

```

执行如下命令运行项目

```
npm run docs:dev
```

![image.png](https://s2.loli.net/2024/10/10/fA3CWLYq8vGFyzV.png)
## 2.项目结构

首页的内容就是由 docs/index.md 文档生成的，由 markdown 文档生成前端页面

```md
--- 
# https://vitepress.dev/reference/default-theme-home-page
layout: home

hero:
  name: "前端工程化学习"
  text: "Vue3 + TypeScript 学习文档"
  tagline: " 你这辈子不用对任何人证明什么，除了你自己。"
  image:
    src: /assets/image.png
    alt: 洛教
  actions:
    - theme: brand
      text: 开始学习
      link: /guide/
    - theme: alt
      text: 快速上手
      link: /faq/
      
features:
  - icon: ⚡
    title: 快速上手
    details: 学习vue3
  - icon: ❄️
    title: 逐渐熟练
    details: 学习如何搭建vue项目
  - icon: 🔥
    title: 快速扩展
    details: 了解其他框架的搭建方式
---
```

vitepress默认主题提供了一个首页布局，可以通过frontmatter指定layout：home在任何页面使用它。

hero指主页中部。

features可以在hero部分之后列出任意熟练的features

## 3.博文结构

主要是有 nav 和 sidebar 部分，在 config.ts文件设置，可以外部引入已经定义好的 nav 文件和 sidebar 文件,也有socialLinks部分定义需要跳转的账户页面。

```ts
import { defineConfig } from 'vitepress'

// https://vitepress.vuejs.org/config/app-configs 
export default defineConfig({
    title:"Vue3-Typescript 学习文档",
    description:"详细学习Vue3-Typescript 的指南",
    themeConfig:{
        nav:[
            {text:"首页",link:"/"},
            {text:"指南",link:"/guide/"},
            {text:"组件",link:"/components/"},
            {text:"API 参考",link:"/api/"},
            {text:"常见问题",link:"/faq/"}
        ],
        socialLinks:[
            {icon:"github",link:"https://github.com/vuejs/vitepress"} 
        ],
        sidebar:{
            "/guide/": [
              {
                text: "开始",
                collapsible: true,
                items: [
                  {text: "介绍",link: "/guide/"},
                  {
                    text: "安装",
                    link: "/guide/installation"
                  },
                  {
                    text: "基本概念",
                    link: "/guide/concepts"
                  }
                ],
              },
            ],
            "/components/": [
              {
                text: "常用组件",
                items: [
                  {
                    text: "介绍",
                    link: "/components/"
                  },
                  {
                    text: "按钮 Button",
                    link: "/components/button"
                  },
                  {
                    text: "表单 Form",
                    link: "/components/form"
                  },
                  {
                    text: "表格 Table",
                    link: "/components/table"
                  },
                ],
              }
            ]
        },
        footer: {
            message: "用心学习 Vue 3和 TypeScript!",
            copyright: "Copyright© 2024 mqxu"
          }
    }
})
```

侧边栏：

![image.png](https://s2.loli.net/2024/10/10/Bb9NZnKYziURkMC.png)

导航：

![image.png](https://s2.loli.net/2024/10/10/5Yf9BTihd6WXagQ.png)
注意每个页面文件夹都应有index.md文件。

## 4.上线

### 1.将其上传到github上

![image.png](https://s2.loli.net/2024/10/10/keu8QnJOVUPT43B.png)


### 2.导入到vercel进行上线

![image.png](https://s2.loli.net/2024/10/10/9p8FCOmsDG5Yfn3.png)
