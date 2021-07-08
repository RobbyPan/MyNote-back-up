## Express请求处理

### 构建模块化路由

```
const express = require('express')
//创建路由对象
const home = express.Router();
//将路由和请求路径进行匹配
app.use('/home',home);
//在home路由下继续创建路由
home.get('/index',() => {
//   /home/index
res.send('欢迎来到博客页面')
});
```

  

```
// home.js
const home = express.Router();
home.get('/index',() => {
res.send('欢迎来到博客展示页面');
});
module.exports = home;
```

```
// admin.js
const home = express.Router();
home.get('/index',() => {
res.send('欢迎来到博客管理页面');
});
module.exports = admin;
```

```
// app.js
const home = require('./route/home.js');
const admin = require('./route/admin.js');
app.use('/home',home);
app.use('/admin',admin);
```

### Get参数的获取

Express框架中使用req.query即可获取GET参数，框架内部会将GET参数转换为对象并返回

```
//接收地址栏中问好后面的参数
//例如:http://localhost:3000/?name=zhangsan&age=30
app.get('/',(req,res) => {
console.log(req.query); //{"name":"zhangsan","age":"30"}
});
```

### Post参数的获取

Express中接受post请求参数需要第三方包body-parser

```
//引入body-parser模块
const bodyParser = require('body-parser');
//配置body-parser模块
//extended:false 方法内部使用querystring模块处理请求参数的格式
//extended:true 方法内部使用第三方模块qs处理请求参数的格式
app.use(bodyParser.urlencoded({extended:false}));
//接受请求
app.post('/add',(req,res) => {
//接收亲求参数
console.log(req.body);
})
```

*express P10*

