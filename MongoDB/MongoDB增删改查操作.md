# MongoDB增删改查操作

## 创建集合

创建集合分两步，一是对集合设定规则，二是创建结合，创建mongoose.Schema构造函数的实例即可创建集合。

```
  // 设定集合规则
 const courseSchema = new mongoose.Schema({
     name: String,
     author: String,
     isPublished: Boolean
 });
  // 创建集合并应用规则
 const Course = mongoose.model('Course', courseSchema); // courses
```

## 创建文档

创建文档实际上就是向集合中插入数据

分为两步：

+ 创建集合实例
+ 调用示例对象下的save方法将数据保存到数据库中

```
// 创建集合实例
 const course = new Course({
     name: 'Node.js course',
     author: '黑马讲师',
     tags: ['node', 'backend'],
     isPublished: true
 });
  // 将数据保存到数据库中
 course.save();
```

创建文档的另一种方法,使用回调函数

```
Course.create({name: 'JavaScript基础', author: '黑马讲师', isPublish: true}, (err, doc) => { 
     //  错误对象
    console.log(err)
     //  当前插入的文档
    console.log(doc)
});
```

create方法也返回promise对象

```
Course.create({name: 'JavaScript基础', author: '黑马讲师', isPublish: true})
      .then(doc => console.log(doc))
      .catch(err => console.log(err))
```

 ## MongoDB数据库导入文件

mongoimport -d 数据库名称 -c 集合名称 -file 要导入的数据文件

**mongoimport需要先配置环境变量**

## MongoDB查询文档

``` 
 //  根据条件查找文档（条件为空则查找所有文档）
Course.find().then(result => console.log(result))
// 返回文档集合
[{
    _id: 5c0917ed37ec9b03c07cf95f,
    name: 'node.js基础',
    author: '黑马讲师‘
},{
     _id: 5c09dea28acfb814980ff827,
     name: 'Javascript',
     author: '黑马讲师‘
}]
```

find()返回的是一个数组，数组里面才是对象，find()中可以传递参数

```
//  根据条件查找文档
Course.findOne({name: 'node.js基础'}).then(result => console.log(result))
// 返回文档
 {
    _id: 5c0917ed37ec9b03c07cf95f,
    name: 'node.js基础',
    author: '黑马讲师‘
}
```

findOne()返回的是一个对象，如果不传递参数，则默认返回集合中第一个文档

``` 
//匹配大于 小于
User.find({age:{$gt:20,$lt:50}}).then(result => console.log(result))
 //  匹配包含
 User.find({hobbies: {$in: ['敲代码']}}).then(result => console.log(result))
//  选择要查询的字段  
 User.find().select('name email -_id').then(result => console.log(result))
 //select()中参数，需要就写，不需要就—
 // 将数据按照年龄进行排序  sort默认升序，如果要降序可以在参数前加－号
 User.find().sort('age').then(result => console.log(result))
//  skip 跳过多少条数据  limit 限制查询数量  可以用来分页
 User.find().skip(2).limit(2).then(result => console.log(result))
```

## 删除文档

``` 
 // 删除单个
Course.findOneAndDelete({}).then(result => console.log(result))
```

查找一条匹配的文档并删除，返回值是删除的文档，如果匹配多个文档，默认删除一的个匹配的文档

```
// 删除多个
User.deleteMany({}).then(result => console.log(result))
```

如果传递空参数，将删除**整个集合**

## 更新文档

```
// 更新单个
User.updateOne({查询条件}, {要修改的值}).then(result => console.log(result))
```

```
// 更新多个
User.updateMany({查询条件}, {要更改的值}).then(result => console.log(result))
```

## mongoose验证

在创建集合规则时，可以设置当前字段的验证规则，验证失败则输入插入失败

* required:true 必传字段
* minlength:3 字符串最小长度
* maxlength:20 字符串最大长度
* min:2 数值最小为2
* max:100 数值最大为100

```
title: {
		type: String,
		// 必选字段
		required: [true, '请传入文章标题'],
		// 字符串的最小长度
		minlength: [2, '文章长度不能小于2'],
		// 字符串的最大长度
		maxlength: [5, '文章长度最大不能超过5'],
		// 去除字符串两边的空格
		trim: true
	},
```

* enum:['html','css','javascript','node.js']
* trim:true 去除字符串两边的空格
* validate: 自定义验证器

```
 author: {
        type: String,
        validate: {
            validator: v => {
                // 返回布尔值
                // true 验证成功
                // false 验证失败
                // v 要验证的值
                return v && v.length > 4
            },
            // 自定义错误信息
            message: '传入的值不符合验证规则'
        }
    }
```

* default: 默认值

获取错误信息：error.errors['字段名称'].message

```
Post.create({ title: 'aa', age: 60, category: 'java', author: 'bd' })
    .then(result => console.log(result))
    .catch(error => {
        // 获取错误信息对象
        const err = error.errors;
        // 循环错误信息对象
        for (var attr in err) {
            // 将错误信息打印到控制台中
            console.log(err[attr]['message']);
        }
    })
```

## 集合关联

通常不同集合的数据之间是有关系的，例如文章信息和用户信息需存储在不同的集合中，但文章是某个用户发表的，要查询文章的所有信息包括发表用户，就需要用到集合关联。

* 使用id对集合进行关联
* 使用populate方法进行关联集合查询

![image-20210527154441385](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210527154441385.png)

```
// 用户集合
const User = mongoose.model('User', new mongoose.Schema({ name: { type: String } })); 
// 文章集合
const Post = mongoose.model('Post', new mongoose.Schema({
    title: { type: String },
    // 使用ID将文章集合和作者集合进行关联
    author: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
}));
//联合查询
Post.find()
      .populate('author')
      .then((err, result) => console.log(result));
```

## 案例实现用户信息的增删改查

1. 搭建网站服务器，实现客户端与服务器端的通信
2. 连接数据库，创建用户集合，向集合中插入文档
3. 当用户访问/list时，将所有用户信息查询出来
4. 将用户信息和表格HTML进行拼接并将拼接结果响应回客户端
5. 当用户访问/add时，呈现表单页面，并实现添加用户信息功能
6. 当用户访问/modify时，呈现修改页面，并实现修改用户信息功能
7. 当用户访问/delete时，实现用户删除功能

