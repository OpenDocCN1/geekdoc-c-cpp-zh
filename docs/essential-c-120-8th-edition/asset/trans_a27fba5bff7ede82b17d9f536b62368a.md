
与名称对应。例如，如果项目名称为 `AddisonWesley.Fezzik`，你应该创建一个名为 `Services` 的子文件夹，并将 `RegistrationService.cs` 放在其中。然后你将创建另一个子文件夹（例如 `Data`），在其中放入程序内实体相关的类（例如 `RealestateProperty`、`Buyer` 和 `Seller`）。

## 指南

- 请使用文件作用域的命名空间（C# 10.0 或更高版本）。
- 请在命名空间名称前加上公司名称，以防止不同公司的命名空间具有相同的名称。
- 在命名空间名称的第二层使用稳定的、与版本无关的产品名称。
- **不要**在不将其放入命名空间的情况下定义类型。
- **考虑**创建一个与命名空间层级结构匹配的文件夹结构。

# XML 注释

第 1 章介绍了注释。然而，你可以使用 XML 注释不仅是为了提供给审查源代码的其它开发者查看。基于 XML 的注释遵循了在 Java 中流行的做法。尽管对于最终生成的可执行文件而言，C# 编译器会忽略所有注释，但开发者可以使用命令行选项指示编译器5 将 XML 注释提取到单独的 XML 文件中。通过利用 XML 文件的生成，开发者可以根据 XML 注释生成 API 文档。此外，C# 编辑器可以解析代码中的 XML 注释并将其作为独立区域显示给开发者（例如，显示与其他代码不同的颜色），或解析 XML 注释数据元素并显示给开发者。

> 5. C# 标准没有规定是由 C# 编译器还是独立的工具来负责提取 XML 数据。然而，所有主流的 C# 编译器都通过编译开关包含了必要的功能，而不是在额外的工具中实现。

第 10 章：良好的类型

图 10.3 展示了 IDE 如何利用 XML 注释，通过关于开发者正在尝试编写的代码提示来提供帮助。此类编码提示在大型程序中提供了巨大的帮助，特别是当多个开发者共享代码时。然而，为了工作，开发者显然必须花时间在代码中输入 XML 注释，并指示编译器创建 XML 文件。下一节将解释如何实现这一目标。

```csharp
// <summary>
/// 显示 <strong>console</strong> 中指定的文本
/// </summary>
/// <param name="text">要在控制台中显示的文本。</param>
// 1 reference
private static void Display(string text)
{
    Console.WriteLine(text);
}
// 0 references
static void Main(string[] args)
{
    Display("Inigo Montoya");
}
// void Program.Display(string text)
// 显示在控制台中指定的文本
```

图 10.3：Visual Studio IDE 中作为提示的 XML 注释

从 Visual Studio 2019 开始，你也可以在注释中嵌入简单的 HTML，它将反映在提示中。例如，用 `<strong>` 和 `</strong>` 括围 console 会导致“console”一词在图 10.3 中以粗体形式显示。

# 将 XML 注释与编程结构关联

考虑列表 10.12 所示的 `DataStorage` 类列表。

### 列表 10.12：使用 XML 注释注释代码

```csharp
// <summary>
/// DataStorage 用于从文件中持久化和检索
/// 员工数据。
/// </summary>
class DataStorage
{
    /// <summary>
    /// 将员工对象保存到以
    /// 员工名称命名的文件中。
    /// </summary>
    /// <remarks>
    /// 此方法使用了 <seealso cref="System.IO.FileStream"/>
    /// 此外
    /// <seealso cref="System.IO.StreamWriter"/>
    /// </remarks>
    /// <param name="employee">
    /// 要持久化到文件的员工</param>
    /// <date>2000年1月1日</date>
    public static void Store(Employee employee)
    {
        // ...
    }

    /** <summary>
     * 加载一个员工对象。
     * </summary>
     * <remarks>
     * 此方法使用了 <seealso cref="System.IO.Stream"/>
     * 此外
     * <seealso cref="System.IO.Reader"/>
     * </remarks>
     * <param name="firstName">
     * 员工的 own</param>
     * <param name="lastName">
     * 员工的姓</param>
     * <returns>
     * 与名称对应的员工对象
     * </returns>
     * <date>2000年1月1日</date> */
    public static static Employee Load(string firstName, string lastName)
    {
        // ...
    }
}

class Program
{
    // ...
}
```

列表 10.12 同时使用了跨越多行的 XML 分隔符注释和单行 XML 注释，后者的每一行都需要单独的三个正斜杠分隔符（///）。

鉴于 XML 注释旨在文档化 API，它们仅仅与 C# 声明关联使用，如列表 10.12 所示的类或方法。任何尝试将 XML 注释与代码内联且不与声明关联的尝试都将导致编译器的警告。编译器之所以建立关联，仅仅是因为 XML 注释紧出现在声明之前。

尽管 C# 允许注释中出现任何标签，但 C# 标准显式定义了一组要使用的标签。

# 生成 XML 文档

要生成 XML 文件，请向项目属性中添加 `DocumentationFile` 元素：

```xml
<?xml version="1.0" encoding="utf-8"?>
<doc>
  <assembly>
    <name>DataStorage</name>
  </assembly>
  <members>
    <member name="T:DataStorage">
      <summary>
      DataStorage 用于从文件中持久化和检索
      员工数据。
      </summary>
    </member>
    <member name="M:DataStorage.Store(Employee)">
      <summary>
      将员工对象保存到以
      员工名称命名的文件中。
      </summary>
      <remarks>
      此方法使用了 <seealso cref="System.IO.FileStream"/>
      此外外
      <seealso cref="System.IO.StreamWriter"/>
      </remarks>
      <param name="employee">
      要持久化到文件的员工</param>
      <date>2000年1月1日</date>
    </member>
    <member name="M:DataStorage.Load(System.String,System.String)">
      <summary>
      加载一个员工对象。
      </summary>
      <remarks>
      此方法使用了 <seealso cref="System.IO.Stream"/>
      此外外
      <seealso cref="System.IO.Reader"/>
      </remarks>
      <param name="firstName">
      员工的姓</param>
      <param name="lastName">
      员工的姓</param>
      <returns>
      与名称对应的员工对象
      </returns>
      <date>2000年1月1日</date>
    </member>
  </members>
</doc>
```

生成的文件仅包含了将元素关联回其相应 C# 声明所需的元数据量。这很重要，因为通常需要将 XML 输出与生成的程序集结合使用以产生任何意义的文档。

# 垃圾回收与弱引用

垃圾回收显然是运行时的一个核心功能。其目的是恢复不再引用的对象所占用的内存。该声明中的重点是内存和引用：垃圾回收器负责恢复内存；它不处理其他资源，如数据库连接、句柄（文件、窗口等）、网络端口和硬件设备（如串口）。此外，垃圾回收器根据是否还有引用来决定清理什么。隐含地意味着垃圾回收器处理引用对象并仅恢复堆上的内存。此外，维持对对象的引用将延迟垃圾回收器重用该对象占用的内存。
