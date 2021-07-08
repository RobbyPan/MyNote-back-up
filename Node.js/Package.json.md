# Package.json

## package.json文件的作用

项目描述文件，记录了当前项目信息，例如项目名称、版本等。

使用npm init -y生成默认文件

```js
  "name": "gulp_demo",//项目名称
  "version": "1.0.0",//项目版本
  "description": "",//项目描述
  "main": "index.js",//主模块
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },//命令的别名 使用npm run 'test'来代替一大段命令
  "author": "Robby",//作者
  "license": "ISC",//项目遵循的协议 默认ISC 即开放源代码协议
  "devDependencies": {
    "gulp": "^4.0.2",
    "gulp-file-include": "^2.3.0"
  },//开发依赖
  "dependencies": {
  }//项目依赖
```

## 依赖

### 项目依赖

+ 在项目开发阶段和线上运行阶段，都需要依赖的第三方包，称为项目依赖
+ 使用npm install包命令下载的文件会默认被添加到package.json文件中的dependencies字段中
+ 使用npm install --production下载项目依赖

```js
"dependencies": { }//项目依赖
```

### 开发依赖

+ 在项目的开发阶段需要依赖，线上运营阶段不需要依赖的第三方包，称为开发依赖
+ 使用npm install包名--save-dev命令将包添加到package.json文件中的devDependencies字段中
+ 使用npm install下载所有的依赖

```js
"devDependencies": {
    "gulp": "^4.0.2",
    "gulp-file-include": "^2.3.0"
  },//开发依赖
```

## package-lock.json文件

+ 记录各个模块间的依赖关系，包括版本、下载地址等
+ 锁定包的版本，确保再次下载时不会因为包版本不同而产生问题
+ 加快下载速度，因为该文件中已经记录了项目所依赖第三方的树状结构和包的下载地址，重新安装只需下载即可，不需要额外工作

