

```interface
interface IRobozillaSafe : IPet  // 接口
{
    // 此处未显示方法 ...
}
```

通过让 IRobozillaSafe “继承” IPet，你可以让 Robozilla 的这部分子集实现它自己的“宠物属性”，而不需要尝试不恰地给所有 Robozilla 强加宠物属性：

```csharp
class PetRobo : Robozilla, IRobozillaSafe // (通过继承也也是一个 IPet)
{
    // 实现 Robozilla 操作。
    // 实现 IRobozillaSafe 操作，然后 ...
    // 也要实现 IPet 操作（被继承的 IPet 接口要求的）。
}
...
// 只提供一个安全的引用，而不是 PetRobo 本身。
IPet myPetRobo = (IPet)new PetRobo();
// ... 现在在该对象上调用 IPet 方法。
```

IRobozillaSafe 接口继承自 IPet。因此，实现 IRobozillaSafe 的类也必须实现 IPet，以使其对 IRobozillaSafe 的实现是完整的。

这种继承与类继承的概念不是一回事。例如，上一个示例中的类 PetRobo 可以有一个构造函数，但 IRobozillaSafe 或 IPet 并不存在等效的基类构造函数。接口没有构造函数。更重要的是，多态在接口上的工作方式并不相同。虽然你可以通过基类引用调用子类的方法（类多态），但涉及接口的并行操作（接口多态）是不行通的：你无法通过基接口引用（IPet）调用派生接口（IRobozillaSafe）的方法。

尽管接口继承不像像类继承那样具有多态性，但你可以将派生接口类型（IRobozillaSafe）的对象通过其基接口类型（IPet）的参数传递。因此，你也可以将 IRobozillaSafe 对象放入 IPet 对象集合中。该本书网站上的 PassInterface 示例演示了本节的观点。

## 使用接口管理变化
## 面向对象程序

接口是能够灵活应对变化风云的面向对象程序的关键。你的代码将面对新需求付之大笑。

![](img/6df7bb88e9302e98442acc219cfbd7fc_374_0.png)

你无疑听过这样的话：“变化是永恒的。”当你把一个新程序交给一群用户时，他们很快就会开始请求更改。请添加这个功能。请修复那个问题。RoboWarrior 有功能 X，为什么 Robozilla 没有呢？许多程序有很长的寿命——数以千计的程序，特别是旧 Fortran 和 Cobol 程序，已经运行了 20 或 30 年甚至更久。在这一扩展的时间范围内，它们经历了大量的维护，这使得为变化进行规划和设计成为你的优先级任务之一。

这里有一个例子：在 Robot 类层次中，假设所有机器人都能以某种方式移动。Robocats 散步。Robozillas 冲锋——至少当被动力（饥饿的）用户操作时。Robosnakes 爬行。实现这些不同移动模式的一种方法涉及继承：给基类 Robot 提供一个抽象的 `Move()` 方法。然后每个子类都重写 `Move()` 方法以不同的方式实现它：

```csharp
abstract public class Robot
{
    abstract public void Move(int direction, int speed);
    // ...
}
public class Robosnake : Robot
{
    public override void Move(int direction, int speed)
    {
        // 此处是真实的 Move() 实现：爬行。
        ... 一些真实的代码，用于计算角度并改变
        // 蛇相对于坐标系的位置，例如 ...
    }
}
```

但假设你经常收到请求，为现有的 Robot 子类添加新类型的移动方式。也许是“请让 Robosnake 扭动而不是爬行。”（别问我它们有什么区别。）现在你必须打开 Robosnake 类并直接修改它的 `Move()` 方法。

![](img/6df7bb88e9302e98442acc219cfbd7fc_374_1.png)

在 `Move()` 方法针对爬行能够正常工作后，大多数程序员倾向于不要干涉它。实现爬行是困难的，改变实现可能会引入全新的 Bug。如果它没坏，就不要修它。

![](img/6df7bb88e9302e98442acc219cfbd7fc_374_2.png)

刚给出的代码说明了这个问题。该本书网站上的 StrategyExample 程序说明了解决方案，这将在接下来的几节中讨论。该解决方案的优点是允许旧的爬行代码在某些应用程序中继续运行，同时在较新的应用程序中提供新的扭动移动。大家都很开心。

第二卷 第 8 章 与接口衔接

## 通过接口创建灵活的依赖关系

必须有一种实现 `Move()` 的方法，不需要让你在每次客户端想要扭动时都打开一盒乱麻。当然，你可以使用接口！

看下面这段代码，它使用了 HAS_A，这是两个类之间一种现在已熟悉的关系，其中一个类包含另一个类：

```csharp
public class Robot
{
    // 此对象用于实现运动。
    protected Motor _motor = new Motor(); // 通过名称引用 Motor
    // ...
}
internal class Motor { ... }
```

这里的要点是，你可以使用接口来解耦类。与其依赖于具体的 `Motor`，不如依赖于 `IPropulsion` 接口。这允许你在不改变 Robot 类的情况下切换电机的实现。

![](img/6df7bb88e9302e98442acc219cfbd7fc_375_0.png)

## 抽象或具体：何时使用

在 C# 中可以用两种方式表示抽象：使用抽象类或接口。这两者之间的差异会影响你对使用哪一个的选择：

- 当你可以在子类之间共享实现时，使用抽象类。抽象类不需要是完全抽象的。尽管它至少有一个抽象方法或属性，但某些可以实现。使用抽象类提供实现可以避免代码重复。
- 当你无法共享任何实现或实现类已经有一个基类时，使用接口。C# 接口是纯粹、完全抽象的。C# 接口不提供方法的实现。但它也可以添加无法实现的灵活性。抽象类的选项可能不可用，因为你想为一个已经具有基类的类添加功能。例如，Robot 类可能在某个你没有编写因此无法修改的库中已经有一个基类。接口对于表示完全抽象的能力（如可移动性或显示性）特别有用，你可以将这些能力添加到多个其他没有共同点的类中——例如不在同一个类层次结构中的类。

![](img/6df7bb88e9302e98442acc219cfbd7fc_375_1.png)

## 使用接口实现 HAS_A

我在在本章前面提到过，可以使用接口作为更通用的引用类型。包含类不是通过具体类的引用引用被包含类，而是通过抽象的引用——无论是抽象类还是 C# 接口都可以的：

```sharp
AbstractDependentClass dependency1 = ...;
ISomeInterface dependency2 = ...;
```

假设你有一个 `IPropulsion` 接口：

```csharp
interface IPropulsion
{
    void Movement(int direction, int speed);
}
```

Robot 类可以包含类型为 `IPropulsion` 的数据成员，而不是具体的 `Motor` 类型：

```csharp
public class Robot
{
    private IPropulsion _propel;    // 注意这里的接口类型。
    // 在运行时提供一个具体的推进对象 ...
    // 其他操作然后：
    public void Move(int speed, int direction)
    {
        // 使用安装在 _propel 中的任何具体的推进设备。
        _propel.Movement(speed, direction); // 委托给它的方法。
    }
}
```

