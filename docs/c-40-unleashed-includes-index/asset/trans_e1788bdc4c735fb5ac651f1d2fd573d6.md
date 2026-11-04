
enable the use of the Convert class with your type, there's little incentive to bother providing an implementation.

## TypeConverter

在类型转换之上提供了一种泛化，由定义在 System.ComponentModel 命名空间中的 TypeConverter 类提供。它的目标是为设计器和运行时库提供处理转换的手段。这通常与 WPF 等 UI 框架一起使用，其中转换的概念为 XAML 语言所知。例如，要指定一个 Point，你可以写成 "3,4" 字符串，它会被转换为 X 坐标和 Y 坐标分别为 3 和 4 的 Point。

TypeConverter 基类型提供了一组可重写的虚方法。这些方法包括 CanConvertFrom、CanConvertTo、ConvertFrom 和 ConvertTo，以及一些很少被重写的方法。下面展示了一个 Point 类型的类型转换器的示例：

```csharp
class PointConverter : TypeConverter
{
    public override bool CanConvertFrom(ITypeDescriptorContext context,
        Type sourceType)
    {
        if (sourceType == typeof(string))
            return true;
        return base.CanConvertFrom(context, sourceType);
    }

    public override bool CanConvertTo(ITypeDescriptorContext context,
        Type destinationType)
    {
        if (destinationType == typeof(string))
            return true;
        return base.CanConvertTo(context, destinationType);
    }

    public override object ConvertFrom(ITypeDescriptorContext context,
        System.Globalization.CultureInfo culture, object value)
    {
        if (value == null)
            throw base.GetConvertFromException(value);

        var s = value as string;
        if (s != null)
        {
            double x, y;
            string[] parts = s.Split(',');

            if (parts.Length != 2 || !double.TryParse(parts[0], out x)
                || !double.TryParse(parts[1], out y))
                throw base.GetConvertFromException(value);
            return new Point(x, y);
        }
        return base.ConvertFrom(context, culture, value);
    }

    public override object ConvertTo(ITypeDescriptorContext context,
        System.Globalization.CultureInfo culture, object value,
        Type destinationType)
    {
        if (value is Point && destinationType == typeof(string))
            return ((Point)value).ToString();

        return base.ConvertTo(context, culture, value, destinationType);
    }
}
```

要为我们的 Point 类型启用类型转换器，我们必须使用自定义特性来注册它：

```csharp
[TypeConverter(typeof(PointConverter))]
struct Point
{
    ...
}
```

通过放置此特性，(UI) 设计器将能够找到一个转换器，用于将用户输入转换为 Point 类型，反之亦然。我们这样的实现存在于 WPF 的 System.Windows 命名空间中定义的 Point 类型（以及 Windows Forms 使用的 System.Drawing 中的 Point）。图 13.9 显示了另一种转换器类型的用法，它处理画刷，允许使用字符串指定它们。画刷是对绘制某些表面的方式的抽象，可以是纯色，如此处所示。

## Chapter 14: Object-Oriented Programming

**IN THIS CHAPTER**

- The Cornerstones of Object Orientation 643
- Inheritance for Classes 657
- Protected Accessibility 669
- Polymorphism and Virtual Members 670
- Abstract Classes 683
- Interfaces 686

由于你已经熟悉构成类和结构体的各种成员，现在你可以再提升一个层次，建立类之间的关系。这是面向对象编程所体现的众多方面之一。

在深入研究面向对象的语言特定细节之前，你首先学习这种编程范式的三大支柱：封装、继承和多态。在熟悉这些概念之后，你将查看一系列使之成为可能的语言和运行时特性，包括虚方法（和 v-表）、keywords such as override, new, protected, and abstract 等关键字。最后，你将研究以抽象类和接口的形式为类型的功能建立契约的不同方式。

### The Cornerstones of Object Orientation

面向对象编程很大程度上建立在三个核心支柱之上，我们稍后会讨论。但首先，你为什么要关心？或者说，面向对象编程（OOP）旨在解决什么类型的问题？

### A Historical Perspective

随着编程艺术不断且日益试图摆脱赤裸裸的贴近机器的指令序列，更多结构化的编程方法进入了程序员的工具箱。

很明显，以寄存器、手动内存管理、有效指令排序等方面对机器状态进行低级操作，并不是编写企业级应用程序（或实际上任何超出内核或驱动程序原语最低层级的东西）的最有吸引力的方式。

编程民主化的首批进步之一是引入文本符号语言，远离原始字节序列。虽然汇编语言是一个明显的首要目标，但更高层次的结构化编程概念更具吸引力。与其处理分支语句（à la goto），为什么不能有语句并抽象掉分支逻辑？图 14.1 说明了 C 代码与其对应汇编的叠加，强调了一些被抽象掉的低级维护任务。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_673_0.png)

**FIGURE 14.1** Control flow and stack maintenance abstractions in C.

另一个常见程序员痛苦的来源是低级语言与特定机器架构绑定。你必须知道指令集、寄存器等方面的大量细节才能编写出好的代码。除了阻碍代码向其他机器移植外，事情很容易出错。此外，对预期逻辑的任何微小更改都可能对代码的其余部分造成巨大影响。例如，向例程添加单个参数可能需要将寄存器溢出到栈分配中。过程式编程的需求变得明显。这个概念大致对应于 C# 和 CLR 中方法和方法调用的概念。额外的间接层被放置在其中。

虽然这样工作是没问题的，但我们刚刚在应用程序中打开了一个大漏洞，因为除了 Inc 和 Dec 之外的代码也可以操作共享的整数全局变量。

这让我们非常接近面向对象的一个支柱，即将状态和操作封装在逻辑单元中的能力，被称为类。事实上，前面的代码遭受的问题不仅仅是全局状态变量的暴露。因为它是全局的（并且是静态的），所以不能有两个或多个计数器在各自的计数器值上操作。这引入了这些类的实例的需求。在 C++ 中，一种最早的真正主流工业级面向对象语言中，我们会写如下内容：

```cpp
class Counter {
    int id, i;
public:
    Counter();
    void Inc();
    void Dec();
};

Counter::Counter() {
    static int n = 0;
    id = n++;
    i = 0;
}

void Counter::Inc() {
    printf("%d -> %d\n", id, ++i);
}

void Counter::Dec() {
    printf("%d -> %d\n", id, --i);
}

void main() {
    Counter *c1 = new Counter();
    Counter *c2 = new Counter();
    c1->Inc();    // 1
    c2->Dec();    // -1
    c2->Inc();    // 0
    c1->Inc();    // 2
    c1->Dec();    // 1
    c2->Inc();    // 1
}
```

忽略类定义与其成员实现之间的分离，这是 C++ 的复杂性之一（通常与头文件概念一起使用）。更重要的是，每个 Counter 都有实例级状态用于其标识符（每个计数器的唯一编号，由构造函数维护），以及当前计数器的值。这种状态不再泄漏到包含类实例的边界之外，这实现了封装。此外，计数器的操作不再是全局函数，而是变成了与类关联的方法。

### Encapsulation

即使之前的讨论已经基本介绍了这个概念，让我们先把它带到 C# 的世界。封装使成员（包括用于状态的字段，以及第 11、12 和 13 章讨论的所有其他成员）能够与类型相关联。事实上，C# 不允许在类型之外定义的全局成员（即使 CLR 允许）。在这个世界里，我们的计数器看起来像这样：

```csharp
class Counter {
    private int _id, _i;
    private static int s_n;

    public Counter() {
        _id = s_n++;
    }

    public void Increment() {
        Console.WriteLine("{0} -> {1}", _id, ++_i);
    }

    public void Decrement() {
        Console.WriteLine("{0} -> {1}", _id, --_i);
    }

    public int Count
    {
        get { return _i; }
    }
}
```

我们已经从第 10 章“方法”中知道 static 和 public 等关键字的含义。我们在这里强调的只是你将成员放在类型中这一事实，在本章中它将限制为类（和接口）。要使用我们的计数器类型，我们可以通过使用 new 关键字来构造实例，这也不应该有什么新意：

```csharp
Counter c1 = new Counter();
Counter c2 = new Counter();
c1.Increment();  // 1
c2.Decrement();  // -1
c2.Increment();  // 0
```
