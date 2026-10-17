
观看视频 构造函数与继承。

## 两个真理一个谎言

## 使用基类构造函数

- 1. 当你创建任何派生类对象时，基类构造函数首先，然后执行派生类构造函数。
- 2. 当基类构造函数需要参数时，必须为你创建的每个派生类包含一个构造函数。
- 3. 当派生类的构造函数需要参数时，所有参数都必须传递给基类构造函数。

> 派生类的构造函数。参数传递给基类构造函数，其他可能某些传递给基类构造函数的参数可能在派生类中需要，或者可能所有参数都在派生类内部使用。错误的陈述是 #3。当派生类的构造函数需要参数时。

## 你来

### 在基类和派生类中添加构造函数

当基类仅包含需要参数的构造函数时，任何派生类必须提供基类构造函数。在接下来的步骤中，你将为 `Loan` 和 `CarLoan` 类添加构造函数，并证明它们按预期工作。

- 1. 打开 `DemoCarLoan2` 程序，并将类名改为 `DemoCarLoan3`。将文件保存为 `DemoCarLoan3`。
- 2. 在 `Loan` 类中，在 `LoanAmount` 字段声明之后，添加一个需要所有 `Loan` 属性值所需的构造函数：

```csharp
public Loan(int num, string name, double amount)
{
 LoanNumber = num; LastName = name;
 LoanAmount = amount;
}
```

（续）

## 第 10 章 继承简介

（续）

在 `CarLoan` 类中，在 `year` 字段声明之后，添加一个接受五个参数的构造函数。它将三个参数传递给基类构造函数，并使用另外两个参数为子类特有的属性赋值。

```csharp
public CarLoan(int num, string name, double amount,
    int year, string make) : base(num, name, amount)
{
    Year = year;
    Make = make;
}
```

在 `DemoCarLoan3` 类的 `Main()` 方法中，删除现有的 `aloan` 和 `aCarLoan` 声明，并将其替换为两个使用传递给构造函数的参数的声明。

```csharp
Loan aloan = new Loan(333, "Hanson", 7_000.00);
CarLoan aCarLoan = new CarLoan(444, "Carlisle",
30_000.00, 2014, "BMW");
```

- 5. 移除为 `Loan` 和 `CarLoan` 赋值的八条语句，但保留显示值的 `Write()` 语句。
- 6. 保存程序，然后编译并执行它。输出结果如图 10-30 所示。两个构造函数都按预期工作。`CarLoan` 构造函数在执行自己的语句之前，已经调用了父类的构造函数来设置必要的字段。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_482_0.png)

图 10-30 `DemoCarLoan3` 输出

## 创建和使用抽象类

在理解继承的概念后，创建类可以变得更容易。当你创建一个子类时，它继承了你需要的所有通用属性；你只需要创建子类所需的新的、更具体的属性。例如，画家（Painter）和雕塑家（Sculptor）比艺术家（Artist）更具体。它们继承了艺术家的所有通用属性，但你必须添加特定于画家和雕塑家的属性。

Copyright 2023 Cengage Learning. All Rights Reserved. 不可部分或全部复制、扫描或复制。WCN 02-200-2022

另一种思考超类的方法是，注意到它包含了其子类共享的特征。派生类是基类类型中更具体的示例；它们在共享的通用特征基础上添加了功能。相反，当你检查一个派生类时，你会发现它更具通用性。

有时你创建一个父类，使其变得非常通用，以至于你从未打算创建该类的任何特定实例。例如，你可能永远不会“仅仅”创建一个艺术家；每个艺术家都更具体地说是画家、雕塑家、插画家等等。你可以创建一个用于扩展但不能实例化的类是**具体类**（concrete class）。**抽象类**（abstract class）是你无法从中创建具体对象、但可以从中继承的类。当你声明抽象类时要使用 `abstract` 关键字，否则你将收到编译器错误。

抽象类类似于普通类，它们可以包含数据字段和方法。区别在于，你不能使用 `new` 操作符创建抽象类的实例。相反，你创建抽象类仅仅是为了提供一个基类，从那里派生其他对象。

抽象类通常包含抽象方法，也可以包含非抽象方法。然而，它们并不要求包含任何方法。回想第 9 章，抽象方法没有语句。任何继承自包含抽象方法的类都通过为该抽象方法提供方法体（实现）来重写该抽象方法。（或者，派生类可以将该方法声明为抽象的；在这种情况下，派生类的子类必须实现该方法。）你可以创建一个没有方法的抽象类，但不能从抽象类之外创建抽象方法。

> 声明为 `virtual` 的方法不需要在子类中重写，但方法必须被重写。

当你创建一个抽象方法时，你提供了 `abstract` 关键字和预期的方法类型，但你没有在方法内部提供语句。你创建一个像 `Animal` 这样的抽象类是为了你可以扩展它。例如，假设你想创建表示不同动物的类。你创建一个通用的抽象类 `Animal` 来只提供一次通用的数据字段，如名称。动物是通用的，但每个特定的动物都会发出独特声音。如果你在抽象 `Animal` 类中创建一个抽象的 `Speak()`，那么你就要求所有派生类都重写并提供特定于派生类的实现。图 10-31 显示了一个包含名称数据字段、一个赋值名称的构造函数以及抽象 `Speak()` 方法的 `Animal` 类。

Copyright 2018 Cengage Learning. All Rights Reserved. 不可部分或全部复制、扫描或复制。WCN 02-200-252

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_483_0.png)

```csharp
abstract class Animal
{
    private string name;
    public Animal(string name)
    {
        this.name = name;
    }
    public string Name
    {
        get
        {
            return name;
        }
    }
    public abstract string Speak();
}
```

图 10-31 `Animal` 类被声明为抽象。（关键字已高亮。）你不能在程序中放置 `Animal myPet = new Animal("Murphy");` 这样的语句，因为程序将无法编译。由于 `Animal` 是抽象类，所以不存在 `Animal` 对象。

你创建一个像 `Animal` 这样的抽象类是为了你可以扩展它。例如，你可以如图 10-32 所示创建 `Dog` 和 `Cat` 类。由于 `Animal` 类包含一个需要字符串参数的构造函数，`Dog` 和 `Cat` 都必须包含为它们的基类提供字符串参数的构造函数。

```csharp
class Dog : Animal
{
    public Dog(string name) : base(name)
    {
    }
    public override string Speak()
    {
        return "woof";
    }
}
class Cat : Animal
{
    public Cat(string name) : base(name)
    {
    }
    public override string Speak()
    {
        return "meow";
    }
}
```

图 10-32 `Dog` 和 `Cat` 类

# 创建和使用抽象类

如果一个在子类中应该被重写的方法有自己的实现，则将基类方法声明为虚拟的（virtual）。如果它没有自己的实现，则将基类和该方法声明为抽象的（abstract）。

`Dog` 和 `Cat` 构造函数除了将名称传递给 `Animal` 构造函数外不执行任何任务。`Dog` 和 `Cat` 内部的重写 `Speak()` 方法是必要的，因为抽象父类 `Animal` 包含一个抽象的 `Speak()` 方法。在每个 `Speak()` 头部中都需要 `override` 关键字（阴影部分）。你可以在 `Dog` 和 `Cat` 的 `Speak()` 方法中编写任何你语句，但这些方法必须存在。

图 10-33 显示了一个实现 `Dog` 和 `Cat` 对象的程序。图 10-34 显示了输出，其中 `Speak()` 为每种动物类型正常运行。

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

**图 10-33** `DemoAnimals` 程序

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_485_0.png)

**图 10-34** `DemoAnimals` 程序的输出

图 10-35 显示了创建 `DemoAnimals` 程序的另一种方法。在这个版本中，`Dog` 和 `Cat` 对象被传递给接受 `Animal` 参数的方法。输出与图 10-34 相同。`Name` 属性和 `Speak()` 方法以多态方式运行，对每个对象类型执行恰当的操作。

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

**图 10-35** `DemoAnimals2` 程序

# 两个真理一个谎言

- 1. 抽象类是你无法从中创建具体对象的类。
- 2. 与普通类不同，抽象类不能包含方法。
- 3. 当基类包含抽象方法时，该基类的后类必须重写该抽象方法，或将重写方法声明为派生的（derived）。

错误的陈述是 #2。抽象类与普通类的相似之处在于它们可以包含数据字段和方法。区别在于，你不能使用 `new` 运算符创建抽象类的实例。然而，你创建了一个其他对象可以从中继承的基类。

# 创建和使用接口

面向对象的编程语言（特别是 C#）允许子类继承自多个父类。例如，你可能会创建一个 `Employee` 类，其中包含与组织中每位员工的数据字段。你还可能创建一个 `Product` 类，持有你组织制造的每种产品的信息。当你为你公司拥有专利的每个产品创建一个 `Patent` 类时，你可能想要包含产品信息以及关于谁负责发明的信息。在这种情况下，从 `Product` 和 `Employee` 类中继承字段和方法将非常方便。继承多个类的能力被称为**多重继承**。

多重继承是一个困难的概念，程序员在使用它时会遇到问题。例如，父类中的变量和方法可能具有相同的名称，当子类使用其中一个名称时就会产生冲突。此外，正如你已经学过的，子类构造函数必须调用其父类构造函数。当存在两个或多个父类时，变成了一个更复杂的任务：当子类有多个父类时，`base` 指向哪个类？

由于所有这些原因，C# 禁止多重继承。然而，C# 为多重继承提供了替代方案，称为接口（interface）。像抽象类一样，**接口**是方法（和其他成员）的集合，只要类提供了重写接口抽象定义的定义，就可以被任何类使用。在抽象类内部，某些方法可以是抽象的，而另一些不需要。在接口内部，所有方法都是抽象的。

> 你最初在“使用类和对象”章节中使用 `IComparable` 接口时就学习了接口。

你创建接口的方式与创建抽象类定义几乎一样，只是你使用 `interface` 关键字而不是 `abstract class`。例如，假设你创建了如图 10-36 所示的 `IWorkable` 接口。为了简单起见，`IWorkable` 接口包含一个名为 `Work()` 的方法。

```
public interface IWorkable
{
    string Work();
}
```

**图 10-36** `IWorkable` 接口

> 虽然不是强制的，但在 C# 中习惯用大写 *I* 开始接口命名。其他语言遵循不同的约定。接口名称通常以 able 结尾。

当一个类实现 `IWorkable` 时，它也必须包含一个返回 `string` 的 `Work()` 方法。实现 `IWorkable` 的每个元素必须声明 `Work()` 方法。`Animal` 类将 `Work()` 定义为抽象方法，这意味着 `Animal` 的后类必须实现 `Work()`。图 10-37 还显示了带有 `IWorkable` 接口的 `Employee`、`Cat` 和 `Dog` 类。

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

**图 10-37** 带有 `IWorkable` 接口的 `Employee`、`Cat` 和 `Dog` 类

当你创建一个实例化 `Employee`、`Dog` 或 `Cat` 的程序时（如 10-38 中的 `DemoWorking` 程序），每个对象类型都知道如何恰当地“Work()”。图 10-39 显示了输出。

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
