
# 输出 1.1

| 51° 52' E | -1° -20' N |
| 48° 52' E | -2° -20' N |
| 51° 52' E | -1° -20' N |

对于 `Coordinate`，你实现 `-` 和 `+` 运算符来返回加减坐标。这允许你连接多个运算符和操作数，例如 `result = ((coordinate1 + arc1) + arc2)`。此外，通过在 `Arc` 上支持相同的 `+/-`（参见本章后面的列表 10.4），你可以消除括号。这种方法之所以有效，是因为第一个操作数 (`arc1 + arc2`) 的结果是 `Arc`，你可以将其添加到下一个类型为 `Arc`。

相比之下，考虑如果你提供一个以两个 `Coordinates` 为参数并返回坐标之间距离 `double` 的运算符会发生什么。对 `Coordinate` 添加 `double` 是未定义的。

## 赋值与二元运算符结合 (`+=`, `-=`, `*= /= ===`, ...)

如前所述，不支持重载赋值运算符。然而，与二元运算符结合的赋值运算符（`+=`、`-=`、`*=`、`/=`、`&=`、`^=`、`<<=` 和 `>>=`）在重载二元运算符时实际上被重载了。给定没有赋值的二元运算符，C# 自动允许结合赋值。使用列表 10.2 中 `Coordinate` 的定义，因此你可以拥有代码

```csharp
coordinate += arc;
```

这等同于

```csharp
coordinate = coordinate + arc;
```

## 条件逻辑运算符 (`&&`, `||`)

类似于赋值运算符，条件逻辑运算符无法显式重载。然而，逻辑运算符 `&` 和 `|` 可以被重载，而条件运算符包含了逻辑运算符，实际上可以重载条件运算符。`x && y` 被处理为 `x & y`，其中 `y` 必须为真。同样，`x || y` 仅在 `x` 为假时被处理为 `x | y`。为了支持对类型进行真假评估（例如在语句中），有必要重载真/假一元运算符。

## 一元运算符 (`+`, `-`, `!`, `~`, `+, --`, true, false)

重载一元运算符与重载二元运算符非常相似，区别在于它们只接受一个参数，该参数也是包含类型。列表 10.4 重载了 `Longitude` 和 `Latitude` 的 `+` 和 `-` 运算符，然后在重载 `Arc` 中相同的运算符时使用了这些运算符。

与数值类型一样，此列表中的 `+` 运算符没有任何效果，提供它是为了保持对称性。

### 列表 10.4: 重载 – 和 + 一元运算符

```cs
// ...
    public static Latitude operator -(Latitude latitude)
{
        return new Latitude(-latitude.Degrees);
    }
    public static Latitude operator +(Latitude latitude)
{
        return latitude;
    }
    // ...
```

```cs
public struct Longitude
{
// ...
    public static Longitude operator -(Longitude longitude)
{
        return new Longitude(-longitude.Degrees);
    }
    public static Longitude operator +(Longitude longitude)
{
        return longitude;
    }
    // ...
}
```

```cs
public readonly struct Arc
{
// ...
    public static Arc operator -(Arc arc)
{
        // 使用定义在
        // Longitude 和 Latitude 上的一元 – 运算符
        return new Arc(-arc.LongitudeDifference, -arc.LatitudeDifference);
    }
```

```cs
public static Arc operator +(Arc arc)
{
    return arc;
```

## 第 10 章：良好的类型 (Well-Formed Types)

重载 `true` 和 `false` 运算符需要满足额外要求，即两者都必须重载——而不仅仅是其中一个。其签名与其他运算符重载相同；但是，如列表 10.5 所示，返回类型必须是 `bool`。

### 列表 10.5: 重载 true 和 false 运算符

```cs
public static bool operator false(object item)
{
    // ...
}
public static bool operator true(object item)
{
    // ...
}
```

你可以在重载了 `true` 和 `false` 运算符的类型可以使用在 `if`、`do`、`while` 和 `for` 控制表达式中。

## 转换运算符

目前，`Longitude`、`Latitude` 和 `Coordinate` 不支持强制转换为替代类型。例如，没有方法可以将 `double` 转换为 `Longitude` 或 `Latitude` 实例。同样，不支持使用字符串为 `Coordinate` 赋值。幸运的是，C# 提供了专门用于处理从一种类型转换为另一种类型的方法定义。此外，方法声明允许指定转换是隐式的（`implicit`）还是显式的（`explicit`）。

## 高级主题

### 强制转换运算符 (`()`)

实现显式和隐式转换运算符在技术上并不等同于重载强制转换运算符 (`()`)。然而，这种操作实际上就是所发生的情况，因此定义强制转换运算符是实现显式或隐式转换的常用术语。

定义转换运算符的风格与定义任何其他运算符相似，不同之处“`operator`”是转换的结果类型。此外，`operator` 关键字紧跟在一个指示转换是隐式还是显式的关键字之后（参见列表 10.6）。

#### 列表 10.6: 提供 Latitude 和 double 之间的隐式转换

```cs
public readonly struct Latitude
{
    // ...
    public double DecimalDegrees(double decimalDegrees)
    {
        DecimalDegrees = Normalize(decimalDegrees);
    }
    public double DecimalDegrees { get; }
    // ...
    public static implicit operator double(Latitude latitude)
    {
        return latitude.DecimalDegrees;
    }
    public static implicit operator Latitude(double degrees)
    {
        return new Latitude(degrees);
    }
    // ...
}
```

通过这些转换运算符，你现在可以隐式地在 `double` 和 `Latitude` 对象之间进行转换。假设 `Longitude` 也存在类似的转换，你可以通过指定每个坐标部分的十进制度数部分（例如：`coordinate = new Coordinate(43, 172);`）来简化 `Coordinate` 对象的创建。

> 注意
> 在实现转换运算符时，返回值或参数必须是封装的类型——以支持封装。C# 不允许你在被转换类型的范围之外指定转换。

## 转换运算符指南

定义隐式和显式转换运算符的区别在于防止意外的隐式转换导致导致不预期的行为。你应该意识到使用显式转换运算符的两个可能后果。首先，抛出异常的转换运算符应该总是显式的。例如，为了防止数据丢失，从 `float` 转换到 `int` 应该是显式的，这需要你是有意为为。此外，确保格式是正确的。第二个考虑是，从 `float` 转换到 `int` 可能会导致数据。如果转换是意外的，请考虑抛出 `System.InvalidException`。

## 引用程序集

## 指南

- 如果转换是隐式的，请不要提供强制转换运算符。
- 不要在隐式转换时抛出异常。

## 引用程序集

与其将所有代码放在一个巨大的二进制文件中，C# 框架允许你将代码分到多个程序。这种方法允许你在多个可执行文件中复用代码。

## 初学者主题

### 类库
`HelloWorld` 程序是你编写的最简单的程序之一。真实世界中的程序更为复杂，随着复杂性的增加，将程序分成部分是有帮助的。为了这样做，开发者将程序移动到独立的编译单元中，称为类库。程序随后引用并依赖类库。

通常，我们的代码对多个程序都有用。例如，在映射程序中使用 `Longitude`、`Latitude` 和 `Coordinate` 类，或者编写数字地理编码程序。这些类和类集合可以编写一次并在多个程序中复用。因此，它们需要分组到程序集库中。

创建一个库而不是控制项目，只有一个例外：对于 .NET CLI，使用 `classlib` 作为项目名称。同样，在 Visual Studio 2022 中，从 `File->New Project...` 项目（`Ctrl+Shift+N`），在搜索框中查找所有 `Class Library` 模板，然后选择 `Class Library——Visual C#` 版本，使用 `GeoCoordinates` 作为项目名称。

接下来，将列表 10.4 中的源码放在每个结构的单独文件中，并以结构体命名，然后生成项目。生成项目会将 C# 代码编译为程序集——一个 `GeoCoordinates.dll` 文件——并将其放在 `.\bin\` 子目录下。

## 第 10 章：良好的类型

### 引用库

给定库，我们需要从程序中引用它。例如，对于使用列表 10.3 中 `Program` 类的新控制程序，我们需要为 `GeoCoordinates.dll` 程序集添加引用，识别库所在的位置并将唯一标识库的元数据嵌入程序中。有几种方法可以实现这一点。首先，你可以引用库项目文件（`*.csproj`），识别哪个项目包含库源码并在两个项目之间建立依赖关系。在编译库之前，无法编译引用库的程序。这种依赖关系会在编译程序时编译库（如果库尚未编译）。换句话说，引用编译后的库（`*.dll`）而不是项目。

第三，你可以引用 `NuGet` 包，如下一节所述。

请注意，并非只有控制程序可以引用库和包。事实上，任何程序集都可以引用任何其他程序集。通常，一个库会引用另一个库，从而形成依赖链。

## 使用 Dotnet CLI 引用项目或库

在第 1 章中，我们讨论了如何创建一个控制台程序。这样做创建了一个包含 `Main` 方法的程序——这是程序开始执行的入口点。要为新创建的程序集添加引用，我们可以在之前的地方继续，使用额外的命令来添加引用：

```bash
dotnet add .\HelloWorld\HelloWorld.csproj package \GeoCoordinates\Debug\netcoreapp2\GeoCoordinates.dll
```

`add` 参数之后是项目所引用的已编译程序集的文件路径。
与其引用程序集，你也可以引用项目文件。正如前面提到的，这会将项目连接起来，因此生成程序时将触发类库的编译（如果尚未编译的话）。这样做的优点是，程序编译时，它会自动定位编译后的类库程序集——无论是在 `debug` 还是 `release` 目录下。引用项目文件的命令如下：

```bash
dotnet add .\HelloWorld\HelloWorld.csproj reference \GeoCoordinates\GeoCoordinates.csproj
```

如果你拥有类库的源代码且该源代码频繁更改，请考虑使用类项目文件来引用类库，而不是引用编译后的程序集。
完成项目或已编译程序集的引用后，你的项目就可以使用列表 10.3 中的 `Program` 类源代码进行编译了。

## 使用 Visual Studio 2022 引用项目或库

在第 1 章中，我们还讨论了如何使用 Visual Studio 创建控制台程序。这创建了一个包含 `Main` 方法的程序。要添加对 `GeoCoordinates` 程序集的引用，点击 `Project->Add Reference...` 菜单项。

接下来，在 `Projects\Solution` 选项卡中，选择 `GeoCoordinates` 项目并点击 `OK` 确认引用。

同样，若要添加程序集引用，请按照之前的相同过程操作，点击 `Project->Add Reference...` 菜单项。但是，这次点击 `Browse...` 按钮并导航到选择 `GeoCoordinates.dll` 程序集。

与使用 `Dotnet CLI` 一样，你可以使用列表 10.3 中的 `Program` 类代码编译程序项目。

## NuGet 打包

从 Visual Studio 2010 开始，微软引入了一种名为 `NuGet` 的库打包系统。该系统旨在提供一种在项目之间以及公司之间轻松共享库的方法。通常，一个库程序集不仅仅是一个单一的编译文件。它可能包含配置文件、其他资源以及相关的元数据。遗憾的是，在 `NuGet` 出现之前，没有可以标识所有依赖项的清单。此外，也没有标准的提供程序或包库来存放被引用的程序集。

`NuGet` 解决了这两个问题。`NuGet` 不仅包含一个可以标识作者、公司、依赖项等信息的清单，它还带有一个默认的包提供程序——`NuGet.Org`，在该网站上，包被上传、更新、索引，然后由想要利用它们的项目下载。通过 `NuGet`，你可以引用一个 `NuGet` 包（`*.nupkg`），它将将从你预配置的其中一个 `NuGet` URL 自动安装。

`NuGet` 包附带有一个清单（`*.nuspec` 文件），其中包含了包中包含的所有额外元数据。此外，它还提供了你可能需要的所有资源——本地化文件、配置文件、内容文件等。最终，`NuGet` 包是将所有单独资源组合成单个 ZIP 文件的归档——尽管扩展名为 `.nupkg`。如果你将文件重命名为 `*.zip` 扩展名，可以使用任何常用工具打开并检查该文件。

## 使用 Dotnet CLI 添加 NuGet 引用

要使用 `Dotnet CLI` 向项目添加 `NuGet` 包，需要：

```bash
dotnet add .\HelloWorld\HelloWorld.csproj package Microsoft.Extensions.Logging
```

要创建一个本地包，请使用 `dotnet` 命令：

```bash
dotnet pack
```

## 使用 Visual Studio 2022 添加 NuGet 引用

如果你按照 Visual Studio 2022 的说明进行操作：

1. 点击 `Project->Manage NuGet Packages...` 菜单项。
2. 选择 `Browse` 选项卡并在搜索框中输入 `Microsoft.Extensions.Logging`。
3. 点击 `Install` 按钮安装该包。

完成这些步骤后，`Microsoft.Extensions.Logging` 库将（添加到你的项目中，并包含它可能具有任何依赖项。

## 类型封装
...

## 类型的封装

程序集必须标记为 `public`。因此，在编译 `Coordinates.dll` 程序集之前，有必要确保类型声明是 `public`（参见列表 10.8）。

### 列表 10.8：在程序集外部使类型可用

```csharp
public struct Coordinate
{
    // ...
}
public struct Latitude
{
    // ...
}
public struct Longitude
{
    // ...
}
public struct Arc
{
    // ...
}
```
