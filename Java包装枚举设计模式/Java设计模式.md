# Java设计模式

## 什么是设计模式

设计模式是指软件开发人员在开发过程中面临的一般问题的解决方案。

## GOF（Gang of Four）

四个人出了一本设计模式的树，第一次提出了设计模式这一个概念，所以称为四人帮。

## 常见设计模式的类型

### 单例模式：

`java`中最简单的设计模式之一，属于创建型模式，提供了一种创建对象的最佳方式。

这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一对象的方法，可以直接访问，不需要实例化该类的对象。

注意：

1. 单例类只能有一个实例。
2. 单例类必须自己给自己创建唯一的实例。
3. 单例类必须给所有其他对象提供这一个实例。

#### 创建方式：

 ##### 懒汉式：

* Lazy初始化
* 多线程安全
* 实现简单
* 加了锁但是效率低下
* 第一次调用才初始化，避免内存浪费。

```java
public class Single {
//    1. 单例类只能有一个实例。
//    2. 单例类必须自己给自己创建唯一的实例。
//    3. 单例类必须给所有其他对象提供这一个实例。
    // 单例必须自己给自己创建唯一的实例，自己创建自己
    private static Single unique;

    // 唯一的实例 肯定不能使用new来创建，因为new是可以new出无数个的
    private Single(){}// 将构造私有化 从而避免外部new()来创建

    // 如何对外提供这个对象,使用一个构造方法,确保是线程安全的
    public static synchronized Single getInstance() {
        if (unique == null) {
            unique = new Single();
        }
        return unique;
    }
}
```

* 只能有一个实例：

1. 使用了`static`来修饰`unique`相当于类变量，创建的时候会实例化。
2. `getInstance`函数在创建的时候会直接检查类变量是否为空，如果不为空再创建，保证只有一个实例。
3. 构造函数是`private`的，所以无法通过构造函数来构造

* 类自己给自己创建

1. 防止出现矛盾（要创建`Single`就必须要有`Single`），将`getInstance()`变为类属性直接通过类来调用。

* 为所有对象提供

1. 防止出现线程的并发问题，所以这里加上了`synchronized`这个关键字。

##### 饿喊式：

* 不Lazy初始化
* 是多线程安全
* 实现简单
* 常用，但容易出现垃圾对象
* 没有加锁，执行更高
* 类加载时就初始化，浪费内存

```java
public class Single{
	private static Single single =new Single();
	
	private Single(){}
    
    public static Single getInstance(){
    
    return single()
    }
}
```

### 策略模式：

在策略模式中，一个类的行为或其算法可以在运行时更改，属于行为型模式。

* 定义一系列的算法，把它们一个个封装起来，并且让他们相互替换
* 解决多种算法相似的情况下，使用if..else..所带来的复杂度和难以维护。
* 将这些算法封装成一个一个的类，任意替换
* 实现同一个接口
* 策略类会增多
* 所有策略类都要对外暴露

```java
package strategymodel;

public interface Strategy {
    public int calculate(int a, int b);

}

package strategymodel;

/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: strategymodel
 * @ Author: Lyd
 * @ CreateTime: 2024-10-31  11:20
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Mutiply implements Strategy {

    @Override
    public int calculate(int a, int b) {
        return a*b;
    }
}

public class Caculate {
    public static void main(String[] args) {
        Context a =new Context(new Add());
        System.out.println(a.operation(1,2));
        Context b =new Context(new Mutiply());
        System.out.println(b.operation(3,4));
    }
}

package strategymodel;

/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: strategymodel
 * @ Author: Lyd
 * @ CreateTime: 2024-10-31  11:19
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Add implements Strategy {

    @Override
    public int calculate(int a, int b) {
        return a+b;
    }
}

public class Context {
    private Strategy strategy;

    public Context(Strategy strategy) {
        this.strategy = strategy;
    }

    public int operation(int num1, int num2) {
        return strategy.calculate(num1, num2);
    }
}
```

解析：

在接口中定义一个抽象方法，然后使用不同的类来实现这个方法，通过一个Context类来将这几个类集合起来，时期能够通过Context来分别访问这几个不同类型的类。

### 工厂模式

创建型模式，提供了创建对象的最佳方式。部队客户端暴露创建逻辑，通过使用一个共同的接口来只想新建的对象。

* 创建一个对象的接口，让子类自己决定实例化哪一个工厂类
* 抓药解决接口选择问题
* 创建过程在子类中进行

```java
package factorymodel;

public interface Factory {
    void Create();
}

package factorymodel;

/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: factorymodel
 * @ Author: Lyd
 * @ CreateTime: 2024-10-31  11:40
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Circle implements Factory {
    @Override
    public void Create() {
        System.out.println("Creating Circle");
    }
}

package factorymodel;

/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: factorymodel
 * @ Author: Lyd
 * @ CreateTime: 2024-10-31  11:43
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Rectangle implements Factory{

    @Override
    public void Create() {
        System.out.println("Create Rectangle");
    }
}

package factorymodel;

/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: factorymodel
 * @ Author: Lyd
 * @ CreateTime: 2024-10-31  11:44
 * @ Description: TODO
 * @ Version: 1.0
 */
public class ShapeFactory {
    public static Factory getShape(String shapeType) {
        if (shapeType.equalsIgnoreCase("Rectangle")) {
            return new Rectangle();
        } else if (shapeType.equalsIgnoreCase("Circle")) {
            return new Circle();
        }else {
            return null;
        }
    }
}

package factorymodel;

/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: factorymodel
 * @ Author: Lyd
 * @ CreateTime: 2024-10-31  11:46
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Test {
    public static void main(String[] args) {
       Factory circle= ShapeFactory.getShape("Circle");
       circle.Create();
        Factory rectangle= ShapeFactory.getShape("Rectangle");
        rectangle.Create();
    }
}
```

解析：

先定义接口，然后利用类来实现接口，最后通过子类来进行划分并创建，最后在调用。

### 代理模式

代理模式是使用一个类来代表另一个类的功能，属于结构型模式

创建拥有现有对象的对象，以便向外界提供功能接口

* 为其他对象提供代理来控制对这个对象的访问

* 解决在直接访问时带来的问题

* 在访问类的时候做控制

* 实现与被代理类组合

* 职责清晰，高扩展性，智能化

  ```java
  package proxymodel;
  
  public interface Image {
      void display();
  }
  
  package proxymodel;
  
  /**
   * @ BelongsProject: javaCode
   * @ BelongsPackage: proxymodel
   * @ Author: Lyd
   * @ CreateTime: 2024-10-31  11:56
   * @ Description: TODO
   * @ Version: 1.0
   */
  public class RealImage implements Image {
      private String fileName;
  
      public RealImage(String fileName) {
          this.fileName = fileName;
          loadFile(fileName);
  
      }
  
      @Override
      public void display() {
          System.out.println(fileName+"displaying");
      }
  
      private void loadFile(String fileName) {
          System.out.println(fileName+"loading");
      }
  }
  
  package proxymodel;
  
  /**
   * @ BelongsProject: javaCode
   * @ BelongsPackage: proxymodel
   * @ Author: Lyd
   * @ CreateTime: 2024-10-31  11:58
   * @ Description: TODO
   * @ Version: 1.0
   */
  public class Proxymodel implements  Image {
      private RealImage realImage;
  
      private String fileName;
  
      public Proxymodel(String fileName) {
          this.fileName = fileName;
      }
  
      @Override
      public void display() {
          if (realImage == null) {
              realImage = new RealImage(fileName);
          }
          realImage.display();
  
      }
  }
  
  package proxymodel;
  
  /**
   * @ BelongsProject: javaCode
   * @ BelongsPackage: proxymodel
   * @ Author: Lyd
   * @ CreateTime: 2024-10-31  12:02
   * @ Description: TODO
   * @ Version: 1.0
   */
  public class Test {
      public static void main(String[] args) {
          Image image=new Proxymodel("1");
          image.display();
          image.display();
      }
  }
  ```

  解析：

  先创建一个接口，然后利用一个类来实现这个接口（这个类主要负责真正的业务），在用一个包含业务类的类来对业务的输入和选择进行处理，最后调用的时候调用的是这个业务类。

### 门面模式

将一个系统划分为小系统，最后使用一个门面来对业务进行分类。

```java
package doormodel;

public interface Shape {
    void Create();
}

package doormodel;

/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: doormodel
 * @ Author: Lyd
 * @ CreateTime: 2024-10-31  12:13
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Circle implements Shape {
    @Override
    public void Create() {
        System.out.println("Creating Circle");
    }
}

package doormodel;


/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: doormodel
 * @ Author: Lyd
 * @ CreateTime: 2024-10-31  12:13
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Rectangle implements Shape {

    @Override
    public void Create() {
        System.out.println("Create Rectangle");
    }
}

package doormodel;

/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: doormodel
 * @ Author: Lyd
 * @ CreateTime: 2024-10-31  12:14
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Door {
    private Circle x;
    private Rectangle y;

    Door() {
        x = new Circle();
        y = new Rectangle();
    }

    public void drawCircle() {
         x.Create();
    }

    public void drawR() {
        y.Create();
    }
}

package doormodel;

/**
 * @ BelongsProject: javaCode
 * @ BelongsPackage: doormodel
 * @ Author: Lyd
 * @ CreateTime: 2024-10-31  12:15
 * @ Description: TODO
 * @ Version: 1.0
 */
public class Test {
    public static void main(String[] args) {
        Door door = new Door();
        door.drawCircle();
        door.drawR();
    }
}
```

解析：

使用一个接口，利用其来进行类的创建，通过一个Door类将业务类的功能集成起来，最后通过这个集成来访问