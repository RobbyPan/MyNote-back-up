# gulpcopy 出现错误

使用gulp copy复制文件夹时

```js
//copy任务 复制文件夹
gulp.task('copy', () => {
    gulp.src('src/images/*')
        .pipe(gulp.dest('dist/images'))
    gulp.src('src/lib/*')
        .pipe(gulp.dest('dist/lib'))
});
```

运行gulp copy出现以下报错

![image-20210428100712936](C:\Users\13272\AppData\Roaming\Typora\typora-user-images\image-20210428100712936.png)

原因：

这是gulp4.0版本使用task时，回调函数使用匿名函数带来的问题，gulpgulp不再支持同步任务

解决方案有很多具体参考 https://www.gulpjs.com.cn/docs/getting-started/async-completion/

比较简单的方法就是 添加callback，来指示函数完成

```js
gulp.task('copy', (cb) => {
    gulp.src('./src/images/*')
        .pipe(gulp.dest('dist/images'))
    cb();
});
```

