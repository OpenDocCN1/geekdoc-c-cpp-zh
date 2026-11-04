
因此，Distance 方法无法以栈分配内存的固定布局来编写。解决此问题的方法是把参数放到别处，例如将参数存储在托管堆上。但等一下，那我们最初为什么要有结构体呢？确实，结构体的主要优势之一是其轻量、栈分配、固定大小的特性。允许子类型化会破坏这一点。

因此，下面的代码将无法编译，并指出接口列表中的 Point2D 不是接口：

```csharp
struct Point2D
{
    int x, y;
}
```

```csharp
struct Point3D : Point2D
{
    int z;
}
```

冒号后部分的命名法对于类和结构体不同。前一种情况称为“类基规范”。后一种情况称为“接口列表”，因为如前所述，base 一词在此上下文中没有意义。

## 阻止继承

允许继承在应用程序编程接口（API）设计方面带来了极大的灵活性。同时，这也给基类的设计者带来了重大责任。如果基类方法的行为发生变化，可能会破坏子类型。如果使用虚方法，情况尤其如此，你将在后面看到。

为避免这类责任，可以使用 sealed 关键字将类标记为不可继承。这样做可以阻止任何人从该类继承：

```csharp
sealed class Student : Person
{
    ...
}
```

```csharp
class GraduateStudent : Student // fails to compile
{
}
```

图 14.8 显示了这种情况下编译器发出的错误。后面你将看到如何将 sealed 关键字应用于成员。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_695_0.png)

图 14.8 接口的多重继承。

## 权衡之举

决定在类上使用 sealed 关键字有点像一种权衡。如果这样做，你就摆脱了未来兼容性保证的部分责任。同时，你也限制了该类型使用者的灵活性。

## 隐藏基类成员

有时，通过在子类中引入同名成员来隐藏基类成员是很有用的。毕竟，在定义子类时，你无法控制基类作者所选择的名称。如果子类上要引入的新成员的最佳名称恰好与基类上的某个成员名称冲突，就可以使用隐藏。后面在“接口”一节中，你将看到在实现接口时如何出现类似情况。

下面的示例说明了我们所说的实例成员和静态成员的情况。尽管这里只展示了方法，但其他成员类型也同样适用。

```csharp
class Bar
{
    public void Foo() { Console.WriteLine("Bar.Foo"); }
    public static void Qux() { Console.WriteLine("Bar::Qux"); }
}

class Baz : Bar
{
    public void Foo() { Console.WriteLine("Baz.Foo"); }
    public static void Qux() { Console.WriteLine("Baz::Qux"); }
}
```

要了解前面代码中会发生什么，请考虑下面这段代码：

```csharp
Bar bar = new Bar();
bar.Foo();
Baz baz = new Baz();
baz.Foo();
Bar bazAsBar = baz;
bazAsBar.Foo();
```

这段代码将打印 Bar.Foo、Baz.Foo 和 Bar.Foo。第二个和第三个输出都值得关注。根据变量的静态类型，会调用不同的 Foo 方法。事实上，编译器已根据该类型选择了要调用的方法。你将看到使用 virtual 修饰符时情况有何不同，从而产生虚拟分派。

注意我们如何使用 bazAsBar 来示例 OOP 的多态特性。这里，我们将一个派生程度更高的类型的对象赋给一个派生程度较低的类型的变量。也就是说，凡是需要 Bar 的地方，我们也可以传入更专用的 Baz。

查看 Baz 的声明时，可能不会立即明显看出 Foo 确实在隐藏一个基类成员。Baz 实现中的代码也可能调用 Foo，并认为这会调用基类成员。但只要有人在该类型上放一个新的 Foo 方法，隐藏继承来的那个，那段代码的含义就会开始改变。为防止此类意外，编译器会发出警告，告知你引入了命名冲突。图 14.9 显示了这一点，并建议了一种解决方案（将 new 关键字用作方法上的修饰符）：

```csharp
class Baz : Bar
{
    public new void Foo() { Console.WriteLine("Baz.Foo"); }
    public new static void Qux() { Console.WriteLine("Baz::Qux"); }
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_696_0.png)

图 14.9 C# 编译器关于可能发生非有意隐藏的警告。

## new 关键字的三种含义

自 C# 2.0 起，new 关键字可用于三个地方。最广为人知的是在表达式上下文中创建给定类型的新实例，通常调用构造函数。（对于委托，情况要复杂一些。）new 关键字的第二个使用位置是隐藏，这在 C# 1.0 中也可用。这里，new 关键字用作修饰符。

随着 C# 2.0 引入泛型，new 关键字被重新用于允许声明泛型约束。我们稍后会讨论泛型和约束，但下面这段代码片段可以让你先睹为快：

```csharp
class Factory<T> where T : new()
{
    // Code is allowed to do new T()
}
```

这里，泛型类型 Factory<T> 无法使用未定义默认构造函数的类型作为类型参数来构造。

new 修饰符只是用于声明意图，并承认以这种方式编写代码可能带来的细微问题。要从内部调用基类成员，可以使用 base 关键字。对于静态成员，使用类型名限定来指示目标成员：

```csharp
class Bar
{
    public void Foo() { Console.WriteLine("Bar.Foo"); }
    public static void Qux() { Console.WriteLine("Bar::Qux"); }
}

class Baz : Bar
{
    public void Foo() { base.Foo(); Console.WriteLine("Baz.Foo"); }
    public static void Qux() { Bar.Qux(); Console.WriteLine("Baz::Qux"); }
}
```

从外部，你可以使用强制转换来指示要操作哪个静态类型，从而使编译器选择预期的方法：

```csharp
static void Main()
{
    Baz baz = new Baz();
    baz.Foo();
    ((Bar)baz).Foo();  // calls base one

    Bar bazAsBar = baz;
    bazAsBar.Foo();
    ((Baz)bazAsBar).Foo();  // calls derived one
}
```

当我们在“多态与虚拟成员”一节中讨论虚方法时，你将了解到 new 和 override 修饰符如何互斥。

### 受保护的可访问性

到目前为止，在解释继承时，我们处理的是可公开访问的成员。然而，还存在一种更细粒度的可访问性级别，称为 *protected*，可与继承和 OOP 结合使用。

public 成员对全世界可见，无论在程序集内部还是外部，而 private 成员仅在声明类型内部（包括嵌套类型）可见。由于类型层次结构建立了“类型家族”，一个相应可访问的级别似乎很有吸引力。这就是 protected 的作用：它允许声明类型中的代码以及派生类型中的代码访问该成员。你在我们开头的 Counter 探索中已经看到了这样的示例：

```csharp
public class Counter
{
    public int Count { get; protected set; }
}
```

在此示例中，Count 属性可从任何位置读取（public），而设置器仅可用于 Counter 或任何子类中的代码：

```csharp
public class ResettableCounter : Counter
{
    public void Reset()
    {
        base.Count = 0;  // base can be omitted
    }
}
```

图 14.10 展示了可访问性，箭头表示“可访问”关系。internal 可访问性级别将在第 25 章“程序集与应用程序域”中讨论程序集时解释。
