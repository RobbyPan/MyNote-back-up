# CSS3盒子模型

CSS3中可以通过box-sizing来指定盒模型，有2个值：即可指定为content-box、border-box，这样我们计算盒子大小的方式就发生了改变。

可以分为两种情况：

1.box-sizing：content-box盒子大小为width+padding+border（以前默认的）

2.box-sizing：border-box盒子大小为width

如果盒子模型我们改为了box-sazing：border-box，那padding和border就不会撑大盒子了（前提padding和border不会超过了width宽度）