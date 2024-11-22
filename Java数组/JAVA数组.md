# JAVA数组

## 数组的定义

存储相同数据类型的一个数据类型

1. 动态初始化,初始化只声明长度和类型，而不直接赋值

```java
int [] number = new int[10]
```

2. 静态初始化,初始化时直接进行赋值

```java
int []number = new int[3]{1,2,3}

int []number={1,2,3,4}
```

**注意**

```java
System.out.println(arr);
```

与`Go`语言不同，当我们直接以数组的名字来进行打印的时候，`Java`打印出的是地址，因为在`Java`中数组为引用类型，栈空间只存放堆空间的地址（指针）

初次之外，当数组只被声明而不被赋值的时候，数组内部数值的值是该类型的默认值

## 数组遍历

数组因为其长度确定，天生就和`for`循环保持在一起

```java
int [] number = new int[10]

for(int i =0;i<number.length;i++){
//操作
}
```

## 数组中的数组

数组中每个元素也是一个数组（平铺下来可看为多维数组或者多维矩阵），定义方式

```java
数据类型 [][] 数组名 = new 数据类型[外层数组长度][内层数组长度]
```

多维数组在`Java`中的内存示意图：

注意，在`java`中数组名（数组）储存在栈内存中，而数据元素储存在堆内存中。

![](C:\Users\L1523\Pictures\Screenshots\屏幕截图 2024-11-21 090409.png)

发现如果是一维数组，则堆内存里直接存的就是数值，而多维数组中，第一层的堆内存存储的是第二层数组的地址 

```java
public class multi_array {
    public static void main(String[] args) {
        int[][] numbers = new int[3][3];
        for(int i =0;i<numbers.length;i++){
            for(int j =0;j<numbers[i].length;j++){
                numbers[i][j] = i+j;
                System.out.print(numbers[i][j]+" ");
            }
        }
    }
}
```

第一个`numbers.length`是外层数组的长度，而第二个`numbers[i].length`找到对应行的数组长度

## 数组排序

常用的排序算法插入排序，快速排序，冒泡排序

### 冒泡排序

每次选出一个最小的或者最大的，每次是相邻交换

```java
public class boom {
    public static void main(String[] args) {
        int [] number = {39,430,2032,321,1312,321};
        for (int i = 0; i < number.length-1; i++) {
            for (int j=0;j<number.length-i-1;j++){
                if(number[j]>number[j+1]){
                    int temp = number[j];
                    number[j] = number[j+1];
                    number[j+1] = temp;
                }
            }
        }
        for (int i = 0; i < number.length; i++) {
            System.out.println(number[i]);
        }

    }
}
```

## 数组的最大最小和过滤重复

### 数组最大和最小

```java
public class Max_Min {
    public static void main(String[] args) {
        int [] numbers = new int [10];
        for(int i = 0; i < numbers.length; i++){
            numbers[i] = i;
        }
        int max = numbers[0];
        int min = numbers[0];
        for (int i = 0; i < numbers.length; i++) {
            if(max<=numbers[i]){
                max = numbers[i];
            }
        }
        System.out.println(max);
        for(int i = 0; i <numbers.length; i++){
            if(min>=numbers[i]){
                min=numbers[i];
            }
        }
        System.out.println(min);
    }
}
```

### 过滤重复

对于数组进行去重，并记录重复元素的个数

```java
public class Repeat {
    public static void main(String[] args) {
        int []num = {1,2,2,3,3,3,4,4,4,4,5,5,5,5,5};
        int []num_1=new int[num.length];
        int []num_2=new int[num.length];
        for (int i = 0; i < num.length; i++) {
            for (int j = 0; j < num_1.length; j++) {
                if (num[i] == num_1[j]) {
                    num_2[j]++;
                    break;
                }
                if (j==num_1.length-1){
                    num_1[i]=num[i];
                    num_2[i]++;
                }
            }


        }
        for (int i = 0; i < num.length; i++) {
            System.out.print(num[i] );
            System.out.print(num_1[i] );
            System.out.print(num_2[i] );
            System.out.println();
        }
    }
}
```

## 数组的系统类`Arrays`

还记得之前讲的数据类型其对应的`class`类吗？，数组对应的`java`类型就是`Arrays`类

1. `toString`将数组中的内容转化为字符串
2. `sort `将数组中的值进行由小到大的排序
3. `copyOf`实现数组的复制

```java
import java.lang.reflect.Array;
import java.util.Arrays;

public class array {
    public static void main(String[] args) {
        int[] arr = {11213,223,3342,4243,1154,34231};
        System.out.println(arr);
        System.out.println(arr.length);
        System.out.println(Arrays.toString(arr));
        Arrays.sort(arr);
        System.out.println(Arrays.toString(arr));
        System.out.println(Arrays.toString(Arrays.copyOf(arr, 3)));
    }
}
```

