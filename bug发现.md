----------------



1. 使用background-size:cover ，想要图片保持原大小比例的情况下尽可能大的范围内显示图片
bug: 部分图片发生旋转，验证发现是在上传图片时导致图片direction 数据丢失，以致小图显示都会旋转
2. 移动端使用position：fixed 需注意，需把fixed的元素放在最外层，否则，可能在ios下发生元素隐藏的bug
或者可以把fix的元素的parent的高度设置为屏幕的100%
3.


-------------------------------
## IOS bug ##
1. 解决IOS滑动触发Body的滑动
导致body内部滚动容器不能滚动；

参考：http://stackoverflow.com/questions/8488447/iphone-web-app-stop-body-scrolling
解决方法其实很简单，用户上拉时设置滑轮到顶部的位置人为的设置1px
滑到底部加载更多的时候也是如此，这样就能不触发body的滑动事件

2. Ios 低版本（9.1）下，checkbox 的样式在选中或取消选中后，样式不变
错误： input:checked ~ label{ ……}
正确，给label 在checked 状态后加样式class ,
原因：低版本下， ios通过input的状态改变样式的，可能不会去刷新渲染
