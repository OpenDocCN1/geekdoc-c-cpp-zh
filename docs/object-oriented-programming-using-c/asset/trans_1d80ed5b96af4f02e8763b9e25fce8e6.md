

# 使用 C# 进行面向对象编程

# 面向对象的软件分析与设计

CRC 代表类（Class）、职责（Responsibilities）和协作（Collaborations）。下面是一个 CRC 卡片，它由三个部分组成，左侧显示类的职责，右侧显示协作关系。

| 类名 | 类职责 | 类协作 |
| :--- | :--- | :--- |

职责是该类需要了解的信息（即属性）以及它应该执行的操作（方法），尽管在 CRC 卡片上，这些并没有像在 UML 图中那样被精确定义。协作是指该类为了履行其职责必须与之工作的的其他类。

下图显示了为系统中的两个类开发的 CRC 卡片。

| 类名 | 类职责 | 类协作 |
| :--- | :--- | :--- |
| 业余爱好者 (Amateur) | 了解跑步者的详细信息（编号等） | 赞助表 (SponsorshipForm) |
| | 记录赞助信息 | |
| | 记录完赛时间 | | |

| 类名 | 类职责 | 类协作 |
| :--- | :--- | :--- |
| 赞助表 (SponsorshipForm) | 记录赞助商列表及相关金额 | |
| | 向此列表添加赞助详情 | |
| | 打印待收集金额列表 | |

# 使用 C# 进行面向对象编程

# 面向对象的软件分析与设计

开发出 CRC 卡片后，我们可以通过角色扮演一系列场景来检查系统运行是否正常。这样我们可以在进入耗时的编程流程并编写缺陷计划之前，先修改设计。

一个示例场景是跑步者获得了额外的赞助。在这种情况下，通过查看上面的 CRC 卡片，跑步者能够与 `SponsorshipForm` 类协作记录赞助信息。`SponsorshipForm` 类拥有赞助商列表，并可以向该列表添加额外的赞助商。因此，设计的某似乎是有效的。

测试各种场景可能会突出我们系统设计中的缺陷，然后我们可以修复这些缺陷——这在浪费时间编写设计方案之前就可以完成了。

## 6.11 细化类

在确定了系统设计中的类并使用 CRC 卡片对其进行记录和测试之后，我们现在可以细化 CRC 卡片，并使用 UML 类图记录我们的类。为了做到这一点，我们需要通过 CRC 卡片记录的通用规范，并解决任何歧义，例如精确的类型。

细化 CRC 卡片后，我们现在可以为提议的设计绘制类图（见下）：

![](img/e143b38d00f95425fa4f3efca0527189_124_0.png)

![](img/e143b38d00f95425fa4f3efca0527189_125_0.png)

![](img/e143b38d00f95425fa4f3efca0527189_125_1.png)

![](img/e143b38d00f95425fa4f3efca0527189_125_2.png)

![](img/e143b38d00f95425fa4f3efca0527189_125_3.png)

![](img/e143b38d00f95425fa4f3efca0527189_125_4.png)

## 6.12 总结

收集用户需求是软件工程过程中的一个重要阶段（但在本文的范围之外）。

将复杂的需求规范转换为优雅、简单的面向对象架构设计是一项需要经验的熟练任务。然而，一个良好的起点是遵循本章介绍的简单流程。

通过一系列任务，我们看到了如何分析对问题的文本描述。我们：

- 寻找了描述中超出系统范围的方面
- 识别了描述中用不同词汇指代同义项的地方
- 使用名词和动词来识别潜在的类、属性和方法
- 查看了类以识别潜在的继承层次结构以及类之间的其他关系（例如关联）
- 使用 CRC 卡片记录生成的类，并通过角色扮演一系列场景来测试设计的有效性，并根据情况修改了我们的设计
- 最后，我们可以细化这些细节并使用类图记录结果。

本章介绍的设计过程将在第 11 章描述的案例中再次详细演示。

![](img/e143b38d00f95425fa4f3efca0527189_126_0.png)

# 7 通用集合以及如何序列化它们

### 引言

本章将首先向读者介绍泛型方法，然后介绍 .NET 框架中的一个重要部分：实现泛型集合的类。最后，将引入序列化的概念，并展示如何对不同的集合进行序列化，因为这是一个非常常见的任务。

### 目标

在本章结束时，你将能够……

- 理解泛型方法的概念
- 理解集合的概念以及不同类型的集合
- 理解序列化的概念以及如何序列化不同的集合

本章由十二部分组成：

1) 泛型方法简介
2) 集合简介
3) 不同类型的集合
4) 列表 (Lists)
5) 哈希集合 (HashSets)
6) 字典 (Dictionaries)
7) 简单的列表示例
8) 使用列表的更真实的示例
9) 使用集合（Sets）的示例
10) 使用字典（Dictionaries）的示例
11) 集合的序列化与反序列化
12) 总结

## 7.1 泛型方法简介

我们之前已经见过运行时是如何根据方法的签名（signature）来识别方法的，即方法的名称和方法所接受的参数列表。

因此，我们可以有两个同名的方法。下面显示了两个寻找最大值的方法……一个是在两个整数中寻找最大值，另一个是在双浮点数中寻找最大值。

```csharp
static public int Highest(int o1, int o2)
{
    if (o1 > o2)
        return o1;
    else
        return o2;
}
static public double Highest(double o1, double o2)
{
    if (o1 > o2)
        return o1;
    else
        return o2;
}
```

给定以下代码，CLR 引擎将调用第一个方法，因为它是根据名称和参数类型来识别方法的。

```csharp
int n1 = 1;
int n2 = 2;
Console.WriteLine("The highest is " + Highest(n1, n2));

double n3 = 1.1;
double n4 = 2.2;
Console.WriteLine("The highest is " + Highest(n3, n4));
```

给定以下 `Student` 类的定义……

```csharp
class Student
{
    String name;
    public Student(String name)
    {
        this.name = name;
    }
    override public string ToString()
    {
        return name;
    }
}
```

我们可以定义这种方法来寻找最大的学生（按字母顺序）。

```csharp
static public Student Highest(Student o1, Student o2)
{
    if (o1.ToString().CompareTo(o2.ToString()) > 0)
        return o1;
    else
        return o2;
}
```

并使用它进行调用……

```csharp
Student s1 = new Student("Alan");
Student s2 = new Student("Clare");
Console.WriteLine("The highest is " + Highest(s1, s2));
```

通过这样做，我们创建了三个功能相同但类型不同的方法。这让我们想到，如果我们能创建一个适用于任何类型的方法就好了。

下面的方法是对此的第一次尝试：

```csharp
static public Object Highest(Object o1, Object o2)
{
    if (o1.ToString().CompareTo(o2.ToString()) > 0)
        return o1;
    else
        return o2;
}
```

该方法接受两个 `Object` 作为参数。`Object` 是所有类的基类，因此该方法可以接受任何更具体类型的两个对象并将它们视为基类型 `Object`。这就是多态。

上面的方法将这两个 `Object` 转换为字符串并比较这些字符串。

因此，可以使用以下代码调用三次方法……

```csharp
int n1 = 1;
int n2 = 2;
Console.WriteLine("The highest is " + Highest(n1, n2));

double n3 = 1.1;
double n4 = 2.2;
Console.WriteLine("The highest is " + Highest(n3, n4));

Student s1 = new Student("Student A");
Student s2 = new Student("Student B");
Console.WriteLine("The highest is " + Highest(s1, s2));
```

