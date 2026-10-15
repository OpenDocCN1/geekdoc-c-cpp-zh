

# LISTING 4.1 continued

```
System.out.println("Die One: " + die1 + ", Die Two: " + die2);
sum = die1.getFaceValue() + die2.getFaceValue();
System.out.println("Sum: " + sum);
sum = die1.roll() + die2.roll();
System.out.println("Die One: " + die1 + ", Die Two: " + die2);
System.out.println("New sum: " + sum);
}
```

- Die One: 5, Die Two: 2
- Die One: 1, Die Two: 4
- Sum: 5
- Die One: 4, Die Two: 2
- New sum: 6

本示例与之前示例的主要区别在于，Die 类并不是 Java 类库预定义的一部分。我们必须自己编写 Die 类，定义 Die 对象要执行的功能，否则该程序无法编译和运行。

每个类都可以包含数据声明和方法声明，如图 4.2 所示。数据声明表示将存储在该类的每个对象中的数据。方法声明定义了这些对象将提供的服务。综合起来，类的成员就是类的数据和方法。

我们在之前示例中编写的类也遵循此模型，但它们在类级别不包含任何数据，并且只包含一个方法（main 方法）。我们将继续定义此类类，例如 RollingDice 类，以定义程序的起点。

真正的面向对象编程，则来自于定义代表具有明确状态和行为的对象的类。例如，在任何给定时刻，Die 对象都显示特定的点数，我们可以将其称为骰子的状态。Die 对象还具有我们可以调用的各种方法，例如掷骰子或获取其点数的能力。这些方法代表了骰子的行为。

> 面向对象编程的核心是定义代表具有明确状态和行为的对象的类。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_191_0.png)

## FIGURE 4.2 The members of a class: data and method declarations

Die 类如清单 4.2 所示。它包含两个数据值：一个整数常量（MAX）表示骰子的最大点数，以及一个整数变量（faceValue）表示骰子的当前点数。它还包含一个名为 Die 的构造函数和四个普通方法：roll、setFaceValue、getFaceValue 和 toString。

你会记得在第 2 章和第 3 章中，构造函数是名称与类相同的特殊方法。当使用 new 操作符创建 Die 类的新实例时，会调用 Die 构造函数。Die 类中其余的方法定义了 Die 对象提供的各种服务。

我们使用文档头块来解释类中每个方法的用途。这种做法不仅对任何试图理解软件的人至关重要，而且还在视觉上将代码分隔开，使得在阅读代码时眼睛可以轻松地从一个方法跳到下一个方法。

图 4.3 列出了 Die 类的方法。从这个角度来看，它与我们在之前示例中使用的任何其他类看起来都不同。唯一重要的区别是，Die 类不是由 Java 标准类库为我们提供的。我们自己编写了它。

Die 类的方法包括掷骰子的能力，产生新的随机点数。roll 方法将新的点数返回给调用方法，但你也可以随时使用 getFaceValue 方法获取当前点数。setFaceValue 方法显式设置点数，就好像你伸手过去把骰子转到你想要的点数一样。任何对象的 toString 方法在你将对象传递给 print 或 println 方法以获取对象的字符串描述时都会自动调用

VideoNote
Dissecting the Die class.

## LISTING 4.2

```
//************************************************************************
// Die.java      Author: Lewis/Loftus
//
// Represents one die (singular of dice) with faces showing values
// between 1 and 6.
//************************************************************************

public class Die
{
    private final int MAX = 6;  // maximum face value

    private int faceValue;  // current value showing on the die

    //-------------------------------------------------------------
    // Constructor: Sets the initial face value.
    //-------------------------------------------------------------
    public Die()
    {
        faceValue = 1;
    }

    //-------------------------------------------------------------
    // Rolls the die and returns the result.
    //-------------------------------------------------------------
    public int roll()
    {
        faceValue = (int)(Math.random() * MAX) + 1;

        return faceValue;
    }

    //-------------------------------------------------------------
    // Face value mutator.
    //-------------------------------------------------------------
    public void setFaceValue (int value)
    {
        faceValue = value;
    }

    //-------------------------------------------------------------
    // Face value accessor.
    //-------------------------------------------------------------
    public int getFaceValue()
```

## Instance Data

请注意，在 Die 类中，常量 MAX 和变量 faceValue 是在类内部声明的，但不在任何方法内部。变量的声明位置定义了其作用域，即该变量可以在程序中引用的区域。通过在类级别声明（而不是在方法内部），这些变量和常量可以在类的任何方法中引用。

faceValue 变量等属性被称为实例数据，因为每次创建该类的实例时都会为该变量保留新的内存空间。每个 Die 对象都有自己的 faceValue 变量和自己的数据空间。这就是每个 Die 对象可以拥有自己的状态的原因。我们在 RollingDice 程序的输出中看到了这一点：一个骰子的点数为 5，另一个骰子的点数为 2。只有当为每个 Die 对象创建 faceValue 变量的内存空间时，这才有可能。

> KEY CONCEPT
> 变量的作用域决定了它可以被引用的位置，这取决于它声明的位置。

我们可以将这种情况描述如下：

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_194_0.png)

die1 和 die2 引用变量指向（即包含地址）它们各自的 Die 对象。每个对象都包含一个具有自己内存空间的 faceValue 变量。因此每个对象可以为其实例数据存储不同的值。

Java 会自动初始化在类级别声明的任何变量。例如，所有 int 和 double 等数值类型的变量都初始化为零。然而，尽管语言执行这种自动初始化，但最好显式初始化变量（通常在构造函数中），以便阅读代码的任何人都能清楚地理解其意图。

## UML Class Diagrams

在本书中，我们使用 UML 图来可视化类和对象之间的关系。UML 代表统一建模语言，已成为表示面向对象程序设计的流行记法。

存在几种类型的 UML 图，每种都旨在显示面向对象程序的特定方面。我们在本书中主要关注 UML 类图，以显示类的内容及其之间的关系。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_195_0.png)

> **KEY CONCEPT**
> 
> UML 类图帮助我们可视化程序中类的内容及其之间的关系。

在 UML 图中，每个类都表示为一个矩形，可能包含三个部分以显示类名、其属性（数据）和其操作（方法）。图 4.4 显示了包含 RollingDice 程序的类的类图。

图 4.4 中连接 RollingDice 和 Die 类的箭头表示类之间存在关系。虚线箭头表示一个类 *使用* 另一个类的方法。其他类型的面向对象类之间的关系使用不同类型的连线和箭头表示。我们将在本书中探讨相关主题时讨论这些其他关系。

请记住，UML 并非专门为 Java 程序员设计。它旨在语言独立。因此，UML 图中使用的语法不一定与 Java 相同。例如，变量的类型显示在变量名之后，用冒号分隔。方法的返回类型以相同的方式显示。

UML 图非常灵活。我们可以根据特定图的<|message|> 包含所需的相关信息。例如，如果这些细节对特定图不相关，我们可以省略类的<|message|> 和方法部分。

UML 图允许你可视化程序的设计。随着我们的程序变得更大，由越来越多的类组成，这些可视化变得越来越有帮助。我们将根据情况需要探索 UML 图的新方面。

**SELF-REVIEW QUESTIONS** *(see answers in Appendix N)*

- **SR 4.5** 什么是对象与类的区别？
- **SR 4.6** 描述 Die 类的实例数据。
- **SR 4.7** 为 Die 类定义的方法中，哪些可以改变 Die 对象的状态——即哪些方法为实例数据赋值？

