
`[DllImport("kernel32.dll", ExactSpelling = true, SetLastError = false)]`

属性所应用的代码声明类型称为目标（target）。表 21.1 显示了可能的目标值。

## 表 21.1 属性目标

| 目标 | 应用范围 |
| --- | --- |
| assembly | 整个程序集 |
| module | 当前程序集模块 |
| field | 类字段 |
| event | 事件 |
| method | 方法、属性 get 访问器或属性 set 访问器 |
| param | 方法或属性 set 访问器的参数 |
| property | 属性 |
| return | 方法、索引器属性或属性 get 访问器的返回值 |
| type | 结构体、类、接口或枚举 |

虽然属性通常应用于其其前的元素，但你也可以显式地指定它应用的目标。例如，你可以指定属性是应用于方法、其参数还是其返回值，如列表 21.4 所示。

## 列表 21.4 属性参数

```csharp
[CustomAttribute]
string Method()
{
    return String.Empty();
}

[method: CustomAttribute]
string Method()
{
    return String.Empty();
}

[method: CustomAttribute]
string Method()
{
    return String.Empty();
}
```

## 使用调用者信息属性

调用者信息属性允许你获取有关方法调用者的信息，例如源文件路径、调用方法的行号以及调用者的名称。调用者信息属性如表 21.2 所示

### 表 21.2 调用者信息属性
| 属性 | 说明 |
| --- | --- |
| CallerFilePathAttribute | 包含调用者的源文件（编译时）的完整路径 |
| CallerLineNumberAttribute | 调用方法所在源文件中的行号 |
| CallerMemberNameAttribute | 调用者的方法或属性名称 |

这些属性应用于可选参数，并更改在省略参数时传递的默认值。列表 21.5 显示了如何使用调用者信息属性的示例。由于这些属性定义在 `System.Runtime.CompilerServices` 命名空间中，你应该在代码文件中添加 `using` 语句以包含此命名空间。

使用调用者信息属性

## 列表 21.5 使用调用者信息属性

```csharp
public void DoSomething()
{
    Log("Performing some action.");
}
public void Log(string message,
    [System.Runtime.CompilerServices.CallerMemberName] string memberName = "",
    [System.Runtime.CompilerServices.CallerFilePath] string filePath = "",
    [System.Runtime.CompilerServices.CallerLineNumber] int lineNumber = 0)
{
    System.Diagnostics.Debug.WriteLine("message: {0}", memberName);
    System.Diagnostics.Debug.WriteLine("filePath: {0}", filePath);
    System.Diagnostics.Debug.WriteLine("lineNumber: {0}", lineNumber);
}
```

调用者信息属性最常见的用途是为跟踪和诊断方法指定调用者名称，或者实现数据绑定接口（如 `INotifyPropertyChanged`）。使用 `CallerMemberNameAttribute` 的示例如列表 21.6 所示。

## 列表 21.6 使用 CallerMemberNameAttribute 的 INotifyPropertyChanged

```csharp
public class Contact : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;
    private string firstName;
    private string lastName;
    public string FirstName
    {
        get
        {
            return this.firstName;
        }
        set
        {
            this.firstName = value;
            NotifyPropertyChanged();
        }
    }
    public string LastName
    {
        get
        {
            return this.lastName;
        }
        set
        {
            this.lastName = value;
            NotifyPropertyChanged();
        }
    }
    private void NotifyPropertyChanged([CallerMemberName] string propertyName = "")
    {
      var handler = PropertyChanged;
      if (handler != null)
      {
        handler(this, new PropertyChangedEventArgs(propertyName));
      }
    }
}
```

表 21.3 显示了使用 `CallerMemberNameAttribute` 时返回的成员名称值。

### 表 21.3 CallerMemberNameAttribute 结果
|发生位置 | 结果 |
| --- | --- |
| 方法、属性、事件 | 方法、属性或事件的名称 |
| 构造函数 | 字符串 ".ctor" |
| 静态构造函数 | 字符串 ".cctor" |
| 析构函数 | 字符串 ".Finalize" |
| 用户定义的转换或运算符 | 生成的名称（例如 op_Addition） |
| 属性 | 属性应用的成员 |
| 无成员 | 可选参数的默认值 |

## 使用常用属性

.NET 框架定义了许多可以在程序使用的属性。最常用的有 `Obsolete` 属性、`Conditional` 属性和全局属性。

### Obsolete 属性
`Obsolete` 属性表示代码声明不再应该使用，并根据配置导致编译器生成警告或错误。该属性可以不带参数使用，但建议提供说明以指示何时生成警告或错误。列表 21.7 显示了使用 `Obsolete` 属性的示例。

## 列表 21.7 Obsolete 属性

```csharp
public class Example
{
    [Obsolete("Consider using OtherMethod instead.", false)]
    public string Method()
    {
        return String.Empty();
    }
    public string OtherMethod()
    {
        return "Test";
    }
}
```

### Conditional 属性
`Conditional` 属性表示代码声明取决于条件符号，并可以应用于类或方法。编译器使用此属性来确定是否包含调用。如果在编译期间存在条件符号，则包含调用；否则不包含。如果 `Conditional` 属性应用于方法，则该方法不能有返回值。列表 21.8 显示了使用 `Conditional` 属性的示例。

## 列表 21.8 Conditional 属性

```csharp
public class Example
{
    [Conditional("DEBUG")]
    public void DisplayDiagnostics()
    {
        Console.WriteLine("Diagnostic information.");
    }
}
```

444 第 21 节：属性编程

```csharp
public string Method()
{
    return "Test";
}
```

### 注意

### #if 和 #endif 预处理器符号
使用 `Conditional` 属性与使用 `#if` 和 `#endif` 预处理器符号类似，但它可以提供一种更整洁的替代方案，从而减少错误。这里展示了使用 `#if/#endif` 替代 `Conditional` 属性的类：

```csharp
public class Example
{
    #if DEBUG
        public void DisplayDiagnostics()
        {
            Console.WriteLine("Diagnostic information.");
        }
    #endif
    public string Method()
{
    return "Test";
}
}
```

虽然你可以混合使用 `Conditional` 属性和 `#if/#endif` 预处理器符号，但如果你这样做，需要非常小心。使用 `#if/#endif` 删除代码发生在编译过程更早阶段，可能会导致编译器无法编译 `Conditional` 方法。

### 全局属性
虽然大多数属性应用于特定的代码声明，但某些属性应用于整个程序集或模块。这些属性出现在源代码中位于任何 `using` 指令之后、任何代码声明（如类或命名空间声明）之前。

## 使用常用属性

### 注意

## 程序集清单 (Assembly Manifest)

程序集清单包含描述程序集中元素之间关系的数据，包括版本和安全信息。清单通常与编译后的文件一起包含。

通常，全局属性放置在 `AssemblyInfo.cs` 文件中，但如果这些文件在单次编译过程中被编译，它们可能会出现在多个文件中。常见的全局属性如表 21.4 所示。

# 表 21.4 全局属性

| 属性 程序集标识属性 | 用途 |
| --- | --- |
| AssemblyName | 程序集的全名 |
| AssemblyVersion | 程序集的版本 |
| AssemblyAssemblyCulture | 程序集支持的文化 |
| AssemblyFlags | 表示是否同时存在多个程序集副本 |
| 信息性属性 | | |
| AssemblyProduct | 为程序集指定产品名称 |
| AssemblyTrademark | 为程序集指定商标 |
| AssemblyInformationalVersion | 为程序集指定信息版本 |
| AssemblyCompany | 为程序集指定公司 |
| AssemblyCopyright | 为程序集指定版权 |
| AssemblyFileVersion | 为 Windows 文件版本资源指定版本号 |

## CLS 规性 (CLSCompliant)

# 程序集清单属性

| 属性 | 用途 |
| --- | --- |
| AssemblyTitle | 为程序集清单指定标题 |
| AssemblyDescription | 为程序集清单指定描述 |
| AssemblyConfiguration | 为程序集清单指定配置 |
| AssemblyDefaultAlias | 为程序集清单指定友好的默认别名 |

## 使用自定义属性

如果你需要为自己的应用程序提供自定义元数据，可以通过定义派生自 `Attribute` 的属性类（直接或间接）来创建自定义属性。

例如，你可以定义一个自定义属性，该属性包含与代码更改相关的 Team Foundation Server 工作项编号，如代码示例 21.9 所示。

# 代码示例 21.9 创建自定义属性

```
[AttributeUsage(AttributeTargets.All, Inherited = false, AllowMultiple = true)]
public sealed class WorkItemAttribute : System.Attribute
{
    private int workItemId;
    public WorkItemAttribute(int workItemId)
    {
        this.workItemId = workItemId;
    }
    public int WorkItemId
    {
        get
        return this.workItemId;
    }
    public string Comment
    {
        get;
        set;
    }
}
```

自定义属性有一个唯一的公共构造函数，其参数组成了属性的位置性参数。任何公有的读写字段或属性——在本例中为 `Comment` 属性——将变为命名参数。最后，`AttributeUsage` 属性表示 `WorkItem` 属性在任何声明上都有效，可以多次应用，并且不会自动应用到派生类型。

## 在运行时访问属性

你可以像代码示例 21.10 所示使用此属性。

# 代码示例 21.10 应用自定义属性

```
[WorkItem(1234, Comment = "Created class showing attributes being used.")]
public class Test
{
    [WorkItem(5678, Comment = "Changed property to use auto-property syntax.")]
    public int P
    {
        get;
        set;
    }
}
```

# 在运行时访问属性

如果你无法在运行时访问信息，那么为应用程序添加元数据将意义不大。.NET Framework 通过一个称为反射（reflection）的过程提供了访问运行时信息的方法，包括属性提供的元数据。由于属性提供了元数据，在查询属性之前，与属性相关的代码实际上不会执行。

使用 `Attribute.GetCustomAttribute` 方法可以轻松检索自定义属性。代码示例 21.11 显示了在运行时访问代码示例 21.9 中定义的自定义属性以及代码示例 21.10 中定义的类的示例。图 21.1 显示了代码示例 21.11 的输出。

# 代码示例 21.11 在运行时访问单个属性

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        WorkItemAttribute attribute =
            Attribute.GetCustomAttribute(typeof(Test), typeof(WorkItemAttribute))
            as WorkItemAttribute;
        if (attribute != null)
        {
            Console.WriteLine("{0}: {1}", attribute.WorkItemId, attribute.Comment);
        }
    }
}
```

# 第 21 小时：使用属性编程

![](img/d08df1b94a49a49b95ebbdc5e982bda6_467_0.png)

图 21.1

运行时检索单个属性的输出。

`Attribute.GetCustomAttribute` 返回单个属性。如果在代码元素上定义了多个相同类型的属性，或者你需要处理不同类型的多个属性，可以使用 `Attribute.GetCustomAttributes` 方法返回一个自定义属性数组。然后你可以枚举生成的数组，从数组元素中检查并提取信息，如代码示例 21.12 所示。

# 代码示例 21.12 在运行时访问多个属性

```csharp
public class Program{
    public static void Main(string[] args)
    {
        var workItems = from attribute in
            Attribute.GetCustomAttributes(typeof(Test))
            OfType<WorkItemAttribute>()
            select attribute;
        foreach (var attribute in workItems)
        {
            Console.WriteLine("{0}: {1}", attribute.WorkItemId, attribute.Comment);
        }
    }
}
```
