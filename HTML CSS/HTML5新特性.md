# HTML5新特性

### HTML5新增的语义化标签

+ <xmp><header>:头部标签
+ <xmp><nav>:导航标签
+ <xmp><article>:内容标签
+ <xmp><section>:定义文档某个区域
+ <xmp><aside>:侧边栏标签
+ <xmp><footer>:尾部标签（脚标）

注意：

+ 这种语义化标准主要是针对搜索引擎的
+ 这些新标签页面中可以使用多次
+ 在IE9中，需要把这些元素转换为块级元素
+ 其实，我们移动端更喜欢使用这些标签



### HTML5多媒体标签

<xmp>视频：<video >

<xmp>音频：<audio>

常见属性

| 属性     | 值                                         | 描述                                                         |
| -------- | ------------------------------------------ | ------------------------------------------------------------ |
| autoplay | autoplay                                   | 视频就绪自动播放（谷歌浏览器需要添加muted来解决自动播放问题） |
| controls | controls                                   | 向用户显示播放控件                                           |
| width    | pixels                                     | 宽度                                                         |
| height   | pixels                                     | 高度                                                         |
| loop     | loop                                       | 循环播放                                                     |
| preload  | auto（预先加载视频）none（不预先加载视频） | 规定是否预加载视频（如果有了autoplay，就忽略该属性）         |
| src      | url                                        | 地址                                                         |
| poster   | imgurl                                     | 加载等待的画面图片                                           |
| muted    | muted                                      | 静音播放                                                     |

### HTML5新增的表单属性

| 属性         | 值        | 说明                                                         |
| ------------ | --------- | ------------------------------------------------------------ |
| required     | required  | 表单拥有该属性表示其内容不能为空，必填                       |
| placeholder  | 提示文本  | 表单的提示信息，存在默认值将不显示                           |
| autofocus    | autofocus | 自动聚焦属性，页面加载完成自动聚焦到指定表单                 |
| autocomplete | off/on    | 当用户在字段开始键入时，浏览器基于之前键入过的值，因该显示出在字段中填写的选项。默认已经打开，如autocomplete="on",关闭autocomplete="off"需要放在表单内，同时加上name属性，同时成功提交 |
| multiple     | multiple  | 可以多选文件提交                                             |







