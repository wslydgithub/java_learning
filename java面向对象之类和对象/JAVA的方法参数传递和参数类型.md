# JAVA的方法参数传递和参数类型

## 方法参数的类型

方法参数可以是基本数据类型也可以是引用类型

如果为基本数据类型，参数传递的是副本，副本里面是这个基本数据类型的值，所以对其修改并不能修改原数据。

如果是引用数据类型，参数传递的也是副本，副本里面是这个参数的地址，所以对其修改是可以修改原数据的。

和C中的值传递和引用传递一致

## 可变参数列表

例子：

```java
public void add(int... a){
	for (int i =0 ;i<a.length;i++){
		System.out.println(a[i])
	}
}
```

和python中的*para一样，都是将输入的参数合成了一个数组（python中叫列表），python中的列表什么类型都可以，但是java中的只能是相同类型，同python一致，可变参数都要放到输入参数的最后。

## this的作用

this是对当前对象的引用，相当于如果你用this._相当于一个引用，是会对原数据修改的