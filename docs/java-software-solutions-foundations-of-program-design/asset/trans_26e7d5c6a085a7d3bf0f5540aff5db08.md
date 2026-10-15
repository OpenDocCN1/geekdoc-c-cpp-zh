

PP 3.6 编写一个应用程序，从用户那里读取三角形的三条边长。使用海伦公式（如下）计算三角形的面积，其中 s 表示三角形周长的一半，a、b 和 c 表示三条边的长度。将面积打印到小数点后三位。

Area = √[s(s − a)(s − b)(s − c)]

PP 3.7 编写一个应用程序，生成一个介于 20 到 40 之间（含）的随机整数，并显示该数字的正弦、余弦和正切值。

PP 3.8 编写一个应用程序，生成一个介于 1 到 10 之间（含）的随机整数半径（r）和高度（h）用于圆柱体，然后计算圆柱体的体积和表面积。

Volume = πr²h

Area = 2πr h

PP 3.9 编写一个应用程序，显示一个包含两个标签的框架，一个用于显示你的名字，另一个用于显示你的姓氏。尝试改变窗口大小，观察标签如何改变彼此的方向。

PP 3.10 编写一个应用程序，显示一个包含两个面板的框架。每个面板应包含两张图片（使用四张不同的图片——由你选择）。固定第一个面板的大小，使其两张图片始终并排显示。允许另一个面板根据需要改变大小。尝试改变窗口大小，观察图片如何改变方向。确保你理解应用程序的行为原因。

PP 3.11 修改 LabelDemo 程序，使其显示第四个标签，标签的文字居于图片上方。

## 编写类

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_186_0.png)

## 章节目标

- 讨论类定义的结构和内容。
- 使用实例数据建立对象状态的概念。
- 描述可见性修饰符对方法和数据的影响。
- 探索方法定义的构成，包括参数和返回值。
- 讨论构造函数的结构和目的。
- 探索图形对象的创建。
- 介绍创建交互式图形用户界面的所需概念。
- 探索一些基本的 GUI 组件和事件。

在第 3 章中，我们使用了类和对象来提供各种服务。也就是说，我们使用了 Java 类库中提供的预定义类，以便使编写程序的过程更简单。在本章中，我们将讨论面向对象编程的核心：编写自己的类来定义自己的对象。本章探讨类定义的基础，包括方法的结构以及数据的范围和封装。本章的 Graphics Track 部分讨论如何编写具有图形表示的类，并介绍创建真正交互式图形用户界面所需的要点。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_186_1.png)

## 4.1 重新审视类和对象

在第 1 章中，我们介绍了基本的面向对象概念，包括对象和类的简要概述。在第 3 章中，我们使用了 Java 标准类库中的几个预定义类来创建对象，并利用它们提供的特定功能。

在本章中，我们将把注意力转向编写自己的类。尽管现有的类库提供了许多有用的类，但面向对象程序开发的本质是设计和实现自己的类以满足特定需求的过程。

回顾对象和类之间的基本关系：类是对象的蓝图。类代表对象的概念，而从该类创建的任何对象都是该概念的实现。

例如，从第 3 章我们知道 String 类代表字符字符串的概念，而每个 String 对象代表包含特定字符的特定字符串。

让我们考虑另一个例子。假设有一个名为 Student 的类，表示大学中的一名学生。从 Student 类创建的对象将代表一名特定的学生。Student 类代表学生的一般概念，而从该类创建的每个对象都代表学校中实际就读的一名学生。在一个帮助管理大学事务的系统中，我们将有一个 Student 类和数千个 Student 对象。

回顾对象具有状态，其由与该对象关联的属性的值定义。学生的属性可能包括学生的姓名、地址、专业和平均绩点。Student 类规定每个学生都有这些属性。每个 Student 对象存储特定学生的这些属性的值。在 Java 中，对象的属性由在类中声明的变量定义。

对象还具有行为，其由与该对象关联的操作定义。学生的操作包括更新该学生的地址和计算该学生的当前平均绩点的能力。Student 类定义了操作，例如平均绩点计算的细节。然后这些操作可以对（或由）特定的 Student 对象执行。请注意，对象行为可能会修改对象状态。在 Java 中，对象的操作由在类中声明的方法定义。

图 4.1 列出了一些类的示例，以及为这些类的对象可能定义的一些属性和操作。程序设计者需要确定需要哪些属性和操作，这取决于程序的目的以及特定对象在该目的中的作用。考虑你可能为这些示例包含的其他属性和操作。

| Class | Attributes | Operations |
|---|---|---|
| Student | Name<br>Address<br>Major<br>Grade point average | Set address<br>Set major<br>Compute grade point average |
| Rectangle | Length<br>Width<br>Color | Set length<br>Set width<br>Set color |
| Aquarium | Material<br>Length<br>Width<br>Height | Set material<br>Set length<br>Set width<br>Set height<br>Compute volume<br>Compute filled weight |
| Flight | Airline<br>Flight number<br>Origin city<br>Destination city<br>Current status | Set airline<br>Set flight number<br>Determine status |
| Employee | Name<br>Department<br>Title<br>Salary | Set department<br>Set title<br>Set salary<br>Compute wages<br>Compute bonus<br>Compute taxes |

图 4.1 类的示例以及一些可能的属性和操作

## 自测题（答案见附录 N）

- SR 4.1 什么是属性？
- SR 4.2 什么是操作？
- SR 4.3 列出可能为表示图书馆中书籍的 Book 类定义的一些属性和操作。
- SR 4.4 真或假？解释。
  a. 编写程序时，我们应该只使用 Java 标准类库中的类——没有必要定义或使用其他类。
  b. 对象上的操作可以改变对象状态。
  c. 对象的当前状态会影响对该对象执行的操作的结果。
  d. 在 Java 中，对象的状态由其方法表示。

## 4.2 类的解剖结构

在我们之前所有的示例中，我们都编写了一个包含单个 main 方法的单个类。这些类代表小型但完整的程序。这些程序通常使用 Java 类库中的预定义类实例化对象，并使用这些对象提供的服务。那些预定义类也是程序的一部分，但我们除了知道如何与它们交互外，几乎不关心它们。我们只需相信它们会提供它们承诺的服务。

让我们看另一个类似的例子。清单 4.1 中显示的 RollingDice 类包含一个 main 方法，该方法实例化了两个 Die 对象（die 的单数形式）。然后它掷骰子并打印结果。它还调用 Die 类提供的其他方法，例如显式设置和获取骰子当前点数的能力。

```java
//****************************** Author: Lewis/Loftus
// RollingDice.java
// Demonstrates the creation and use of a user-defined class.
//******************************

public class RollingDice
{

// Creates two Die objects and rolls them several times.
//-------------------------
public static void main (String[] args)
{
Die die1, die2;
int sum;
die1 = new Die();
die2 = new Die();
die1.roll();
die2.roll();
System.out.println ("Die One: " + die1 + ", Die Two: " + die2);
die1.roll();
die2.setFaceValue(4);
}
}
```

