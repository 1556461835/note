# JS 中的require 和 import 区别
在研究react和webpack的时候，经常看到在js文件中出现require，还有import，这两个都是为了JS模块化编程使用。CSS的是@import   

1. ES6 模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。   
2. ES6模块不是对象，而是通过export命令显示指定输出代码，再通过import输入。  
3. ES6模块默认使用严格模式，无论是否声明“use strict”   
4. Module 主要由两个命令组成，import和export，export用于规定模块的对外接口，import命令用于输入其他模块提供的功能
5. And：export语句输出的接口，都是和其对应的值是动态绑定的关系，即通过该接口取到的都是模块内部实时的值。

6. 位置：export模块可以位于模块中的任何位置，但是必须是在模块顶层，如果在其他作用域内，会报错。
7. export default

之前的例子中，使用import导入时，都需要知道模块中所要加载的变量名或函数名，用户可能不想阅读源码，只想直接使用接口，就可以用export default命令，为模块指定输出
```
// export-default.js
export default function () {
  console.log('foo');
}
其他模块加载该模块时，import命令可以为该匿名函数指定任意名字。

// import-default.js
import customName from './export-default';
customName(); // 'foo'
```
