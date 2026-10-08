

```csharp
override public void Withdraw(decimal withdrawal)
{
    Console.WriteLine("invokes SavingsAccount.Withdrawal()");
}
public class SpecialSaleAccount : SavingsAccount // 哎！
{
    override public void Withdraw(decimal withdrawal)
    {
        Console.WriteLine("invokes SpecialSaleAccount.Withdrawal()");
    }
}
```

这段代码会产生以下编译器错误：

```
'SpecialSaleAccount': cannot inherit from sealed class 'SavingsAccount'
```

你使用 `sealed` 关键字来保护你的类免受子类的窥探方法。例如，允许程序员扩展一个实现系统安全的类，可能会导致某人创建一个安全后门。

密封一个类可以防止另一个程序（可能在互联网的某个地方）使用你类的修改版本。远程程序可以原样使用该类，也可以不使用，但它不能在继承你类的部分内容的同时覆盖其他部分。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_356_0.png)

# 第 8 章：与接口交互

**本章内容**

- 超越 IS_A 和 HAS_A：C# 接口
- 创建你自己的接口或使用 .NET 提供的接口
- 使用接口统一不同的类层次结构
- 在接口后隐藏类类的公共接口的一部分
- 管理软件变更 —— 通过接口实现灵活性

一个类可以包含对另一个类的引用；这个陈述描述了简单的 HAS_A 关系。一个类可以通过继承的魔力扩展另一个类——这就是 IS-A 关系。C# 接口实现了另一种非常重要的关联：CAN_BE_USED_AS（可以被用作）关系。

本章将介绍 C# 接口，并展示了它们增加面向对象编程力量和灵活性的众多方法。

## 介绍 CAN_BE_USED_AS

如果你想记记笔记，可以用笔随写，可以在智能手机上输入，也可以在笔记本电脑的键盘上敲击。你可以相当地说，这三个对象——笔、智能手机和电脑——都实现了 `TakeNote` 操作。假设你利用继承的魔法在 C# 中实现这一概念。

```csharp
abstract class ThingsThatRecord // 基类
{
    abstract public void TakeNote(string note);
}
public class Pen : ThingsThatRecord // 子类
{
    override public void TakeNote(string note)
    // ... 用笔随手记笔记 ...
}
```

```csharp
public class PDA : ThingsThatRecord // 另一个子类
{
    override public void TakeNote(string note)
    // 在 PDA 上划写笔记 ...
}
public class LapTop : ThingsThatRecord // 第三个子类
{
    override public void TakeNote(string note)
    // 击、击、击 ...
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_359_0.png)

如果你对 `abstract` 一词感到困惑，请参阅本迷你书的第 7 章并阅读该章的讨论。如果整个继承概念是一个谜团，请查看本迷你书的第 6 章。

下面的简单方法展示了继承方法运行良好：

```csharp
void RecordTask(ThingsThatRecord recorder) // 参数类型是基类。
{
    // 所有扩展 ThingsThatRecord 的类都有 TakeNote 方法。
    recorder.TakeNote("Shopping list");
    // 等等。
}
```

参数类型是 `ThingsThatRecord`，所以你可以将任何子类传递给此方法，使得该方法非常通用。

这似乎是一个好主意，但它有两个缺点：

- 一个根本性问题：笔、PDA 和笔记本电脑真的有 IS-A 关系吗？这三个物品在现实生活中是同一种类型吗？我不认为，你呢？我只能说 `ThingsThatRecord` 是一个糟糕的基类。
- 一个纯技术性问题：你可以合理地将 `LapTop` 和 `PDA` 都派生为 `Computer` 的子类。但没有人会说笔 IS-A 电脑。你可以将笔描述为一种机械书写设备或会弄脏你衣服的设备。但一个 C# 类不能同时继承两个基类——一个 C# 类只能是一种类型的物品。

所以，笔、PDA 和笔记本电脑的共同点仅在于它们都是 CAN_BE_USED_AS 记录设备。继承并不适用于这里。

## 了解接口是什么

C# 中的接口类似于一个没有数据成员且没有抽象方法的类，几乎像一个抽象类——几乎是：

```csharp
interface IRecordable
{
    void TakeNote(string note);
}
```

接口以 `interface` 关键字开头。它除了抽象方法外一无一物。它没有数据成员，也没有实现的方法。

接口可以包含一些其他特征，包括属性（本迷你书的第 5 章介绍）、事件（本迷你书的第 9 章介绍）和索引器（在第一本书末尾介绍）。

C# 接口无法展示的元素中包括：

- 访问修饰符，如 `public` 或 `private`（参见本迷你书的第 5 章）
- `virtual`、`override` 或 `abstract` 关键字（本迷你书的第 7 章）
- 数据成员（参见本迷你书的第 2 章）
- 实现的方法

C# 接口的所有成员都是 `public`（你甚至无法在定义方法时访问修饰符），且接口本身可以是 `public`、`internal` 或 `private`。

与抽象类不同，C# 接口不是一个类。它不包含方法体。

## 如何实现接口

要使用 C# 接口，请在一个或多个类中实现它。类头部所示：

```csharp
class Pen : IRecordable // 看起来像继承，但不是
```

接口规定实现接口的类必须提供实现。例如，任何实现 `IRecable` 的类必须提供 `TakeNote` 的实现。

```csharp
class Pen : IRecordable
{
    public void TakeNote(string note) // 接口方法必须是 public
    {
        // 用笔记录 ...
    }
}
```

这个示例满足了两个要求：注意类实现了 `IRecable`，并且提供了 `TakeNote()` 的实现。

指示类继承基类（如 `ThingsThatRecord`）的语法与类实现 C# 接口（如 `IRecable`）的语法本质不同：

```csharp
public class PDA : ThingsThatRecord ...
public class PDA : IRecordable ...
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_361_0.png)

> Visual Studio 可以帮助你实现接口。将鼠标指针悬停在类头部的接口名称上。接口名称第一个字符下方会出现下线。移动鼠标直到菜单打开并选择“实现接口 <name>”。预告！一个骨架框架 —— 你来填充细节。

## 如何命名你的接口

.NET 的接口命名规范在名称前带有字母 `I`。接口名称通常是形容词，如 `IRecordable`。

## 为什么 C# 包含接口

接口的本质是接口描述了一种能力，例如游泳安全培训或 A 类驾照。作为类类，当我实现 `TakeNote` 能力时，我就获得了 `IRecordable` 勋章。

更此外，接口是一份合同。如果你同意实现接口中定义的每个方法，你就可以声称该能力。不仅如此，使用你程序的客户端保证能够调用所有这些方法。实现接口是一个承诺 —— 由编译器强制执行。

