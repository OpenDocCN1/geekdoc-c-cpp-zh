
# 回到 Main () 事件

如果你到目前为止一直在跟着我们学习，那么你已经准备好进入精彩部分，回到 `Main()`。`CreateList()` 方法用于返回一个未排序的列表，它存储在 `students` 数组中。

你可能认为有必要将 `students` 数组转换为 `comparableObjects` 数组，以便将学生传递给 `Array's Sort()` 方法：

```
IComparable<Student[]> comparables = (IComparable<Student>)students;
```

但事实并非如此，`Sort()`看到传递的数组由实现 `IComparable<something>` 的对象组成，只需对每个 `Student` 对象调用 `CompareTo()` 即可排序。很棒吧？

然后，将排序后的 `Student` 对象数组传递给本地定义的 `DisplayArray()` 方法。`DisplayArray()` 使用 `foreach` 遍历实现 `Display()` 方法的对象数组，该方法由对象实现 `IDisposable` 予以保证。在循环中，它对每个对象调用 `Display()` 并使用 `WriteLine()` 将结果显示在控制台上。

`Main()` 中的程序继续对鸟类进行排序和显示！我想我们可以同意，鸟类与学生没有任何关系。同样的 `Sort()` 和 `DisplayArray()` 方法处理 `Bird` 就像处理 `Student` 一样。

排序学生列表
Lisa : 100
Marge : 85
Bart : 50
Maggio : 30
Homer : 0

排序鸟类列表
Bluejay
Cardinal
Finch
Hawk
Oriole
Robin
Sparrow
按回车键终止...

# 统一类层次结构

8-1 显示了机器人（Robot）和动物（Animal）层次结构。每个层次结构中的某些（并非所有）类不仅继承自基类 `Robot` 或 `Animal`，还实现了 `IPet` 接口（你看，并不是所有动物都是宠物），如下代码所示 —— 我跳过了许多细节：

```cs
// 两个抽象基类和一个接口
abstract class Animal
{
    abstract public void Eat(string food);
    abstract public void Sleep(int hours);
    abstract public int NumberOfLegs { get; }
    public void Breathe() { } // 非抽象，显示了实现。
}
abstract class Robot
{
    public virtual void Speak(string whatToSay) { ... } // 未实现
    abstract public void LiftObject(object object);
    abstract public int NumberOfLegs { get; }
}
```

```cs
interface IPet
{
    void AskForStrokes();
    void DoTricks();
    int NumberOfLegs { get; } // 接口中的属性看起来如下。
    string Name { get; set; } // 实现中 get/set 必须是 public 的。
}
// 此类继承（并部分实现）
class Animal 也实现了 IPet。
class Cat : IPet
{
    public Cat(string name) { Name = name; }
    // 1. 重写并实现了 Animal 成员（未显示）。
    // 2. 为 IPet 提供了额外的实现。
    #region IPet Members
    public void AskForStrokes()
    public void DoTricks()
    public string Name { get; set; }
    // 从基类继承了 NumberOfLegs 属性，满足了
    // IPet 对 NumberOfLegs 属性的要求。
    #endregion
    public override string ToString() { return Name; }
}
```

```cs
class Cobra : Animal
{
    // 1. 仅继承或重写所有 Animal 方法（未显示）。
}
class Robotilla : Robot // 不是 IPet
{
    // 1. 重写 Speak。
    public override void Speak(string whatToSay)
    {
        Console.WriteLine("DESTROY ALL HUMANS!");
    }
    // 2. 实现 LiftObject 和 NumberOfLegs，未全部显示。
    public override void LiftObject(object object)
    public override int NumberOfLegs { get { return 2; }}
}
class RobotCat : Robot, IPet
{
    public RobotCat(string name) { Name = name; }
    // 1. 重写了一些 Robot 成员，未全部显示：
    #region IPet Members
    public void AskForStrokes()
    public void DoTricks() { ... }
    public string Name { get; set; }
    #endregion
```

# 隐藏在接口之后

（注意 `IPet` 中的属性 —— 这就是你在接口中指定属性的方法。如果你同时需要 getter 和 setter，只需在 get; 之后添加 set;）

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_373_0.png)

我向你展示了两个继承自 `Animal` 的类和两个继承自 `Robot` 的类。然而，你可以看到 `Cobra` 和 `Robotilla` 类都没有实现 `IPet` —— 可能正当理由的。我计划在沙发上和我的宠物一起看电视，而一个机器人哥斯拉 就太坏了。这些层次结构中的某些类表现出了你可能说的“宠物属性”，而有些则没有。

`InterfacesBridgingHierarchies` 示例展示了你的网站如何让这些项目通过其页面。

本节的要点是，任何类都可以实现接口，只要它提供了正确的方法和属性。`Robotcat` 和 `Robog` 执行 `AskStrokes()` 和 `DoTricks()` 动作并拥有 `NumberOfLegs` 属性，就像 `Animal` 层次结构中的 `Cat` 和 `Dog` 一样 —— 而同一层次结构中的其他类并没有实现 `IPet`。

