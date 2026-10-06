
```csharp
using static System.Console;
class DemoAnimals
{
    static void Main()
    {
        Dog spot = new Dog("Spot");
        Cat puff = new Cat("Puff");
        WriteLine(spot.Name + " says " + spot.Speak());
        WriteLine(puff.Name + " says " + puff.Speak());
    }
}
```

**Figure 10-33** DemoAnimals program

```
C:\CH\Chapter.10\DemoAnimals
Spot says woof
Puff says meow
C:\CO\Chapter.10>
```

**Figure 10-34** Output of the DemoAnimals program

Figure 10-35 shows an alternate way to create the DemoAnimals program. In this version the Dog and Cat objects are passed to a method that accepts an Animal parameter. The output is the same as in Figure 10-34. The `Name` property and `Speak()` method operate polymorphically, acting appropriately for each object type.

```csharp
using static System.Console;
class DemoAnimals2
{
    static void Main()
    {
        Dog spot = new Dog("Spot");
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

**Figure 10-35** The DemoAnimals2 program

## 两个真理，一个谎言

### 创建和使用抽象类

- 1. 抽象类是无法创建具体对象的类。
- 2. 与普通类不同，抽象类不能包含方法。
- 3. 当基类包含抽象方法时，基类的后代必须重写该抽象方法，或将覆盖的方法声明为派生。

陈述是 #2。抽象类与普通类的区别在于，它们仅仅通过使用 `new` 运算符提供类的实例。区别在于，你不能创建数据字段和方法。

### 创建和使用接口

某些面向对象的编程语言（特别是 C++）允许子类继承自多个类。例如，你可能会创建一个 `Employee` 类，其中包含与组织中每位员工相关的数据字段。你可能还会创建一个 `Product` 类，持有你组织制造的每种产品的信息。当你为你公司持有专利的每个产品创建一个 `Patent` 类时，你可能想要包含产品信息，以及负责该发明的员工信息。在这种情况下，从 `Product` 和 `Employee` 类中继承字段和方法将非常方便。继承自多个类的能力被称为**多重继承**。

多重继承是一个困难的概念，程序员在使用它时会遇到很多问题。例如，父类中的变量和方法可能具有相同的名称，当子类使用其中一个名称时，就会产生冲突。此外，正如你已经学到的，子类的构造函数必须调用其父类的构造函数。当存在两个或多个父类时，这变成了一个更复杂的任务：当子类有多个父类时，应该引用哪个类？

由于这些原因，C# 禁止多重继承。然而，C# 确实提供了多重继承的替代方案，即**接口**。

# 第 10 章 继承简介

接口是方法（可能还有其他成员）的集合，只要该类提供了以重写接口抽象定义的定义，就可以被任何类使用。在抽象类中，某些方法可以是抽象的，而其他则不一定。在接口中，所有方法都必须是抽象。

你首次在“使用类和对象”章节中通过使用 `IComparable` 接口学习了接口。

你创建接口的方式与创建抽象类定义非常相似，只是你使用的是 `interface` 关键字而不是 `abstract class`。例如，假设你创建了一个如图 10-36 所示的 `IWorkable` 接口。为了简单起见，`IWorkable` 接口包含一个名为 `Work()` 的方法。

虽然不是强制要求的，但在 C# 中，接口名称通常以大字母 I 开头。其他语言遵循不同的约定。接口名称经常以 `able` 结尾。

```csharp
public interface IWorkable
{
    string Work();
}
```

**图 10-36** IWorkable 接口

当任何类实现 `IWorkable` 时，它必须包含一个返回字符串的 `Work()` 方法。图 10-37 显示了两个实现 `IWorkable` 的类：`Employee` 类和 `Animal` 类。因为每个类都实现了 `IWorkable`，所以每个类都必须声明一个 `Work()` 方法。`Employee` 类实现 `Work()` 以返回 "I do my job" 字符串。抽象类 `Animal` 将 `Work()` 定义为抽象方法，这意味着 `Animal` 的后代必须实现 `Work()`。图 10-37 还显示了 `Animal` 的两个子类：`Dog` 和 `Cat`。注意 `Work()` 在每个类中的定义是不同的。

```csharp
class Employee : IWorkable
{
    public Employee(string name)
    {
        Name = name;
    }
    public string Name {get; set;}
    public string Work()
    {
        return "I do my job";
    }
}
abstract class Animal : IWorkable
{
    public Animal(string name)
    {
        Name = name;
    }
    public string Name {get; set;}
    public abstract string Work();
}
class Dog : Animal
{
    public Dog(string name) : base(name)
    {
    }
    public override string Work()
    {
        return "I bark";
    }
}
class Cat : Animal
{
    public Cat(string name) : base(name)
    {
    }
    public override string Work()
    {
        return "I meow";
    }
}
```

（注：我根据图 10-33 和 10-34 的上下文重构了 Dog 和 Cat 缺失的逻辑使代码能够运行，因为 OCR 文本被截断了。）

**图 10-37** Employee, Animal 和 Dog 类

图 10-35 显示了创建 DemoAnimals 程序的另一种方式。在这个版本中，Dog 和 Cat 对象被传递给一个接收 Animal 参数的方法。输出与图 10-34 相同。`Name` 属性和 `Speak()` 方法以多态方式运行，对每个对象类型采取适当的操作。

# 第 10 章 继承简介

## 两个真相和一个谎言

## 创建和使用接口

- 1. 接口是方法（可能还有其他成员）的集合，只要该类提供了对接口抽象定义的重写，它就可以被任何类使用。
- 2. 抽象类和接口的区别在于，抽象类中的所有方法都是抽象的，但接口可以包含非抽象方法。
- 3. 一个类只能继承一个基类，但它可以实现任意数量的接口。

![](img/b0a31988f44670d0728c4f372d8dab77_495_0.png)

## 使用扩展方法

在编写 C# 程序时，有时你希望某个类有一个对你有用的额外方法。如果你创建了原始类，你有两个选择：

- 你可以修改现有类，包含新的实用方法。
- 你可以从现有类派生一个子类，并为它提供一个新方法。

然而，有时类是由别人创建的，你可能不被允许修改或扩展它们。当然，你可以创建一个包含你新方法的完全新类，但这将重复许多在创建第一个类时已经完成的工作。在这些情况下，最佳选择是编写扩展方法。你可以为任何类型编写**扩展方法**。扩展方法是在 C# 3.0 中引入的。

程序员有时会在类头中将类定义为密封的（sealed），例如 `sealed InventoryItem`。**密封类**不能被扩展。例如，内置的 `String` 类就是一个密封类。

例如，你在整本书中一直预编写的 `Int32` 类来声明整数。假设你在一家经常使用账户号码的公司工作，该公司决定为每个账户号码增加额外的数字。为了简单起见，假设所有账户号码都是两位，新的第三位数字应该是前两个数字之和的最右侧数字。你可以通过创建一个名为 `AccountNumber` 的类来处理这个问题，包含一个产生额外数字的方法，并将应用程序中每个客户账户的实例重新定义为 `AccountNumber` 对象。然而，如果你已经有很多将账户定义为整数的应用程序，你可能更喜欢创建一个扩展 `Int32` 的扩展方法。

在第 2 章中，你学过 C# 内置类型（如 `int`）是 `System` 命名空间中类的别名，例如 `Int32`。

当组织为账户号码增加额外数字时，这些额外数字被称为校验位（check digits）。校验位有助于确保账户号码和其他数字中的所有数字都输入正确。校验位使用不同的公式计算。如果用于计算校验位的数字错误，那么生成的校验位很可能也是错误的。

图中包含一个扩展 `Int32` 类的方法。扩展方法中的第一个参数指定要扩展的类型，并且必须以关键字 `this` 开头。例如，`AddCheckDigit()` 方法中的第一个（在此情况下也是唯一的）参数是 `this int num`，如图中阴影所示。在图 10-40 的 `AddCheckDigit()` 方法中，通过除以 10 并取结果整数从两位账户号码中提取第一位数字，通过取余数提取第二位数字。将这两个数字相加，并从方法返回该和的最后一位数字。例如，第一个变成 4，第二个变成 9，第三个变成 13 的最后一位，即 3。然后将原始数字 (49) 乘以 10 并加上第三位数字，得到 493。

```csharp
public static int AddCheckDigit(this int num)
{
    int first = num / 10;
    int second = num % 10;
    int third = (first + second) % 10;
    int result = num * 10 + third;
    return result;
}
```

**图 10-40** AddCheckDigit() 扩展方法

扩展方法必须是静态的，并且必须存储在静态类中。例如，图 10-41 中的 `DemoExtensionMethod` 程序显示了一个在类头阴影部分声明为静态并使用扩展方法的应用程序。静态方法 `AddCheckDigit()` 的用法就像它是 `Int32` 类的实例方法一样。

```csharp
using System;

static class DemoExtensionMethod
{
    static void Main()
    {
        int accountNum = 49;
        int resultNum = accountNum.AddCheckDigit();
        Console.WriteLine("Original number: {0}", accountNum);
        Console.WriteLine("Check digit: {0}", resultNum % 10);
        Console.WriteLine("Resulting number: {0}", resultNum);
    }
}
```

**图 10-41** 扩展方法的执行

# 识别 GUI 中的继承

- 创建或使用新派生类的程序员已经理解了基类是如何运作的，因此学习新类特征所需的时间减少了。
- 当你在 C# 中创建派生类时，基类的源代码不会被更改。因此，基类保持了它的完整性。
- 不打算实例化且仅包含静态成员的类被声明为静态类（static classes）。你不能扩展静态类。例如，`System.Console` 就是一个静态类。

当你考虑类时，你需要考虑它们之间的共性，然后就可以根据这些共性创建用于继承的基类。当你看到自己的超类被他人扩展时，你甚至可能会获得职业上的回报。

![](img/b0a31988f44670d0728c4f372d8dab77_500_0.png)

> 错误的语句是 #3。派生类的创建者节省了测试时间，因为基类代码已经过测试，并且可能在各种情况下被使用；换句话说，基类代码是可靠的。

## 章节总结

- 你在面向对象编程语言中创建的类可以从现有类继承数据和方法。使用继承的能力使得程序更容易编写、更容易理解，并且更不容易出错。作为继承基础的类被称为基类（base class）、超类（superclass）或父类（parent class）。当你创建一个继承自基类的类时，它被称为派生类（derived class）、扩展类（extended class）、子类（subclass）或子类（child class）。
- 当你创建一个另一个类的扩展或子类时，你在派生类名和它的基类名之间使用单个冒号。子类继承父类的所有方法、属性和字段。继承仅以单方向运行——从父类继承，反之则不然。
- 如果你可以在类外部访问私有数据，信息隐藏原则就会被破坏。然而，当你从派生类访问父类数据时，你使用 `protected` 关键字声明类字段，这在 `public` 和 `private` 访问之间为你提供了一个中间级别的安全保护。
- 当你声明一个与其父类内具有相同名称和参数的类方法时，你重写（override）了该类方法，并允许你的类对象表现出多态行为。当派生类重写了类成员但你想访问父类版本时，你可以使用 `base` 关键字。
- 每个派生类对象都是“是”（is a）该派生类和基类的特定实例。因此，你可以将派生类对象赋值给其任何一个基类类型的对象。当你这样做时，C# 允许从派生类到基类的隐式转换。
- 你在 C# 中创建的每个类都继承自一个名为 `Object` 的单类。由于所有类都继承自 Object 类，因此所有类都继承了四个类公共实例方法：`Equals()`、`GetHashCode()`、`GetType()` 和 `ToString()`。
- 当实例化一个子类的成员对象时，基类的构造函数首先执行，然后执行派生类的构造函数。
- 抽象类（abstract class）是你无法从中创建具体对象，但可以从其继承的类。通常，抽象类包含抽象方法；抽象方法没有方法体。任何继承自包含抽象方法的类必须通过为该抽象方法提供体（实现）来重写该抽象方法。
- 接口（interface）提供了多继承的替代方案。与抽象类一样，接口是方法（以及其他成员）的集合，只要类定义了要实现接口的抽象定义，任何类都可以使用它。在抽象类内部，某些方法可以是抽象的，而另一些则不需要。在接口内部，所有方法都是抽象的。一个类只能继承一个抽象类，但它可以实现任意数量的接口。
- 扩展方法（Extension methods）是你可以编写并添加到任何类型的方法。它们是静态方法，但它们的运行方式像实例方法。它们的参数列表以 `this` 关键字开头，并跟在被操作的数据类型之后。
- 扩展方法是你可以编写并添加到任何类型的方法。它们是静态方法，但它们的运行方式像实例方法。它们的参数列表以 `this` 关键字开头的。

## 核心术语

- 继承是将通用的知识应用到更具体的类上。
- 统一建模语言 (UML) 图表是图形化工具。
- 基类是作为基础的类。
- 抽象类是你无法从中创建具体对象的类。
- 子类是派生类。
- 派生类或扩展类是子类。
- 超类是父类。
- 父类是基类。
- 子类是派生类。
- `protected` 访问在 `public` 和 `private` 之间提供中间级别的安全保护。
- `base` 关键字用于访问父类版本。
- `override` 关键字用于重写方法。
- 多态性允许类对象表现出不同行为的能力。
- 隐式转换是从派生类到基类的转换。
- 构造函数的执行顺序是基类先执行，派生类后执行。
- 抽象方法没有方法体。
- 接口是方法（以及其他成员）的集合。
- 扩展方法是静态方法，但运行方式像实例方法。
- 静态类不能被扩展。
- 具体类是用来创建实例的。
- 抽象类是你无法从中创建具体对象的。
- 多继承是允许从多个类继承。
- 接口只要类定义了要实现接口的抽象定义，任何类都可以使用。
- 继承是基类。
- 派生类是子类。
- 派生类是扩展的类。
- 派生类是父类的扩展。
- 扩展方法是你可以用来编写并添加到任何类型的方法。
- 继承是基类。

## 复习题

1. 特定类型通过继承假设通用类的特征

   a. 多态   c. 继承

   b. 封装  d. 结构

2. 在创建新类时使用继承的以下哪项不是好处？

   a. 因为不需要创建父类中已有的字段和方法。
