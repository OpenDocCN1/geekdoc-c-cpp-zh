
## 表 2.5 常见的 Guid 成员

| 名称 | 描述 |
| --- | --- |
| CompareTo | 将当前实例与指定的*Guid*进行比较 |
| Empty | 一个只读实例，表示值保证全为零的*Guid* |
| NewGuid | 创建*Guid*结构体的新实例 |
| Parse | 将*GUID*的字符串表示转换为等效的*Guid*实例 |
| TryParse | 将*GUID*的字符串表示转换为等效的*Guid*实例，并指示转换是否成功 |

## 统一资源标识符（URI）

统一资源标识符（URI）是可用于内网或互联网上资源的一种紧凑表示形式，它可以是绝对 URI（如网页地址），也可以是必须相对于基础 URI 进行扩展的相对 URI。

*Uri* 类允许你创建新的 URI 值并访问 URI 的各个部分，同时提供用于处理 URI 的方法，例如解析、比较和组合。表 2.6 列出了一些常见成员。

## 表 2.6 常见的 Uri 成员

| 名称 | 描述 |
| --- | --- |
| AbsoluteUri | 获取绝对 URI |
| Compare | 使用指定的比较规则比较两个 URI 实例的指定部分 |
| EscapeUriString | 将 URI 字符串转换为其转义表示形式 |
| IsFile | 获取一个值，指示指定的*Uri*是否为文件 URI |
| LocalPath | 获取文件名的本地操作系统表示 |
| MakeRelativeUri | 确定两个*Uri*实例之间的差异 |
| TryCreate | 创建一个新的*Uri*，但如果无法创建*Uri*，则不抛出异常 |

*Uri* 类的实例是不可变的。若要创建可修改的 URL，请使用*UriBuilder*类。*UriBuilder*类允许你轻松更改 URI 的属性，而无需在每次修改时创建新实例。表 2.7 中显示的所有属性都是*Uri*（在其中它们是只读的）和*UriBuilder*共有的，除了*Uri*属性，该属性仅在*UriBuilder*上可用。

## 表 2.7 常见的 Uri 和 UriBuilder 属性

| 名称 | 描述 |
| --- | --- |
| Fragment | 获取或设置 URI 的片段部分 |
| Host | 获取或设置服务器的主机名或 IP 地址 |
| Password | 获取或设置与访问 URI 的用户关联的密码 |
| Path | 获取或设置由 URI 定义的资源路径 |
| Port | 获取或设置 URI 的端口号 |
| Query | 获取或设置包含在 URI 中的任何查询信息 |
| Scheme | 获取或设置 URI 的方案名称 |
| Uri | 获取由指定的 UriBuilder 实例构造的 Uri 实例 |
| UserName | 获取或设置与访问 URI 的用户关联的用户名 |

示例 2.1 展示了如何使用 UriBuilder 类。

## 示例 2.1 使用 UriBuilder

```csharp
Uri immutableUri = new Uri("http://www.example.com");
Console.WriteLine(immutableUri);

UriBuilder mutableUri = new UriBuilder(immutableUri);
Console.WriteLine(mutableUri);

mutableUri.Scheme = "https";
mutableUri.Host = "www.example.com";
mutableUri.Path = "exampleFile.html";
Console.WriteLine(mutableUri);
```

## BigInteger

System.Numerics.BigInteger 类型表示一个任意大的整数值，该值没有理论上的上限或下限。一旦创建了一个 BigInteger 实例，你就可以像使用其他整数类型一样使用它，从而执行基本的数学运算和比较。

BigInteger 结构体还包括直接对应于其他整数类型成员的成员，但还添加了对应于 Math 类提供的方法以及特定于处理 BigInteger 实例的成员。表 2.8 展示了常见成员。

## 表 2.8 常见的 BigInteger 成员

| 名称 | 描述 |
| :--- | :--- |
| Abs | 返回 BigInteger 值的绝对值 |
| DivRem | 返回除法操作的商和余数 |
| GreatestCommonDivisor | 返回两个 BigInteger 值的最大公约数 |
| IsEven | 指示当前 BigInteger 值是否为偶数 |
| IsOne | 指示当前 BigInteger 值是否为 BigInteger.One |
| IsZero | 指示当前 BigInteger 值是否为 BigInteger.Zero |
| Max | 返回两个 BigInteger 值中较大的一个 |
| Min | 返回两个 BigInteger 值中较小的一个 |
| MinusOne | 获取表示负一（-1）的值 |
| One | 获取表示一（1）的值 |
| Remainder | 对两个 BigInteger 值执行整数除法并返回余数 |
| Sign | 获取指示当前 BigInteger 值符号的数字 |
| Zero | 获取表示零（0）的值 |

示例 2.2 展示了一些使用 BigInteger 类型的方法。

## 示例 2.2 使用 BigInteger

```csharp
BigInteger b1 = new BigInteger(987321.5401);
BigInteger b2 = (BigInteger)435623411897L;
BigInteger b3 = BigInteger.Parse("435623411897");

Console.WriteLine(BigInteger.Pow(Int32.MaxValue, 2));
Console.WriteLine(b2 == b3);
Console.WriteLine(BigInteger.GreatestCommonDivisor(b1, b2));
```

## 运算符

C# 支持多种运算符，但我们仅涵盖较常用的那些。**运算符**是一种特殊符号，用于指示在表达式中执行哪种运算。所有 C# 预定义类型都支持运算符，尽管并非所有类型都支持相同的运算符。

表 2.9 按优先级顺序列出了所有 C# 运算符。在每个类别内，运算符具有相等的优先级。

**表 2.9** C# 中的运算符及运算符优先级

| 类别 | 运算符 |
| :--- | :--- |
| 基本 | x, y f(x) a[x] x++ x-- new typeof checked unchecked -> |
| 一元 | + - ! - ++x --x (T)x true false & sizeof |
| 乘法 | * / % |
| 加法 | + - |
| 移位 | << >> |
| 关系和类型测试 | < > <= >= is as |
| 相等 | == != |
| 逻辑与 | & |
| 逻辑异或 | ^ |
| 逻辑或 | \|
| 条件与 | && |
| 条件或 | \|\| |
| 条件 | ? : |
| 赋值 | = += -= *= /= %= &= \|= ^= <<= >>= |
| 空合并 | ?? |
| Lambda | => |

### 算术和赋值运算符

你在之前的许多示例中已经看到赋值运算符（=）。该运算符仅将右操作数的值存储在由左操作数指示的变量中。两个操作数必须具有相同的类型，或者右操作数必须能隐式转换为左操作数的类型。

C# 提供了支持标准数学运算（加法 (+)、减法 (-)、乘法 (*) 和除法 (/)）的算术运算符。C# 算术运算符的行为与你在学校学到的算术规则之间存在细微差别。特别是，整数除法的行为因所除的数据类型不同而略有不同。将一个整数除以另一个整数时，结果是整数。任何余数都会被丢弃，并且结果向零舍入。要获取整数除法的余数，你必须使用取模运算符（%）。

C# 还支持复合赋值运算符，它将算术运算和赋值组合在单个运算符中。每个标准算术运算符和取模运算符都有一个相应的运算（+=、-=、*=、/=）以及取模运算符（%=），它们将加法、减法、乘法、除法和取模除法与赋值组合在一起。

例如，假设你需要将一个变量递增 1。使用标准算术运算符，这样的操作通常看起来像这样：

```csharp
i = i + 1;
```

然而，通过使用加法复合赋值运算符，此操作可以像这样执行：

```csharp
i += 1;
```

将这种简化进一步扩展，你可以使用**递增**（++）和**递减**（--）运算符将值增加或减少 1。递增和递减运算符可以出现在被修改变量的前面（前缀）或后面（后缀），并将该变量的内容改变一个单位。前缀形式的结果是变量在发生更改之前的值，而后缀形式的结果则是更改后的值。

示例 2.3 中显示的所有操作都是等效的，并展示了如何使用基本运算符、复合赋值运算符和递增运算符。

## 示例 2.3 递增值

```csharp
i = i + 1;
i += 1;
i++;
```

