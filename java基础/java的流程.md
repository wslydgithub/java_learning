# java的流程

## main方法

java程序的入口是main函数，一个java源代码中只有一个main方法,并且main方法所在的类名，必须和源文件一致。

## 选择结构

```java
if (){

}
```

```java
if (){

}else{

}
```

嵌套

```java
if (){

}else if(){

}else{

}
```

和C语言一致，不再多说

### switch-case分支语句

```java
switch (){
	case 取值1：{
			语句1;
			break;
				}
	case 取值2：{
			语句2;
			break;
				}
	default:{
			语句块
	}
}
```

在JDK1.5之前可以传入byte,short,int,char

long,String不可以出传入

在JDK1.7之后可以传入String

## 循环结构

while, do while ,for都和C一样，没什么好说的

### 循环控制

break和continue都一样

return作用

1.返回方法所规定的类型

2.方法结束



