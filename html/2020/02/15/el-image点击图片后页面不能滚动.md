# el-image点击图片后页面不能滚动
原因：el-image源码有一个函数向body添加了overflow:hidden

暂时的解决方法：为body添加overflow:auto!important

element的github上发现了针对这个问题的issue，在其中一个找到了暂时的解决方案： https://github.com/ElemeFE/element/issues/18490