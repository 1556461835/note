### vue 路由传参 params 与 query两种方式的区别

 router文件下index.js里面，是这么定义路由的：
 ```
    {
      path:"/detail",
      name:"detail",
      component:home
    }
 ```
![alt文本](amWiki/images/params.png "router")

 params只能用name来引入路由：
 ```
 this.$router.push({
   name:"detail",
   params:{
    name:'nameValue',
    code:10011
 }
 });
 ```
--------------------------------------------------------------
** 总结 **
1. 用法上：
刚才已经说了，query要用path来引入，params要用name来引入，
2. 接收参数都是类似的，分别是this.$route.query.name和this.$route.params.name。注意接收参数的时候，已经是$route而不是$router了哦！！
3. 展示上：
query更加类似于我们ajax中get传参，params则类似于post，说的再简单一点，前者在浏览器地址栏中显示参数，后者则不显示；
4. params、query不设置也可以传参，params不设置的时候，刷新页面或者返回参数会丢失，这一点的在上面说过了
