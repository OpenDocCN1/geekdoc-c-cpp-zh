
你不必担心这种不一致性，因为不符合 CLS 的属性极其罕见。事实上，在我使用 .NET Framework 的期间，我从未见过其中一个。

> 请注意，只有 `Attribute`、`Type` 和 `MethodInfo` 类实现了遵循 `inherit` 布尔参数的反射方法。所有查找属性的反射方法都会忽略 `inherit` 参数，并且不会检查继承层次结构。如果你需要检查值、属性、字段、构造函数或参数上是否存在已继承的属性，你必须调用 `Attribute` 类中的其中一个方法。

还有一点你应该注意：当你将类传递给 `IsDefined`、`GetCustomAttribute` 或 `GetCustomAttributes` 时，这些方法会搜索你指定的属性的应用，或者任何派生自该指定类的属性类应用。如果你的代码正在寻找某个特定的属性，你应该对返回的值进行额外的检查，以确保这些方法返回的是你正在寻找的确切类。你可能还会考虑将你的属性类定义为 `sealed`（密封的），以减少潜在的混义并消除这种额外的检查。

以下是一些示例代码，它列出了类型中定义的所有方法，并显示应用到每个方法上的属性。这些代码仅用于演示；通常情况下，你不会像我这样将这些特定的自定义属性应用到这些目标上。

```csharp
using System;
using System.Diagnostics;
using System.Reflection;
[assembly: CLSCompliant(true)]
[Serializable]
[DefaultMemberAttribute("Main")]
[DebuggerAttribute("Richter", Name = "Jeff", Target = typeof(Program))]
public sealed class Program {
[Conditional("Debug")]
[Conditional("Release")]
public void DoSomething() {}
public Program() {
}
[CLSCompliant(true)]
[STAThread]
public static void Main() {
// 显示应用到此类型的属性集
ShowAttributes(typeof(Program));
```

```csharp
// 获取与类型关联的方法集
var members = 
    from m in typeof(Program).GetType().DeclaredMembers.OfType<MethodBase>()
    where m.IsPublic
    select m;

foreach (MemberInfo info in members) {
    // 显示应用到此成员的属性集
    ShowAttributes(member);
}

private static void ShowAttributes(MemberInfo attributeTarget) {
    var attributes = attributeTarget.GetCustomAttributes<Attribute>();

    Console.WriteLine("Attributes applied to {0}: {1}",
        attributeTarget.Name, attributes.Count == 0 ? "None" : String.Empty);

    foreach (Attribute attribute in attributes) {
        // 显示每个应用属性的类型
        Console.WriteLine("{0}", attribute.GetType().ToString());

        if (attribute is DefaultMemberAttribute) {
            Console.WriteLine("MemberName={0}",
                ((DefaultMemberAttribute)attribute).MemberName);
        }

        if (attribute is ConditionalAttribute) {
            Console.WriteLine("ConditionString={0}",
                ((ConditionalAttribute)attribute).ConditionString());
        }

        if (attribute is CLSCompliantAttribute) {
            Console.WriteLine("IsCompliant={0}",
                ((CLSCompliantAttribute)attribute).IsCompliant());
        }

        DebuggerDisplayAttribute dda = null;
        if (dda != null) {
            Console.WriteLine("Value={0}, Name={1}, Target={2}",
                dda.Value, dda.Name, dda.Target);
        }
    }
    Console.WriteLine();
}
```

生成并运行此应用程序将产生以下输出：

Attributes applied to Program:
System.SerializableAttribute
System.Diagnostics.DebuggerDisplayAttribute
Value=Richter, Name=Jeff, Target=Program
System.Reflection.DefaultMemberAttribute MemberName=Main

Attributes applied to DoSomething:
System.Diagnostics.ConditionalAttribute
ConditionString=Release
System.Diagnostics.ConditionalAttribute
ConditionString=Debug

Attributes applied to Main:
System.CLSCompliantAttribute
IsCompliant=True
System.STAThreadAttribute

Attributes applied to :ctor: None

# 两个属性实例之间的相互匹配

现在你的代码已经了如何检查属性实例是否应用到目标上，它可能想要检查属性的字段以查看它们具有什么值。实现此点的方法是编写显式检查属性类字段值的代码。`System.Attribute` 重写了 `Object` 的 `Equals` 方法，在内部，该方法比较两个对象的类型。如果它们不相同，`Equals` 返回 `false`。如果类型相同，`Equals` 将使用反射来比较两个对象字段的值（通过对每个字段调用 `Equals`）。如果所有字段都匹配，则返回 `true`；否则返回 `false`。你可能会在你的属性类中重写 `Equals` 以消除对反射的使用，提高性能。

`System.Attribute` 还暴露了一个虚拟方法 `Match`，你可以重写它以提供更丰富的语义。`Match` 的默认实现只是调用 `Equals` 并返回其结果。以下代码演示了如何重写 `Equals` 和 `Match`（如果一个属性代表另一个的子集，则返回 `true`），并展示了如何使用 `Match`。

```csharp
[Flags]
internal enum Accounts {
  Savings = 0x0001,
  Checking = 0x0002,
  Brokerage = 0x0004
}
```

```csharp
[AttributeUsage(AttributeTargets.Class)]
internal sealed class AccountsAttribute : Attribute {
  private Accounts m_accounts;
```

```csharp
public AccountsAttribute(Accounts accounts) {
  m_accounts = accounts;
}
```

```csharp
public override bool Match(Object obj) {

// 如果基类实现了 Match 且基类
// 不是 Attribute，则取消下面行的注释。
// if (base.Match(obj)) return false;
```

```csharp
// 由于 'this' 不是空，obj 是空，
// 那么对象无法匹配
// 注意：如果由于信任基类型
// 正确实现了 Match，则可以删除此行。
// if (obj == null) return false;
```

```csharp
// 如果对象是不同类型，它们无法匹配
// 注意：如果你信任基类型
// 正确实现了 Match，则可以删除此行。
// if (this.GetType() != obj.GetType()) return false;
```

```csharp
// 将 obj 强制转换为你的类型以访问字段。注意：此强制转换
// 不失败，因为我们知道对象是相同类型
AccountsAttribute other = (AccountsAttribute) obj;
```

```csharp
// 按照你看到的方式比较字段
// 此示例检查 'this' 账户是否是
// 其他账户的子集
// if (other.m_accounts & m_accounts) != m_accounts
return false;
```

```csharp
return true; // 对象匹配
}
public override bool Equals(Object obj) {
// 如果基类实现了 Equals 且基类
// 不是 Attribute，则取消下面行的注释。
// if (base.Equals(obj)) return false;
```

```csharp
// 由于 'this' 不是空，obj 是空，
// 那么对象无法匹配
// 注意：如果信任基类型
// 正确实现了 Equals，则可以删除此行。
// if (obj == null) return false;
```

```csharp
// 如果对象是不同类型，它们无法匹配
// 注意：如果你信任基类型
// 正确实现了 Equals，则可以删除此行。
// if (this.GetType() != obj.GetType()) return false;
```

```csharp
// 将 obj 强制转换为你的类型以访问字段。注意：此强制转换
// 不失败，因为我们知道对象是相同类型
AccountsAttribute other = (AccountsAttribute) obj;
```

```csharp
// 按照你看到的方式比较字段
// 此示例检查 'this' 账户是否是
// 其他账户的子集
// if (other.m_accounts & m_accounts) != m_accounts
return false;
```

```csharp
return true; // 对象相等
}

// 因为重写了 Equals 所以重写 GetHashCode
public override Int32 GetHashCode() {
    return (Int32) m_accounts;
}
```

```csharp
[Accounts(Accounts.Savings)]
internal sealed class ChildAccount { }
```

```csharp
[Accounts(Accounts.Savings | Accounts.Brokerage)]
internal sealed class AdultAccount {
```

```csharp
public sealed class Program {
    public static void Main() {
        CanWriteCheck(new ChildAccount());
        CanWriteCheck(new AdultAccount());
        // 这只是演示该方法在一个没有应用 AccountsAttribute
        // 类型上正常工作
        CanWriteCheck(new Program());
    }
private static void CanWriteCheck(Object obj) {
    // 构建属性类型的实例并将其初始化
    // 我们显式寻找的内容。
    Attribute checking = new AccountsAttribute(Accounts.Checking);
    // 构建应用到类型上的属性实例
    Attribute validAccounts =
    obj.GetType().GetCustomAttribute<AccountsAttribute>(false);
    // 如果属性应用到类型上并且
    // 属性指定了“Checking”账户，那么
    // 该类型就可以写支票
    if ((validAccounts != null && checking.Match(validAccounts)) {
        Console.WriteLine("{0} types can write checks.", obj.GetType());
    } else {
        Console.WriteLine("{0} types can NOT write checks.", obj.GetType());
    }
}
}
```
```

