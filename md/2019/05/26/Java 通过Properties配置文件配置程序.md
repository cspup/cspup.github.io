# Java 通过Properties配置文件配置程序
我们有时会希望让配置灵活变动，最好不通过修改代码中的变量实现，这时配置文件就起到了作用。

Java给我们提供了一个类：java.util.Properties;这样在java中使用Properties配置文件就变得简单多了。

Properties类继承自Hashtable类并实现了Map接口，使用键值对的形式来保存属性，是它的键和值都是字符串类型。 

1. load()方法 从文件输入流中加载属性列表  
```Java 
Properties properties=new Properties(); 
InputStream in = getClass().getClassLoader().getResource("config.properties").openStream();//打开配置文件
properties.load(in);
path = (String) properties.get("path");//从配置文件中获取path属性
```
2. store() 方法，配置属性写到文件中
```Java
  FileOutputStream out = new FileOutputStream(file, "config.properties");
pro.store(out, "Comment");
```
3. getProperty ( String key)  
通过参数 key ，得到 key 所对应的 属性。
4. setProperty ( String key, String value)  
设置key对应的属性
5. clear()  
清除装载的属性。