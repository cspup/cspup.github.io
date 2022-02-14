# spring+mybatis 事务错误不回滚
今天在写一个涉及到两个表的删除操作时发现，删除一个表失败另一个成功，失败后数据不回滚，也就是说有一个表删除了，但是另一个表没有被删除，这就造成了数据的不匹配。经过查找发现还是配置的问题  
原来的appliactionContext.xml配置：
```xml
<context:component-scan base-package="yemu.controller">
 <context:component-scan base-package="yemu.service"></context:component-scan></context:component-scan>
```
spring-mvc配置：  
```xml
<context:component-scan base-package="yemu.controller" />
```
服务器启动时，有一个扫描文件的先后顺序，扫描顺序web.xml->spring配置文件->spring MVC配置文件。当扫描装配到Controller时，sevice还没有进行事务增强处理所以没有事务处理能力。所以一定要先扫描service再扫描Controller，扫描Controller应该放到SpringMVC配置文件中。  
修改后applicationContext.xml:  
```xml
<context:component-scan base-package="yemu.service" />
```
sping-mvc.xml:  
```xml
<context:component-scan base-package="yemu.controller"/>
```