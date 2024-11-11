# Java中的函数式编程

## 函数编程的思想

强调做什么，而面向对象的编程，则是说强调以对象的方式来做，也就是必须要指定一个对象来做事。

```java
new Thread(new Runnable(){
	@override
	public void run(){
}
}).start()
```

在这个例子中，我们想要通过线程实现`run()`方法，也就是想让`run()`内部的代码让`Thread()`知道，`Thread()`需要一个`Runable()`接口，要实现这个接口就需要定义一个实例类，并重写`run()`方法，所以本质上我们并不想要`Runnable()`这个接口，更不想为它分配内存，所以这里直接就采用了匿名内部类的方法

## 函数式编程的本质是什么？

传递一段代码，创建对象只是因`java`纯面向对象的语法的限制来做而已。

问题：在上面的例子中，虽然我们使用了匿名内部类，已经大大减少了对象的依赖，但是匿名内部类的语法还是过于冗余。

解决方法：使用`Lambda`表达式，这种表达式只针对于有一个抽象方法的接口实现。

```java
new Thread(()-> System.out.println()).start
```

在这个例子中`()-> System.out.println()`这就是我们所说的`Lambda表达式`

## Lambda表达式的语法

`(参数类型 参数名，参数类型 参数名...)->{表达式主体}`

参数列表中传递的参数是实现接口中方法的参数。

`->`表示参数数据的指向，是不能省略的。

表达式主题，是抽象方法的具体实现

## Lambda表达式的限制

当接口中有且只有一个抽象方法时，才能使用Lambda表达式来代替匿名内部类，因为Lambda是基于函数式接口(有且仅有一个抽象方法的接口)实现的

```java
@FunctionalInterface
```

以这种标记的为功能性接口

例子：

```java
@FunctionalInterface
public interface Function {
    public int add(int a,int b);
}

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
        Function jisuan = (int x1,int x2)->x1+x2;
        System.out.println(jisuan.add(1,2));
    }
}
```

## 方法引用

Lambda的表达式的主体只有一条语句时，程序不仅可以省略包含花括号，还可以使用`::`来引用方法和构造器

### 类名引用静态方法

使用类名来使用静态方法(因为是静态方法所以属于类，可以不用构造出实例)

```java
public class Math {
    public static int abs(int a){
        if (a>0) {
            return a;
        }else {
            return -a;
        }
    }
}

@FunctionalInterface
public interface Function {
    public int func(int a);
}

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
        Function abs = Math::abs;
        System.out.println(abs.func(1));

    }
}
```

### 对象名引用方法

和类引用静态方法很想，只是将类名变为实例化的对象

```java
public class Math {
    public static int abs(int a){
        if (a>0) {
            return a;
        }else {
            return -a;
        }
    }

    public int turn(int a){
        return -a;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
        // 静态方法
        Function abs = Math::abs;
        System.out.println(abs.func(1));
        // 匿名内部类
        Function turn=new Function(){
            @Override
            public int func(int a) {
                return -a;
            }
        };
        System.out.println(turn.func(1));
        // 实现类
        Math math =new Math();
        Function turn1 = math::turn;
        System.out.println(turn1.func(1));
    }
}
```

### 构造器

使用类的构造器

```java
public class Math {
    Math(int a){
        System.out.println(a+"...");
    }
    public static int abs(int a){
        if (a>0) {
            return a;
        }else {
            return -a;
        }
    }

    public int turn(int a){
        return -a;
    }
}

@FunctionalInterface
public interface Function_build {
    public Math func(int a);
}

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
        // 静态方法
        Function abs = Math::abs;
        System.out.println(abs.func(1));
        // 匿名内部类
        Function turn=new Function(){
            @Override
            public int func(int a) {
                return -a;
            }
        };
        System.out.println(turn.func(1));
        // 实现类
        Math math =new Math(1);
        Function turn1 = math::turn;
        System.out.println(turn1.func(1));

        Function_build turn3=Math::new;
        System.out.println(turn3.func(1));
    }
}
```