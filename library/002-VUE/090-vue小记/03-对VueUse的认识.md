# 关于Vue.use()详解

#### 问题
```
相信很多人在用Vue使用别人的组件时，会用到 Vue.use() 。例如：Vue.use(VueRouter)、Vue.use(MintUI)。但是用 axios时，就不需要用 Vue.use(axios)，就能直接使用。那这是为什么呐？
```

#### 答案
因为axios没有install
大家应该就明白了吧，用 axios时，之所以不需要用 Vue.use(axios)，就能直接使用，
是因为开发者在封装 axios 时，没有写 install 这一步。至于为啥没写，那就不得而知了。
