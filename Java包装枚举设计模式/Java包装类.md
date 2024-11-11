# Java包装类

## 为什么需要包装类

`java`中很多方法都需要接收引用数据类型的对象，但是在`java`中基本数据类型又不是类，所以如果我们要传入一个基本数据类型该怎么办呢？这个时候就需要将基本数据类型包装成引用类型。

## 包装类的继承关系

![](C:\Users\L1523\Desktop\大学任务\java\屏幕截图 2024-10-28 193258.png)

![](C:\Users\L1523\Desktop\大学任务\java\屏幕截图 2024-10-28 193340.png)

## 自动装箱和自动拆箱

自动装箱：指的是将基本数据类型的变量赋给对应的包装类变量

（基本数据类型->包装类）

自动拆箱：指的是将包装类对象类型直接赋给一个对应的基本数据类型变量（包装类->基本数据类型）

注意**自动**这两个字，说明在进行类型转化的过程中是自动的，而用户可以直接赋值，不需要手动转化。

```java
public class Main {
    public static void main(String[] args) {
        int i =10;
        // 自动装箱 基本数据类型->转化为引用数据类型
        Integer integer = i;
        System.out.println(integer); // 打印出来也不是地址

        // 自动拆箱 将包装类变量赋值给相应的基本数据类型
        Integer x =100;
        int y = x;
        System.out.println(y);
    }
}

输出：
10
100
```

## 包装类的API

* 基本数据类型、基本包装类型以及字符串之间的相互转换

1. 通过引用数据类型字符串`String`类的`valueOf()`方法可以将8种基本数据类型转化为对应的字符串类型。
2. 通过8种包装类的静态方法`valueOf()`既可以将对应的基本数据类型转化为包装类，也可以将变量内容匹配的字符串转化为对应的包装类（character除外）。
3. 通过8种包装类的有参构造函数将基本数据类型转化为包装类，也可以将变量内容匹配的字符串转化为对应的包装类（character除外）。
4. 通过8种包装类的静态方法`parseXXX()`将变量内容匹配的***字符串***转换位对应的基本数据类型。
5. 包装类都重写了Object类种的`toString（）`方法，以字符串的形式返回被包装的数据类型的值

```java
public class Main {
    public static void main(String[] args) {
        int a =101;
        boolean f =false;
        float b=1.11f;
        // 使用的是String的valueOf函数，直接将基本数据类型转化为包装类
        String s1 = String.valueOf(a);
        String s2 =String.valueOf(f);
        String b1 =String.valueOf(b);
        System.out.println(s1);
        System.out.println(s2);
        System.out.println(b1);

        // 使用八种包装类的valueOf函数来将基本数据类型转化为包装类
        Integer s11 = Integer.valueOf(a);
        Boolean s21 =Boolean.valueOf(f);
        Float b11 =Float.valueOf(b);
        System.out.println(s11);
        System.out.println(s21);
        System.out.println(b11);

        // 使用有参构造
        Integer s12 = new Integer(a);
        Boolean s22 =new Boolean(f);
        Float b12 =new Float(b);
        System.out.println(s12);
        System.out.println(s22);
        System.out.println(b12);

        // 使用pares将包装类转为基本数据类型
        int s13 = Integer.parseInt(s1);
        boolean s23 =Boolean.parseBoolean(s2);
        float b13 =Float.parseFloat(b1);
        System.out.println(s13);
        System.out.println(s23);
        System.out.println(b13);

        // toString方法
        String s14 = Integer.toString(s12);
        String s24 =Boolean.toString(s23);
        String b14 =Float.toString(b12);
        System.out.println(s14);
        System.out.println(s24);
        System.out.println(b14);


    }
}
```

