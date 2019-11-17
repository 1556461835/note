1. 项目目录
```
├── assets                         // 资源文件。用于组织未编译的静态资源入LESS、SASS 或 JavaScript
│   └── logo.jpg                   // 默认logo图片
├── components                     // 组件。用于自己编写的Vue组件，比如滚动组件，日历组件，分页组件
│   └── AppLogo.vue                // 默认logo组件
├── layouts                        // 布局。页面都需要有一个布局，默认为 default。它规定了一个页面如何布局页面。所有页面都会加载在布局页面中的 <nuxt /> 标签中。
│   └── default.vue                // 默认模板页面，类似mvc中的layout
├── lib
│   └── Util.js                    // 对登录，退出，post请求，get请求的封装
│   └── ApiURL.js                  // 所有对外接口，统一接口输出文件
│   └── Keys.js                    // 加密的key
│   └── tools.js                   // 封装的方法 1.两个数组的交集；2.两个数组的并集；3.判断要查询的数组是否至少有一个元素包含在目标数组中
                                   // 4.用来验证的列表；5.当前浏览器名称；6.则判断obj对象是否有键值对；7.这两个对象的值只能是数字或字符串
├── middleware                     // 中间件。存放中间件。可以在页面中调用： middleware: 'middlewareName' 。
├── pages                       　 // 页面。一个 vue 文件即为一个页面。
│   └── index.vue                  // 默认首页面
├── plugins                        // 用于存放JavaScript插件的地方
│   └── element-ui.js              // 上边我们安装的UI框架
│   └── api.js                     //  
├── static                         // 用于存放静态资源文件，比如图片，此类文件不会被 Nuxt.js 调用 Webpack 进行构建编译处理。 服务器启动的时候，该目录下的文件会映射至应用的根路径 / 下。
├── store                       　 // 用于组织应用的Vuex 状态管理。
├── .editorconfig                  // 开发工具格式配置
├── .eslintrc.js                   // ESLint的配置文件，用于检查代码格式
├── .gitignore                     // 配置git不上传的文件
├── nuxt.config.js                 // 用于组织Nuxt.js应用的个性化配置，比如网站title，已便覆盖默认配置
├── package.json                   // npm包管理配置文件
└── README.md                      // 说明文档
```
