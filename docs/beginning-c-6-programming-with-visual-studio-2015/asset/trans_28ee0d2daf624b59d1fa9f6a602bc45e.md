
关键字`abstract`和`sealed`是不允许的，因为这两个修饰符在接口的上下文中都没有意义（接口不包含实现，因此不能直接实例化，并且必须可继承才有用）。

接口继承的指定方式与类继承类似。主要区别在于可以使用多个基接口，如下所示：

```
public interface IMyInterface : IMyBaseInterface, IMyBaseInterface2
{
    // Interface members.
}
```

接口不是类，因此不从System.Object继承。但是，System.Object的成员可以通过接口类型变量使用，纯粹是为了方便。此外，如前所述，不可能像类那样实例化接口。下面的“试一试”提供了一些类定义以及使用它们的代码示例。

## 试一试 定义类：Ch09Ex01\Program.cs

- 1. 创建一个名为Ch09Ex01的新控制台应用程序，并将其保存在目录C:\BegVCSharp\Chapter09中。
- 2. 按如下方式修改Program.cs中的代码：

```
using static System.Console;
namespace Ch09Ex01
{
    public abstract class MyBase {}
    internal class MyClass : MyBase {}
    public interface IMyBaseInterface {}
    internal interface IMyBaseInterface2 {}
    internal interface IMyInterface : IMyBaseInterface, IMyBaseInterface2 {}
    internal sealed class MyComplexClass : MyClass, IMyInterface {}
    class Program
    {
        static void Main(string[] args)
        {
            MyComplexClass myObj = new MyComplexClass();
            WriteLine(myObj.ToString());
            ReadKey();
        }
    }
}
```

- 3. 执行项目。图9-1显示了输出。

![](img/cf72ea860016d2d680fc085fc06f265a_218_0.png)

图9-1

## SYSTEM.OBJECT

因为所有类都继承自System.Object，所以所有类都可以访问该类的受保护成员和公共成员。因此，有必要了解一下其中有哪些可用成员。System.Object包含表9-2中描述的方法。

表9-2：System.Object的方法

| 方法 | 返回类型 | 虚拟 | 静态 | 描述 |
|---|---|---|---|---|
| Object() | N/A | No | No | System.Object类型的构造函数。由派生类型的构造函数自动调用。 |
| ~Object()（也称为Finalize()——参见下一节） | N/A | No | No | System.Object类型的析构函数。由派生类型的析构函数自动调用；不能手动调用。 |
| Equals(object) | bool | Yes | No | 将此方法调用的对象与另一个对象进行比较，如果相等则返回true。默认实现检查object参数是否引用了同一个对象（因为对象是引用类型）。如果要以不同的方式比较对象，例如比较两个对象的状态，可以重写此方法。 |
| Equals(object, object) | bool | No | Yes | 比较传入的两个对象，检查它们是否相等。此检查使用Equals(object)方法执行。如果两个对象都是null引用，则此方法返回true。 |
| ReferenceEquals(object, object) | bool | No | Yes | 比较传入的两个对象，检查它们是否引用同一个实例。 |

### 表9.2（续）

| 方法 | 返回类型 | 虚拟 | 静态 | 描述 |
|---|---|---|---|---|
| ToString() | string | Yes | No | 返回与对象实例对应的字符串。默认情况下，这是类类型的限定名称，但可以重写此方法以提供适合该类类型的实现。 |
| MemberwiseClone() | object | No | No | 通过创建新的对象实例并复制成员来复制对象。此成员复制不会导致这些成员的新实例。新对象的任何引用类型成员都引用与原始类相同的对象。此方法是受保护的，因此只能从类内部或派生类中使用。 |
| GetType() | System.Type | No | No | 以System.Type对象的形式返回对象的类型。 |
| GetHashCode() | int | Yes | No | 在需要时用作对象的哈希函数。哈希函数以某种压缩形式返回标识对象状态的值。 |

这些是.NET Framework中对象类型必须支持的基本方法，尽管你可能永远不会使用其中一些方法（或者只在特殊情况下使用它们，例如GetHashCode()）。

在使用多态时，GetType()很有用，因为它使你可以根据对象的类型对对象执行不同的操作，而不是像通常那样对所有对象执行相同的操作。例如，如果有一个函数接受object类型的参数（意味着你可以向它传递几乎任何内容），那么在遇到某些对象时，你可以执行额外的任务。结合使用GetType()和typeof（一个C#运算符，将类名转换为System.Type对象），你可以执行如下比较：

```
if (myObj.GetType() == typeof(MyComplexClass))
{
    // myObj is an instance of the class MyComplexClass.
}
```

返回的System.Type对象能够做的远不止这些，但这里只介绍这些。重写ToString()方法也非常有用，尤其是在对象的内容可以很容易地用单个人类可读字符串表示的情况下。在后续章节中你会反复看到这些System.Object方法，所以必要时你将了解更多细节。

## 构造函数和析构函数

在C#中定义类时，通常不需要定义相关的构造函数和析构函数，因为如果你不提供它们，编译器会在生成代码时自动添加。但是，如果需要，你可以提供自己的构造函数和析构函数，以便分别初始化和清理对象。

可以使用以下语法向类添加简单的构造函数：

```
class MyClass
{
    public MyClass()
    {
        // Constructor code.
    }
}
```

此构造函数与包含它的类同名，没有参数（使其成为类的默认构造函数），并且是公共的，因此可以使用此构造函数实例化类的对象（有关更多信息，请参阅第8章）。

也可以使用私有默认构造函数，这意味着不能使用此构造函数创建该类的对象实例（它是不可创建的——同样，请参阅第8章的讨论）：

```
class MyClass
{
    private MyClass()
    {
        // Constructor code.
    }
}
```

最后，可以通过提供参数以类似的方式向类添加非默认构造函数：

```
class MyClass
{
    public MyClass()
    {
        // Default constructor code.
    }
    public MyClass(int myInt)
    {
        // Nondefault constructor code (uses myInt).
    }
}
```

你可以提供无限数量的构造函数（直到内存耗尽或参数集用完，所以也许“几乎无限”更合适）。

析构函数的声明语法略有不同。.NET中使用的析构函数（由System.Object类提供）称为Finalize()，但这并不是你用来声明析构函数的名称。你不需要重写Finalize()，而是使用以下语法：

```
class MyClass
{
    ~MyClass()
    {
        // Destructor body.
    }
}
```

因此，类的析构函数使用类名（就像构造函数一样）声明，并带有波浪号（~）前缀。析构函数中的代码在垃圾回收发生时执行，使你可以释放资源。析构函数被调用后，还会隐式调用基类的析构函数，包括调用System.Object根类中的Finalize()。这种技术使.NET Framework能够确保这一点，因为重写Finalize()意味着需要显式执行基类调用，这有潜在危险（你将在下一章学习如何调用基类方法）。

### 构造函数执行顺序

如果你在类的构造函数中执行多个任务，那么将这些代码集中在一个地方会很方便，这具有与将代码拆分为函数相同的好处，如第6章所示。你可以使用方法（参见第10章）来实现这一点，但C#提供了一种很好的替代方法。你可以配置任何构造函数在执行自己的代码之前调用任何其他构造函数。

不过，首先你需要更仔细地了解默认情况下实例化类实例时会发生什么。除了有助于集中初始化代码（如前所述）之外，这本身也值得了解。在开发过程中，由于构造函数调用期间的错误，对象的行为往往与你预期的不同——通常是你没有正确实例化类的继承层次结构中的某个基类，或者没有正确地向基类构造函数提供信息。了解对象生命周期这一阶段发生的事情，可以更容易地解决这类问题。

要实例化派生类，必须先实例化其基类。要实例化该基类，必须先实例化它自己的基类，依此类推，一直回到System.Object（所有类的根）。因此，无论使用哪个构造函数来实例化类，总是会先调用System.Object.Object()。

无论你在派生类中使用哪个构造函数（默认构造函数还是非默认构造函数），除非另有指定，否则将使用基类的默认构造函数。（你将在
