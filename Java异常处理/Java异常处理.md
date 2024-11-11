# Java异常处理

## 异常和错误

* 异常：在`java`程序运行的过程中，出现的非正常情况，导致`JVM`的非正常停止。
* 异常体系：

`java`中提供了异常(`Throwable`)的两个子类，`Error`和`Exception`

`Error`表示的是严重错误问题，无法处理的问题，只能事先避免，比如内存溢出。

`Exception`表示异常类，它表示程序本身可以解决的问题，比如数组下标的越界。

## 异常分类

* 编译时异常，检查异常，必须显示的处理，否则程序无法通过编译。
* 运行时异常，非检查异常，无须显示处理，也可以和编译时异常一样处理

`RuntimeException`所有类及其子类都被称为运行时异常，其他的都是编译时异常。

## 异常处理机制

异常处理机制：程序出现异常时，系统能够捕获这个异常，并选取指定异常的代码块进行运行。如果没有捕获的块，则爆出异常

### 处理格式

`try catch`模式，使用实例

```java
try{

}catch(异常){

}
```

变式：

每一个try语句块之后，都可以跟上一个或者多个catch语句块，以便处理不同类型的异常，但是不同种类异常的顺序应该是从子类到父类，一步一步扩大的，但是只会处理第一个异常，也就是第一个符合类型的异常

## finally块

`finally`是错误处理的最终出口，类比一下`python`,不管你出现的错误是什么或者说有没有出现错误，`finally`都是最终的出口，一般其负责的是资源的释放，关闭打开的文件，关闭数据库的连接等等。

```java
public class Main {
    public static void main(String[] args) {
        try {
            System.out.println("Hello world!");
            int [] a = {1,2,3};
            System.out.println(a[3]);
        }catch (Exception e) {
            System.out.println(e);
        }finally {
            System.out.println("solve down");
        }

    }
}
```

## throws和throw关键字

### throws关键字

程序中会声明许多方法，这些方法可能会因为出现错误而引发异常，但是我们并不想直接在该方法中进行处理，而是调用其他方法统一处理，所以这时就要使用`throws`关键字来在这个方法上抛出异常。

格式

```java
修饰符 返回值类型 方法名（参数） throws 异常类1，异常类2，....{
}
```

编译时异常是一定要处理的，有两种方案，第一种是`try catch`，第二种就是`throws`谁调用谁处理。

运行时异常可以不处理，出现问题后，可以来修改代码

```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Main {
    // throws抛出运行时错误
    public static void  throwDemo1() throws ArrayIndexOutOfBoundsException{
        int arr[]={1,2,3};
        System.out.println(arr[3]);
    }

    public static void  throwDemo2() throws ParseException {
        String data ="2024-11-4";
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        Date date = sdf.parse(data);
    }

    public static void main(String[] args) {
        try{
//            throwDemo1();
            throwDemo2();
        }catch (ParseException | ArrayIndexOutOfBoundsException e) {
            System.out.println(e);
        }


    }
}
```

### throw关键字

在某些情况下，程序想要自行抛出异常，这时就需要使用`throw`关键字自行抛出，并生成指定的异常对象后抛出。

throw定义在方法中，用来抛出一个异常对象,类似于`Golang`中的那个`Error.new()`

格式

```java
throw new 异常类名（）
```

```java
    public static void  throwDemo3(int []arr) {
        if (arr ==null){
            throw new NullPointerException("arr is null");
        }
    }
    public static void main(String[] args) {
//        try{
////            throwDemo1();
//            throwDemo2();
//        }catch (ParseException | ArrayIndexOutOfBoundsException e) {
//            System.out.println(e);
//        }
        int a[] = null;
        throwDemo3(a);


    }
```

### throw和throws的区别

throws:

* 用于方法体后面
* 相当于把异常传给了调用的人，所以有调用者来处理
* 表示有出现异常的可能，并不一定会发生

throw:

* 用于方法体中
* 直接在方法内部处理错误
* 一旦执行，就一定抛出异常

## 子类和父类关键字使用throws关键字

### 父类构造函数使用throws关键字抛出编译时异常

子类抛出的异常必须大于或等于父类抛出的异常，并且只能抛出，无法捕获

![](C:\Users\L1523\Desktop\大学任务\java\屏幕截图 2024-11-04 090652.png)

### 父类构造函数使用throws关键字抛出运行时异常

子类可以选择声明或者不声明（可处理也可以不处理），子类抛出的异常必须大于或等于父类抛出的异常，并且只能抛出，无法捕获

## 方法重写中使用throws关键字

在方法重写时，父类声明了异常，子类的处理方法

* 子类不处理异常（不定义`throws`）
* 子类处理部分异常（只定义一部分异常）
* 子类处理小于或者等于父类的异常

子类重写父类该方法时抛出运行时异常，父类被重写的方法上可以不抛出异常

父类方法没有抛出异常，子类重写父类方法时抛出编译异常，处理方法

* 父类抛出异常，并且异常要大于或等于子类的异常
* 子类直接捕获异常，不抛出

## `RuntimeException`和自定义异常类

### `RuntimeException`

属于运行时异常，常见运行时异常

* `NullPointerException`：空指针异常
* `ArrayIndexException`：数组下标越界异常
* `ClassCastException`：强制转换异常

Exception常见的`API`

* `printStackTrace`输出错误信息，追踪异常事务发生时执行堆栈的内容

使用时，结合`try catch`使用

```java
try{

}catch(Exception e){
	e.printStackTrace();
}
```

* `getMessage`得到异常事件的信息，需要输出

```java
try{

}catch(Exception e){
	System.out.print(e.getMessage());
}
```

### 自定义异常类

集成`Exception`：

```java
public class ScoreException extends Exception{
	public ScoreException(){};
	public ScoreException(String Message){
	super(Message); // 调用的是父类的方法
	};
}
```

## 垃圾回收机制（`GC`）

是`JVM`自带的一个线程，进行自主内存管理，如果要自行处理，要调用

```java
System.gc()
```

但是具体的实现是由`JVM`决定

### 内存泄漏

不再使用的内存但是没有被回收

`GC`判断是否回收内存的依据是，该对象是否由引用指向，所以当该对象不再使用时，尽量设置为`Null`