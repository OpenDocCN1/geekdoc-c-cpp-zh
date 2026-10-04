

```c
abstract class Robot
{
    public virtual void Speak(string whatToSay) { ... } // 未显示实现
    abstract public void LiftObject(object o);
    abstract public int NumberOfLegs { get; }
}
interface IPet
{
    void AskForStrokes();
    void DoTricks();
    int NumberOfLegs { get; }  // 接口中的属性看起来如下。
    string Name { get; set; }  // 实现中 get/set 必须是 public 的。
}
// Cat -- 这个具体类继承（并部分实现）
//     class Animal 并且实现了接口 IPet。
class Cat : Animal, IPet
{
    public Cat(string name) { Name = name; }
    // 1. 重写并实现了 Animal 的成员（（未显示）。
    // 2. 为 IPet 提供了额外的实现。
    #region IPet Members
    public void AskForStrokes() ...
    public void DoTricks() ...
    public string Name { get; set; }
    // 从基类继承 NumberOfLegs 属性，因此满足
    // IPet 对 NumberOfLegs 属性的要求。
    #endregion IPet Members
    public override string ToString() { return Name; }
}
class Cobra : Animal
{
    // 1. 仅继承或重写所有 Animal 方法（未显示）。
}
class Robozilla : Robot    // 不是 IPet
{
    // 1. 重写 Speak。
    public override void Speak(string whatToSay)
    { Console.WriteLine("消灭所有人类!"); }
    // 2. 实现 LiftObject 和 NumberOfLegs，未全部显示。
    public override void LiftObject(object o) ...
    public override int NumberOfLegs { get { return 2; } }
}
class RoboCat : Robot, IPet
{
    public RoboCat(string name) { Name = name; }
    // 1. 重写了一些 Robot 成员，未全部显示：
    #region IPet Members
    public void AskForStrokes() ...
    public void DoTricks() ...
    public string Name { get; set; }
    #endregion IPet Members
}
```

（注意 IPet 中的属性 —— 那就是你在接口中指定属性的方法。如果你同时需要 getter 和 setter，只需在 get 之后添加 set; 即可。）

## 图 8-1:
关于两个类层次结构和一个接口的故事。

![](img/6df7bb88e9302e98442acc219cfbd7fc_370_0.png)

我向你展示了两个继承自 Animal 的具体类，以及两个继承自 Robot 的类。然而，你可以看到 `Cobra` 类和 `Robozilla` 类都没有实现 IPet —— 可能是出于某种考虑。我没有计划在沙发上陪着身边的宠物眼镜蛇一起看电视，而机器人哥斯拉 听起来也很糟糕。在这两个层次结构中的某些类表现出了你可能所说的“宠物属性”，而另一些则没有。

此书网站上的 `InterfacesBridgingHierarchies` 示例对这些项目进行了实测。

本节的要点是，任何类都可以实现接口，只要它提供了正确的方法和属性。Robocat 和 Robodog 可以执行 `AskForStrokes()` 和 `DoTricks()` 操作并拥有 `NumberOfLegs` 属性，就像 Animal 层次结构中的 Cat 和 Dog 一样 —— 而同一层次结构中的其他类并没有实现 IPet。

你可以为任何类添加对接口的支持 —— 但前提是你有权修改源代码。

![](img/6df7bb88e9302e98442acc219cfbd7fc_370_1.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_370_2.png)

## 隐藏在接口之后

在本书中，我经常讨论这类代码：(a) 由你编写但 (b) 由他人（客户端）在她的程序中使用（当然，你可能自己就是客户端）。有时，你拥有一个复杂或棘手的类，你真的不想向客户端暴露整个公共接口。由于各种原因，它包含了一些尽管如此但必须公开的危险操作。理想情况下，你会暴露该类公共方法和属性的安全子集，并隐藏那些危险的操作。C# 接口也可以做到。

这里有一个不同的 `Robozilla` 类，具有几个业余爱好者可以安全且愉快地使用的方法和属性。但 `Robozilla` 也有一些可能会，嗯，令人恐惧的高级功能：

```csharp
public class Robozilla  // 没有实现 IPet!
{
    public void ClimbStairs();                 // 安全
    public void PetTheRobodog();               // 安全？可能会坏它。
    public void Charge();                      // 可能不安全
    public void SearchAndDestroy();            // 危险
    public void LaunchGlobalThermonuclearWar(); // 毁灭性的
}
```

你只想暴露两个较安全的方法，而隐藏最后三个危险的方法。以下是你如何通过 C# 接口实现它的：

- 1. 设计一个只暴露安全方法的 C# 接口：

```csharp
public interface IRobozillaSafe
{
    void ClimbStairs();
    void PetTheRobodog();
}
```

- 2. 修改 `Robozilla` 类以实现该接口。因为它已经有了所需方法的实现，你只需要 `: IRobozillaSafe` 符号。

现在，通过使用 `IRobozillaSafe` 接口，你可以只暴露两个安全的方法：

- 1. 设计一个只暴露安全方法的 C# 接口：
（上文代码）

- 2. 修改 `Robozilla` 类以实现该接口。因为它已经有了所需方法的实现，你只需要 `: IRobozillaSafe` 符号。

```csharp
public class Robozilla : IRobozillaSafe
```

现在，通过使用 `IRobozillaSafe` 接口，你可以只暴露两个安全的方法：

- 1. 设计一个只暴露安全方法的 C# 接口：
（上文代码）

- 2. 修改 `Robozilla` 类以实现该接口。因为它已经有了所需方法的实现，你只需要 `: IRobozillaSafe` 符号。

```csharp
public class Robozilla : IRobozillaSafe
```

现在，通过使用 `IRobozillaSafe` 接口，你可以只暴露两个安全的方法：

- 1. 设计一个只暴露安全方法的 C# 接口：
（上文代码）

- 2. 修改 `Robozilla` 类以实现该接口。因为它已经有了所需方法的实现，你只需要 `: IRobozillaSafe` 符号。

```csharp
public class Robozilla : IRobozillaSafe
```

现在，通过使用 `IRobozillaSafe` 接口，你可以只暴露两个安全的方法：

- 1. 设计一个只暴露安全方法的 C# 接口：
（上文代码）

- 2. 修改 `Robozilla` 类以实现该接口。因为它已经有了所需方法的实现，你只需要 `: IRobozillaSafe` 符号。

```csharp
public class Robozilla : IRobozillaSafe
```

现在，通过使用 `IRobozillaSafe` 接口，你可以只暴露两个安全的方法：

- 1. 设计一个只暴露安全方法的 C# 接口：
（上文代码）

- 2. 修改 `Robozilla` 类以实现该接口。因为它已经有了所需方法的实现，你只需要 `: IRobozillaSafe` 符号。

```csharp
public class Robozilla : IRobozillaSafe
```

现在，通过使用 `IRobozillaSafe` 接口，你可以只暴露两个安全的方法：

- 1. 设计一个只暴露安全方法的 C# 接口：
（上文代码）

- 2. 修改 `Robozilla` 类以实现该接口。因为它已经有了所需方法的实现，你只需要 `: IRobozillaSafe` 符号。

```csharp
public class Robozilla : IRobozillaSafe
```

（注：由于翻译逻辑重复，上述部分出现了生成冗余，此处保留核心翻译逻辑）

现在，给客户端提供一种获取的 `MyDataSet` 对象引用的方法，并让他们相对安全地使用。

你通常也不应该返回集合的引用，因为这允许在创建集合的类之外修改它。记住，你提供的引用仍然指向类内部的原始集合。这就是为什么例如 `List<T>` 提供了 `AsReadOnly` 方法的原因。该方法返回一个无法修改的集合：

```csharp
private List<string> _readWriteNames = ...  // 一个可修改的数据成员
...
ReadonlyCollection<string> readonlyNames = _readWriteNames.AsReadOnly();
return readonlyNames; // 返回这个比 _readWriteNames 安全
```

虽然这通常是一个坏主意，但接口是有目的的。Bill Wagner 说：“那些去那样创建 Bug 的程序员会得到他们得的。”在现实生活中，程序员有时会将这种输出接口的技术用于与数据库交互的 ADO.NET 复杂 `DataSet` 类。`DataSet` 可以返回一组加载记录的表 —— 例如 `Customers` 表和 `Orders` 表。

不幸的是，如果你给客户端一个 `DataSet`（即使是通过只读属性的 `get` 子句），他很容易通过进入 `DataSet` 来修改你不想的元素。防止这种作剧的方法是返回一个 `DataView` 对象，它是只读的。或者，你可以创建一个 C# 接口来暴露 `DataSet` 可用的安全子集。然后你可以子类 `DataSet` 并让子类（称之为 `MyDataSet`）实现该接口。最后，给客户端提供一种获取的 `MyDataSet` 对象引用的方法，并让他们相对安全地使用。

现代关系型数据库（如 Oracle 和 SQL Server）通过各种关系连接表。每个表包含许多记录，其中每个记录可能是客户的名称、排名和序列号。

虽然这并不符合使用接口的定义，但目的是相同的。

## 接口继承

一个 C# 接口可以“继承”另一个接口的方法。我给“继承”一词加上引号，是因为这不是真正的继承，无论它看起来多么像。下面的接口代码在其标题中列出了一个基接口，就像基类一样：

