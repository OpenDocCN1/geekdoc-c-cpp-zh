
请注意，无论提供的是非限定的“Name”（因为它在作用域内）还是完全（或部分）限定名称（如 `Person.Name`），结果都只是最终的标识符（点号名称中的最后一个元素）。你仍然可以使用 C# 5.0 的 `CallerMemberName` 参数特性来获取属性的名称；参见 http://itl.tc/CallerMemberName 查看示例。

## 特性

在深入了解如何编程特性之前，我们应该考虑一个用例来展示它们的实用性。在列表 18.3 的 `CommandLineHandler` 示例中，你根据与属性名称匹配的命令行选项动态设置类的属性。然而，当命令行选项是无效的属性名称时，这种方法是不够的。例如，`/?` 无法得到支持。此外，这种机制没有提供区分哪些选项是必需的，哪些是可选的方法。

与其依赖于选项名称和属性名称之间的精确匹配，你可以使用特性来标识被修饰构造的额外元数据——在这种情况下，是特性所修饰的选项。使用特性，你可以将一个属性标记为 `Required` 并提供一个 `/ ?` 选项别名。换句话说，特性是一种将额外数据与属性（以及其他构造）关联起来的手段。

特性出现在方括号内，位于它们修饰的构造之前。例如，你可以修改 `CommandLineInfo` 类以包含特性，如列表 18.8 所示。

### 列表 18.8：使用特性修饰属性

```csharp
class CommandLineInfo
{
    [CommandLineSwitchAlias("?")]
    public bool Help { get; set; }
    [CommandLineSwitchRequired]
    public string Out { get; set; }
    public System.Diagnostics.ProcessPriorityClass Priority { get; set; } =
    System.Diagnostics.ProcessPriorityClass.Normal;
}
```

在列表 18.8 中，`Help` 和 `Out` 属性被特性修饰。这些特性的目的是允许 `/Help` 的别名 `/?`，并指示 `/Out` 是必需参数。其思想是在 `CommandLineHandler.TryParse()` 方法内部，你启用对选项别名的支持，并且在假设解析成功的情况下，检查是否指定了所有必需的开关。

在同一构造上组合属性有两种方式。首先，你可以在同一个方括号内使用逗号分隔属性。或者，你可以将每个属性放在各自独立的方括号中。列表 18.9 提供了示例。

### 列表 18.9：使用多个属性修饰属性

```csharp
[CommandLineSwitchRequired]
[CommandLineSwitchAlias("FileName")]
public string Out { get; set; }

[CommandLineSwitchRequired,
 CommandLineSwitchAlias("FileName")]
public string Out { get; set; }
```

除了修饰属性外，开发人员还可以使用属性来修饰类、接口、结构体、枚举、委托、事件、方法、构造函数、字段、参数、返回值、程序集、类型参数和模块。对于这些情况中的大多数，应用属性涉及的语法与列表 18.9 中所示的方括号语法相同。然而，这种语法不适用于返回值、程序集和模块。

程序集属性用于添加关于程序集的元数据。例如，Visual Studio 的项目向导会生成一个 `AssemblyInfo.cs` 文件，其中包含许多关于程序集的属性。列表 18.10 就是这样一个文件的示例。

### 列表 18.10：`AssemblyInfo.cs` 中的程序集属性

```csharp
using System.Reflection;
using System.Runtime.CompilerServices;
using System.Runtime.InteropServices;
// General information about an assembly is controlled
// through the following set of attributes. Change these
// attribute values to modify the information
// associated with an assembly.
[assembly: AssemblyTitle("CompressionLibrary")]
[assembly: AssemblyDescription("")]
[assembly: AssemblyConfiguration("")]
[assembly: AssemblyCompany("IntelliTect")]
[assembly: AssemblyProduct("Compression Library")]
[assembly: AssemblyCopyright("Copyright© IntelliTect 2006-2018")]
[assembly: AssemblyTrademark("")]
[assembly: AssemblyCulture("")]
// Setting ComVisible to false makes the types in this
// assembly not visible to COM components. If you need to
// access a type in this assembly from COM, set the ComVisible
// attribute to true on that type.
[assembly: ComVisible(false)]
// The following GUID is for the ID of the typelib
// if this project is exposed to COM
[assembly: Guid("417a9609-24ae-4323-b1d6-cef0f874a2c3")]
// Version information for an assembly consists
// of the following four values:
//      Major Version
//      Minor Version
//      Build Number
//      Revision
// You can specify all the values or you can
// default the Revision and Build Numbers
// by using the '*' as shown below:
// [assembly: AssemblyVersion("1.0.*")]
[assembly: AssemblyVersion("1.0.0.0")]
[assembly: AssemblyFileVersion("1.0.0.0")]
```

程序集属性定义了诸如公司、产品和程序集版本号等信息。与程序集类似，将属性用法标识为模块需要加上 `module::` 前缀。程序集和模块属性的限制是，它们必须出现在 `using` 指令之后，但在任何命名空间或类声明之前。列表 18.10 中的属性是由 Visual Studio 项目向导生成的，应包含在所有项目中，以标记生成的二进制文件，使其包含关于可执行文件或动态链接库（DLL）内容的相关信息。

返回属性，如列表 18.11 所示，出现在方法声明之前，但使用相同类型的语法结构。

### 列表 18.11：指定返回属性

```csharp
[return: Description(
        "Returns true if the object is in a valid state.")]
public bool IsValid()
{
    // ...
    return true;
}
```

除了 `assembly:` 和 `return:`，C# 还允许显式目标识别 `module:`、`class:` 和 `method:`，分别对应修饰模块、类和方法的属性。然而，正如前文所述，`class:` 和 `method:` 是可选的。

使用属性的一大便利在于，语言会考虑属性命名约定，该约定要求在名称末尾加上 `Attribute`。然而，在前面的所有列表中的属性使用中，尽管每个使用的属性都遵循了命名约定，但都没有出现这种后缀。这是因为虽然应用属性时允许使用完整名称（如 `DescriptionAttribute`、`AssemblyVersionAttribute` 等），但 C# 使该后缀变为可选。通常，应用属性时不会出现这种后缀；相反，它只在定义属性或内联使用属性（如 `typeof(DescriptionAttribute)`）时出现。

## 准则

- **DO** 对包含公共类型的程序集应用 `AssemblyVersionAttribute`。
- **CONSIDER** 应用 `AssemblyFileVersionAttribute` 和 `AssemblyCompanyCopyrightAttribute` 以提供有关程序集的额外信息。
- **DO** 应用以下信息程序集属性：
  - `System.Reflection.AssemblyTitleAttribute`,
  - `System.Reflection.AssemblyCompanyAttribute`,
  - `System.Reflection.AssemblyProductAttribute`,
  - `System.Reflection.AssemblyDescriptionAttribute`,
  - `System.Reflection.AssemblyFileVersionAttribute`, 和
  - `System.Reflection.AssemblyCopyrightAttribute`.

## 自定义属性

定义自定义属性相对简单。属性是对象；因此，要定义一个属性，你需要定义一个类。使一般类变成属性的特征是它派生自 `System.Attribute`。因此，你可以创建一个 `CommandLineSwitchRequiredAttribute` 类，如列表 18.12 所示。

### 列表 18.12：定义自定义属性

```csharp
public class CommandLineSwitchRequiredAttribute : Attribute
{
}
```

通过那个简单的定义，你现在就可以像列表 18.8 中展示的那样使用该属性。到目前为止，还没有代码对该属性做出响应；因此，包含该属性的 `Out` 属性对命令行解析没有任何影响。

## 准则

- DO 在自定义属性类名称后加上 `Attribute` 后缀。

## 查找属性

除了提供用于反射类型成员的特性外，`Type` 还包括用于检索修饰该类型的属性的方法。类似地，所有反射类型（例如，`PropertyInfo` 和 `MethodInfo`）都包含用于检索修饰类型的属性列表的成员。列表 18.13 定义了一个方法，用于返回命令行中缺失的必需开关列表。

### 列表 18.13：检索自定义属性

```csharp
using System;
using System.Collections.Specialized;
using System.Reflection;
public class CommandLineSwitchRequiredAttribute : Attribute
{
    public static string[] GetMissingRequiredOptions(
        object commandLine)
    {
        List<string> missingOptions = new List<string>();
        PropertyInfo[] properties =
            commandLine.GetType().GetProperties();
        foreach (PropertyInfo property in properties)
        {
            Attribute[] attributes =
                (Attribute[])property.GetCustomAttributes(
                    typeof(CommandLineSwitchRequiredAttribute),
                    false);
            if ((attributes.Length > 0) &&
                (property.GetValue(commandLine, null) == null))
            {
                missingOptions.Add(property.Name);
            }
        }
        return missingOptions.ToArray();
    }
}
```

检查属性的代码相对简单。给定一个 `PropertyInfo` 对象（通过反射获得），你调用 `GetCustomAttributes()` 并指定所需的属性，然后指示是否检查任何重载方法。（或者，你可以调用不带属性类型的 `GetCustomAttributes()` 方法来返回所有属性。）

虽然可以将查找 `CommandLineSwitchRequiredAttribute` 属性的代码直接放在 `CommandLineHandler` 的代码中，但将代码放在 `CommandLineSwitchRequiredAttribute` 类本身中可以实现更好的对象封装。这通常是自定义属性的模式。在属性类的静态方法中放置查找属性的代码，还有什么比这更好的位置呢？

## 通过构造函数初始化属性

对 `GetCustomAttributes()` 的调用返回一个对象数组，可以将其强制转换为 `Attribute` 数组。由于我们示例中的属性没有实例成员，因此返回的属性中提供的唯一元数据信息是它是否存在。然而，属性也可以封装数据。列表 18.14 定义了一个 `CommandLineAliasAttribute` 属性——一个提供别名命令行选项的自定义属性。例如，你可以提供对 `/Help` 或 `/?` 作为缩略语的命令行支持。类似地，`/S` 可以提供 `/Subfolders` 的别名，表示命令应遍历所有子目录。

要支持此功能，你需要为该属性提供一个构造函数。具体而言，对于别名，你需要一个接受字符串参数的构造函数。（类似地，如果你希望允许多个别名，你需要定义一个具有 `params` 字符串数组作为参数的属性。）

### 示例 18.14：提供属性构造函数

```csharp
public class CommandLineSwitchAliasAttribute : Attribute
{
    public CommandLineSwitchAliasAttribute(string alias)
    {
        Alias = alias;
    }
    public string Alias { get; private set; }
}
class CommandLineInfo
{
    [CommandLineSwitchAlias("?")]
    public bool Help { get; set; }
    // ...
}
```

将属性应用到构造体时，仅允许使用常数值和 `typeof()` 表达式作为参数。此约束旨在支持将它们序列化到生成的 CIL 中。这意味着属性构造函数应要求使用合适类型的参数；创建一个接受 `System.DateTime` 类型参数的构造函数几乎没有价值，因为 C# 中没有 `System.DateTime` 常量。

从 `PropertyInfo.GetCustomAttributes()` 返回的对象将使用指定的构造函数参数进行初始化，如示例 18.15 所示。

### 示例 18.15：检索特定属性并检查其初始化

```csharp
PropertyInfo property =
    typeof(CommandLineInfo).GetProperty("Help");
CommandLineSwitchAliasAttribute attribute =
    (CommandLineSwitchAliasAttribute)
        property.GetCustomAttributes(
            typeof(CommandLineSwitchAliasAttribute), false)[0];
if (attribute.Alias == "?")
{
    Console.WriteLine("Help(?)");
}
```

此外，如示例 18.16 和 18.17 所示，你可以在 `CommandLineSwitchAliasAttribute` 的 `GetSwitches()` 方法中使用类似的代码，该方法返回一个包含所有开关（包括来自属性名的开关）的字典集合，并将每个名称与命令行对象上的对应属性关联起来。

### 示例 18.16：检索自定义属性实例

```csharp
using System;
using System.Reflection;
using System.Collections.Generic;
public class CommandLineSwitchAliasAttribute : Attribute
{
    public CommandLineSwitchAliasAttribute(string alias)
    {
```
