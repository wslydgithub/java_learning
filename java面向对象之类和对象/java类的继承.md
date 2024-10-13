# java类的继承

## 继承作用

避免大量重复冗余方法的定义和方法。

## 继承的关键字

`extends`

例子：

```java
public class Student extends Person
{
}
```

这就创建了一个继承了父类Person的子类Student

## 子类和父类的继承机制

注意：`java`中只有单继承，没有多继承，一个儿子只能有一个父亲，但是一个父亲可以有多个儿子，和python不一样，`python`是多继承的。

## 单继承和间接继承，以及顶级父类

`java`不支持多继承，但是支持简介继承，就比如每一个`java`类都继承了`Object`类，所以在`java`中定义的子类都是间接继承`Object`类。

### Object.equals()

`Object`类中有一个equals()方法，但是这个equals()方法比较的是地址，因为类是引用类型，所以存放的是地址，

### Object.hashCode()

这个方法是输出所创建对象的地址

## 对象向上转型

子类转换为父类，成为对象向上转化

格式： 父类名称 对象名称 = new 子类名称( )

```java
Person s2 = new Student()
```

作用：把创建的子类对象当做父类看待和处理，其实就是将子类转化为父类，转化之后就不能再使用子类的方法

## 对象向下转型

父类转化为子类

子类名称 子类 = (子类名称) 父类对象

注意：可能会出现`ClassCastException`异常,小心使用

## super关键字

###  super访问构造函数

在`java`的继承中，子类的构造函数，必须依赖父类的构造函数，super(参数)访问父类的构造函数，super调用父类的构造函数，必须位于构造函数的第一行

```java
// 父类
public class Person
{
	public Person( )
	{
	
	}
}
```

```java
// 子类
public class Student extends Person
{
    // 子类的构建函数
	public Student( )
	{
        // 调用父类的构造函数
		super();
	}
}
```

但是如果父类的构造函数时默认的构造函数，子类的构造函数可以写super(),

### super访问父类属性

访问方法 super.属性,当子类和父类的属性同名时，要使用super.属性来调用

### super访问父类方法

访问父类方法时，super.父类方法

### super和this的区别

super()访问父类的构造函数，this()访问的是子类自身的构造函数，但是都要位于第一行

## final关键字

### final修饰变量

final修饰的变量，如果是基本数据类型的变量，则其数值一旦初始化之后不可以进行更改。

final修饰的变量，如果是引用数据类型的变量，则其一旦初始化之后，不可以让其再指向另一个对象

final相当于Go中的const，修饰的都是常量

final可以修饰局部变量

### final修饰方法

final关键字修饰方法，相当于常量方法，也就是如果final修饰方法，子类不能对其重写，也不能定义和其名称，参数类型，个数，以及参数顺序都一样的方法。但是如果是private则可以，因为private方法只属于该类，与其子类无关

### final修饰类

final修饰的类不能被子类继承，final类的方法也默认为final，也就是不能被重写，final中变量的值是可以改变的