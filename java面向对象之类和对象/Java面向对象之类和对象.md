# Java面向对象之类和对象

## 面向过程和面向对象

面向过程：主要就是针对每一个步骤是否完成

面向对象：我的理解就是其将过程进行了一次包装，将其分配给一个对象单独完成，从而将重心从过程转到对象，更符合现实生活（比如企业中的职位）

面向过程是自己去办事，面向对象就是托人去办事。

***注意：***这个**对象**可以是任何事物，可以是猪狗等具体的事物，也可以是存取等动作或函数，当然后者一般以方法的形式出现。

## Java中类和对象之间的关系

**类**：class 可以看作是一个模板，是一个抽象的事物。

**对象**：由类产生的具体的事物，对象具有唯一性。

java中创建对象的语句：

***注意：java中一定是先有类，再有对象***

类名 对象名 = new 类名（）

例子：

```java
Person man = new Person();
```

### new关键字

1. 表示创建一个对象
2. 表示实例化一个对象
3. 变式申请堆内存的空间

![](C:\Users\L1523\Desktop\大学任务\java\java面向对象之类和对象\屏幕截图 2024-10-06 103745.png)

### 类和对象之间的关系

类的作用是生产出具体的对象

## 类和对象的组成

### 实例变量和静态变量

***实例变量：***

声明在类中，但是在方法和语句块之外

没有static修饰

默认值，数值为0，boolean为false，引用为null

实例变量是属于该类的对象，必须产生该类对象，才能调用实例变量。（调用的时候就是这样`实例名.实例变量`，没有实例名，你调用什么？）

***静态变量：***

独立于方法之外的变量，static修饰，也叫做类变量，static是不能修饰局部变量。

### 实例变量和静态变量之间的区别

简而言之，在真正编程的过程中，随对象改变的叫实例变量，不随对象改变的叫静态变量，举个例子，CCNU的学生，姓名，学号这些是实例变量，因为随着学生对象的变化而变化，但是所属学校名是静态变量，因为不管是哪一个学生对象都是CCNU的学生。

## 匿名构造块和构造函数

java的构造函数是一种特殊的方法，没有返回类型，函数名和类名保持一致。一般使用的new的时候就自动调用该方法。

作用：初始化成员属性和成员方法。

格式：

修饰符 类名 （参数列表）{}

类名（参数列表）{}

```java
    /*
     * @description: Person类的构造函数
     * @author: Lyd
     * @date:  11:14
     * @param: [name, age, height]
     * @return:
     **/
    public Person(String name, int age, int height) {
        return; //可以有return的关键字，但是不能跟东西
    }
```

如果一个类没有构造方法，那jvm会自动添加一个无参的构造函数，当然构造函数可以调用构造函数。例子

```java
/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: PACKAGE_NAME
 * @ Author: Lyd
 * @ CreateTime: 2024-10-06  10:29
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Person {
    // 姓名
    String name;

    // 年龄
    int age;

    // 身高
    int height;

    /*
     * @description: Person类的构造函数
     * @author: Lyd
     * @date:  11:14
     * @param: [ob_name, ob_age, ob_height]
     **/
    public Person(String ob_name, int ob_age, int ob_height) {
        name=ob_name;

        age=ob_age;

        height=ob_height;
        
    }

    /*
     * @description:
     * @author: Lyd
     * @date:  11:13
     * @param: [args]
     * @return: void
     **/
    public static void  main(String[] args)
    {
        // 声明一个人
        Person person = new Person("张三",18,180);

        System.out.println("这个人的姓名是"+person.name+"，年龄是"+person.age+",身高是"+person.height);
    }
    
}
```

### 匿名构造块

格式{}

对象创建之前，都会执行这个匿名构造块。（比如new了两个对象，那这个匿名构造块就执行两次）

匿名构造块可以有多个。

### 构造函数的重载

重载是多态的一个典型特征，同一个方法名，不同的实现结果就是多态。

类中有多个构造函数，参数列表不同

重载构造函数来表示对象的多个初始化方式

```java
/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: PACKAGE_NAME
 * @ Author: Lyd
 * @ CreateTime: 2024-10-06  10:29
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Person {
    // 姓名
    String name;

    // 年龄
    int age;

    // 身高
    int height;

    /*
     * @description:
     * @author: Lyd
     * @date:  12:03
     * @param: []
     * @return:
     **/
    public Person() {}

    /*
     * @description: Person类的构造函数
     * @author: Lyd
     * @date:  11:14
     * @param: [name, age, height]
     * @return:
     **/
    public Person(String ob_name, int ob_age, int ob_height) {
        name=ob_name;

        age=ob_age;

        height=ob_height;

    }

    /*
     * @description:
     * @author: Lyd
     * @date:  11:13
     * @param: [args]
     * @return: void
     **/
    public static void  main(String[] args)
    {
        // 声明一个人
        Person person = new Person("张三",18,180);
        Person person1 = new Person();
        System.out.println("这个人的姓名是"+person1.name+"，年龄是"+person1.age+",身高是"+person1.height);
        System.out.println("这个人的姓名是"+person.name+"，年龄是"+person.age+",身高是"+person.height);
    }

}
```

## 方法的定义和调用

方法是类和对象行为特征的抽象，java中方法不能独立存在，必须定义在类体中。

### 方法定义

语法：

权限修饰 返回值类型 方法名（参数类型 参数名）{

​		//方法体

​		//返回值

}

***方法一定要有返回值，但是返回类型是void***

方法不能嵌套（方法内部不能再定义方法）

### 方法调用

有两种调用方式

本类中调用：方法名（参数列表）

外部类的调用：对象.方法名（参数列表）

```java
public class Person {
    // 姓名
    String name;

    // 年龄
    int age;

    // 身高
    int height;

    /*
     * @description: Person类的构造函数
     * @author: Lyd
     * @date:  11:14
     * @param: [name, age, height]
     * @return:
     **/
    public Person(String ob_name, int ob_age, int ob_height) {
        name=ob_name;

        age=ob_age;

        height=ob_height;

    }

    public void show(){
        System.out.println("Name: "+name+" Age: "+age+" Height: "+height);
    }


    /*
     * @description:
     * @author: Lyd
     * @date:  11:13
     * @param: [args]
     * @return: void
     **/
    public static void  main(String[] args)
    {
        // 声明一个人
        Person person = new Person("张三",18,180);
        person.show();
    }

}
```

方法定义的时候，实例变量可以直接使用，调用的时候要注意

## 方法的重载和编译时的多态

一个类中多个方法名称相同，参数列表不同（个数，类型，顺序），与返回值类型和修饰符无关，和构造方法的重载和多态很像。

***早期绑定***：被调用的目标方法如果再编译期间可知，且运行期保持不变，则可以将这个方法与所属的类型绑定

重载的方法时早期绑定。

## 面向对象的封装机制

封装指的是隐藏对象的属性和实现细节，进对外提供公共访问方式。

作用：隐藏细节并提高访问的安全性。

### 封装的实现

用`private`关键字来修饰，之后new了之后就无法从外部直接访问。

### 简而言之

该露露，改藏藏

高内聚就是类内部数据操作细节自己完成，不允许外部干扰。

低耦合：仅暴露方法给外部使用。

数据的隐藏：禁止直接访问一个对象中数据的实际表示，而通过操作方法来访问。