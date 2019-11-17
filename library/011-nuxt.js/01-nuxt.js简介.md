# 关于Nuxt.js
2016 年 10 月 25 日，zeit.co 背后的团队对外发布了 Next.js，一个 React 的服务端渲染应用框架。几小时后，与 Next.js 异曲同工，一个基于 Vue.js 的服务端渲染应用框架应运而生，我们称之为：Nuxt.js。
## Nuxt.js 是什么？
Nuxt.js 是一个基于 Vue.js 的通用应用框架  
通过对客户端/服务端基础架构的抽象组织，Nuxt.js 主要关注的是应用的 UI渲染。   
我们的目标是创建一个灵活的应用框架，你可以基于它初始化新项目的基础结构代码，或者在已有 Node.js 项目中使用 Nuxt.js。   
Nuxt.js 预设了利用 Vue.js 开发服务端渲染的应用所需要的各种配置。  
## Nuxt.js 框架是如何运作的？
基于 Vue、Webpack 和 Babel   

Nuxt.js 集成了以下组件/框架，用于开发完整而强大的 Web 应用：  

* [Vue 2](https://github.com/vuejs/vue)
* Vue-Router
* Vuex (当配置了 Vuex 状态树配置项 时才会引入)
* Vue 服务器端渲染 (排除使用 mode: 'spa')
* Vue-Meta  
压缩并 gzip 后，总代码大小为：57kb （如果使用了 Vuex 特性的话为 60kb）。   
另外，Nuxt.js 使用 Webpack 和 vue-loader 、 babel-loader 来处理代码的自动化构建工作（如打包、代码分层、压缩等等）。   

## 特性
* 基于 Vue.js
* 自动代码分层
* 服务端渲染
* 强大的路由功能，支持异步数据
* 静态文件服务
* ES2015+ 语法支持
* 打包和压缩 JS 和 CSS
* HTML 头部标签管理
* 本地开发支持热加载
* 集成 ESLint
* 支持各种样式预处理器： SASS、LESS、 Stylus 等等
* 支持 HTTP/2 推送

## 流程图
下图阐述了 Nuxt.js 应用一个完整的服务器请求到渲染（或用户通过 <nuxt-link> 切换路由渲染页面）的流程：  
![流程图](https://zh.nuxtjs.org/nuxt-schema.svg)

|流程步骤|翻译|
|:---:|:---:|
|incoming request|传入请求|
|nuxtserverlnit store action|nuxtserverlnit存储操作|
|middleware|中间件|
|validate|验证|
|asyncdata|异步数据|
|render|提供|
|navigate|导航|
## 服务端渲染
您可以使用Nuxt.js作为框架来处理项目的所有UI呈现。     

启动时nuxt，它将启动具有热更新加载的开发服务器，并且Vue 服务器端渲染配置为自动为服务器呈现应用程序。    
