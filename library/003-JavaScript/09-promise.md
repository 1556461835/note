# 「前端进阶」完全吃透Promise，深入JavaScript异步
## promise是什么？
promise的意思是承诺，有的人翻译为许愿，但它们代表的都是未实现的东西，等待我们接下来去实现。

Promise最早出现在commnjs，随后形成了Promise/A规范。在Promise这个技术中它本身代表以目前还不能使用的对象，但可以在将来的某个时间点被调用。使用Promise我们可以用同步的方式写异步代码。其实Promise在实际的应用中往往起到代理的作用。例如，我们像我们发出请求调用服务器数据，由于网络延时原因，我们此时无法调用到数据，我们可以接着执行其它任务，等到将来某个时间节点服务器响应数据到达客户端，我们即可使用promise自带的一个回调函数来处理数据
## Promise能帮我们解决什么痛点
JavaScript实现异步执行，在Promise未出现前，我们通常是使用嵌套的回调函数来解决的。但是使用回调函数来解决异步问题，简单还好说，但是如果问题比较复杂，我们将会面临回调金字塔的问题（pyramid of Doom）。  
```
var a = function() {
    console.log('a');
};

var b = function() {
    console.log('b');
};

var c = function() {
    for(var i=0;i<100;i++){
        console.log('c')
    }
};

a(b(c())); // 100个c -> b -> a
```

我们要桉顺序的执行a，b，c三个函数，我们发现嵌套回调函数确实可以实现异步操作（在c函数中循环100次，发现确实是先输出100个c，然后在输出b，最后是a）。但是你发现没这种实现可读性极差，如果是几十上百且回调函数异常复杂，那么代码维护起来将更加麻烦。   

那么，接下来我们看一下使用promise（promise的实例可以传入两个参数表示两个状态的回调函数，第一个是resolve，必选参数；第二个是reject，可选参数）的方便之处。   
```
var promise = new Promise(function(resolve, reject){
    console.log('............');
    resolve(); // 这是promise的一个机制，只有promise实例的状态变为resolved，才会会触发then回调函数
});

promise.then(function(){
    for(var i=0;i<100;i++) {
        console.log('c')
    }
})
.then(function(){
    console.log('b')
})
.then(function(){
    console.log('a')
})
```
### promise的3种状态
上面提到了promise的 resolved 状态，那么，我们就来说一下promise的3种状态，未完成（unfulfilled）、完成（fulfilled）、失败（failed）。

在promise中我们使用resolved代表fulfilled，使用rejected表示fail
---------------------
### ES6的Promise有哪些特性
1.promise的状态只能从 未完成->完成, 未完成->失败 且状态不可逆转。   

2.promise的异步结果，只能在完成状态时才能返回，而且我们在开发中是根据结果来选择来选择状态的，然后根据状态来选择是否执行then()。   

3.实例化的Promise内部会立即执行，then方法中的异步回调函数会在脚本中所有同步任务完成时才会执行。因此，promise的异步回调结果最后输出。示例代码如下  
```
var promise = new Promise(function(resolve, reject) {
  console.log('Promise instance');
  resolve();
});

promise.then(function() {
  console.log('resolved result');
});
for(var i=0;i<100;i++) {
console.log(i);
/*
Promise instance
1
2
3
...
99
100
resolved result
*/
```
### resolve中可以接受另一个promise实例
resolve中接受另一个另一个对象的实例后，resolve本实例的返回状态将会有被传入的promise的返回状态来取代。    

reject状态替换实例，代码如下：   
```
const p1 = new Promise(function (resolve, reject) {
    cosole.log('2秒之后，调用返回p1的reject给p2');
    setTimeout(reject, 3000, new Error('fail'))
})

const p2 = new Promise(function (resolve, reject) {
    cosole.log('1秒之后，调用p1');
    setTimeout(() => resolve(p1), 1000)
})

p2
  .then(result => console.log(result))
  .catch(error => console.log(error))

// fail
```
resolve状态替换实例，代码如下：
```
const p1 = new Promise(function (resolve, reject) {
    cosole.log('2秒之后，调用返回p1的resolve给p2');
    setTimeout(resolve, 3000, 'success')
})

const p2 = new Promise(function (resolve, reject) {
    cosole.log('1秒之后，调用p1');
    setTimeout(() => resolve(p1), 1000)
})

p2
  .then(result => console.log(result))
  .catch(error => console.log(error))

// success
```
注意：promise实例内部的resolve也执行的是异步回调，所以不管resolve放的位置靠前还是靠后，都要等内部的同步函数执行完毕，才会执行resolve异步回调。  
```
new Promise((resolve, reject) => {
    console.log(1);
    resolve(2);
    console.log(3);
}).then(result => {
    console.log(result);
});
/*
1
3
2
*/
```

## 基本用法
首先看完上面的内容，我们应该了解基本的Promise使用了
### ajax XMLHttpRequest封装
```
//get 请求封装
function get(url) {
  // Return a new promise.
  return new Promise(function(resolve, reject) {
    // Do the usual XHR stuff
    var req = new XMLHttpRequest();
    req.open('GET', url);

    req.onload = function() {
      // This is called even on 404 etc
      // so check the status
      if (req.status == 200) {
        // Resolve the promise with the response text
        resolve(req.response);
      }
      else {
        // Otherwise reject with the status text
        // which will hopefully be a meaningful error
        reject(Error(req.statusText));
      }
    };

    // Handle network errors
    req.onerror = function() {
      reject(Error("Network Error"));
    };

    // Make the request
    req.send();
  });
}
```
### 2.Promse API
1.静态方法   
   2.prototype上方法   
Promise.prototype.then() 来分析
`首先来看看 `Promise.prototype.then()`返回一个`Promise`,但`Promise`内部有返回值，且 返回值，可以是个值，也可能就是一个新`Promise``
```
- *如果then中的回调函数返回一个值，那么then返回的Promise将会成为接受状态，并且将返回的值作为接受状态的回调函数的参数值。*
- *如果then中的回调函数抛出一个错误，那么then返回的Promise将会成为拒绝状态，并且将抛出的错误作为拒绝状态的回调函数的参数值。*
- *如果then中的回调函数返回一个已经是接受状态的Promise，那么then返回的Promise也会成为接受状态，并且将那个Promise的接受状态的回调函数的参数值作为该被返回的Promise的接受状态回调函数的参数值。*
- *如果then中的回调函数返回一个已经是拒绝状态的Promise，那么then返回的Promise也会成为拒绝状态，并且将那个Promise的拒绝状态的回调函数的参数值作为该被返回的Promise的拒绝状态回调函数的参数值。*
- *如果then中的回调函数返回一个未定状态（pending）的Promise，那么then返回Promise的状态也是未定的，并且它的终态与那个Promise的终态相同；同时，它变为终态时调用的回调函数参数与那个Promise变为终态时的回调函数的参数是相同的。*
--------------------------------------------------------------------------------
/*then 回调中，
	1. 返回是return function,则返回一个Promise 【参见对比3代码】
	2. 不是一个function,则 then 将创建一个没有经过回调函数处理的新 Promise 对象，这个新 Promise 只是简单地接受调用这个 then 的原 Promise 的终态作为它的终态。（MDN中解释）【参见对比1代码】
	3. 返回一个function，但没有return ，则相当于 then(null)
  */
//对比1 穿透问题  返回是'foo' 而不是 'bar'
Promise.resolve('foo')
    .then(Promise.resolve('bar'))
    .then(function(result){
    	console.log(result)
	})


//对比2  打印undefined
Promise.resolve('foo')
    .then(function(){Promise.resolve('bar')})
    .then(function(result){
        console.log(result)
    })


//对比3  返回 'bar'
Promise.resolve('foo')
    .then(function() {
        return Promise.resolve('bar')
    }).then(function(result) {
        console.log(result)
    })
```
### 3. Prmise 链式调用——重点（难点）
链式调用

  1.   核心就是 then catch 等方法返回一个Promise
  2.   链式 调用数据传递（注意）
  1. 值传递问题
  简单例子
```
     //正常状态
     const promise1 = new Promise((resolve, reject) => {
         resolve('0000')//
     })
     promise1.then(result => {
         console.log(result) //0000
     	   return '1111';//类似于 return Promise.resolve('1111'); 参数是data，promise 状态时 resolve
     }).then(data => {
         console.log(data) // 1111
     })
```     
     2. 异步操作队列
     上面至今是return 值，直接调用 下一下then就OK了。  

     但如果return Promise,则？   
```
Promise.resolve(111).then(function(d){
	console.log(d);
	return Promise.resolve(d+111);//返回promise
}).then(function(d2){
	console.log(d2);
})
// 111,222
```
1. Promise 异常处理基本套路
基本处理异常中，有两种方案then(undefined, func) 与catch()

但then(undefined, func) 与catch()不同，具体参见代码方案3
```
//方案1 使用 Promise.prototype.catch()来catch
const promise1 = new Promise((resolve, reject) => {
    reject('no')//
})
promise1.then(result => {
    console.log(result) // 永远不会执行
}).catch(error => {
    console.log(error) // no
})
```
-----------------------------------------------
```
//方案2 使用 Promise.prototype.then()中第二个参数 来处理
const promise1 = new Promise((resolve, reject) => {
    reject('no')//
})
promise1.then(result => {
    console.log(result) // 永远不会执行
}，error => {
    console.log(error) // no
})
```
---------------------
```
//方案2  （方案1  方案2 对比）
var promise2 = new Promise((resolve, reject) => {
    resolve('yes')//
})
promise2.then(result => {
    throw new Error('then');
    console.log(result)
},error => {
    console.log('1111',error) // no
}).catch(error=>{
   console.log('2222',error)// 最终 err在此处被捕获，而不是 then 中
})
```

---------------------
作者：喵容
来源：CSDN
原文：https://blog.csdn.net/qq_40128367/article/details/82992263
版权声明：本文为博主原创文章，转载请附上博文链接！
