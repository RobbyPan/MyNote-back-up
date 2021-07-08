# Node.js异步编程

## 同步API，异步API

+ 同步API：只有当前API执行完成后，才能继续执行下一个API 

```
console.log('before');
console.log('after');
```

+ 异步API：当前API的执行不会阻塞后续代码的执行

```
console.log('before');
setTimeout(
   () => { console.log('last');
}, 2000);
console.log('after');
```

### 同步API，异步API的区别（获取返回值）

同步API可以从返回值中拿到API执行的结果, 但是异步API是不可以的，异步API需要使用**回调函数**来获取

 ```
  // 同步
   function sum (n1, n2) { 
       return n1 + n2;
   } 
   const result = sum (10, 20);
  // 异步
   function getMsg () { 
       setTimeout(function () { 
           return { msg: 'Hello Node.js' }
       }, 2000);
   }
   const msg = getMsg ();
 ```

#### 回调函数

自己定义函数让别人去调用

```
 // getData函数定义
 function getData (callback) {}
  // getData函数调用
 getData (() => {});
```

#### 使用回调函数获取异步API执行结果

```
function getMsg (callback) {
    setTimeout(function () {
        callback ({ msg: 'Hello Node.js' })
    }, 2000);
}
getMsg (function (msg) { 
    console.log(msg);
});
```

### 同步API，异步API的区别（代码执行顺序）

+ 同步AP从上到下依次执行，前面代码会阻塞后面代码的执行

```
for (var i = 0; i < 100000; i++) { 
    console.log(i);
}
console.log('for循环后面的代码');
```

+ 异步API不会等待API执行完成后再向下执行代码

```
console.log('代码开始执行'); 
setTimeout(() => { console.log('2秒后执行的代码')}, 2000);
setTimeout(() => { console.log('"0秒"后执行的代码')}, 0); 
console.log('代码结束执行');
```

##### 代码执行顺序分析

```
console.log('代码开始执行');
setTimeout(() => {
    console.log('2秒后执行的代码');
}, 2000); 
setTimeout(() => {
    console.log('"0秒"后执行的代码');
}, 0);
console.log('代码结束执行');
```

![image-20210429165117626](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210429165117626.png)

### Node.js中的异步API

```
fs.readFile('./demo.txt', (err, result) => {});
```

```
 var server = http.createServer();
 server.on('request', (req, res) => {});
```

如果异步API后面代码的执行依赖当前异步API的执行结果，但实际上后续代码在执行的时候异步API还没有返回结果，这个问题要怎么解决呢？

```
fs.readFile('./demo.txt', (err, result) => {});
console.log('文件读取结果');
```

需求：依次读取A文件、B文件、C文件

回调函数嵌套回调函数=>**回调地狱**

### Promise

promise出现的目的是解决Node.js异步编程中回调地狱的问题

```
let promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        if (true) {
            resolve({name: '张三'})
        }else {
            reject('失败了') 
        } 
    }, 2000);
});
promise.then(result => console.log(result); // {name: '张三'})
       .catch(error => console.log(error); // 失败了)
```

### 异步函数

异步函数是异步编程语法的终极解决方案，它可以让我们将异步代码写成同步的形式，让代码不再有回调函数嵌套，使代码变得清晰明了。

```
const fn = async () => {};
```

```
async function fn () {}
```

#### async关键字

1. 普通函数定义前加async关键字 普通函数变成异步函数
2. 异步函数默认返回promise对象
3. 在异步函数内部使用return关键字进行结果返回 结果会被包裹的promise对象中 return关键字代替了resolve方法
4. 在异步函数内部使用throw关键字抛出程序异常
5. 调用异步函数再链式调用then方法获取异步函数执行结果

6. 调用异步函数再链式调用catch方法获取异步函数执行的错误信息

#### await关键字

1. await关键字只能出现在异步函数中
2. await promise await后面只能写promise对象 写其他类型的API是不不可以的

3. await关键字可是暂停异步函数向下执行 直到promise返回结果

### promisify改造现有异步API

```
const fs = require('fs');
//改造现有异步函数API，让其返回promise对象，从而支持异步函数语法
const promisify = require('unti').promisify;
//调用promisify方法发改造现有异步API 让其返回promise对象
const readFile = promisify(fs.readFile);

async function run(){
let r1 = await readFile('./1.txt','utf8')
let r2 = await readFile('./2.txt','utf8')
let r3 = await readFile('./3.txt','utf8')
consle.log(r1)
consle.log(r2)
consle.log(r3)
}
run();
```



