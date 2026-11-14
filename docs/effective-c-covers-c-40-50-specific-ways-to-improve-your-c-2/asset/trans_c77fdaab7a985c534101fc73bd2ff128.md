

与原始对象相同的对象。深拷贝会创建一个新对象，同时复制所有成员变量。在拷贝中，所有引用类型都会被递归克隆。对于整数等内置类型，深拷贝和浅拷贝产生相同的结果。一种类型支持哪一种？这取决于该类型。但在同一个对象中混合使用浅拷贝和深拷贝会造成不少不一致性。当你涉足ICloneable领域时，很难抽身。通常，完全避免使用ICloneable会让类更简单。它更易于使用，也更容易实现。

任何仅包含内置类型作为成员的值类型都不需要支持ICloneable；简单的赋值比Clone()更高效地复制结构的所有值。Clone()必须对其返回值进行装箱，以便将其强制转换为System.Object引用。调用者必须执行另一次强制转换才能从装箱中提取值。你已经有足够多的事情要做了。不要编写一个仅仅复制赋值操作的Clone()函数。

包含引用类型的值类型呢？最明显的情况是包含字符串的值类型：

```
public struct ErrorMessage
{
    private int errCode;
    private int details;
    private string msg;

    // details elided
}
```

string是一个特殊情况，因为这个类是不可变的。如果你赋值一个错误消息对象，两个错误消息对象都引用同一个字符串。这不会引起与一般引用类型可能发生的任何问题。如果你通过任一引用更改msg变量，你会创建一个新的字符串对象（参见第16条）。

创建包含任意引用变量的结构的一般情况更加复杂，而且也少得多。结构的内置赋值创建一个浅拷贝，两个结构都引用同一个对象。要创建深拷贝，你需要克隆包含的引用类型，并且需要知道该引用类型通过其Clone()方法支持深拷贝。即便如此，只有当包含的引用类型也支持ICloneable，并且其Clone()方法创建深拷贝时，这才有效。

现在让我们继续讨论引用类型。引用类型可以支持ICloneable接口，以指示它们支持浅拷贝或深拷贝。你可以谨慎地添加对ICloneable的支持，因为这样做要求所有从你的类型派生的类也必须支持ICloneable。考虑这个小层次结构：

```
class BaseType : ICloneable
{
    private string label = "class name";
    private int[] values = new int[10];

    public object Clone()
    {
        BaseType rVal = new BaseType();
        rVal.Label = label;
        for (int i = 0; i < values.Length; i++)
            rVal.values[i] = values[i];
        return rVal;
    }
}
```

```
class Derived : BaseType
{
    private double[] dValues = new double[10];

    static void Main(string[] args)
    {
        Derived d = new Derived();
        Derived d2 = d.Clone() as Derived;

        if (d2 == null)
            Console.WriteLine("null");
    }
}
```

如果你运行这个程序，会发现d2的值为null。Derived类没有从BaseType继承ICloneable.Clone()，但该实现对于Derived类型不正确：它只克隆基类型。BaseType.Clone()创建一个BaseType对象，而不是Derived对象。这就是为什么在测试程序中d2为null——它不是Derived对象。但是，即使你能克服这个问题，BaseType.Clone()也无法正确复制在Derived中定义的dValues数组。当你实现ICloneable时，你强制所有派生类也实现它。事实上，你应该提供一个钩子函数，让所有派生类使用你的实现（参见第23条）。为了支持克隆，派生类只能添加值类型或实现ICloneable的引用类型作为成员变量。这是对所有派生类非常严格的限制。向基类添加ICloneable支持通常会给派生类型带来如此沉重的负担，以至于你应该避免在非sealed类中实现ICloneable。

当整个层次结构都必须实现ICloneable时，你可以创建一个抽象的Clone()方法，并强制所有派生类实现它。在这些情况下，你需要定义一种方法，让派生类能够创建基类成员的副本。这是通过定义一个受保护的拷贝构造函数来完成的：

```csharp
class BaseType
{
    private string label;
    private int[] values;

    protected BaseType()
    {
        label = "class name";
        values = new int[10];
    }

    // Used by derived values to clone
    protected BaseType(BaseType right)
    {
        label = right.label;
        values = right.values.Clone() as int[];
    }
}
```

```csharp
sealed class Derived : BaseType, ICloneable
{
    private double[] dValues = new double[10];

    public Derived()
    {
        dValues = new double[10];
    }

    // Construct a copy
    // using the base class copy ctor
    private Derived(Derived right) :
        base(right)
    {
        dValues = right.dValues.Clone()
            as double[];
    }

    public object Clone()
    {
        Derived rVal = new Derived(this);
        return rVal;
    }
}
```

基类不实现ICloneable；它们提供一个受保护的拷贝构造函数，使派生类能够复制基类部分。叶子类（都应该是sealed的）在必要时实现ICloneable。基类不强制所有派生类实现ICloneable，但它为任何想要ICloneable支持的派生类提供了必要的方法。

ICloneable确实有其用途，但它是例外而非常规。值得注意的是，当.NET Framework添加泛型支持时，并没有添加ICloneable<T>。你绝不应该为值类型添加对ICloneable的支持；改用赋值操作。当类型确实需要复制操作时，你应该为叶子类添加对ICloneable的支持。可能在需要ICloneable支持的场景中使用的基类应该创建一个受保护的拷贝构造函数。在所有其他情况下，避免使用ICloneable。

## 第33条：仅在响应基类更新时使用new修饰符

你在类成员上使用new修饰符，以重新定义从基类继承的非虚拟成员。不过，仅仅因为你能做某事，并不意味着你应该这样做。重新定义非虚拟方法会产生歧义行为。大多数开发者会看到这两段代码，并立即认为它们做的完全是同一件事，如果这两个类通过继承相关联：

```
object c = MakeObject();

// Call through MyClass reference:
MyClass c1 = c as MyClass;
c1.MagicMethod();

// Call through MyOtherClass reference:
MyOtherClass c2 = c as MyOtherClass;
c2.MagicMethod();
```

当涉及new修饰符时，情况并非如此：

```
public class MyClass
{
    public void MagicMethod()
    {
        // details elided.
    }
}
```

```
public class MyOtherClass : MyClass
{
    // Redefine MagicMethod for this class.
    public new void MagicMethod()
    {
        // details elided
    }
}
```

这种做法会导致大量开发者困惑。如果你在同一个对象上调用同一个函数，你期望执行相同的代码。更改用于调用函数的引用（标签）会改变行为，这感觉非常不对。这是不一致的。MyOtherClass对象会根据你引用它的方式表现出不同的行为。new修饰符并不会事后将非虚拟方法变成虚拟方法。相反，它允许你在类的命名空间中添加一个不同的方法。

非虚拟方法是静态绑定的。任何引用MyClass.MagicMethod()的源代码都会调用该函数。运行时不会查找在任何派生类中定义的不同版本。另一方面，虚拟函数是动态绑定的。运行时根据对象的运行时类型调用适当的函数。

