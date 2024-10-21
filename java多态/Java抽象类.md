# Java抽象类

抽象类和抽象方法适用于类较大，没有办法找到公共的方法的情况时使用的。

比如 如何使用一个方法来表示不同动物的行动方式？

`abstract`是`java`中抽象类和抽象方法的关键字，使用`abstract`修饰的方法被称为抽象方法，抽象方法的方法体是***空的***，使用抽象方法的类被称为抽象类，并且一定要用`abstract`来修饰

注意：抽象类是不可以被`new`关键字创建的，毕竟是***抽象***的嘛，怎么可以被实例化呢？

虽然可以有构造函数，但是不能用new创建，但是构造函数初始化的作用没有改变。

方法定义：

```java
public abstract class 类名
{	
	// 定义抽象方法
	public abstract 返回类型 方法名([参数列表]); // 没有方法体
	// 其他方法和属性

}
```

例子：

```java
public class Main {
    public static void main(String[] args) {
//        Person a = new Person()
        Person a =new Student();
        a.work();

        Person s =new Teacher();
        s.work();
    }
}

public abstract class Person {

    // 定义了一个抽象的方法
    public abstract void work();

}

public class Student extends Person {
    public void work(){
        System.out.println("学习");
    }
}

public class Teacher  extends Person{

    public void work(){
        System.out.println("教书");
    }
}
```

## 抽象类的作用

抽象类类似于一个模板，方便开发人员根据抽象类的格式来创建新类。***抽象类可以没有抽象方法，但是有抽象方法的一定是抽象类，抽象方法只能使用protocted和public修饰，因为抽象方法就是让继承的，private无法继承，final也不行，因为不能修改，同理 static也是一样***子类继承抽象类，必须实现抽象类中的所有方法

抽象类特点：

1.抽象类不能创建对象

2.抽象类可以有构造函数

3.抽象类可以没有抽象方法，但是有抽象方法的一定是抽象类

4.子类继承抽象类，必须实现抽象类中的所有方法，否则子类也必须是抽象类

5.抽象方法不能使用private，final,static修饰



