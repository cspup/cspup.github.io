# Java类的初始化顺序
笔试经常遇到的题，总是做错，总结一下吧。  

初始化顺序：1.父类的静态代码（方法/变量）=》2.子类的静态代码（方法/变量）=》3.父类的初始化代码块=》4.父类的构造器=》5.子类的初始化代码块=》6.子类的构造器

示例代码：
```Java
class A{
    public A() {
        System.out.println("4：A的构造方法");
    }
    { System.out.println("3：A的初始化代码，创建类的时候就执行"); }
    static { System.out.println("1：A的静态代码块，加载类的时候就执行"); }
}

public class B extends A {
    public B(){
        System.out.println("6：B的构造方法");
    }
    {System.out.println("5：B的初始化代码");}
    static {System.out.println("2：B的静态代码块");}
    public static void main(String[] args) {
        new B();
    }
}
```
运行结果：  
1：A的静态代码块，加载类的时候就执行  
2：B的静态代码块  
3：A的初始化代码，创建类的时候就执行  
4：A的构造方法  
5：B的初始化代码  
6：B的构造方法  