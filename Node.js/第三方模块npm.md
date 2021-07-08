## 第三方模块npm

npm(node package manager):node的第三方模块管理工具

下载：npm install

卸载: npm uninstall

全局安装与本地安装

+ 命令行工具：全局安装
+ 库文件：本地安装

### nodemon

使用npm install nodemon -g全局下载

命令行工具中用nodemon替代node执行js文件

使用ctrl+c结束执行文件

### nrm

nrm(npm registry manager):npm下载地址切换工具

步骤

1.使用npm install nrm -g全局下载

2.nrm ls查询下载地址列表

3.切换npm下载地址nrm use 下载地址名称

### Gulp使用

1. 使用npm install gulp下载gulp库文件
2. 在项目根目录下建立gulpfile.js文件
3. 重构项目的文件夹结构，src目录放置源代码文件，dist目录放置构建后文件
4. 在gulpfile.js文件中编写任务
5. 在命令行工具中执行gulp任务

