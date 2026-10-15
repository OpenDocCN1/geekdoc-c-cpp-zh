

由于 `Person.Name` 不是虚的，程序员 A 会期望 `Display()` 使用 Person 的实现，即使传入的是 Person 派生的数据类型 Contact。然而，程序员 B 会期望在变量数据类型为 Contact 的所有情况下都使用 `Contact.Name`。 （程序员 B 不会有使用 `Person.Name` 的代码，因为最初并不存在 `Person.Name` 属性。）为了在不破坏任一程序员预期行为的情况下添加 `Person.Name`，你不能假设 `virtual` 是有意为之的。此外，由于 C# 要求重写成员必须显式使用 `override` 修饰符，必须假设其他语义，而不是允许在基类中添加成员导致派生类无法编译。

这种语义是 `new` 修饰符，它会将派生类中重新声明的成员隐藏起来，不让基类看到。与其调用最派生的成员，基类的成员会调用在继承链中位于带有 `new` 修饰符的成员之前的、最派生的成员。如果继承链只包含两个类，基类中的成员将表现得好像派生类上没有声明该方法一样（如果派生实现重写了基类成员）。尽管编译器会在未指定 `override` 或 `new` 时报告 Output 6.2 或 Output 6.3 中所示的警告，但此时会假设 `new`，从而保持期望的版本安全。

请考虑 Listing 6.14 作为示例。其输出显示在 Output 6.4 中。

## LISTING 6.14: override versus new Modifier

```csharp
public class Program
{
    public class BaseClass
    {
        public void DisplayName()
        {
            Console.WriteLine("BaseClass");
        }
    }

    public class DerivedClass : BaseClass
    {
        // Compiler WARNING: DisplayName() hides inherited
        // member. Use the new keyword if hiding was intended.
        public virtual void DisplayName()
        {
            Console.WriteLine("DerivedClass");
        }
    }
}
```

```
}

public class SubDerivedClass : DerivedClass
{
    public override void DisplayName()
    {
        Console.WriteLine("SubDerivedClass");
    }
}

public class SuperSubDerivedClass : SubDerivedClass
{
    public new void DisplayName()
    {
        Console.WriteLine("SuperSubDerivedClass");
    }
}

public static void Main()
{
    SuperSubDerivedClass superSubDerivedClass
        = new SuperSubDerivedClass();

    SubDerivedClass subDerivedClass = superSubDerivedClass;
    DerivedClass derivedClass = superSubDerivedClass;
    BaseClass baseClass = superSubDerivedClass;

    superSubDerivedClass.DisplayName();
    subDerivedClass.DisplayName();
    derivedClass.DisplayName();
    baseClass.DisplayName();
}
```

## OUTPUT 6.4

```
SuperSubDerivedClass
SubDerivedClass
SubDerivedClass
BaseClass
```

这些结果出现的原因如下。

- SuperSubDerivedClass: SuperSubDerivedClass.DisplayName() 显示 SuperSubDerivedClass，因为没有派生类，因此没有重载。
- SubDerivedClass: SubDerivedClass.DisplayName() 是重写基类虚成员的最派生成员。SuperSubDerived Class.DisplayName() 因其 new 修饰符而被隐藏。

- SubDerivedClass: DerivedClass.DisplayName() 是虚的，而 Sub DerivedClass.DisplayName() 是重写它的最派生成员。同样，SuperSubDerivedClass.DisplayName() 因 new 修饰符而被隐藏。
- BaseClass: BaseClass.DisplayName() 没有重新声明任何基类成员并且不是虚的；因此，直接调用它。

就 CIL 而言，new 修饰符对编译器生成的语句没有影响。然而，“new”方法会导致在方法上生成 newslot 元数据属性。从 C# 角度来看，其唯一作用是消除否则会出现编译器警告。

## sealed Modifier

正如你可以使用 sealed 修饰符防止类被继承一样，虚成员也可以被 sealed（参见 Listing 6.15）。这种方法可防止子类重写在继承链更高位置最初声明为虚的基类成员。这种情况会在子类 B 重写基类 A 的成员，然后需要防止在子类 B 之下的任何进一步重写时出现。

## LISTING 6.15: Sealing Members

```
class A
{
    public virtual void Method()
    {
    }
}
class B : A
{
    public override sealed void Method()
    {
    }
}
class C : B
{
    // ERROR: Cannot override sealed members
    // public override void Method()
    // {
    // }
}
```

在此示例中，对类 B 的 `Method()` 声明使用 `sealed` 修饰符可防止类 C 重写 `Method()`。

通常，将类标记为 sealed 很少这样做，应仅保留在有充分理由支持此类限制的情况下。事实上，随着单元测试变得突出，因为需要支持在真实实现位置创建模拟（测试替身）对象，保留类型未密封变得越来越可取。密封类可能合理的场景之一是，当密封单个虚成员的成本超过保留类未密封的好处时。然而，更有针对性地密封单个成员——也许是因为基实现中存在正确行为所需的依赖关系——可能更可取。

## base Member

在选择重写成员时，开发人员通常希望调用基类上的成员（参见 Listing 6.16）。

## Listing 6.16: Accessing a Base Member

```csharp
using static System.Environment;

public class Address
{
    public string StreetAddress;
    public string City;
    public string State;
    public string Zip;

    public override string ToString()
    {
        return $"{ StreetAddress + NewLine }"
             + $"{ City }, { State } { Zip }";
    }
}

public class InternationalAddress : Address
{
    public string Country;

    public override string ToString()
    {
        return base.ToString() +
               NewLine + Country;
    }
}
```

在 Listing 6.16 中，InternationalAddress 继承自 Address 并实现了 ToString()。要调用父类的实现，你使用 base 关键字。语法几乎与此相同，包括支持将 base 用作构造函数的一部分（稍后讨论）。

顺便说一下，在 Address.ToString() 实现中，你必须重写，因为 ToString() 也是 object 的成员。任何用 override 装饰的成员都会自动被指定为 virtual，因此额外的子类可以进一步专门化实现。

> **NOTE**
> 
> 任何用 override 装饰的方法都是自动虚的。基类方法只有在是 virtual 时才能被重写，重写方法因此也是 virtual 的。

## Constructors

实例化派生类时，运行时首先调用基类的构造函数，以便不绕过基类初始化。然而，如果基类上没有可访问的（非私有）默认构造函数，就不清楚如何构造基类；反过来，C# 编译器会报告错误。

为了避免因缺少可访问的默认构造函数而导致的错误，程序员需要在派生类构造函数头中显式指定要运行的基构造函数（参见 Listing 6.17）。

## LISTING 6.17: Specifying Which Base Constructor to Invoke

```
public class PdaItem
{
    public PdaItem(string name)
    {
        Name = name;
    }

    // ...
}

public class Contact : PdaItem
{
```

```
public Contact(string name) :
    base(name)
{
    Name = name;
}

public string Name { get; set; }
// ...
}
```

通过在代码中标识基构造函数，你让运行时知道在调用派生类构造函数之前调用哪个基构造函数。

## Abstract Classes

到目前为止的许多继承示例都定义了一个名为 PdaItem 的类，该类定义了 Contact、Appointment 等共有的方法和属性，这些类型对象派生自 PdaItem。然而，PdaItem 本身并不打算被实例化。PdaItem 实例本身没有意义；它只有在用作基类时才有意义——在派生自它的类型集合中共享默认方法实现。这些特征表明 PdaItem 需要是一个抽象类而不是具体类。抽象类仅设计用于派生。不可能实例化抽象类，除非在实例化派生自它的类的上下文中。非抽象且可以直接实例化的类是具体类。

## BEGINNER TOPIC

## Abstract Classes

抽象类代表抽象实体。它们的抽象成员定义了从抽象实体派生的对象应包含的内容，但不包括实现。通常，抽象类中的大部分功能都是未实现的。然而，在类成功派生自抽象类之前，它需要为其抽象基类中的抽象方法提供实现。

要定义抽象类，C# 要求在类定义中使用 abstract 修饰符，如 Listing 6.18 所示。

