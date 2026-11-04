
## 大对象堆

完全坦白地说，我应该指出托管堆上还有第四个空间，称为大对象堆（LOH）。它为大小为 85,000 字节或更大的对象提供空间。这些对象不受基于代的回收机制约束，因为认为频繁移动它们的代价太高。典型示例包括已加载到内存中的图像。

## 装箱

.NET 类型系统做出的核心设计选择之一，是对值类型和引用类型采用统一视图。这样一来，每个类型都派生自所有类型的“母亲”：System.Object。尤其是在泛型出现之前的时代，这有几个优点，因为您可以定义通用数据结构（例如列表）来容纳任意类型的对象：

```
public class ArrayList
{
    private object[] items;
    ...
}
```

在 Java 等语言中，没有这种统一，要求用户跳过看似人为设置的障碍，把（相当于）值类型的对象打包进某个“盒子”，然后才能用在期望 Object 类型实例的地方：

```
// How things would look in Java, requiring explicit boxing.
Object number = new Integer(42);
```

与 C 和 C++ 等非托管语言相比，.NET 平台试图抽象掉以内存为中心的设计选择，例如使用类型的开发人员原本不得不做出的栈分配和堆分配。对象的分配位置仅取决于其类型，而不取决于其用途。这与例如 C++ 形成直接对比，在 C++ 中，人们既可以使用 new 关键字在堆上分配对象，也可以在栈上分配对象。

事实上，可以公允地说，即使在 .NET 上使用栈来分配值类型对象，也很大程度上只是一个实现细节。使用栈进行值类型分配的最大优势之一是它使释放变得简单。只需降低栈的高水位标记（例如从方法返回时），就可以释放位于栈顶的对象。因为没有人能引用那些单元（也就是说，在行为良好且经过验证的程序中；参见图 9.9），所以这样做是安全的。

在这个统一类型系统（就值类型与引用类型而言）的世界中，您认为类型继承层次结构的根（即 System.Object）应该具有什么特征？它必须是引用类型还是值类型？如果不深入讨论运行时的实现细节，这个问题没有简单答案。可以说，将 System.Object 设为引用类型，并让值类型通过一个受到运行时特殊处理的 System.ValueType 派生自它，会更方便。下面这段代码可用于可视化某个值类型（例如 System.Int32）所涉及的继承层次结构：

```
int x = 42;

var int32 = x.GetType();
Console.WriteLine(int32);

var valueType = int32.BaseType;
Console.WriteLine(valueType);

var @object = valueType.BaseType;
Console.WriteLine(@object);

var nothing = @object.BaseType;
Console.WriteLine(nothing == null ? "Root of hierarchy" : "Oops*");
```

## 反射

前面的代码片段使用了一种称为反射的运行时设施，它允许我们在运行时查看对象的类型及其所有成员。我们将在第 21 章“反射”中稍后讨论反射的使用。现在，只需查看 GetType 和 BaseType 调用的返回类型，即 System.Type。此类型充当类型的描述符。System.Type 的实例描述一个类型。它可以比作数据库系统中的元数据目录表，例如，这些表反映了表上定义的列。

因为 System.Object 是引用类型，这种对象的接收方会希望访问堆以获取封装的数据。然而，因为值类型派生自此基类型，似乎存在一个问题：

```
Bar(42);
...

void Bar(object x)
{
    // Use x one way or another
}
```

这里，Bar 方法期望一个静态类型为 System.Object 的参数，因此在 Bar 方法内部使用此对象的代码会在堆上查找该对象。本质上，System.Object 是托管代码中类似于指针的东西。然而，如果我们向它传递一个 Int32 值 42，这是否意味着要查看堆中的地址 42？显然，要使前面的代码正常工作，还缺少某些东西。相反，下面的代码片段不存在这个问题，因为接收端看到传入的 Int32 具有该特定类型：

```
Foo(42);
...

void Foo(int x)
{
    // Use x one way or another
}
```

换言之，有一种约定：值类型参数必须位于栈上。（调用方将它们压入栈，被调用方在栈上找到它们。）但在第一个示例中，接收引用类型参数意味着要在堆上查找。图 9.13 展示了将一个值（它仅仅是不透明的位序列）当作引用来错误处理，会如何违反内存安全和类型安全。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_509_0.png)

图 9.13 将值类型当作引用会违反类型安全。

为了解决这个问题，运行时有一种称为装箱（以及反向操作称为拆箱）的机制，以这样的方式传递值类型对象：可以通过引用的视角安全地查看它。为此，它基本上将该值“装箱”到一个堆分配的单元中，并标记类型信息。只有当值类型的实例要被当作 System.Object 处理时，才需要发生这种情况。要反向转换，单元的内容可以传回栈，直接作为值类型使用。

为了便于说明，编译那个调用 Bar 的小代码片段，并在 ILDASM 中查看。为了也展示拆箱，将接收到的参数强制转换回 int，如下所示：

```
class Box
{
    static void Main()
    {
        Bar(42);
    }

    static void Bar(object value)
    {
        // For some mysterious reason, we know we'll always
        // get an Int32 through the value parameter.
        int a = (int)value;
    }
}
```

图 9.14 显示了为 Main 方法生成的代码。如您所见，编译器发出了一个 box 指令，将 int32 值包装在堆分配的对象中，以确保接收端可以安全地访问该对象。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_510_0.png)

图 9.14 值类型对象在调用 Bar(object) 之前被装箱。

在接收端，由于将 object 类型的参数强制转换为 Int32，会发生相反的操作。此时，整数值需要传回栈，这由 unbox 操作完成，如图 9.15 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_511_0.png)

图 9.15 拆箱将堆分配的装箱内容传回栈。

整个机制总结在图 9.16 中。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_511_1.png)

图 9.16 对之前已装箱的值进行拆箱。

装箱最具吸引力的方面之一也是其主要缺点。因为整个装箱和拆箱过程对开发人员是透明的（除了强制转换，它看起来就像任何其他普通强制转换），所以根本不清楚正在发生堆分配。在某些情况下，这可能导致性能欠佳，通常是在与大量非泛型集合一起使用时：

```
var lst = new ArrayList();
for (int i = 0; i < 100000; i++)
    lst.Add(i);
```

下面展示了一个很好的例子，说明处理可变值类型时可能出现的问题：

```
using System;

class Program
{
    static void Main()
    {
        var kid = new Kid();
        Console.WriteLine(kid.Location.X + ", " + kid.Location.Y);
        kid.Location.X = 3;
        kid.Location.Y = 4;
        Console.WriteLine(kid.Location.X + ", " + kid.Location.Y);
    }
}

class Kid
{
    public Point Location { get; set; }
}

struct Point
{
    public int X { get; set; }
    public int Y { get; set; }
}
```

您预期结果会是什么？让我们来看一看。由于运行时对字段进行零初始化，坐标的初始输出应全为零。有趣的部分发生在 Main 方法的第三行和第四行。因为我们试图移动对象，所以我们检索原始的 Location 对象，其类型为 Point。因为此类型是结构体，所以它按值复制。换句话说，我们刚刚得到了 (0, 0) 点的局部副本，现在将尝试修改它：

```
// How line 3 would be translated
_temp = kid.Location; // Oops, this creates a copy
_temp.X = 3;
// How line 4 would be translated
_temp = kid.Location; // Again, a copy is made
_temp.Y = 4;
```

如果这段代码能够正常编译，那么 kid 的位置根本不会改变，因为除了该点的局部副本之外，什么都没有改变。幸运的是，C# 编译器会阻止您犯这个错误：
