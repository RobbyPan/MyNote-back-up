# node创建web服务器

```js
//用于创建网站服务器的模块
const http = require('http');
// app对象是网站服务器对象
const app = http.createServer();
// 当客户端有请求来的时候
app.on('request', (req, res) => {
    res.end('<h2>hello user</h2>')
});
// 监听3000端口
app.listen(3000);
console.log('网站服务器启动成功');
```

## http 请求报文

1.请求方式(Request Method)

+ GET 请求数据
+ POST 发送数据

2.请求地址(Request URL)

```
app.on('request',(req,res) => {
req.headers//获取请求报文
req.url//获取请求地址
req.method//获取请求方法
});
```

## 响应报文

1.HTTP状态码

+ 200 请求成功
+ 404 请求的资源没有被找到
+ 500 服务器端错误
+ 400 客户端请求有语法错误

2.内容类型

+ text/html
+ text/css
+ application/javascript
+ image/ipeg
+ application/json

通过res.writeHead()方法来指定响应状态码和内容类型

```
res.writeHead(200,{'content-type':'text/html;charset=utf8'})
```

## 请求参数

客户端向服务器端发送请求时，有时需要携带一些客户资料，客户信息需要通过请求参数的形式传递到服务器端，比如登录操作

### GET请求

+ 参数被放置再浏览器地址栏中，例如：http://localhost:3000/?name=zhangsan&age=20

### POST请求(gulp p18)

+ 参数被放置在请求体中进行传输
+ 获取post参数需要使用data事件和end事件
+ 使用querystring系统模块将参数转换成对象格式

```
//导入系统模块querystring用于将HTTP参数转换成对象格式
const qureystring = require('querystring');
app.on('request',(req,res) => {
let postData = '';
//监听参数传输事件
req.on('data',(chunk) => postData += chunk;);
//监听参数传输完毕事件
req.on('end',() => {
console.log(querystring.parse(postData));
});
});
```

## 路由

http://localhost:3000/index
http://localhost:3000/login
路由是指客户端请求地址与服务器端程序代码的对应关系。简单的说，就是请求什么响应什么。

![image-20210429100007740](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210429100007740.png)

```
// 当客户端发来请求的时候
 app.on('request', (req, res) => {
     // 获取客户端的请求路径
     let { pathname } = url.parse(req.url);
     if (pathname == '/' || pathname == '/index') {
         res.end('欢迎来到首页');
     } else if (pathname == '/list') {
         res.end('欢迎来到列表页页');
     } else {
        res.end('抱歉, 您访问的页面出游了');
     }
 });
```

## 静态资源

服务器端不需要处理，可以直接响应给客户端的资源就是静态资源，例如CSS、JavaScript、image文件。

## 动态资源

相同的请求地址不同的响应资源，这种资源就是动态资源。

http://www.itcast.cn/article?id=1
http://www.itcast.cn/article?id=2

![image-20210429102516271](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210429102516271.png)

## mime插件

mime可以通过资源类型自动识别返回资源类型