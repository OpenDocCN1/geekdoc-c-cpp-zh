

# 398 第 7 章：继承

virtual Modifier
# 支持实例方法和属性的重写，但不支持字段或任何静态成员。它要求在基类和派生类中都必须显式操作。基类必须将其允许重写的每个成员标记为 `virtual`。如果公共或受保护的成员没有包含 `virtual` 修饰符，子类将无法重写这些成员。

## 语言对比：Java——默认虚拟方法

默认情况下，Java 中的方法是虚拟的，如果倾向于非虚拟行为，则必须显式地标记为 `final`。相比之下，C# 默认是非虚拟的。

列表 7.9 显示了属性重写的示例。

列表 7.9：重写属性

```csharp
public class PdaItem
{
    public virtual string Name { get; set; }
    // ...
}
```

```csharp
public class Contact : PdaItem
{
    public override string Name
    {
        get
        {
            return $"{FirstName} {LastName}";
        }
        set
        {
            string[] names = value.Split(' ');
            // 错误处理未显示
            FirstName = names[0];
            LastName = names[1];
        }
    }

    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

```csharp
// ...
}
```

`PdaItem` 不仅在 `Name` 属性上包含了 `virtual` 修饰符，`Contact` 的 `Name` 属性也使用了 `override` 关键字装饰。删除 `virtual` 将导致错误，而省略 `override` 将导致警告，正如你很快就会看到的。C# 要求重写方法必须显式使用 `override` 关键字。换句话说，`virtual` 将方法或属性标记为派生类型中可以被替换（重写）。

## 语言对比：Java 和 C++——隐式重写

与 Java 和 C++ 不同，C# 的派生类中需要 `override` 关键字。C# 不允许隐式重写。要重写一个方法，基类和派生类的成员必须匹配，并具有相应的 `virtual` 和 `override` 关键字。此外，当指定 `override` 关键字时，假设派生类的实现替换了基类的实现。

重写成员会导致运行时调用最派生的实现（参见列表 7.10 及其输出 7.1）。

## 列表 7.10：运行时调用虚拟方法的最派生实现

```csharp
public class Program
{
    public static void Main()
    {
        Contact contact;
        PdaItem item;

        contact = new Contact();
        item = contact;

        // 通过 PdaItem 变量设置名称
        item.Name = "Inigo Montoya";

        // 显示 FirstName & LastName
```

```csharp
// 属性已设置
Console.WriteLine(
  $"{contact.FirstName} {contact.LastName}"
)
```

# 输出 7.1

Inigo Montoya

在列表 7.10 中，当给值给在 `PdaItem` 上声明的 `item.Name` 时，contact 的 `FirstName` 和 `LastName` 仍然被设置。规则是，每当运行时遇到虚拟方法时，它都会调用该虚拟成员的最派生且重写的实现。在这种情况下，代码实例化了一个 `Contact` 并调用了 `Contact.Name`，因为 `Contact` 包含了 `Name` 最派生的实现。

虚拟方法仅提供默认实现——即派生类可以完全重写的实现。然而，由于继承设计的复杂性，考虑（并且最好实现）一个需要虚拟方法定义的特定场景，比默认将成员声明为虚拟的更为重要。

这一步也很重要，因为将方法从虚拟方法转换为非虚拟方法可能会破坏重写了该方法的派生类。一旦发布了虚拟成员，如果你想避免引入破坏性更改，它应该保持为虚拟。因此，在引入虚拟成员时要小心——例如，可以考虑先将其设为 `private protected`。

## 语言对比：C++——构造期间方法调用的分发

在 C++ 中，构造期间调用的方法不会分发虚拟方法。相反，在构造期间，类型与基类型而非派生类型关联，并且虚拟方法调用基类实现。相比之下，C# 将虚拟调用分发到最派生类型，即使派生构造函数尚未执行。无论如何，在 C# 中应避免这种情况。

最后，只有实例成员可以是虚拟的。CLR 使用的是具体类型。

## 协变类型

通常，重写方法的签名必须与基方法的签名匹配。然而，从 C# 9.0 开始，有一项改进允许重写方法指定与基方法不同的返回类型。这种特性被称为**协变类型**。

列表 7.11：协变类型

```csharp
public class Base
{
    public virtual Base Create() => new();
}

public class Derived : Base
{
    public override Derived Create() => new();
}
```

# 第 7 章：继承

注意 Base 类的 `Create()` 返回 `Base`，而 Derived 类的返回 `Derived`。协变将在第 12 章详细讨论。

## 修饰符

当重写方法未使用 `override` 时，编译器会发出与输出 7.2 或 7.3 类似的警告。

# 输出 7.2

```
警告 CS014: '<derived method>' 了继承的成员。要使当前成员重写，请添加 override 关键字。
```

# 输出 7.3

```
警告 CS008: 在 '<derived property>' 上需要 new 关键字，因为它隐藏了继承的成员
```

明显的解决方案是添加 `override` 修饰符（假设基成员是虚拟的）。然而，正如警告所示，`new` 修饰符也是一种选择。考虑表 7.1 所示的场景——这是一个更通用的“脆弱基类问题”的具体示例。

## 表 7.1：为什么需要 new 修饰符

| 活动 | 代码 |
| :--- | :--- |
| 程序员 A 定义包含 FirstName 和 LastName 属性的 Person 类 | `public class Person {
  public string FirstName { get; set; }
  public string LastName { get; set; }
}` |
| 程序员 B 继承 Person 并定义了带有额外属性 Name 的 Contact，此外他还定义了 Program 类，其 Main() 方法实例化 Contact，然后打印名称。 | `public class Contact : Person {
  public string Name {
    get
    return FirstName + " " + LastName;
    set
      string[] names = value.Split(' ');
      // 错误处理未显示
      FirstName = names[0];
      LastName = names[1];
  }
}` |

