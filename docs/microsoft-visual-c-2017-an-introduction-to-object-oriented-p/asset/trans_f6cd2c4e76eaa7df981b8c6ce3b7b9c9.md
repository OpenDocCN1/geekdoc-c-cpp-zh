

# 创建和使用抽象类

如果一个在子类中应该被重写的方法有自己的实现，则将基类方法声明为虚拟的（virtual）。如果它没有自己的实现，则将基类和该方法声明为抽象的（abstract）。

**Dog** 和 **Cat** 构造函数除了将名称传递给 **Animal** 构造函数外不执行任何任务。**Dog** 和 **Cat** 内部的重写 `Speak()` 方法是必要的，因为抽象父类 `Animal` 包含一个抽象的 `Speak()` 方法。在每个 `Speak()` 头部中都需要 `override` 关键字（阴影部分）。你可以在 **Dog** 和 **Cat** 的 `Speak()` 方法中编写任何你语句，但这些方法必须存在。

图 10-33 显示了一个实现 **Dog** 和 **Cat** 对象的程序。图 10-34 显示了输出，其中 `Speak()` 为每种动物类型正常运行。

```
static System.Console;
class DemoAnimals {
    static void Main() {
        Dog spot = new Dog("Spot");
        Cat puff = new Cat("Puff");
        WriteLine(spot.Name + " " says " + spot.Speak());
        WriteLine(puff.Name + " " says " + puff.Speak());
    }
}
```

**图 10-33** DemoAnimals 程序

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_485_0.png)

**图 10-34** DemoAnimals 程序的输出

图 10-35 显示了创建 DemoAnimals 程序的另一种方法。在这个版本中，**Dog** 和 **Cat** 对象被传递给接受 **Animal** 参数的方法。输出与图 10-34 相同。**Name** 属性和 `Speak()` 方法以多态方式运行，对每个对象类型执行恰当的操作。

```
using static System.Console;
class DemoAnimals2
{
    static void Main()
    {
        Dog Spot = new Dog("Spot");
        Cat puff = new Cat("Puff");
        DisplayAnimal(spot);
        DisplayAnimal(puff);
    }
    public static void DisplayAnimal(Animal creature)
    {
        WriteLine(creature.Name + " says " + creature.Speak());
    }
}
```

**图 10-35** DemoAnimals2 程序

# 两个真理一个谎言

- 1. 抽象类是你无法从中创建具体对象的类。
2. 与普通类不同，抽象类不能包含方法。
3. 当基类包含抽象方法时，该基类的后类必须重写该抽象方法，或将重写方法声明为派生的（derived）。

错误的陈述是 #2。抽象类与普通类的相似之处在于它们可以包含数据字段和方法。区别在于，你不能使用 `new` 运算符创建抽象类的实例。然而，你创建了一个其他对象可以从中继承的基类。

# 创建和使用接口

面向对象的编程语言（特别是 C#）允许子类继承自多个父类。例如，你可能会创建一个 `Employee` 类，其中包含与组织中每位员工的数据字段。你还可能创建一个 `Product` 类，持有你组织制造的每种产品的信息。当你为你公司拥有专利的每个产品创建一个 `Patent` 类时，你可能想要包含产品信息以及关于谁负责发明的信息。在这种情况下，从 `Product` 和 `Employee` 类中继承字段和方法将非常方便。继承多个类的能力被称为**多重继承**。

多重继承是一个困难的概念，程序员在使用它时会遇到问题。例如，父类中的变量和方法可能具有相同的名称，当子类使用其中一个名称时就会产生冲突。此外，正如你已经学过的，子类构造函数必须调用其父类构造函数。当存在两个或多个父类时，变成了一个更复杂的任务：当子类有多个父类时，`base` 指向哪个类？

由于所有这些原因，C# 禁止多重继承。然而，C# 为多重继承提供了替代方案，称为接口（interface）。像抽象类一样，**接口**是方法（和其他成员）的集合，只要类提供了重写接口抽象定义的定义，就可以被任何类使用。在抽象类内部，某些方法可以是抽象的，而另一些不需要。在接口内部，所有方法都是抽象的。

> 你最初在“使用类和对象”章节中使用 `IComparable` 接口时就学习了接口。

你创建接口的方式与创建抽象类定义几乎一样，只是你使用 **interface** 关键字而不是 **abstract class**。例如，假设你创建了如图 10-36 所示的 **IWorkable** 接口。为了简单起见，**IWorkable** 接口包含一个名为 **Work()** 的方法。

```
public interface IWorkable
{
    string Work();
}
```

**图 10-36** IWorkable 接口

> 虽然不是强制的，但在 C# 中习惯用大写 *I* 开始接口命名。其他语言遵循不同的约定。接口名称通常以 able 结尾。

当一个类实现 **IWorkable** 时，它也必须包含一个返回 **string** 的 **Work()** 方法。实现 **IWorkable** 的每个元素必须声明 **Work()** 方法。**Animal** 类将 **Work()` 定义为抽象方法，这意味着 **Animal** 的后类必须实现 `Work()`。图 10-37 还显示了带有 IWorkable 接口的 Employee、Cat 和 Dog 类。

```csharp
abstract class Animal : IWorkable
{
    public string Name { get; set; }
    public Animal(string name) { Name = name; }
    public abstract string Work();
}

class Dog : Animal
{
    public Dog(string name) : base(name) { }
    public override string Work() { return "I bark"; }
}

class Cat : Animal
{
    public Cat(string name) : base(name) { }
    public override string Work() { return "I meow"; }
}
```

**图 10-37** 带有 IWorkable 接口的 Employee、Cat 和 Dog 类

当你创建一个实例化 Employee、Dog 或 Cat 的程序时（如 10-38 中的 DemoWorking 程序），每个对象类型都知道如何恰当地“Work()”。图 10-39 显示了输出。

```
using static System.Console;
class DemoWorking
{
    static void Main()
    {
        Employee bob = new Employee("Bob");
        Dog spot = new Dog("Spot");
        Cat puff = new Cat("Puff");
        WriteLine(bob.Name + " " says " + bob.Work());
        WriteLine(spot.Name + " " says " + spot.Work());
        WriteLine(puff.Name + " " says " + puff.Work());
    }
}
```

**图 10-38** DemoWorking 程序

**图 10-39** DemoWorking 程序的输出

