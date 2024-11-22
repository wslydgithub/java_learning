# Java图形用户界面

## 图形用户界面概述

使用的包`awt`,`swing`

包括菜单，输入输出，按钮，画板，窗口和对话框

## 窗体容器和其组件

### 窗体容器`JFame`类

`JFame`是一个带有标题、边框的一个顶层窗体，窗体是一个容器，其内部可以添加取头容器，所有的`Swing`组件只有在容器中，才可以被显示

**操作**

1. 空构造函数`JFame`
2. 有参构造函数`JFame(String)`，创建一个标题为String的窗口
3. 设置窗口是否可以可见`public void setVisible(boolean b)`
4. 撤销窗口并释放资源`public void dispose()`
5. 关闭图标的处理`public void setDefaultCloseOperation(int Operation)`

