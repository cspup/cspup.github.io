# 使用z-index实现侧栏收缩
遇到一个十分神奇的bug：vue项目在本地开发环境下侧栏能够正常收缩，但是在部署到服务器时收缩功能不好用了,在改bug时意外发现了一种简单粗暴的实现侧栏收缩的方法。

使用css的堆叠属性z-index来实现侧栏收缩。

首先需要给侧栏设置一个较小的z-index值，然后给主体部分设置一个比它大的z-index值，这样当主体部分向侧栏移动时就会覆盖掉侧栏部分。这个方法还需要让主体部分预先留出好侧栏收缩前收缩后的宽度。

css代码如下：
```CSS
<style>
.sidebar{
  z-index: 1;
  width: 200px;
  height: 100%;
  font-size: 0;
  top: 0;
  bottom: 0;
  left: 0;
  overflow: hidden;
}
.main{
  z-index: 1001;
  margin-left: 200px;
}
.main.isCollapse{
  margin-left: 50px;
}
</style>
```