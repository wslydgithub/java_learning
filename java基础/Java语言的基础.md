# Java语言的基础

## 1. JDK

JDK简而言之就是一个各种java工具的集成，包括java的运行环境，以及java的各种基本库

## 2. JRE

JRE是JDK的一部分，包含了java的运行环境，但是不包括开发环境，也就是只管运行不管编写，编写的任务是在JDK的其他部分的。

## 3. JVM

JVM本身是一个虚拟机，是JRE的一部分，java程序可以在JVM上运行。

***注意：***

正因为有***JVM***这个虚拟机，这样才使java程序的移植性特别强，因为每一个java程序所生成的*.class文件都可以到**JVM***中运行，甚至在不同的操作系统上运行，因为不同的操作系统都有不同版本的***JVM***。

所以我们可以看出，java程序是跨平台的，但是***JVM***则不是跨平台的，不同的操作系统需要不同的***JVM***。

**小tip:**

为什么我们需要将bin目录放到path中呢？是因为bin目录中一般是各种软件的私人命令，path是让windows系统能够找到这个bin目录并能够识别这些私人命令。

## 2.编写

### 1. java最基本的单元是类

因为java是一个纯面向对象的语言，所以java中最基础的对象是类，比如

```java
public class Example{
	public static void main(String[] args){
		System.out.println("Hello,world");
	}
}
```

注意：类的名称要和我们编写的.java程序的名字保持一致，一个.java文件中只有一个public class的定义，其次，java有着明确的命名要求，定义类的时候第一个首字母大写。

### 2.主方法

主方法也就是main方法，是任何一个java程序的起点和入口。

### 3.java的运行过程

我们编写的是.java文件，通过javac命令生成.class文件，之后通过java命令来执行.class文件

![](C:\Users\L1523\Desktop\大学任务\java\java基础\屏幕截图 2024-09-29 203237.png)
