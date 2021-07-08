# Express框架

Express是一个基于Node平台的web应用开发框架，它提供了一些列强大特性，帮你创建各种web应用。 使用npm install express命令下载。

## Express框架特性

* 提供了方便简洁的路由定义方式
* 对获取HTTP请求参数进行了简化处理
* 对模板引擎支持程度高，方便渲染动态HTML页面
* 提供了中间件机制有效控制HTTP请求
* 拥有大量第三方中间件对功能进行拓展

## 原生Node.js与Express框架对比

#### 路由

![image-20210605135039013](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210605135039013.png)

#### 获取请求参数

![image-20210605135111489](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210605135111489.png)

 ## 中间件

### 什么是中间件

中间件就是一堆方法，可以接受客户端发来的请求、可以对请求做出响应，也可以将请求继续交给下一个中间件继续处理。

![image-20210605144514753](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210605144514753.png)

中间件主要由两部分组成，中间件方法以及请求处理函数

中间件方法由Express提供，负责拦截请求，请求处理函数由开发人员提供，负责处理请求。

```\
app.get('请求路径','处理函数') //接收并处理get请求
app.post('请求路径','处理函数') //接收并处理post请求
```

可以针对同一个请求设置多个中间件，对同一个请求进行多次处理。

默认情况下，请求从上到下依次匹配中间件，一旦匹配成功则终止匹配。

可以调用next方法将请求的控制权交给下一个中间件，直到遇到结束请求的中间件。

```
app.get('/request',(req,res,next) => {
req.name = '张三';
next();
});
app.get('/request',(req,res) => {
res.send(req.name);
});
```

### app.use中间件用法

app.use匹配所有请求方式，可以直接传入请求处理函数，代表接收所有的请求。

```
app.use((req,res,next) => {
console.log(req.url);
next();
});
```

app.use第一个参数也可以传入请求地址，代表不论什么请求方式，只要是这个请求地址就接收这个请求。

```
app.use('/admin',(req,res,next) => {
conlose.log(req.url);
next();
});
```

### 中间件应用

1. 路由保护，客户端在访问需要登陆的页面时，可以先使用中间件判断用户登陆状态，用户如果未登录，则拦截请求，直接响应，禁止用户进入需要登录的页面。
2. 网站维护公告，在所有路由的最上面定义接收所有请求的中间件，直接为客户端做出响应，网站正在维护中。
3. 自定义404页面`res.status(404).sen('当前访问页面不存在')`

### 错误处理中间件

在程序执行过程中，不可避免的会主线一些无法预料的错误，比如文件读取失败，数据库连接失败。错误处理中间件是一个集中处理错误的地方。

```
app.use((err,req,res,next) => {
res.status(500).send('服务器发生未知错误');
})
```

*错误处理中间件只能处理同步代码*

当程序出现错误时，调用next()方法，并且将错误信息通过参数的形式传递给next()方法，即可触发错误处理中间件。

```
app.get("/",(req,res,next) => {
fs.readFile("/....",(err,data) => {
if(err){
next(err);
      }
   });
});
```

### 捕获错误

在node.js中，异步API的错误信息都是通过回调函数获取的，支持Promise对象的异步API发生错误可以通过catch方法捕获。

try catch可以捕获异步函数以及其他同步代码在执行过程中发生的错误，但是不能捕获其他API发生的错误。

```
app.get("/",async(req.res.next) => {
try{
await User.find({name:'张三'})
}catch(ex){
next(ex);
}
});
```

