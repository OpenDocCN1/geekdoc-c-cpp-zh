

let unsignednativeint = 76sun
let long = 12345678912345789L
let unsignedlong = 12345678912345789UL
let float32 = 42.8F
let float = 42.8

printf "int" = %d or "%A" int
printf "string" = %s or "%A" string string
printf "char" = %c or "%A" char char
printf "bool" = %b or "%A" bool bool
printf "bytearray" = "%A" bytearray

printf "hex int" = %x or "%A" hexint
printf "HEX INT" = %x or "%A" hex bigint
printf "oct int" = %o or "%A" octal octint
printf "bin int" = %b or "%A" binaryinteger binaryinteger
printf "signed byte" = "%A" signedbyte
printf "unsigned byte" = "%A" unsignedbyte

printf "small" = %s smallint
printf "small int" = %A" smallint
printf "int" = %i or "%A" integer integer
printf "uint" = %u or "%A" usignedint usignedint
printf "native int" = "%A" native int

printf "unsigned native int" = "%A" unsignednative
printf "long" = %ld or "%A" long long
printf "unsigned long" = "%A" unsignedlong
printf "float" = %f or "%A" float32 float32
printf "double" = %f or "%A" float float

# 执行结果

```
int = 42
string = This is a string or "This is a string"
char = c or 'c'
bool = true or false
bytearray = [84uy; 104uy; 105uy; 115uy; 32uy; 105uy; 115uy; 107uy; 92uy; 92uy 111uy; 116uy; 112uy; 115uy; 116uy; 114uy; 105uy; 107uy; 103uy]
hex int = 34 or 52
HEX INT = 34 or 52
oct int = 42 or 34
bint int = 42 or 42
signed byte = 68uy
unsigned byte = 102uy
small int = 16s
small uint = 16us
int = 345 or 345
uint = 345 or 345u
native int = 765n
unsigned native int = 765sun
long = 123456789123456789L
unsigned long = 123456789123456789UL
float = 42.800000 or 42.7999992f
double = 42.800000 or 42.8
```

第 1 章 C# 和 F 数据结构 13

控制台（Console）具有输入（In）、输出（Out）和错误（Error）标准流。F# 提供了 stdin、stdout、stderr，它们分别对应这三个标准流。对于转换任务，你已经拥有了所有的构建模块。让我们在列表 1-13 中尝试一下吧。

# 列表 1-13 C# 和 F# 版本的 0 到 100 之间奇数之和

```
C# 版本
// 累加 0 到 100 之间的所有奇数并在控制台中输出结果
int sum = 0;
for (int i = 0; i<100; i++)
{
    if (i%2 != 0)
    sum += i;
}
Console.WriteLine("the sum of odd numbers from 0 to 100 is {0}", sum);
```

```
F# 版本
let mutable sum = 0
for i = 0 to 100 do
    if i%2 <> 0 then sum <- sum + i
printf "the sum of odd numbers from 0 to 100 is %A" sum
```

列表 1-14 显示了如何使用列表和 for...in 循环来解决相同的问题。与列表 1-13 相比，这个版本有以下变化：

- 使用 for...in 遍历 0 到 100，`[1..100]` 是一个 F# 列表定义
- 使用 printf 函数遍历 100，它不会输出 "\n"
- 将 %A 替换为 %d，这告诉编译器变量 sum 变量必须是整数

# 列表 1-14 在 for 循环中使用 F# 列表

```
let mutable sum = 0
for i in [0..100] do
    if i%2 <> 0 then sum <- sum + i
printf "the sum of odd numbers from 0 to 100 is %d \n" sum
```

# 运行你的程序

你可以通过两种方式在 Visual Studio 中运行你的程序：创建一个 F# 项目（就像你创建 C# 项目一样），或者使用 Visual Studio 2012 中 F# 支持的以下项目类型：

- F# Application：是一个控制台应用程序模板。
- F# Library：是一个类库模板。
- F# Tutorial：包含 F# 示例的控制台应用程序。建议浏览所有内容。
- F# Portable Library：可以在 Silverlight、手机和 Windows 平台（包括 Windows 8）上执行。
- F# Silverlight Library：是一个类库模板。

如果你想执行此处所示的代码，F# application 项目是一个很好的选择。Visual Studio Express 2012 是免费的。尽管它的名称暗示用于 Web 开发，但你仍然可以使用它创建控制台应用程序。

# 创建控制台应用程序

图 1 显示了项目模板。你可以选择 F# Application 并接受默认名称。F# application 模板创建一个包含默认 Program.fs 文件的解决方案。为了运行整个章节，只需将 Program.fs 的内容替换为列表 1-13 中的 F# 代码。创建其他项目类型的步骤基本相同，所以我就留到此为止。

# 新项目

| .NET Framework 4.5 | 排序：默认 | 已安装的模板 (Ctrl+E) |
|---|---|---|
| 最近 | | |
| 已安装 | F# Application | Visual F |
| 模板 | 用于创建命令行应用程序的项目 | |
| Visual F | F# Library | Visual F |
| Windows | F# Tutorial | Visual F |
| LightSwitch | F# Portable Library | Visual F |
| 其他语言 | F# Silverlight Library | Visual F |
| 其他项目类型 | | |
| 建模项目 | | |
| 示例 | | |
| 在线 | 类型提供模板 | |

| 名称：ConsoleApplication1 | 浏览... | |
|---|---|
| 位置：C:\CodeShar | 为解决方案创建目录 |
| 解决方案名称：ConsoleApplication1 | 添加到源码控制 |

![](6aaf94e2830ab8ce1c5946bef6)

```
// 在 http://Fshar.net 了解更多关于 F#
// 查看 "F# Tutorial" 项目获取更多帮助。

let main () =
    printf "%d\n" 42
    return 0 // 返回整数
```

图 1-2 带有 Program.fs 的 F# 控制台应用程序

第一部分 C# 和 F#

# 使用 F# Interactive

对于像列表 1-13 那样的简单程序，F# 自带了 F# Interactive (FSI) 功能。你可以使用它来测试 F# 代码。在 Visual Studio 中，F# Interactive 窗口可以在 View 菜单中找到。根据你使用的开发配置，你可以在 View、Other Windows 下找到 F# Interactive，也可以直接在 View 菜单中访问它，如图 1-3 所示。FSI 窗口的示例位于图 1-4。

| View | Build | Debug | SQL | Tools |
|---|---|---|---|---|
| Solution Explorer | | | | Ctrl+A |
| Team Explorer | | | | Ctrl+M |
| Server Explorer | | | | Alt+S |
| Architecture Explorer | | | | Ctrl+R |
| SQL Server Object Explorer | | | | Ctrl+S |
| Bookmark Window | | | | Ctrl+K, Ctrl+W |
| Call Hierarchy | | | | |
| Class View | | | | Ctrl+C |
| Code Definition | | | | Shift+V |
| Object Browser | | | | Alt+J |
| F# Interactive | | | | Alt+F |
| Error List | | | | Ctrl+E |
| Output | | | | Alt+2 |
| Start Page | | | | |

图 1-3 从 View 菜单访问 F# Interactive

![](63aaf9e2830ab98ce1c5946bef6_36_0.png)

图 1-4 F# Interactive 窗口

FSI 窗口接受用户输入，因此你可以直接在其中执行代码。你可以使用分号（；）让 FSI 知语句已结束并可以执行。FSI 的一个主要局限是 FSI 窗口不提供 IntelliSense。如果你不想创建一个完整的项目又想使用 IntelliSense，F# 脚本文件是你的最佳选择。你可以前往 File、New 创建一个新的脚本文件，如图 1-5 所示。

# 添加新项 - F#ForC#

![](63aaf9e2830ab98ce1c5946bef6_37_0.png)

图 1-5 F# 模板

> 注意：图 1-5 中列出了许多项目模板。我稍后会介绍它们。现在，你只需要一个 F# 源文件和一个 F# 脚本文件。

F# 源文件和 F# 脚本文件之间的主要区别是生成操作（build action）。F# 源文件是扩展名为 .fs 的文件，其操作是编译（Compile）。F# 脚本文件的扩展名也是 .fs，但其生成操作设置为无（None），这导致它默认进入生成过程。无论你决定使用什么类型的文件，都可以通过选择它并使用上下文（即右键点击）菜单选项执行交互（Execute Interactive）来执行代码。如果你喜欢编写代码，只要开发配置设置为 F#，Alt+Enter 就是快捷键。此命令代表另一个菜单选项在交互执行（Execute In Interactive）。正如名称所示，该选项用于将一行代码发送到 FSI。

执行交互行的快捷键是 Alt+.。

```
let mutable sum = 0.
for i in 1 to 100 do
    if i % 2 = 0 then
        sum <- sum + i
printf "sum of odd numbers from 0 to 100 is %d" sum
```

图 1-6 通过上下文菜单在 FSI 中执行代码

