
类型中成员的顺序对 C# 代码来说很少有意义，但在与其他语言和环境交互时可能很重要。在这些情况下，在多个部分中声明的类型中成员的顺序是未定义的。

## 10.2.7 分部方法

分部方法可以在类型声明的一个部分中定义，并在另一个部分中实现。实现是可选的；如果没有部分实现该分部方法，则分部方法声明及其所有调用都会从由各部分组合而成的类型声明中移除。

分部方法不能定义访问修饰符，但隐式是私有的。它们的返回类型必须为 void，并且它们的参数不能具有 out 修饰符。仅当标识符 partial 紧挨在 void 类型之前出现时，才会在方法声明中将其识别为特殊关键字；否则它可以作为普通标识符使用。分部方法不能显式实现接口方法。

分部方法声明有两种：如果方法声明的主体是分号，则该声明称为定义分部方法声明。如果主体以块的形式给出，则该声明称为实现分部方法声明。在类型声明的各个部分中，对于给定签名，只能有一个定义分部方法声明，并且对于给定签名，只能有一个实现分部方法声明。如果给出了实现分部方法声明，则必须存在相应的定义分部方法声明，并且这些声明必须按以下规定匹配：

- 这些声明必须具有相同的修饰符（尽管不一定按相同顺序）、方法名、类型参数数量和参数数量。
- 声明中的对应参数必须具有相同的修饰符（尽管不一定按相同顺序）和相同的类型（类型参数名称的差异除外）。
- 声明中的对应类型参数必须具有相同的约束（类型参数名称的差异除外）。

实现分部方法声明可以与相应的定义分部方法声明出现在同一部分中。

只有定义分部方法参与重载决策。因此，无论是否给出了实现声明，调用表达式都可能解析为对该分部方法的调用。由于分部方法总是返回 void，因此此类调用表达式将始终是表达式语句。此外，由于分部方法是隐式私有的，因此此类语句将始终出现在声明该分部方法的类型声明的某个部分内。

如果分部类型声明的任何部分都不包含针对给定分部方法的实现声明，则调用它的任何表达式语句都会简单地从组合类型声明中移除。因此，该调用表达式（包括任何组成表达式）在运行时没有效果。该分部方法本身也会被移除，并且不会成为组合类型声明的成员。

如果针对给定分部方法存在实现声明，则保留对该分部方法的调用。该分部方法会产生一个类似于实现分部方法声明的方法声明，但以下情况除外：

- 不包含 partial 修饰符
- 生成的方法声明中的特性是定义分部方法声明和实现分部方法声明的特性的组合，顺序未指定。不会移除重复项。
- 生成的方法声明的参数上的特性是定义分部方法声明和实现分部方法声明的对应参数的组合特性，顺序未指定。不会移除重复项。

如果为分部方法 M 给出了定义声明但没有给出实现声明，则以下限制适用：

- 创建指向方法的委托（§7.6.10.5）是编译时错误。
- 在转换为表达式树类型的匿名函数（§6.5.2）中引用 M 是编译时错误。
- 作为 M 调用的一部分出现的表达式不会影响确定赋值状态（§5.3），这可能导致编译时错误。
- M 不能作为应用程序的入口点（§3.1）。

分部方法有助于允许类型声明的一个部分自定义另一个部分的行为，例如，由工具生成的部分。考虑以下分部类声明：

```
partial class Customer
{
    string name;
    public string Name {
        get { return name; }
        set {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }
    }
    partial void OnNameChanging(string newName);
    partial void OnNameChanged();
}
```

如果编译该类时没有任何其他部分，则定义分部方法声明及其调用将被移除，并且生成的组合类声明将等效于以下内容：

```
class Customer
{
    string name;
    public string Name {
        get { return name; }
        set { name = value; }
    }
}
```

但是，假设给出了另一个部分，它提供了这些分部方法的实现声明：

```
partial class Customer
{
    partial void OnNameChanging(string newName)
    {
        Console.WriteLine("Changing " + name + " to " + newName);
    }
    partial void OnNameChanged()
    {
        Console.WriteLine("Changed to " + name);
    }
}
```

那么生成的组合类声明将等效于以下内容：

```
class Customer
{
    string name;
    public string Name {
        get { return name; }
        set {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }
    }
    void OnNameChanging(string newName)
    {
        Console.WriteLine("Changing " + name + " to " + newName);
    }
    void OnNameChanged()
    {
        Console.WriteLine("Changed to " + name);
    }
}
```

## 10.2.8 名称绑定

尽管可扩展类型的每个部分都必须在同一命名空间中声明，但这些部分通常写在不同的命名空间声明中。因此，每个部分可能存在不同的 using 指令（§9.4）。在解释某个部分内的简单名称（§7.5.2）时，只考虑包含该部分的命名空间声明的 using 指令。这可能导致同一标识符在不同部分中具有不同含义：

```
namespace N
{
    using List = System.Collections.ArrayList;
    partial class A
    {
        List x;        // x has type System.Collections.ArrayList
    }
}
namespace N
{
    using List = Widgets.LinkedList;
    partial class A
    {
        List y;        // y has type Widgets.LinkedList
    }
}
```

## 10.3 类成员

类的成员由它的类成员声明引入的成员以及从直接基类继承的成员组成。

```
class-member-declarations:
    class-member-declaration
    class-member-declarations  class-member-declaration
```

```
class-member-declaration:
constant-declaration
field-declaration
method-declaration
property-declaration
event-declaration
indexer-declaration
operator-declaration
constructor-declaration
destructor-declaration
static-constructor-declaration
type-declaration
```

类类型的成员分为以下类别：

- 常量，表示与类关联的常量值（§10.4）。
- 字段，即类的变量（§10.5）。
- 方法，实现类可以执行的计算和操作（§10.6）。
- 属性，定义命名特征以及与读取和写入这些特征相关联的操作（§10.7）。
- 事件，定义类可以生成的通知（§10.8）。
- 索引器，允许以与数组相同的方式（在语法上）为类的实例编制索引（§10.9）。
- 运算符，定义可应用于类实例的表达式运算符（§10.10）。
- 实例构造函数，实现初始化类实例所需的操作（§10.11）
- 析构函数，实现永久丢弃类实例之前要执行的操作（§10.13）。
- 静态构造函数，实现初始化类本身所需的操作（§10.12）。
- 类型，表示类的局部类型（§10.3.8）。

可以包含可执行代码的成员统称为类类型的函数成员。类类型的函数成员是该类类型的方法、属性、事件、索引器、运算符、实例构造函数、析构函数和静态构造函数。

类声明会创建一个新的声明空间（§3.3），并且由类声明直接包含的类成员声明会将新成员引入此声明空间。以下规则适用于类成员声明：

- 实例构造函数、析构函数和静态构造函数必须与直接包含它们的类具有相同的名称。所有其他成员的名称必须不同于直接包含它们的类的名称。
- 常量、字段、属性、事件或类型的名称必须不同于同一类中声明的所有其他成员的名称。
- 方法的名称必须不同于同一类中声明的所有其他非方法的名称。此外，方法的签名（§3.6）必须不同于同一类中声明的所有其他方法的签名，并且同一类中声明的两个方法不能具有仅 ref 和 out 不同的签名。

