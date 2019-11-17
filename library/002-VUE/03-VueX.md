## VueX的使用



#### Vue / Viex

Vuex是一个状态管理库(全局数据仓库)，为应用中的所有组件提供集中式的状态存储与操作，保证了所有状态以可预测的方式进行修改。

{  
  data:{}  //当前组件数据  
}  

#### Vuex的使用
```
import Vue from "vue";
import Vuex from "vuex";  
Vue.use(Vuex)  
export default new Vuex.Store({
    //应用状态的数据结构
    state: {
    },
    //
    actions: {
    },
    mutations: {
    },
    getters: {
    },  
    modules: {

    }
})
```  

#### getters的理解
在介绍state中我们了解到，在Store仓库里，state就是用来存放数据，若是对数据进行处理输出，比如数据要过滤，一般我们可以写到computed中。但是如果很多组件都使用这个过滤后的数据，比如饼状图组件和曲线图组件，我们是否可以把这个数据抽提出来共享？这就是getters存在的意义。我们可以认为，【getters】是store的计算属性。


#### 辅助函数的使用
1. mapaction  
在组件中使用 this.$store.dispatch('xxx') 分发 action，或者使用 mapActions 辅助函数将组件的 methods 映射为 store.dispatch 调用（需要先在根节点注入 store）：
```
import { mapActions } from 'vuex'

export default {
  // ...
  methods: {
    ...mapActions([
      'increment', // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`
      // `mapActions` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
    ]),
    ...mapActions({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
    })
  }
}
```

#### mutations与actions的区别
1、流程顺序
“相应视图—>修改State”拆分成两部分，视图触发Action，Action再触发Mutation。

2、角色定位
基于流程顺序，二者扮演不同的角色。
Mutation：专注于修改State，理论上是修改State的唯一途径。
Action：业务代码、异步请求。

3、限制
角色不同，二者有不同的限制。
Mutation：必须同步执行。
Action：可以异步，但不能直接操作State。
