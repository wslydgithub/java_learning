# Java枚举类

## 枚举定义

首先，枚举是一种特殊的类，是有固定个数的类型，举个例子，性别就是枚举类，只有男和女。

定义枚举类型实际上是定义一个类，所以`enum`关键字的作用就像是`class`或者`interface`

当你使用`enum`关键字时，所定义的类实际上是集成了`java.lang.Enum`类,每一个被枚举的成员就是定义的枚举类型的一个实例，默认为`final`,常量无法改变值，并且它们也是`public`和`static`的成员，所以可以通过类名来进行调用。

```java
public enum Ssex {
    MALE,FEMALE;// 直接定义实例
}
```

在枚举类中直接定义实例

## 枚举的结构

枚举是可以和其他类一样，添加方法和属性

```java
public enum Ssex {
    MALE,FEMALE;// 直接定义实例
    // 属性
    public static String str;
    //MALE,FEMALE;// 直接定义实例
    
    // 方法
    public void show(){
        System.out.println(str);
    }
}
```

枚举本身是一个类，所以其中也是可以定义方法和属性的，并且方法和属性前面的修饰也可以自己定义，但是枚举类的实例必须定义在第一列，否则会报错

### 带构造方法的枚举

枚举也可以有构造方法，但是需要对于实例进行相应的修改

```java
public enum Ssex {
    MALE("male"),FEMALE("female");// 直接定义实例
    // 属性
    private final String str;
    //MALE,FEMALE;// 直接定义实例

    Ssex(String str){
        this.str = str;
    }
    // 方法
    public void show(){
        System.out.println(str);
    }

}

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
        Ssex a =new("你好"); // 这个地方会报错
    }
}
```

枚举定义了构造函数时，这个函数只能在枚举类中使用，不能再通过`new()`来新建

### 带抽象方法的枚举

```java
public enum Ssex {
    MALE{
        @Override
        public void show() {
            System.out.println("Male");
        }
    },
    FEMALE{
        @Override
        public void show() {
            System.out.println("Female");
        }
    };
    
    // 方法
    public abstract void show();
}
```

根据抽象方法的定义我们知道，枚举的每一个实例都要实现这个抽象方法，所以再MALE和FEMALE后面跟了一个方法的重写。

## 枚举的应用

枚举是一种类型，用于定义变量，并限制变量的赋值，赋值时通过枚举名.值来取值，常用API

### values()

取得所有枚举的值，并以数组形式放回

### compareTo()

比较枚举的顺序

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
        Ssex ly =Ssex.MALE;
        Ssex lc = Ssex.FEMALE;
       System.out.println(Arrays.toString(Ssex.values()));
        System.out.println(ly.compareTo(lc));// 0-1
    }
}
```