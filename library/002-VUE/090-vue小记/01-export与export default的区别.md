# export与export default的区别
1.export default 和export都可以用于导出常量，函数，文件，模块等；

2.可以在模块中通过import+(常量 | 函数 | 文件 | 模块)名的方式，将其导入，以便能够对其进行使用

3.在一个文件或者模块中，export,import可以有多个，但是export default只能有一个。

4.通过export方式导出，在导入的时候需要加{}，export default不需要在导入的时候加{}

## 首先要知道export，import ，export default是什么
ES6模块主要有两个功能：export和import
export用于对外输出本模块（一个文件可以理解为一个模块）变量的接口
import用于在一个模块中加载另一个含有export接口的模块。
也就是说使用export命令定义了模块的对外接口以后，其他JS文件就可以通过import命令加载这个模块（文件）。这几个都是ES6的语法.
