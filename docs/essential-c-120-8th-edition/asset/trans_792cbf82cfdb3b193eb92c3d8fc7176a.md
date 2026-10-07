

# 使用指令

这些行<sup>4</sup>中的每一行都是全局指令，告诉编译器为指定命名空间内出现的任何类型推断命名空间限定符。例如，`global using global::System` 允许使用 `Console.WriteLine("Hello! My name is Inigo Montoya!")` 这样的隐式使用指令，而不是完全限定 `System.Console.WriteLine(...)`，因为 `Console` 定义在 `System` 命名空间中。

当然，你可以提供自己的全局使用声明。例如，假设频繁使用 `System.Text.StringBuilder` 类（在第 2 章最初引入）。与其通过完全限定引用它，你可以为 `System.Text` 命名空间提供全局使用指令，然后只需使用简称 `StringBuilder` 引用该类型（参见列表 5.10），同样依赖 `System.Console` 的隐式使用。

## 列表 5.10：配合 StringBuilder 使用指令

```csharp
// 全局指令将指定命名空间中的所有类型
导入到项目中
global using System.Text;
//
public class Program
{
    public static void Main()
    {
        // 关于 new() 的解释请参见第 6 章
        StringBuilder name = new();

        Console.WriteLine("Enter your first name: ");
        name.Append(Console.ReadLine()!.Trim());

        Console.WriteLine("Enter your middle initial: ");
        name.Append($"{Console.ReadLine()!.Split('.').Trim()} ");

        Console.WriteLine("Enter your last name: ");
        name.Append($"{Console.ReadLine()!.Trim()}");

        Console.WriteLine($"Hello {name}!");
    }
}
```

- 4. 忽略显示代码由编译器生成的注释。

238 页 第 5 章：参数与方法

全局使用指令适用于整个项目，无论它们出现在哪个文件中。虽然 C# 允许多次使用相同的全局使用声明，但这样做是冗余的。出于此原因，按照惯例，最好将所有全局使用指令置于一个命名为 `Usings.cs` 的单文件中。将它们集中在此处提供了一个放置或删除它们的众良好位置。

虽然全局使用指令适用于整个项目，但 C# 同时也支持仅适用于当前文件的指令。然而，全局使用声明必须出现在任何其他（非全局）使用指令之前，我们将在 `.csproj` 使用 `using` 元素之后介绍这些。

## csproj Using 元素

可以在项目文件 (.csproj) 中通过 `Using` 元素指定全局使用声明，如列表 5.11 所示。

### 列表 5.11：带有 Using 元素的示例 .NET 控制台项目文件

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net7.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>
  <ItemGroup>
    <Using Include="System.Net" />
    <Using Static="true" Include="System.Console" />
  </ItemGroup>
</Project>
```

需要注意的是，与 `ImplicitUsings` 元素不同，`Using` 元素是 `ItemGroup` 的子元素，而不是 `PropertyGroup` 元素。而且，由于指定了用于 `System.Net` 的 `Using` 元素，不再需要完全限定 `HttpClient`（它是 `System.Net` 命名空间的一部分）。相反，当存在另一个带有 `Static` 属性的 `Using` 语句时，编译器将生成 `global using System.Net` 指令，我们将在下一节中进一步解释。

## 高级主题

## 嵌套使用指令

你不仅可以在文件顶部拥有使用指令，还可以在命名空间声明的顶部包含它们。例如，如果声明了一个新的命名空间 `EssentialCSharp`，则在命名空间声明顶部使用使用指令是可能的（参见列表 5.12）。

### 列表 5.12：在命名空间声明内部指定 using 指令

```csharp
// using 指令将指定命名空间中的所有类型
// 导入整个文件
using System.Text.RegularExpressions;

public class Program
{
    public static void Main()
    {
        // ... 无需用 System.Text.RegularExpressions
        // 限定 RegEx 类型，因为有了
        // 使用 指令
        Match match = Regex.Match(name, pattern);
        // ...
    }
}
```

在文件顶部放置使用指令与在命名空间声明顶部放置使用指令的区别是，该指令仅在命名空间声明内有效。如果代码在 `EssentialCSharp` 声明上方或下方包含一个新的命名空间声明，则不同命名空间内的 `using System` 指令将不会生效。代码很少以这种方式编写，特别是考虑到每个文件提供单一类型声明的标准做法。

## using static 指令

使用指令允许你通过省略名称中的命名空间部分来缩写类型名称——这样对于指定命名空间内的任何类型，只需指定类型名。相比之下，`using static` 指令允许你从指定类型的任何静态成员中同时省略命名空间和类型名。指定 `using static System.Console` 指令允许你使用 `WriteLine()` 而不是 `System.Console.WriteLine()` 的完全限定方法名。继续此示例，我们可以更新列表 5.2 以利用静态 `System.Console` 指令来创建列表 5.13。

## 列表 5.13：使用 static 指令

在这种情况下，代码的可读性没有损失：`WriteLine()`、`Write()` 和 `ReadLine()` 都与控制台有关。然而，有时并非如此。例如，如果两个类型具有重名，使用 `static` 将导致歧义。

274 页 第 5 章：参数与方法

## using static 指令

使用指令允许你通过省略名称中的命名空间部分来缩写类型名称——这样对于指定命名空间内的任何类型，只需指定类型名。相比之下，`using static` 指令允许你从指定类型的任何静态成员中同时省略命名空间和类型名。指定 `using static System.Console` 指令允许你使用 `WriteLine()` 而不是 `System.Console.WriteLine()` 的完全限定方法名。继续此示例，我们可以更新列表 5.2 以利用静态 `System.Console` 指令来创建列表 5.13。

## 列表 5.13：使用 static 指令

在这种情况下，代码的可读性没有损失：`WriteLine()`、`Write()` 和 `ReadLine()` 都与控制台有关。然而，有时并非如此。例如，如果两个类型具有重名，使用 `static` 将导致歧义。

275 页 

你不仅可以在文件顶部拥有使用指令，还可以在命名空间声明的顶部包含它们。例如，如果声明了一个新的命名空间 `EssentialCSharp`，则在命名空间顶部使用使用指令是可能的（参见列表 5.12）。

## 别名 (Aliasing)

从 C# 12.0 开始，使用指令还允许映射命名空间或任何类型，包括元组（第 23 章）、数组类型和泛型类型（第 12 章）。别名是在使用指令应用的文本内使用的替代名称。别名的两个常见理由是消除相同类型的歧义以及缩写长名称。在列表 5.14 中，例如，是为了引用 `System.Timers.Timer` 类型。仅仅添加 `using Timers` 不以让代码避免限定 `Timer`。因为 `System.Threading` 也包含一个名为 `Timer` 的类型。

### 列表 5.14：声明类型别名

```csharp
using CountdownTimer = System.Timers.Timer;
using StartStop = (DateTime Start, DateTime Stop);

public class HelloWorld
{
    public static void Main()
    {
        CountdownTimer timer;
        StartStop startStop;
    }
}
```

## 列表 5.15：声明同名的类型别名

```csharp
// 声明 Timer 引用 System.Timers.Timer
// 避免与 System.Threading.Timer 冲突
using Timer = System.Timers.Timer;

public class HelloWorld
{
    public static void Main()
    {
        Timer timer;

        // ...
    }
}
```

由于别名指令，`Timer` 不再是歧义引用。此外，要引用 `System.Threading.Timer` 类型，你必须限定该类型或定义不同的别名。

当然，C# 10 及更高版本还支持全局别名指令，例如：

```csharp
global using Timer = Timers.Timer;
```

与其他所有全局指令一样，可以在 `csproj` 文件中配置全局别名指令：

```xml
<Using Include="System.Timers.Timer" Alias="Timer"/>
```

# Main 方法的返回值与参数

到为止，可执行文件的 Main 方法声明一直是可能的简单声明。你没有在你的中包含任何参数或非 void 返回类型

