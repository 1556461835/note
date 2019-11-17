# 自定义axios

一般有自定义请求url,是否跨域，请求头，拦截请求和响应等方法一般有自定义请求url,是否跨域，请求头，拦截请求和响应等方法。

## axios封装
在vue项目中，和后台交互获取数据这块，我们通常使用的是axios库，它是基于promise的http库，可运行在浏览器端和node.js中。他有很多优秀的特性，例如拦截请求和响应、取消请求、转换json、客户端防御XSRF等。所以我们的尤大大也是果断放弃了对其官方库vue-resource的维护，直接推荐我们使用axios库。如果还对axios不了解的，可以移步axios文档。  

### 安装
`npm install axios`

### 引入
一般我会在项目的src目录中，新建一个request文件夹，然后在里面新建一个http.js和一个api.js文件。http.js文件用来封装我们的axios，api.js用来统一管理我们的接口。   

### 环境的切换
我们的项目环境可能有开发环境、测试环境和生产环境。我们通过node的环境变量来匹配我们的默认的接口url前缀。axios.defaults.baseURL可以设置axios的默认请求地址就不多说了。  
```
// 环境的切换
if (process.env.NODE_ENV == 'development') {    
    axios.defaults.baseURL = 'https://www.baidu.com';}
else if (process.env.NODE_ENV == 'debug') {    
    axios.defaults.baseURL = 'https://www.ceshi.com';
}
else if (process.env.NODE_ENV == 'production') {    
    axios.defaults.baseURL = 'https://www.production.com';
}
```

### 设置请求超时
通过axios.defaults.timeout设置默认的请求超时时间。例如超过了10s，就会告知用户当前请求超时，请刷新等。   
`axios.defaults.timeout = 10000  设置超时时间为10秒`

### 
