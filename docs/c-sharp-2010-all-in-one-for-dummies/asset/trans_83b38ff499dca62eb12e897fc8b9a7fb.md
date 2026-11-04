
// Two abstract base classes and one interface
abstract class Animal
{
    abstract public void Eat(string food);
    abstract public void Sleep(int hours);
    abstract public int NumberOfLegs { get; }
    public void Breathe() { ... } // Nonabstract, implementation not shown.
}
abstract class Robot
{
    public virtual void Speak(string whatToSay) { ... } // Impl not shown
    abstract public void LiftObject(object o);
    abstract public int NumberOfLegs { get; }
}
interface IPet
{
    void AskForStrokes();
    void DoTricks();
    int NumberOfLegs { get; } // Properties in interfaces look like this.
    string Name { get; set; } // get/set must be public in implementations.
}
// Cat -- This concrete class inherits (and partially implements)
// class Animal and also implements interface IPet.
class Cat : Animal, IPet
{
    public Cat(string name) { Name = name; }
    // 1. Overrides and implements Animal members (not shown).
    // 2. Provides additional implementation for IPet.
    #region IPet Members
    public void AskForStrokes() ...
    public void DoTricks() ...
    public string Name { get; set; }
    // Inherits NumberOfLegs property from base class, thus meeting
    // IPet's requirement for a NumberOfLegs property.
    #endregion IPet Members
    public override string ToString() { return Name; }
}
class Cobra : Animal
{
    // 1. Inherits or overrides all Animal methods only (not shown).
}
class Robozilla : Robot    // Not IPet
{
    // 1. Override Speak.
    public override void Speak(string whatToSay)
    { Console.WriteLine("DESTROY ALL HUMANS!"); }
    // 2. Implement LiftObject and NumberOfLegs, not all shown.
    public override void LiftObject(object o) ...
    public override int NumberOfLegs { get { return 2; } }
}
class RoboCat : Robot, IPet
{
    public RoboCat(string name) { Name = name; }
    // 1. Override some Robot members, not all shown:
    #region IPet Members
    public void AskForStrokes() ...
    public void DoTricks() ...
    public string Name { get; set; }
    #endregion IPet Members
}

（注意 IPet 中的属性——这就是在接口中指定属性的方式。如果你同时需要 getter 和 setter，只需在 get; 后面加上 set;。)

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_373_0.png)

我已经向你展示了两个继承自 Animal 的具体类，以及两个继承自 Robot 的具体类。然而，你可以看到，Cobra 类和 Robozilla 类都没有实现 IPet——这大概是有充分理由的。我可不想让我的宠物眼镜蛇趴在沙发上陪我看电视，而机器哥斯拉听起来也很糟糕。这两个层次结构中的部分类表现出了你可能称之为“宠物性”的特征，而另一些则没有。

### 网络资源

本书网站上的 InterfacesBridgingHierarchies 示例对这些内容进行了实际检验。

### 技术细节

本节的重点是，任何类都可以实现接口，只要它提供了正确的方法和属性。Robotcat 和 Robotdog 可以执行 AskForStrokes() 和 DoTricks() 操作，并拥有 NumberOfLegs 属性，Animal 层次结构中的 Cat 和 Dog 也可以——而同样的层次结构中的其他类则没有实现 IPet。

你可以为任何类添加对接口的支持——但前提是你能够自由修改源代码。

## 隐藏在接口后面

在本书中，我经常讨论这样的代码：(a) 你编写的，但 (b) 其他人（客户）在她的程序中使用（当然，你自己也可能是那个客户）。有时，你有一个复杂或棘手的类，你真的不想向客户暴露整个公共接口。由于各种原因，它包含一些危险的操作，但这些操作又必须是公共的。理想情况下，你会暴露类中公共方法和属性的一个安全子集，而隐藏那些危险的。C# 接口也能做到这一点。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_375_0.png)

程序员（我想我能猜到是谁）可以用一个简单的强制转换来破解我的小计谋：

```csharp
Robozilla myZillaZilla = (Robozilla)myZilla;
```

不过，这样做通常是个坏主意。接口是有其用途的。Bill Wagner 说过：“费那么大劲去制造 bug 的程序员，后果自负。”

在现实生活中，程序员有时会将这种“发放接口”的技术用于 ADO.NET 中与数据库交互的复杂 DataSet 类。DataSet 可以返回一组装满记录的数据库表——例如一张 Customers 表和一张 Orders 表。（现代关系数据库，如 Oracle 和 SQL Server，包含通过各种关系链接的表。每张表包含大量记录，其中每条记录可能是，例如，一个 Customer 的姓名、级别和序列号。）

不幸的是，如果你将一个 DataSet 引用交给客户（即使是通过只读属性的 get 子句），他可以很容易地通过深入 DataSet 并修改你不希望被修改的元素来把局面搞糟。防止这种破坏的方法之一是返回一个只读的 DataView 对象。或者，你可以创建一个 C# 接口，以公开 DataSet 上可用操作的安全子集。然后你可以对 DataSet 进行子类化，并让该子类（称之为 MyDataSet）实现该接口。最后，给客户一种途径，让他们获得一个活动 MyDataSet 对象的接口引用，并通过接口让他们在相对安全的前提下使用它。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_375_1.png)

你通常也不应该返回集合的引用，因为这样会让任何人在创建该集合的类之外修改它。请记住，你给出的引用仍然可以指向你类内部的原始集合。这就是为什么 `List<T>` 之类的类提供了 `AsReadOnly()` 方法。该方法返回一个无法被修改的集合：

```csharp
private List<string> _readWriteNames = ...; // A modifiable data member
ReadOnlyCollection<string> readonlyNames = _readWriteNames.AsReadOnly();
return readonlyNames; // Safer to return this than _readWriteNames.
```

尽管这算不上是使用接口，但其目的是相同的。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_375_2.png)

本书网站上的 HidingBehindAnInterface 示例展示了本节中的 Robozilla 代码。

## 继承接口

C# 接口可以“继承”另一个接口的方法。我在“继承”这个词上加引号，是因为无论看起来如何，这都不是真正的继承。下面的接口代码在其标题中列出了一个基础接口，就像基类一样。

```csharp
interface IRobozillaSafe : IPet  // Base interface
{
    // Methods not shown here ...
}
```

通过让 IRobozillaSafe “继承” IPet，你可以让 Robozilla 的这个子集实现自己的“宠物性”，而不会不恰当地将宠物性强加给整个 Robozilla：

```csharp
class PetRobo : Robozilla, IRobozillaSafe // (also an IPet by inheritance)
{
    // Implement Robozilla operations.
    // Implement IRobozillaSafe operations, then ...
    // Implement IPet operations too (required by the inherited IPet interface).
}
// ...
// Hand out only a safe reference, not one to PetRobo itself.
IPet myPetRobo = (IPet)new PetRobo();
// ... now call IPet methods on the object.
```

IRobozillaSafe 接口继承自 IPet。因此，实现 IRobozillaSafe 的类也必须实现 IPet，以使其对 IRobozillaSafe 的实现完整。

这种类型的继承与类继承并不是同一个概念。例如，前面例子中的 PetRobo 类可以有一个构造函数，但 IRobozillaSafe 或 IPet 并不存在与基类构造函数等价的东西。接口没有构造函数。更重要的是，多态性在接口上的工作方式并不相同。虽然你可以通过基类的引用调用子类的方法（类多态），但涉及接口的类似操作（接口多态）却行不通：你不能通过基础接口引用（IPet）调用派生接口（IRobozillaSafe）的方法。

尽管接口继承在多态性上不同于类继承，但你仍然可以将派生接口类型（IRobozillaSafe）的对象作为其基础接口类型（IPet）的参数传递。因此，你也可以将 IRobozillaSafe 对象放入 IPet 对象的集合中。本书网站上的 PassInterface 示例演示了本节中的这些概念。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_376_0.png)

