## gulp default报错

在gulp构建任务中，想要一次执行多个task任务

```js
gulp.task('default', ['htmlmin', 'cssmin', 'jsmin', 'copy']);
```

发现报错：

Task function must be specified

![image-20210428110106066](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210428110106066.png)

查看官方文档https://www.gulpjs.com.cn/docs/getting-started/async-completion/

> 当使用 `series()` 组合多个任务（task）时，任何一个任务（task）的错误将导致整个任务组合结束，并且不会进一步执行其他任务。当使用 `parallel()` 组合多个任务（task）时，一个任务的错误将结束整个任务组合的结束，但是其他并行的任务（task）可能会执行完，也可能没有执行完。

gulp4.0不再支持用数组来组合多个task，需要使用series()或paralles()，故修改代码如下；

```js
gulp.task('default', gulp.series('htmlmin', 'cssmin', 'jsmin', 'copy'));
```

执行成功

![image-20210428110732760](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210428110732760.png)

