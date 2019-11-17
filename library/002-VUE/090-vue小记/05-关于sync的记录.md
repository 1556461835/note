### 修饰符.sync的使用方法

在父子组件传值的过程中，子组件想要修改父组件的状态时往往使用到.sync，很多时候往往不解其意，现在记录一下

1. 父组件监听子组件的时候多加了一个修饰符.sync(“:dialog-form-visible.sync="dialogFormVisible”)，子组件中`this.$emit('update:dialogFormVisible', newVal)`这里使用了vue语法糖：   
.sync 其实是一个缩写 @update:isShow=”val=>isShow=val”语法糖。
