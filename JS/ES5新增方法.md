## ES5新增方法

### 数组

迭代（遍历）方法：forEach() 、map()、filter()、some()、every();

#### forEach()

forEach(function(value,index,array){

value=每个数组元素

index=每个数组元素的索引号

array=数组本身

})![image-20210426085602383](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210426085602383.png)

#### filter()

![image-20210426085818315](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210426085818315.png)

#### some()

![image-20210426090115063](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210426090115063.png)

#### filter()与some()比较

+ filter()也是查找满足条件的元素，返回的是一个数组，而且是把所有满足条件的元素返回回来
+ some()也是查找满足条件的元素是否存在，返回的是一个布尔值，如果查找到第一个满足条件的元素就终止循环

### trim去除字符串两端空格

str.trim()

不影响字符串本身，它返回的是一个新的字符串。

## 对象方法

#### Object.keys()

Object.keys()用于获取对象自身所有的属性

Object.keys(obj)

+ 效果类似于for...in
+ 返回一个由属性名组成的数组

#### Object.defineProperty()

Object.defineProperty()定义对象中新属性或修改原有的属性

Object.defineProperty(obj,prop,descriptor)

+ obj：必需。目标对象
+ prop：必需。需定义或修改的属性的名字
+ descriptor：必需。目标属性所拥有的特性

![image-20210426124925693](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210426124925693.png)

