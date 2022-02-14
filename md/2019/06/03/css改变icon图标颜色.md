# css改变icon图标颜色
icon是一种图标文字，是设计师们使用“专用字符编辑程序”而创建的图标字体。

通过css改变icon投影的颜色就可以实现图标颜色的改变。实际的icon图片实际上在iconwrap外面，设置了一个overflow：hidden隐藏掉了，显示的只是图标的投影。通过改变fliter:drop-shadow()就可以实现改变图标颜色的功能。

```CSS
.iconwrap{
            display:block;
            float: right;
            height: 50px;
            width: 100px;
            overflow: hidden;
        }
        .icon {
            display:block;  
            width: 20px;
            height: 20px;
            float: left;
            margin-top: 15px;
            position: relative;
            left: -30px;
            filter: drop-shadow(#000000 30px 0);
        }
        .iconwrap:hover .icon{
            filter: drop-shadow(rgb(220,40,40) 30px 0);   
        }
```
<div align=center>
<img src="./深度截图_选择区域_20190603200314.png">
<center>鼠标不在时</center>
</div>
<br>
<div align=center>
<img src="./深度截图_选择区域_20190603200445.png">
<center>鼠标触发事件时</center>
</div>

