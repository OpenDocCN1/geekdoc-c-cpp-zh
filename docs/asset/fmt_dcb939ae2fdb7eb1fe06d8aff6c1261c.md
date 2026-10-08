
如果 `Mammal` 有公共默认构造函数，这将是有效的。然而，并不是所有类都有公共默认构造函数（例如，记住只有在你没有写任何非默认构造函数时，编译器才会生成默认构造函数），在这种情况下，忘记调用基类构造函数会导致编译错误。

### 类的赋值

书中的之前的示例展示了如何使用类类型声明变量，以及如何使用 `new` 关键字创建对象。示例还说明了 C# 的类型检查规则如何防止你将一种类型的对象赋值给声明为不同类型的变量。例如，根据这里显示的 `Mammal`、`Horse` 和 `Whale` 类的定义，在这些定义之后的代码是非法的：

```cs
class Mammal
{
}
```

```cs
class Horse : Mammal
{
}
```

```cs
class Whale : Mammal
{
}
```
```cs
Horse myHorse = new Horse();
Whale myWhale = myHorse; // 错误 - 类型不同
```

然而，可以使用不同类型的变量引用对象，只要所使用的类型是继承层次结构较高的类。因此，以下语句是合法的：

```cs
Horse myHorse = new Horse();
Mammal myMammal = myHorse; // 合法，Mammal 是 Horse 的基类
```

从逻辑角度考虑，所有的马（`Horses`）都是哺乳动物（`Mammals`），因此你可以安全地将一个 `Horse` 类型的对象赋值给 `Mammal` 类型的变量。继承层次结构意味着你可以简单地将 `Horse` 看作一种特殊的 `Mammal`；它拥有 `Mammal` 的所有属性，并根据你为 `Horse` 类添加的任何方法和字段定义的额外属性。你也可以让 `Mammal` 变量指向一个鲸鱼（`Whale`）对象。然而，这里有一个重大的限制：当使用 `Mammal` 变量引用 `Horse` 或 `Whale` 对象时，你只能访问 `Mammal` 类定义的方法和字段。`Horse` 或 `Whale` 类定义的任何额外方法都无法通过 `Mammal` 类可见。

点击此处查看代码图像

```
Horse myHorse = new Horse(...);
Mammal myMammal = myHorse;
myMammal.Breathe(); // OK - Breathe 是 Mammal 类的一部分
myMammal.Trot(); // error - Trot 不是 Mammal 类的一部分
```

![](img/74dd8343b56b72576ea64f076a8146ee_406_0.png)

> 注意：前面的讨论解释了为什么你可以将任何内容赋值给对象变量作为 `System.Object` 的别名，并且所有类无论是直接还是间接地都继承自 `System.Object`。

请注意，反的情况并不成立。你不能无保留地将一个 `Mammal` 对象赋值给 `Horse` 变量：

点击此处查看代码图像

```
Mammal myMammal = new Mammal(...);
Horse myHorse = myMammal; // error
```

这看起来像是一个奇怪的限制，但请记住，并不是所有的 `Mammal` 对象都是 `Horse`——有些可能是鲸鱼。只要你首先检查该 `Mammal` 是否真的是 `Horse`，你就可以将 `Mammal` 对象赋值给 `Horse` 变量，你可以使用 `as` 运算符或使用类型转换（第 7 章“创建和管理类和对象”讨论了 `is` 和 `as` 运算符以及类型转换）。下面的代码示例使用了 `as` 运算符来检查 `myMammal` 是否指向 `Horse`，如果是，则赋值给 `myHorseAgain` 的结果是 `myHorseAgain` 指向同一个 `Horse` 对象。如果 `myMammal` 指向某种 `Mammal`，则 `as` 运算符返回 `null`。

点击此处查看代码图像

```
Horse myHorse = new Horse(...);
Mammal myMammal = myHorse; // myMammal 指向一个 Horse

myHorseAgain = myMammal as Horse; // OK - myMammal 是一个 Horse

Whale myWhale = new Whale(...);
myMammal = myWhale;

myHorseAgain = myMammal as Horse; // returns null - myMammal 是一个 Whale
```

### 定义新方法

计算机编程领域最困难的任务之一是为标识符思考独特且有意义名称。如果你正在为一个类定义方法，而该类是继承层次结构的一部分，迟早你都会重用一个层次结构中更上某个类已经在使用的名称。如果基类和派生类恰好声明了两个签名相同的方法，你将在编译应用程序时会收到一个警告。

> 注意：方法签名指的是方法的名称以及参数的数量和类型，但不包括其返回类型。两个具有相同名称且带有相同参数列表的方法具有相同的签名，即使它们返回不同的类型。

派生类中的方法会掩盖（或隐藏）基类中具有相同签名的方法。例如，如果你编译代码，编译器生成一个警告消息，通知你 `Horse.Talk` 隐藏了继承的方法 `Mammal.Talk`：

点击此处查看代码图像

```cs
class Mammal
{
  ...
  public void Talk() // 假设所有哺乳动物都会说话
  {
    ..
  }
}
```

```cs
class Horse : Mammal
{
  public void Talk() // 马的说话方式与其他哺乳动物不同
}
```

### 多态示例

```cs
return "This is a mammal";
}
class Horse : Mammal {
    ...
    public override string GetTypeName() {
        return "This is a horse";
    }
}
class Whale : Mammal {
    ...
    public override string GetTypeName() {
        return "This is a whale";
    }
}
class Aardvark : Mammal {
    ...
}
```

你需要注意两点：首先是 `Horse` 和 `Whale` 类中 `GetTypeName` 方法使用的 `override` 关键字；其次是 `Aardvark` 类没有定义 `GetTypeName` 方法。

现在请检查以下代码块：

点击此处查看图像

```cs
Mammal myMammal;
myHorse = new Horse(...);
myWhale = new Whale(...);
Aardvark myAardvark = new Aardvark(...);
```

点击此处查看代码图像

```cs
myMammal = myHorse;
Console.WriteLine(myMammal.GetTypeName()); // Horse
myMammal = myWhale;
Console.WriteLine(myMammal.GetTypeName()); // Whale
myMammal = myAardvark;
Console.WriteLine(myMammal.GetTypeName()); // Aardvark
```

这三个不同的 `Console.WriteLine` 语句将输出什么？初一看，你认为它们都会打印“This is a mammal”，因为每条语句都对 `myMammal` 变量调用了 `GetTypeName` 方法，而它是一个 `Mammal`。然而，在第一种情况下，你可以看到 `myMammal` 实际上是指向 `Horse` 的引用。（记住，允许将 `Horse` 赋值给 `Mammal` 变量，因为 `Horse` 类继承自 `Mammal` 类。）由于 `GetTypeName` 方法被定义为 `virtual`，运行时会确定应该调用 `Horse.GetTypeName` 方法，因此该语句实际上打印了消息“This is a horse”。同样的逻辑也适用于第二个 `Console.WriteLine` 语句，它输出消息“This is a whale”。第三条语句对 `Aardvark` 对象调用了 `Console.WriteLine`。然而，`Aardvark` 类没有 `GetTypeName` 方法，因此调用了 `Mammal` 类中的默认方法，返回字符串“This is a mammal”。

这种根据语句的上下文调用不同方法的现象被称为**多态**（`polymorphism`），字面上的意思是“许多形式”。

### 理解受保护访问

`public` 和 `private` 访问关键字创建了访问权限的两个极端：类的公有字段和方法对所有人可见，而类的私有字段和方法仅对类本身可见。

当你孤立考虑类时，这两个极端就足够了。然而，正如所有经验丰富的面向对象程序员所知，孤立的类无法解决复杂问题。继承是连接类的强大方式，派生类与其基类之间存在着特殊且紧密的关系。通常，基类允许派生类访问其某些成员，同时不对属于继承层次结构的类隐藏这些成员是非常有用的。在这种情况下，你可以用 `protected` 关键字标记成员。其工作原理如下：

- 如果类 `A` 自另一个类 `B`，它可以访问 `B` 的 `protected` 类成员。也就是说，在派生类 `A` 内部，`B` 的 `protected` 成员实际上是公开的。
- 如果类 `A` 不派自另一个类 `B`，它无法访问 `B` 的任何 `protected` 成员。因此，在类 `A` 内部，`B` 的 `protected` 成员实际上是私有的。

C# 允许程序员完全自由地将方法和字段声明为 `protected`。然而，大多数面向对象编程指南建议尽可能将字段严格保持为 `private`，仅在必要时放宽限制。`public` 字段违反了封装，因为类的所有用户都对字段有直接、无限制的访问。`protected` 字段为类的用户维护了封装，因为这些用户无法访问受保护的字段。然而，`protected` 字段仍然允许继承自基类的其他类破坏封装。

> 注意：你不仅可以在派生类中访问受保护的基类成员，也可以在派自派生类的类中访问。

在接下来的练习中，你将为不同类型的车辆定义一个简单的类层次结构。你将定义一个名为 `Vehicle` 的基类以及名为 `Airplane` 和 `Car` 的派生类。你将在 `Vehicle` 类中定义名为 `StartEngine` 和 `StopEngine` 的通用方法，并在两个派生类中添加一些特定于这些类的方法。最后，你将在 `Vehicle` 类中添加一个名为 `Drive` 的虚方法，并在两个派生类中覆盖该方法的默认实现。

## 创建类层次结构

- 1. 如果尚未运行，请启动 `Microsoft Visual Studio 2017`。
