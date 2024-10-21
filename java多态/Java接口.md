# Java接口

## 接口特点

1. 不能实例化
2. 没有构造函数
3. 属性默认`public static final`修饰
4. 方法默认为抽象方法

## 接口作用

`java`使用接口来实现多继承。

## 接口定义

在`java`中，接口是对外提供的一些功能的声明，关键字`interface`

## 接口注意

1. 在接口中的所有属性都默认为`public static final`修饰
2. `implements`关键字

```java
public class Test1 {
    static MediaBook a = new MediaBook();
    public static void main(String[] args) {
        System.out.println(a.getName());
        a.output();
    }
}

```

## 接口特性

### 接口和类之间的区别

#### `JDK1.8`之前

1. 接口中的属性，只能是`public static final`来修饰，而且必须初始化，而类中的属性则没有限制，可以只声明不赋值。

2. 接口属于抽象值,接口中的方法在`JDK1.8`之前接口中的方法都是抽象方法，并且不能有构造方法，**注意`Java`中抽象类可以有构造函数的原因是，抽象类可以有实例化的方法，但是接口中只能是抽象方法**

3. 接口可以继承接口，用的关键字为`extends`,使用接口的继承来实现类的多继承，

   举一个例子：

   ```java
   public interface MyInterfaceOne {
   
   }
   
   public interface MyInterfaceTwo extends MyInterfaceOne{
   
   }
   
   public interface MyInterfaceThree {
       
   }
   
   public class Book{
   
   }
   
   public class MyClass extends Book implements MyInterfaceTWo,MyInterfaceThree {
   
   }
   ```

   这时，`MyClass`类就既继承了`Book`类的实例方法，又继承了`MyInterfaceOne`和`MyInterfaceTwo`两个接口的抽象方法(因为`implements`可以实现多个接口，所以也可以通过`MyInterfaceThree`这种方法来写)，实现了多继承，当然你也可以通过方法重写来对于Book中的各种实例方法重写，也可以通过在`Myclass`类中对两个接口的抽象方法进行一个实例化。

### `JDK1.8`之后

1. 接口可以实现多继承，即在`extends`关键词之后再跟上其他的接口（多个）
2. 方法允许`abstract`，`default`以及`static`方法，后两个方法是有方法体的

