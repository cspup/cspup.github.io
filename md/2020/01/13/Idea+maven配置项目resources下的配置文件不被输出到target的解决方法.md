# Idea+maven配置项目resources下的配置文件不被输出到target的解决方法
用maven配置项目时，resources下的配置文件没有被输出到target文件夹下，导致配置文件不生效。

在maven的pom.xml配置文件中在resources下添加你的配置文件夹。

```xml
<resource>
   <directory>src/main/resources</directory>
</resource>
```
这个方法是比较通用的解决方法，即使有多个配置文件夹也可以添加上。

还有一种解决方法，就是可以在Intellij IDEA中设置项目的资源目录。不过使用这种方法，如果换一台电脑就要重新设置一遍，还是第一种方法比较好。