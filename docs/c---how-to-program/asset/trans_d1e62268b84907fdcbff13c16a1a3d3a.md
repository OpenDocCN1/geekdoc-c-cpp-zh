
函数模板定义以关键字 template 开始（第 4 行），后面跟着用尖括号（< 和 >）括起来的函数模板的模板参数列表。模板参数列表中的每个参数（每个都称为形式类型参数）前面都有关键字 typename 或关键字 class（二者是同义词）。形式类型参数是基本类型或用户定义类型的占位符。这些占位符用于指定函数参数的类型（第 5 行）、指定函数的返回类型，以及在函数定义体内声明变量（第 7 行）。函数模板的定义方式与其他函数类似，但使用形式类型参数作为实际数据类型的占位符。

```cpp
// Fig. 15.12: maximum.h
// Function template maximum header file.

template < class T >  // or template< typename T >
T maximum( T value1, T value2, T value3 )
{
   T maximumValue = value1; // assume value1 is maximum

   // determine whether value2 is greater than maximumValue
   if ( value2 > maximumValue )
      maximumValue = value2;

   // determine whether value3 is greater than maximumValue
   if ( value3 > maximumValue )
      maximumValue = value3;

   return maximumValue;
}
```

**图 15.12** | *函数模板 maximum 头文件。*

图 15.12 中的函数模板声明了一个形式类型参数 T（第 4 行），作为函数 maximum 要测试的数据类型的占位符。对于特定的模板定义，类型参数的名称在模板参数列表中必须唯一。当编译器在程序源代码中检测到对 maximum 的调用时，传递给 maximum 的数据类型会在整个模板定义中替换 T，并且 C++ 会创建一个完整的源代码函数，用于确定指定数据类型的三个值中的最大值。然后编译新创建的函数。因此，模板是为一系列相似函数生成代码的手段。

> **常见编程错误 15.11**
> 
> *没有在函数模板的每个形式类型参数前放置关键字 class 或关键字 typename（例如，写成 `<class S, T>` 而不是 `<class S, class T>`）是语法错误。*

### 15.13.2 使用函数模板

图 15.13 使用 maximum 函数模板（第 18、28 和 38 行）来确定三个 int 值、三个 double 值和三个 char 值中的最大值。

```cpp
1 // Fig. 15.13: fig15_13.cpp
2 // Demonstrating function template maximum.
3 #include <iostream>
4 using namespace std;
5
6 #include "maximum.h" // include definition of function template maximum
7
8 int main()
9 {
10    // demonstrate maximum with int values
11    int int1, int2, int3;
12
13    cout << "Input three integer values: ";
14    cin >> int1 >> int2 >> int3;
15
16    // invoke int version of maximum
17    cout << "The maximum integer value is: "
18    << maximum( int1, int2, int3 );
19
20    // demonstrate maximum with double values
21    double double1, double2, double3;
22
23    cout << "\n\nInput three double values: ";
24    cin >> double1 >> double2 >> double3;
25
26    // invoke double version of maximum
27    cout << "The maximum double value is: "
28    << maximum( double1, double2, double3 );
29
30    // demonstrate maximum with char values
31    char char1, char2, char3;
32
33    cout << "\n\nInput three characters: ";
34    cin >> char1 >> char2 >> char3;
35
36    // invoke char version of maximum
37    cout << "The maximum character value is: "
38    << maximum( char1, char2, char3 ) << endl;
39 }
```

输入三个整数值：1 2 3
最大整数值为：3

输入三个双精度值：3.3 2.2 1.1
最大双精度值为：3.3

输入三个字符：A C B
最大字符值为：C

**图 15.13** | *演示函数模板 maximum。*

在图 15.13 中，第 18、28 和 38 行的调用分别创建了三个函数——分别期望三个 int 值、三个 double 值和三个 char 值。

例如，为 int 类型创建的函数模板特化会按如下方式将每次出现的 T 替换为 int：

```cpp
int maximum( int value1, int value2, int value3 )
{
    int maximumValue = value1; // assume value1 is maximum
    // determine whether value2 is greater than maximumValue
    if ( value2 > maximumValue )
        maximumValue = value2;
    // determine whether value3 is greater than maximumValue
    if ( value3 > maximumValue )
        maximumValue = value3;
    return maximumValue;
}
```

## 15.14 对象技术与 UML 简介

在本节中，我们讨论面向对象，这是一种思考世界和编写计算机程序的自然方式。这里的目标是帮助你培养面向对象的思维方式，并向你介绍统一建模语言™（UML™）——一种图形化语言，它允许设计面向对象软件系统的人使用行业标准表示法来表示这些系统。在这里，我们将首先回顾在 1.8 节中介绍的一些面向对象编程概念，然后介绍我们在 15.15 节以及第 16～23 章中使用的一些额外术语。

### 15.14.1 基本对象技术概念

在现实世界中，无论你看向哪里，都会看到对象——人、动物、植物、汽车、飞机、建筑物、计算机等等。人类以对象的方式思考。电话、房屋、交通信号灯、微波炉和饮水机只是我们每天在周围看到的另外几个对象。

### 属性和行为

对象有一些共同之处。它们都有属性（例如大小、形状、颜色和重量），并且都表现出行为（例如球会滚动、弹跳、充气和放气；婴儿会哭、睡觉、爬行、走路和眨眼；汽车会加速、刹车和转弯；毛巾会吸水）。人类通过研究现有对象的属性并观察它们的行为来了解这些对象。不同的对象可以具有相似的属性，并表现出相似的行为。例如，可以在婴儿与成人之间、人类与黑猩猩之间进行比较。我们将研究软件对象具有的属性和行为种类。

### 面向对象设计与继承

面向对象设计（OOD）用类似于人们描述现实世界对象的术语来为软件建模。它利用类关系，即某个类（例如车辆类）的对象具有相同的特征——汽车、卡车、红色小拖车和旱冰鞋有许多共同之处。OOD 利用继承关系，即通过吸收现有类的特征并添加自身独有的特征来派生新的对象类。类“convertible”（敞篷车）的对象

规范帮助 C++ 程序员确定这样一组类：从这些类创建出的对象协同工作以实现系统。

类之于对象，就像蓝图之于房屋——类是构建该类对象的“计划”。正如我们可以根据一张蓝图建造许多房屋，我们也可以从一个类实例化（创建）许多对象。你不能在蓝图的厨房里做饭；你可以在房屋的厨房里做饭。你不能在蓝图的卧室里睡觉；你可以在房屋的卧室里睡觉。

类可以与其他类建立关系。在银行的面向对象设计中，“银行柜员”类与“客户”类、“现金抽屉”类、“保险柜”类等其他类相关，等等。这些关系称为关联。将软件打包为类，使未来的软件系统能够重用这些类。

> **软件工程观察 15.11**
> 
> *在构建新类和程序时重用现有类可以节省时间、金钱和精力。重用还有助于构建更可靠、更有效的系统，因为现有类通常已经经过了大量测试、调试和性能调优。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_607_0.png)

确实，借助对象技术，你可以通过组合现有类来构建所需的许多新软件，就像汽车制造商组合可互换零件一样。你创建的每个新类都可以成为宝贵的软件资产，你和其他人可以重用它来加速并提高未来软件开发工作的质量。

### 15.14.3 面向对象分析与设计

很快你将用 C++ 编写更大的程序。你将如何为程序创建代码？也许，像许多初学者程序员一样，你只会打开计算机然后开始输入。这种方法对小型程序可能有效，但如果你被要求为一家大型银行创建一个控制数千台自动取款机的软件系统，那会怎样？或者，如果你被要求加入一个由 1000 名软件开发人员组成的团队，构建下一代美国空中交通管制系统，那又会怎样？对于如此庞大而复杂的项目，你不能只是坐下来就开始编写程序。

为了创建最佳解决方案，你应该遵循一个详细的过程来分析项目需求（即确定系统应该做*什么*），并开发满足这些需求的设计（即决定系统应该*如何*做）。理想情况下，在编写任何代码之前，你会经历这个过程并仔细审查设计（或让其他软件专业人员审查你的设计）。如果这个过程涉及从面向对象的角度分析和设计系统，那么它称为面向对象分析与设计（OOAD）。经验丰富的程序员知道，分析与设计可以帮助避免采用计划不周的系统开发方法（这种方法可能不得不在实现中途放弃，从而可能浪费大量时间、金钱和精力），从而节省许多小时。

OOAD 是分析问题并开发解决问题方法的这一过程的通用术语。像接下来几章讨论的那些小问题不需要详尽的 OOAD 过程。

随着问题以及解决它们的人群规模增大，OOAD 方法很快变得比伪代码更合适。理想情况下，一个团队应该就解决其问题的严格定义的过程以及统一的沟通方式达成一致
