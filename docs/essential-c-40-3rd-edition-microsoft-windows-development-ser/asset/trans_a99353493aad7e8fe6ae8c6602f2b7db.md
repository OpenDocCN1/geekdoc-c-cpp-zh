

## TABLE 6.1: Why the New Modifier? (Continued)

| Activity | Code |
| :--- | :--- |
| 稍后，程序员 A 添加了 Name 属性，但她没有将 getter 实现为 FirstName + " " + LastName，而是将其实现为 LastName + ", " + FirstName。此外，她没有将 virtual 用作属性，并且她在 DisplayName() 方法中使用了该属性。 | public class Person
{
    public string Name
    {
        get
        {
            return LastName + ", " + FirstName;
        }
        set
        {
            string[] names = value.Split(';');
            // Error handling not shown.
            LastName = names[0];
            FirstName = names[1];
        }
    }
    public static void Display(Person person)
    {
        // Display <LastName>, <FirstName>
        Console.WriteLine( person.Name );
    }
} |

由于 Person.Name 不是 virtual，程序员 A 期望 Display() 使用 Person 的实现，即使传入的是 Person 派生的数据类型 Contact。但是，程序员 B 期望在变量数据类型为 Contact 的所有情况下都使用 Contact.Name。（程序员 B 不会有使用 Person.Name 的代码，因为最初不存在 Person.Name 属性。）为了在不破坏任一程序员预期行为的前提下添加 Person.Name，你不能假设意图是 virtual。此外，由于 C# 要求重写成员显式使用 override 修饰符，必须假设某种其他语义，而不是允许在基类中添加成员导致派生类不再编译。

该语义是 new 修饰符，它从基类中隐藏派生类的重新声明成员。基类中的成员不再调用最派生的成员，而是调用继承链中 new 修饰符成员之前的最派生成员。如果继承链仅包含两个类，则基类中的成员将表现得好像派生类中未声明任何方法一样（如果派生实现重写了基类成员）。尽管编译器会报告输出 6.2 或输出 6.3 中显示的警告，但如果既未指定 override 也未指定 new，则将假定为 new，从而维持所需的版本安全性。

例如，请参阅清单 6.14。其输出显示在输出 6.4 中。

## 清单 6.14: override 与 new 修饰符

```
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
}
```

```
OUTPUT 6.4:

SuperSubDerivedClass
SubDerivedClass
DerivedClass
BaseClass
```

出现这些结果的原因如下。

- SuperSubDerivedClass: SuperSubDerivedClass.DisplayName() 显示 SuperSubDerivedClass，因为没有派生类，因此没有重载。
- SubDerivedClass: SubDerivedClass.DisplayName() 是重写基类 virtual 成员的最派生成员。SuperSubDerivedClass.DisplayName() 因其 new 修饰符而被隐藏。
- SubDerivedClass: DerivedClass.DisplayName() 是 virtual，而 SubDerivedClass.DisplayName() 是重写它的最派生成员。与之前一样，SuperSubDerivedClass.DisplayName() 因 new 修饰符而被隐藏。
- BaseClass: BaseClass.DisplayName() 未重新声明任何基类成员，且不是 virtual；因此，它会被直接调用。

就 CIL 而言，new 修饰符对编译器生成的语句没有影响。但是，“new”方法会导致在方法上生成 newslot 元数据属性。从 C# 角度来看，其唯一效果是删除否则会出现的编译器警告。

## sealed 修饰符

正如可以使用类上的 sealed 修饰符来防止继承一样，virtual 成员也可以被 sealed（请参阅清单 6.15）。这防止子类重写继承链中较高位置最初声明为 virtual 的基类成员。当子类 B 重写基类 A 的成员，然后需要防止在子类 B 之下进行任何进一步重写时，就会出现这种情况。

## 清单 6.15: 密封成员

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

在此示例中，在类 B 的 Method() 声明上使用 sealed 修饰符可防止 C 重写 Method()。

## base 成员

在选择重写成员时，开发人员通常希望调用基类上的成员（请参阅清单 6.16）。

## 清单 6.16: 访问基类成员

```
public class Address
{
    public string StreetAddress;
    public string City;
    public string State;
    public string Zip;

    public override string ToString()
    {
        return string.Format("{0}" + Environment.NewLine +
            "{1}, {2} {3}",
            StreetAddress, City, State, Zip);
    }
}

public class InternationalAddress : Address
{
    public string Country;

    public override string ToString()
    {
        return base.ToString() + Environment.NewLine +
            Country;
    }
}
```

在清单 6.16 中，InternationalAddress 继承自 Address 并实现 ToString()。要调用父类的实现，请使用 base 关键字。语法与此几乎相同，包括支持将 base 用作构造函数的一部分（稍后讨论）。

顺便说一句，在 Address.ToString() 实现中，你也必须重写，因为 ToString() 也是 object 的成员。任何用 override 修饰的成员都会自动指定为 virtual，因此其他子类可以进一步特殊化该实现。

## 构造函数

在实例化派生类时，运行时首先调用基类的构造函数，以免绕过基类初始化。但是，如果基类上没有可访问的（非私有）默认构造函数，则不清楚如何构造基类，C# 编译器会报告错误。

为了避免因没有可访问的默认构造函数而导致的错误，程序员需要在派生类构造函数头中显式指定要运行的基类构造函数（请参阅清单 6.17）。

## 清单 6.17: 指定要调用的基类构造函数

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
    public Contact(string name) :
        base(name)
    {
        Name = name;
    }

    public string Name { get; set; }

    // ...
}
```

通过在代码中标识基类构造函数，你可以让运行时在调用派生类构造函数之前知道要调用哪个基类构造函数。

## 抽象类

迄今为止的许多继承示例都定义了一个名为 PdaItem 的类，该类定义了 Contact、Appointment 等（均为派生自 PdaItem 的类型对象）共有的方法和属性。但是，PdaItem 本身不打算被实例化。PdaItem 实例本身没有意义；只有在用作基类（以在从中派生的一组数据类型之间共享默认方法实现）时才有意义。这些特征表明 PdaItem 需要是抽象类而不是具体类。抽象类仅用于派生。除非在实例化从中派生的类的上下文中，否则无法实例化抽象类。非抽象且可以直接实例化的类是具体类。

