
继承链中位于具有新修饰符成员之前的部分。如果继承链仅包含两个类，基类中的成员将表现得好像派生类没有声明任何方法一样（如果派生类实现覆盖了基类成员）。虽然编译器会报告在输出 7.2 或输出 7.3 中显示的警告，但如果既未指定 `override` 也未指定 `new`，则默认假定为 `new`，从而保持所需的版本安全性。

请以清单 7.14 为例。其输出见输出 7.4。

### 清单 7.14: `override` 与 `new` 修饰符

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

**输出 7.4**

> SuperSubDerivedClass  
> SubDerivedClass  
> SubDerivedClass  
> BaseClass

产生这些结果的原因如下：

-   **SuperSubDerivedClass**: `SuperSubDerivedClass.DisplayName()` 显示 `SuperSubDerivedClass`，因为不存在派生类，因此没有重载。
-   **SubDerivedClass**: `SubDerivedClass.DisplayName()` 是用于覆盖基类虚成员的最派生成员。`SuperSubDerivedClass.DisplayName()` 因其具有 **new** 修饰符而被隐藏。
-   **SubDerivedClass**: `DerivedClass.DisplayName()` 是虚方法，而 `SubDerivedClass.DisplayName()` 是用于覆盖它的最派生成员。与之前一样，`SuperSubDerivedClass.DisplayName()` 因具有 **new** 修饰符而被隐藏。
-   **BaseClass**: `BaseClass.DisplayName()` 未重新声明任何基类成员，且它不是虚方法；因此，它被直接调用。

就 CIL 而言，**new** 修饰符对编译器生成的语句没有影响。然而，“new” 方法会导致在该方法上生成 **newslot** 元数据属性。从 C# 的角度来看，其唯一的效果是消除否则会出现的编译器警告。

## sealed 修饰符

正如可以使用 `sealed` 修饰符防止类继承一样，虚成员也可以被标记为 `sealed`（参见清单 7.15）。这种方法可以防止子类覆盖在继承链更上方最初被声明为 `virtual` 的基类成员。当子类 B 覆盖了基类 A 的成员，然后需要防止在子类 B 之下进行任何进一步的覆盖时，就会出现这种情况。

### 清单 7.15: 密封成员

```csharp
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

在此示例中，在类 B 的 `Method()` 声明上使用 `sealed` 修饰符可以防止类 C 覆盖 `Method()`。

一般来说，将类标记为 `sealed` 很少见，且仅应保留在那些有强烈理由支持此类限制的情况中。事实上，保持类型未密封的趋势越来越强烈，因为单元测试已成为主流，以支持使用模拟（测试替身）对象创建代替真实实现。一种可能允许密封类的场景是，当密封单个虚成员的成本超过了保持类未密封的好处时。然而，更针对性地密封单个成员——也许是因为基础实现中存在某些依赖关系以确保正确行为——可能更可取。

## base 成员

在选择覆盖某个成员时，开发人员通常希望调用基类中的该成员（参见清单 7.16）。

### 清单 7.16: 访问基类成员

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

在清单 7.16 中，InternationalAddress 继承自 Address 并实现了 ToString()。要调用父类的实现，请使用 base 关键字。其语法与此几乎相同，包括支持将 base 用作构造函数的一部分（稍后讨论）。

附带一提，在 Address.ToString() 实现中，你必须进行覆盖，因为 ToString() 也是 object 的成员。任何用 override 标记的成员都会自动被指定为虚方法，因此额外的子类可以进一步特化其实现。

> **注意**
> 任何用 override 标记的方法都是自动变为虚方法的。只有当基类方法是虚方法时，才能被覆盖，因此覆盖的方法也是虚方法。

## 构造函数

在实例化派生类时，运行时首先调用基类的构造函数，以确保基类的初始化不会被绕过。然而，如果基类没有可访问的（非私有的）默认构造函数，则不清楚如何构造基类；反过来，C# 编译器会报告错误。

为了避免因缺少可访问的默认构造函数而导致的错误，程序员需要在派生类构造函数头中明确指定要运行哪个基类构造函数（参见清单 7.17）。

### 清单 7.17: 指定调用的基类构造函数

```csharp
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

通过在代码中识别基类构造函数，你让运行时知道在调用派生类构造函数之前应该调用哪个基类构造函数。

## 抽象类

到目前为止的许多继承示例都定义了一个名为 `PdaItem` 的类，该类定义了 Contact、Appointment 等类型对象所共有的方法和属性，这些类型对象派生自 PdaItem。然而，PdaItem 本身并不打算被实例化。单独的 PdaItem 实例没有意义；只有当它被用作基类时，它才有意义——用于在派生自它的一组数据类型之间共享默认方法实现。这些特征表明 PdaItem 需要是一个抽象类，而不是一个具体类。抽象类专为派生而设计。除了实例化一个从其派生的类的情况下，不可能实例化抽象类。非抽象且可以直接实例化的类是具体类。

### 初学者主题

#### 抽象类

抽象类代表抽象实体。它们的抽象成员定义了从抽象实体派生的对象应包含的内容，但不包含实现。通常，抽象类中的许多功能都是未实现的。然而，在一个类成功从抽象类派生之前，它需要提供其抽象基类中抽象方法的实现。

要定义抽象类，C# 要求类定义具有 abstract 修饰符，如清单 7.18 所示。

### 清单 7.18: 定义抽象类

```csharp
// Define an abstract class
public abstract class PdaItem
{
    public PdaItem(string name)
    {
        Name = name;
    }

    public virtual string Name { get; set; }
}
```
