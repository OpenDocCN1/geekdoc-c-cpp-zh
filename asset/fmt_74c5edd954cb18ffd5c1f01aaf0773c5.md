
Click here to view code image

```
Console.WriteLine(Util.Sum(2, 4, 6, 8, 10));
```

+   12. 在“调试”菜单上，单击“不调试启动”以生成并运行应用程序。

应用程序运行时，显示以下消息：

```
Using parameter list
30
```

这次，提供的参数多于接受可选参数的方法所指定的，因此编译器生成了调用接受参数数组的方法的代码。

+   13. 按 Enter 并返回 Visual Studio。

### 摘要

在本章中，你学习了如何使用 `params` 数组定义可以接受任意数量参数的方法。你还看到了如何使用 `object` 类型的 `params` 数组创建可以接受任意数量任意类型参数的方法。此外，你还看到了编译器在需要在调用接受参数数组的方法和接受可选参数的方法之间进行选择时如何解析方法调用。

+   如果你想继续下一章，保持 Visual Studio 2015 运行并转到第 12 章“使用继承工作”。

+   如果你现在想退出 Visual Studio 2015，在“文件”菜单上单击“退出”。如果看到“保存”对话框，单击“是”并保存项目。

### 快速参考

| 要 | 执行此操作 |
|---|---|
| 编写接受任意数量给定类型参数的方法 | 编写参数为给定类型的 `params` 数组的方法。例如，接受任意数量 `bool` 参数的方法是这样声明的：

```
someType Method(params bool[] flags)
{
    ...
}
``` |
| 编写接受任意数量任意类型参数的方法 | 编写参数为元素类型为 `object` 的 `params` 数组的方法。例如：

```
someType Method(params object[] paramList)
{
    ...
}
``` |

## 第12章 使用继承

完成本章后，你将能够：

- 创建一个从基类继承特性的派生类。
- 通过使用 `new`、`virtual` 和 `override` 关键字控制方法的隐藏和重写。
- 通过使用 `protected` 关键字限制继承层次结构中的访问权限。
- 将扩展方法定义为使用继承的替代机制。

继承是面向对象编程世界中的一个关键概念。你可以使用继承作为一种工具，避免在定义具有许多共同特性的不同类时重复编写代码，并且这些类之间明显相关。也许它们是同一类型的不同类，每个类都有其独特的特征——例如，工厂的 `经理`、`体力劳动者` 和 `所有员工`。如果你要编写一个模拟工厂的应用程序，你将如何指定经理和体力劳动者具有许多相同的特征，但也具有不同的特征？例如，他们都有员工编号，但经理的职责不同，执行的任务也与体力劳动者不同。

这就是继承发挥作用的地方。

### 什么是继承？

如果你询问几位经验丰富的程序员 `inheritance` 这个术语的含义，你通常会得到不同且相互矛盾的答案。部分混淆源于单词 inheritance 本身有几种细微不同的含义。如果有人在遗嘱中将某物传给你，你就说你继承了它。同样，我们说你从母亲那里继承了半数基因，从父亲那里继承了半数基因。这两种用法与编程中的继承关系不大。

编程中的继承完全是关于分类的——它是类之间的关系。例如，当你在学校时，你可能学习过哺乳动物，并且你了解到马和鲸是哺乳动物的例子。它们各自具有哺乳动物所具有的每个属性（它呼吸空气，它哺乳幼崽，它是恒温的，等等），但每个也都有其独特的特征（一匹马有蹄子，但鲸有鳍和尾鳍）。

如何在程序中建模马和鲸？一种方法是创建两个分别名为 `Horse` 和 `Whale` 的不同类。每个类可以以自己的方式实现该类型哺乳动物特有的行为，例如 `Trot`（马）或 `Swim`（鲸）。但如何处理马和鲸共有的行为，例如 `Breathe` 或 `SuckleYoung`？你可以向两个类都添加名称相同的重复方法，但如果随后你还决定开始建模其他类型的哺乳动物，例如 `Human` 和 `Aardvark`，这种情况就会成为维护的噩梦。

在 C# 中，你可以使用类继承来解决这些问题。马、鲸、人和土豚都是哺乳动物类型，因此你可以创建一个名为 `Mammal` 的类，提供这些类型所表现的通用功能。然后你可以声明 `Horse`、`Whale`、`Human` 和 `Aardvark` 类都继承自 `Mammal`。这些类随后自动包含 `Mammal` 类的功能（`Breathe`、`SuckleYoung` 等），但你也可以为每个类增加特定哺乳动物类型特有的功能——`Horse` 类的 `Trot` 方法和 `Whale` 类的 `Swim` 方法。如果你需要修改 `Breathe` 等通用方法的工作方式，你只需在一个地方更改，即 `Mammal` 类。

### 使用继承

你通过使用以下语法声明一个类继承自另一个类：

Click here to view code image

```
class DerivedClass : BaseClass
{
    ...
}
```

派生类继承自基类，基类中的方法成为派生类的一部分。在 C# 中，一个类最多只能从一个基类派生；一个类 *不允许* 从两个或多个类派生。但是，除非 `DerivedClass` 被声明为 `sealed`，你可以使用相同的语法派生其他继承自 `DerivedClass` 的类。（你将在第13章“创建接口和定义抽象类”中学习密封类。）

Click here to view code image

```
class DerivedSubClass : DerivedClass
{
    ...
}
```

继续前面描述的示例，你可以按如下方式声明 `Mammal` 类。方法 `Breathe` 和 `SuckleYoung` 对所有哺乳动物都是共通的。

```
class Mammal
{
    public void Breathe()
    {
        ...
    }

public void SuckleYoung()
{
    ...
}
...
}
```

然后你可以为每种不同的哺乳动物类型定义类，根据需要添加更多方法，如以下示例所示：

```
class Horse : Mammal
{
    ...
    public void Trot()
    {
        ...
    }
}
```

```
class Whale : Mammal
{
    ...
    public void Swim()
    {
        ...
    }
}
```

### Note

如果你是 C++ 程序员，你会注意到你不能也不需要显式指定继承是 public、私有还是 protected。C# 继承始终隐式为 public。如果你熟悉 Java，请注意冒号的使用，并且没有 extends 关键字。

如果你在应用程序中创建一个 `Horse` 对象，你可以调用 `Trot`、`Breathe` 和 `SuckleYoung` 方法：

```
Horse myHorse = new Horse();
myHorse.Trot();
myHorse.Breathe();
myHorse.SuckleYoung();
```

同样，你可以创建一个 `Whale` 对象，但这次你可以调用 `Swim`、`Breathe` 和 `SuckleYoung` 方法；`Trot` 不可用，因为它仅在 `Horse` 类中定义。

### Important

继承仅适用于类，不适用于结构。你不能使用结构定义自己的继承层次结构，也不能定义派生自类或另一个结构的结构。

所有结构实际上都继承自一个名为 `System.ValueType` 的抽象类。（第13章探讨抽象类。）这纯粹是 Microsoft .NET Framework 定义栈式值类型的通用行为方式的实现细节；你不太可能在自己的应用程序中直接使用 `ValueType`。

### 重新审视 System.Object 类

`System.Object` 类是所有类的根类。所有类都隐式派生自 `System.Object`。因此，C# 编译器会静默地将 `Mammal` 类重写为以下代码（如果你真的想，也可以显式编写）：

```
class Mammal : System.Object
{
    ...
}
```

`System.Object` 类中的任何方法都会自动沿继承链传递给派生自 `Mammal` 的类，例如 `Horse` 和 `Whale`。从实际角度来看，这意味着你定义的所有类都自动继承 `System.Object` 类的所有特性。这包括诸如 `ToString`（在第2章“使用变量、运算符和表达式”中讨论）等方法，用于将对象转换为字符串，通常用于显示目的。

### 调用基类构造函数

除了继承的方法外，派生类自动包含基类中的所有字段。这些字段通常需要在创建对象时进行初始化。你通常在构造函数中执行这种初始化。请记住，所有类至少有一个构造函数。（如果你不提供，编译器会为你生成一个默认构造函数。）

派生类中的构造函数调用其基类的构造函数作为初始化的一部分是良好的实践，这使基类构造函数能够执行其所需的任何额外初始化。你可以在为继承类定义构造函数时指定 `base` 关键字来调用基类构造函数，如此示例所示：

Click here to view code image

```
class Mammal // base class
{
    public Mammal(string name)  // constructor for base class
    {
        ...
    }
    ...
}

class Horse : Mammal // derived class
{
    public Horse(string name)
        : base(name) // calls Mammal(name)
    {
        ...
    }
    ...
}
```

如果你没有在派生类构造函数中显式调用基类构造函数，编译器会尝试在执行派生类构造函数中的代码之前静默插入对基类默认构造函数的调用。以之前的示例为例，编译器会将此

```
class Horse : Mammal
{
    public Horse(string name)
    {
        ...
    }
    ...
}
```

重写为此：

```
class Horse : Mammal
{
    public Horse(string name)
        : base()
    {
        ...
    }
    ...
}
```

如果 `Mammal` 有一个公共默认构造函数，这就可以工作。然而，并非所有类都有公共默认构造函数（例如，请记住只有当你不编写任何非默认构造函数时，编译器才会生成默认构造函数），在这种情况下，忘记调用正确的基类构造函数会导致编译时错误。

### 分配类

本书之前的示例展示了如何使用类声明变量

type and how to use the new keyword to create an object. There are also examples of how the type-checking rules of C# prevent you from assigning an object of one type to a variable declared as a different type. For example, given the definitions of the `Mammal`, `Horse`, and `Whale` classes shown here, the code that follows these definitions is illegal:

Click here to view code image

```
class Mammal
{
    ...
}
class Horse : Mammal
{
    ...
}
class Whale : Mammal
{
    ...
}
...
Horse myHorse = new Horse(...);
Whale myWhale = myHorse;            // error - different types
```

However, it is possible to refer to an object from a variable of a different type as long as the type used is a class that is higher up the inheritance hierarchy. So the following statements are legal:

Click here to view code image

```
Horse myHorse = new Horse(...);
Mammal myMammal = myHorse; // legal, Mammal is the base class of Horse
```

If you think about it in logical terms, all Horses are Mammals, so you can safely assign an object of type `Horse` to a variable of type `Mammal`. The inheritance hierarchy means that you can think of a `Horse` simply as a special type of `Mammal`; it has everything that a `Mammal` has with a few extra bits defined by any methods and fields you added to the `Horse` class. You can also make a `Mammal` variable refer to a `Whale` object. There is one significant limitation, however: When referring to a `Horse` or `Whale` object by using a `Mammal` variable, you can access only methods and fields that are defined by the `Mammal` class. Any additional methods defined by the `Horse` or `Whale` class are not visible through the `Mammal` class.

Click here to view code image

```
Horse myHorse = new Horse(...);
Mammal myMammal = myHorse;
myMammal.Breathe();            // OK - Breathe is part of the Mammal class
myMammal.Trot();             // error - Trot is not part of the Mammal class
```

## Note

The preceding discussion explains why you can assign almost anything to an object variable. Remember that object is an alias for `System.Object`, and all classes inherit from `System.Object`, either directly or indirectly.

Be warned that the converse situation is not true. You cannot unreservedly assign a `Mammal` object to a `Horse` variable:

Click here to view code image

```
Mammal myMammal = new Mammal(...);
Horse myHorse = myMammal;  // error
```

This looks like a strange restriction, but remember that not all `Mammal` objects are Horses—some might be Whales. You can assign a `Mammal` object to a `Horse` variable as long as you first check that the `Mammal` is really a `Horse`, by using the `as` or `is` operator or by using a cast (Chapter 7, “Creating and managing classes and objects” discusses the `is` and `as` operators and casts). The code example that follows uses the `as` operator to check that `myMammal` refers to a `Horse`, and if it does, the assignment to `myHorseAgain` results in `myHorseAgain` referring to the same `Horse` object. If `myMammal` refers to some other type of `Mammal`, the `as` operator returns null instead.

Click here to view code image
