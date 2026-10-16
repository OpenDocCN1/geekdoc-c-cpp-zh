
```
// do some clever casting to get pCents to point to cents
// inside amount2
CurrencyStruct* pTempCurrency = (CurrencyStruct*)pCents;
pCents = (byte*)--pTempCurrency;
WriteLine("Address of pCents is now 0x{0:X}", (ulong)pCents);
```

最后，你使用 `fixed` 关键字创建一些指向类实例字段的指针，并使用这些指针设置该实例的值。注意，这也是你第一次能够查看堆上存储项的地址，而不是栈上的地址：

```
WriteLine("\nNow with classes");
// now try it out with classes
var amount3 = new CurrencyClass();

fixed(long* pDollars2 = &(amount3.Dollars))
fixed(byte* pCents2 = &(amount3.Cents))
{
    WriteLine($"amount3.Dollars has address 0x{(ulong)pDollars2:X}");
    WriteLine($"amount3.Cents has address 0x{(ulong)pCents2:X}");
    *pDollars2 = -100;
    WriteLine($"amount3 contains {amount3}");
}
```

编译并运行这段代码，会得到类似如下的输出：

```
Size of CurrencyStruct struct is 16
Address of amount1 is 0xD290DCD7C0
Address of amount2 is 0xD290DCD7B0
Address of pAmount is 0xD290DCD7A8
Address of pDollars is 0xD290DCD7A0
Address of pCents is 0xD290DCD798
amount1 contains $ 20.50
amount2 has address 0xD290DCD7B0 and contains $ 0.0
Address of pCents is now 0xD290DCD7B8

Now with classes
amount3.Dollars has address 0xD292C91A70
amount3.Cents has address 0xD292C91A78
amount3 contains $ -100.0
```

请注意此输出中显示的 `amount2` 的未初始化值，并注意 `CurrencyStruct` 结构体的大小是 16——考虑到其字段的大小（一个 `long` 和一个 `byte` 总共应为 9 字节），这比预期的要大一些。

## 使用指针优化性能

目前为止，所有示例都是为了演示你可以用指针做的各种事情。你以一种或许只对那些喜欢了解底层机制的人感兴趣的方式玩弄了内存，但这并不能真正帮助你写出更好的代码。现在你将运用你对指针的理解，看一个示例，了解明智地使用指针如何带来显著的性能优势。

## 创建基于栈的数组

本节探讨指针有用的主要领域之一：在栈上创建高性能、低开销的数组。正如第 2 章“核心 C#”中所讨论的，C# 对处理数组提供了丰富的支持。第 7 章“数组与元组”更详细地介绍了数组。尽管 C# 使得使用一维数组、矩形数组或交错多维数组都非常容易，但它的缺点在于这些数组实际上是对象；它们是 `System.Array` 的实例。这意味着数组存储在堆上，并带来所有相关的开销。在某些情况下，你可能需要创建一个短生命周期的高性能数组，而不希望有引用对象的开销。你可以使用指针来实现这一点，但这仅对于一维数组来说比较容易。

要创建高性能数组，你需要使用一个新关键字：`stackalloc`。`stackalloc` 命令指示 .NET 运行时在栈上分配一定数量的内存。当你调用 `stackalloc` 时，需要提供两条信息：

- 你要存储的数据类型
- 你需要存储的这些数据项的数量

例如，要分配足够的内存来存储 10 个 `decimal` 数据项，可以编写以下代码：

```
decimal* pDecimals = stackalloc decimal[10];
```

此命令只是分配栈内存；它不会尝试将内存初始化为任何默认值。对于此示例而言，这没有问题，因为你正在创建一个高性能数组，而对值进行不必要的初始化会损害性能。

类似地，若要存储 20 个 `double` 数据项，可以这样编写：

```
double* pDoubles = stackalloc double[20];
```

尽管这行代码将要存储的变量数量指定为常量，但它同样可以是在运行时计算出的数量。因此，你可以将前面的示例写成这样：

```
int size;
size = 20; // 或者在运行时计算出的其他值
double* pDoubles = stackalloc double[size];
```

从这些代码片段可以看出，`stackalloc` 的语法略微不寻常。它后面紧接着你要存储的数据类型的名称（必须是值类型），然后是所需存储空间的项数，放在方括号中。分配的字节数等于这个数字乘以 `sizeof(数据类型)`。前面的代码示例中使用方括号暗示了数组，这并不令人意外。如果你为 20 个 `double` 分配了空间，那么你所拥有的就是一个包含 20 个 `double` 的数组。你可以拥有的最简单的数组类型是一块内存，它一个接一个地存储元素（见图 5.7）。

![](img/3d365b72b289213a91ade7eb366b8f35_236_0.png)

*图 5.7*

此图还显示了 `stackalloc` 返回的指针，它始终是指向所分配数据类型的指针，并且指向新分配内存块的顶部。要使用该内存块，你只需解引用返回的指针即可。例如，要分配 20 个 `double` 的空间，然后将第一个元素（数组的元素 0）设置为值 3.0，可以这样编写：

```
double* pDoubles = stackalloc double[20];
*pDoubles = 3.0;
```

要访问数组的下一个元素，你可以使用指针运算。如前所述，如果对指针加 1，其值将增加它所指向数据类型的大小。在这种情况下，这个增量恰好足以带你到达已分配块中的下一个空闲内存位置。因此，你可以将数组的第二个元素（元素编号 1）设置为值 8.4：

```
double* pDoubles = stackalloc double[20];
*pDoubles = 3.0;
*(pDoubles + 1) = 8.4;
```

同理，你可以使用表达式 `*(pDoubles + x)` 访问数组中索引为 `x` 的元素。

实际上，你拥有了一种可以访问数组元素的方法，但对于通用用途来说，这种语法过于复杂。幸运的是，C# 定义了一种使用方括号的替代语法。当方括号应用于指针时，C# 对方括号给出了非常精确的含义；如果变量 `p` 是任何指针类型，`x` 是整数，那么表达式 `p[x]` 总是被编译器解释为 `*(p+x)`。这对于所有指针都成立，不仅限于使用 `stackalloc` 初始化的指针。借助这种简写符号，你现在有了一种非常便捷的语法来访问数组。事实上，这意味着你访问基于栈的一维数组的语法与访问由 `System.Array` 类表示的基于堆的数组的语法完全相同：

```
double* pDoubles = stackalloc double [20];
pDoubles[0] = 3.0; // pDoubles[0] 等同于 *pDoubles
pDoubles[1] = 8.4; // pDoubles[1] 等同于 *(pDoubles+1)
```

> 注意：将数组语法应用于指针的想法并不新鲜。自从 C 和 C++ 语言发明以来，这一直是这两种语言的基本组成部分。事实上，C++ 开发人员会认识到，使用 `stackalloc` 获得的基于栈的数组与经典的基于栈的 C 和 C++ 数组基本一致。这种语法及其将指针和数组联系起来的方式，是 C 语言在 20 世纪 70 年代流行起来的原因之一，也是指针使用在 C 和 C++ 中成为一种如此流行的编程技术的主要原因。

尽管你的高性能数组可以像普通 C# 数组一样访问，但仍需提醒一句。以下 C# 代码会引发异常：

```
double[] myDoubleArray = new double [20];
myDoubleArray[50] = 3.0;
```

异常发生是因为你试图使用越界的索引访问数组；索引为 50，而允许的最大值是 19。然而，如果你使用 `stackalloc` 声明等效数组，则数组周围没有可以执行边界检查的对象。因此，以下代码不会引发异常：

```
double* pDoubles = stackalloc double [20];
pDoubles[50] = 3.0;
```

在这段代码中，你分配了足够的内存来容纳 20 个 `double`。然后你从该内存起始位置加上 `50*sizeof(double)` 的位置开始，设置 `sizeof(double)` 个内存位置来存放 `double` 值 3.0。不幸的是，该内存位置远远超出了你为这些 `double` 分配的内存区域。无法知道该地址可能存储着什么数据。最好的情况是，你可能使用了一些当前未使用的内存，但同样有可能你刚刚覆盖了栈中某些用于存储其他变量，甚至存储当前正在执行的方法的返回地址的位置。同样，你会看到，从指针中获得的高性能是有代价的；你需要确定自己知道自己在做什么，否则你将会遇到一些非常奇怪的运行时错误。

## QuickArray 示例

关于指针的讨论以一个名为 QuickArray 的 `stackalloc` 示例结束。在此示例中，程序只是询问用户希望为数组分配多少个元素。然后代码使用 `stackalloc` 分配一个该大小的 `long` 数组。该数组的元素被填充为从 0 开始的整数的平方，并将结果显示在控制台上（代码文件 `QuickArray/Program.cs`）：

```
using static System.Console;

namespace QuickArray
{
    public class Program
    {
        unsafe public static void Main()
        {
            Write("How big an array do you want? \n>");
            string userInput = ReadLine();
            uint size = uint.Parse(userInput);

            long* pArray = stackalloc long[(int) size];
            for (int i = 0; i < size; i++)
            {
                pArray[i] = i*i;
            }

            for (int i = 0; i < size; i++)
            {
                WriteLine($"Element {i} = {*(pArray + i)}");
            }

            ReadLine();
        }
    }
}
```

以下是 QuickArray 示例的输出：

```
How big an array do you want?
> 15
```

```
Element 0 = 0
Element 1 = 1
Element 2 = 4
Element 3 = 9
Element 4 = 16
Element 5 = 25
Element 6 = 36
Element 7 = 49
Element 8 = 64
Element 9 = 81
Element 10 = 100
Element 11 = 121
Element 12 = 144
Element 13 = 169
Element 14 = 196
```

## 平台调用

并非所有的 Windows API 调用功能都可以从 .NET Framework 中使用。这不仅适用于旧的 Windows API 调用，也适用于 Windows 10 或 Windows Server 2016 中的全新功能。也许你已经编写了一些导出非托管方法的 DLL，并且也希望从 C# 中使用它们。

要重用不包含 COM 对象的非托管库——它只包含导出的函数——你可以使用平台调用（P/Invoke）。借助 P/Invoke，CLR 会加载包含应调用函数的 DLL，并对参数进行封送处理。

要使用非托管函数，首先必须确定该函数导出时的名称。你可以使用带有 `/exports` 选项的 `dumpbin` 工具来完成此操作。

例如，以下命令

```
dumpbin /exports c:\windows\system32\kernel32.dll | more
```

会列出 DLL `kernel32.dll` 中所有导出的函数。在该示例中，可以使用 `CreateHardLink` Windows API 函数为现有文件创建硬链接。使用此 API 调用，你可以让多个文件名引用同一个文件，只要这些文件名位于同一块硬盘上。此 API 调用在 .NET Framework 4.5.1 中不可用，因此必须使用平台调用。

要调用原生函数，你必须定义一个 C# 外部方法，其参数数量相同，并且非托管方法中定义的自变量类型必须在托管代码中具有匹配的类型。

Windows API 调用 `CreateHardLink` 在 C++ 中的定义如下：

```
BOOL CreateHardLink(
    LPCTSTR lpFileName,
    LPCTSTR lpExistingFileName,
    LPSECURITY_ATTRIBUTES lpSecurityAttributes);
```

此定义必须映射到 .NET 数据类型。非托管代码中的返回类型是 `BOOL`；它直接映射到 `bool` 数据类型。`LPCTSTR` 定义了一个指向 const 字符串的长指针。Windows API 对数据类型使用了匈牙利命名约定。`LP` 表示长指针，`C` 表示 const，`STR` 表示以 null 结尾的字符串。`T` 将该类型标记为泛型类型，该类型会解析为 `LPCSTR`（ANSI 字符串）或 `LPWSTR`（宽 Unicode 字符串），具体取决于编译器设置到 32 位还是 64 位。C 字符串映射到 .NET 的 `String` 类型。`LPSECURITY_ATTRIBUTES` 是一个指向 `SECURITY_ATTRIBUTES` 结构体的长指针。因为可以向此参数传递 `NULL`，所以将该类型映射到 `IntPtr` 是可以的。此方法的 C# 声明必须标记为 `extern` 修饰符，因为 C# 代码中没有此方法的实现。相反，该方法实现位于 `kernel32.dll` 中，并通过 `[DllImport]` 属性进行引用。.NET 声明 `CreateHardLink` 的返回类型是 `bool`，而原生方法 `CreateHardLink` 返回的是 `BOOL`，因此一些额外的说明会很有用。由于 C++ 中存在不同的布尔数据类型（例如原生 `bool` 和 Windows 定义的 `BOOL`，它们的值不同），`[MarshalAs]` 属性指定了 .NET 的 `bool` 类型应映射到哪种原生类型：

```
[DllImport("kernel32.dll", SetLastError = true, EntryPoint = "CreateHardLinkW", CharSet = CharSet.Unicode)]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool CreateHardLink(string newFileName, string existingFileName, IntPtr securityAttributes);
```

> 注意：网站 `http://www.pinvoke.net` 对于从原生代码到托管代码的转换非常有帮助。

可以使用 `[DllImport]` 属性指定的设置如下表所示。

| DllImport 属性或字段 | 描述 |
| --- | --- |
| `EntryPoint` | 你可以为函数的 C# 声明指定一个与非托管库中不同的名称。非托管库中方法的名称在 `EntryPoint` 字段中定义。 |
| `CallingConvention` | 根据用于编译非托管函数的编译器或编译器设置，你可以使用不同的调用约定。调用约定定义了如何处理参数以及如何将它们压入栈中。你可以通过设置枚举值来定义调用约定。Windows API 在 Windows 操作系统上通常使用 `StdCall` 调用约定，而在 Windows CE 上使用 `Cdecl` 调用约定。将值设置为 `CallingConvention.Winapi` 可在 Windows 和 Windows CE 环境中都适用于 Windows API。 |
| `CharSet` | 字符串参数可以是 ANSI 或 Unicode。通过 `CharSet` 设置，你可以定义如何管理字符串。`CharSet` 枚举定义的可能值有 `Ansi`、`Unicode` 和 `Auto`。`CharSet.Auto` 在 Windows NT 平台上使用 Unicode，在 Microsoft 较早的操作系统上使用 ANSI。 |
| `SetLastError` | 如果非托管函数使用 Windows API `SetLastError` 设置了错误，你可以将 `SetLastError` 字段设置为 `true`。这样，之后就可以使用 `Marshal.GetLastWin32Error` 读取错误号。 |

为了使 `CreateHardLink` 方法更易于在 .NET 环境中使用，你应该遵循以下准则：
