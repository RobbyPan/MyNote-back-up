# 系统模块FS 

## 文件操作

const fs = require('fs');

### 读取文件内容

fs.readFile('文件路径/文件名称',['文件编码'],callback);

例:

fs.readFile('../css/base.css','utf-8'(err,doc)=>{

if(err == null){

console.log(doc);

 }

});

### 写入文件内容

fs.writeFile('文件路径/文件名称','数据'，callback);

例:

const content = '<h3>正在使用fs.writeFile写入文件内容</h3>';

fs.writeFile('../index.html',content,err => {

if(err != null){

console.log(err);

return;

}

console.log('文件写入成功');

})

### 路径拼接

path.join('路径','路径',...)

### 相对路径or绝对路径

一般情况下都是用绝对路径，因为相对路径一般是相对命令行工具的当前工作目录

使用路径模块中的__dirname获取绝对路径，再使用pathjoin来拼接。