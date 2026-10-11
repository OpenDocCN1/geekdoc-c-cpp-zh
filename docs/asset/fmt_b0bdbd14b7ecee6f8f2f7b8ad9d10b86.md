
**输出 7.4**

> SuperSubDerivedClass  
> SubDerivedClass  
> SubDerivedClass  
> BaseClass

产生这些结果的原因如下：

- `SuperSubDerivedClass`: `SuperSubDerivedClass.DisplayName()` 显示 `SuperSubDerivedClass`，因为不存在派生类，因此没有重载。
- `SubDerivedClass`: `SubDerivedClass.DisplayName()` 是用于覆盖基类虚成员的最派生成员。`SuperSubDerivedClass.DisplayName()` 因其具有 `new` 修饰符而被隐藏。
- `SubDerivedClass`: `DerivedClass.DisplayName()` 是虚方法，而 `SubDerivedClass.DisplayName()` 是用于覆盖它的最派生成员。与之前一样，`SuperSubDerivedClass.DisplayName()` 因具有 `new` 修饰符而被隐藏。
- `BaseClass`: `BaseClass.DisplayName()` 未重新声明任何基类成员，且它不是虚方法；因此，它被直接调用。

就 CIL 而言，`new` 修饰符对编译器生成的语句没有影响。然而，“new” 方法会导致在该方法上生成 `newslot` 元数据属性。从 C# 的角度来看，其唯一的效果是消除否则会出现的编译器警告。

### sealed 修饰符

正如可以使用 `sealed` 修饰符防止类继承一样，虚成员也可以被标记为 `sealed`（参见清单 7.15）。这种方法可以防止子类覆盖在继承链更上方最初被声明为 `virtual` 的基类成员。当子类 B 覆盖了基类 A 的成员，然后需要防止在子类 B 之下进行任何进一步的覆盖时，就会出现这种情况。

#### 清单 7.15: 密封成员

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

### base 成员

在选择覆盖某个成员时，开发人员通常希望调用基类中的该成员（参见清单 7.16）。

#### 清单 7.16: 访问基类成员

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

在清单 7.16 中，`InternationalAddress` 继承自 `Address` 并实现了 `ToString()`。要调用父类的实现，请使用 `base` 关键字。其语法与此几乎相同，包括支持将 `base` 用作构造函数的一部分（稍后讨论）。

附带一提，在 `Address.ToString()` 实现中，你必须进行覆盖，因为 `ToString()` 也是 `object` 的成员。任何用 `override` 标记的成员都会自动被指定为虚方法，因此额外的子类可以进一步特化其实现。

> **注意**
> 任何用 `override` 标记的方法都是自动变为虚方法的。只有当基类方法是虚方法时，才能被覆盖，因此覆盖的方法也是虚方法。

## 构造函数

在实例化派生类时，运行时首先调用基类的构造函数，以确保基类的初始化不会被绕过。然而，如果基类没有可访问的（非私有的）默认构造函数，则不清楚如何构造基类；反过来，C# 编译器会报告错误。

为了避免因缺少可访问的默认构造函数而导致的错误，程序员需要在派生类构造函数头中明确指定要运行哪个基类构造函数（参见清单 7.17）。

#### 清单 7.17: 指定调用的基类构造函数

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

##### 抽象类

到目前为止的许多继承示例都定义了一个名为 `PdaItem` 的类，该类定义了 `Contact`、`Appointment` 等类型对象所共有的方法和属性，这些类型对象派生自 `PdaItem`。然而，`PdaItem` 本身并不打算被实例化。单独的 `PdaItem` 实例没有意义；只有当它被用作基类时，它才有意义——用于在派生自它的一组数据类型之间共享默认方法实现。这些特征表明 `PdaItem` 需要是一个抽象类，而不是一个具体类。抽象类专为派生而设计。除了实例化一个从其派生的类的情况下，不可能实例化抽象类。非抽象且可以直接实例化的类是具体类。

### 初学者主题

##### 抽象类

抽象类代表抽象实体。它们的抽象成员定义了从抽象实体派生的对象应包含的内容，但不包含实现。通常，抽象类中的许多功能都是未实现的。然而，在一个类成功从抽象类派生之前，它需要提供其抽象基类中抽象方法的实现。

要定义抽象类，C# 要求类定义具有 `abstract` 修饰符，如清单 7.18 所示。

#### 清单 7.18: 定义抽象类

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

# 示例 7.19：定义抽象成员

```csharp
public class Program
{
    public static void Main()
    {
        PdaItem item;
        // 错误：无法创建抽象类的实例
        // item = new PdaItem("Inigo Montoya");
    }
}
```

尽管抽象类不能被实例化，但这种限制只是抽象类的一个次要特征。它们的主要意义在于包含**抽象成员**。抽象成员是指没有实现的方法或属性。其目的是强制所有派生类提供实现。

请以示例 7.19 为例。

```csharp
// 定义一个抽象类
public abstract class PdaItem
{
    public PdaItem(string name)
    {
        Name = name;
    }
    public virtual string Name { get; set; }
    public abstract string GetSummary();
}

using static System.Environment;

public class Contact : PdaItem
{
    public override string Name
    {
        get
        {
            return $"{ FirstName } { LastName }";
        }
        set
        {
            string[] names = value.Split(' ');
            // 未显示错误处理
            FirstName = names[0];
            LastName = names[1];
        }
    }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Address { get; set; }
    public override string GetSummary()
    {
        return @"FirstName: " + $"{ FirstName }" + NewLine +
               $"LastName: { LastName }" + NewLine +
               $"Address: { Address }" + NewLine;
    }
    // ...
}

public class Appointment : PdaItem
{
    public Appointment(string name) :
        base(name)
    {
        Name = name;
    }
    public DateTime StartDateTime { get; set; }
    public DateTime EndDateTime { get; set; }
    public string Location { get; set; }
    // ...
    public override string GetSummary()
    {
        return $"Subject: { Name }" + NewLine +
             $"Start: { StartDateTime }" + NewLine +
             $"End: { EndDateTime }" + NewLine +
             $"Location: { Location }";
    }
}
```

示例 7.19 将 `GetSummary()` 成员定义为抽象，因此它不包含任何实现。然后代码在 `Contact` 中重写该成员并提供实现。由于抽象成员旨在被重写，因此这些成员自动被视为虚方法，不能显式声明为虚方法。此外，抽象成员不能是私有的，因为派生类将无法看到它们。

开发设计良好的对象层次结构出奇地困难。因此，在编程处理抽象类型时，您应该确保至少实现一个（最好更多）继承自该抽象类型的具体类型，以验证设计。

> **注意**
> 抽象成员必须被重写，因此它们自动是虚成员，不能显式声明为虚成员。

# 语言对比：C++ —— 纯虚函数

C++ 允许使用晦涩的符号 `=0` 定义抽象函数。这些函数在 C++ 中称为纯虚函数。然而与 C# 不同的是，C++ 不要求类本身有任何特殊声明。与 C# 的 `abstract` 类修饰符不同，当类包含纯虚函数时，C++ 中的类声明没有任何变化。

如果你没有在 `Contact` 中提供 `GetSummary()` 的实现，编译器将报告错误。

> **注意**
> 通过声明抽象成员，抽象类程序员表明，要在具体类与抽象基类（即 `PdaItem`）之间建立“是一种”关系，必须实现这些抽象成员，这些成员是抽象类无法提供适当默认实现的成员。

### 初学者主题

# 多态性

当同一成员签名在两个或更多类中的实现存在差异时，这种场景展示了一个关键的面向对象原则：**多态性**。Poly 意为“多”，morph 意为“形态”，因此多态性指的是同一签名存在多种实现。此外，由于同一签名不能在单个类内使用多次，因此该成员签名的每个实现都出现在不同的类中。

多态性的理念在于，对象本身最知道如何执行特定操作。此外，通过强制执行调用这些操作的通用方式，多态性是一种利用共性时鼓励代码重用的技术。给定多种类型的文档，每种文档类型类都知道如何最好地为其对应的文档类型执行 `Print()` 方法。因此，而不是定义一个包含 switch 语句和特殊逻辑来打印每种文档类型的单一打印方法，利用多态性你可以调用与你要打印的特定文档类型对应的 `Print()` 方法。例如，在文字处理文档类上调用 `Print()` 会按照文字处理的具体方式进行操作，而在图形文档类上调用相同的方法将产生特定于图形的打印行为。然而，给定这些文档类型，你只需调用 `Print()` 即可打印文档，无论类型如何。

将自定义打印实现从 switch 语句中移出带来许多维护优势。首先，实现出现在每种文档类型类的上下文中，而不是在远离的地方；这符合封装原则。其次，添加新的文档类型不需要更改 switch 语句。相反，新文档类型类只需实现 `Print()` 签名即可。

抽象成员旨在成为实现多态性的一种方式。基类指定方法的签名，派生类提供实现（参见示例 7.20）。

# 示例 7.20：使用多态性列出 PdaItems

```csharp
public class Program
{
    public static void Main()
    {
        PdaItem[] pda = new PdaItem[3];
        Contact contact = new Contact("Sherlock Holmes");
        contact.Address = "221B Baker Street, London, England";
        pda[0] = contact;
        Appointment appointment =
            new Appointment("Soccer tournament");
        appointment.StartDateTime = new DateTime(2008, 7, 18);
        appointment.EndDateTime = new DateTime(2008, 7, 19);
        appointment.Location = "Estádio da Machava";
        pda[1] = appointment;
        contact = new Contact("Hercule Poirot");
        contact.Address =
            "Apt 56B, Whitehaven Mansions, Sandhurst Sq, London";
        pda[2] = contact;
        List(pda);
    }
    public static void List(PdaItem[] items)
    {
        // 使用多态性实现。派生类型
        // 知道实现 GetSummary() 的具体细节。
        foreach (PdaItem item in items)
        {
            Console.WriteLine("---------");
            Console.WriteLine(item.GetSummary());
        }
    }
}
```

示例 7.20 的结果如输出 7.5 所示。

# 输出 7.5

```text
FirstName: Sherlock
LastName: Holmes
Address: 221B Baker Street, London, England
Subject: Soccer tournament
Start: 7/18/2008 12:00:00 AM
End: 7/19/2008 12:00:00 AM
Location: Estádio da Machava
FirstName: Hercule
LastName: Poirot
```
