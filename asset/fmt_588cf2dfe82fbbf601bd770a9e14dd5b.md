
```csharp
class VirtualMemoryManager {
  // ...

  /// <summary>
  /// 内存分配类型。此参数必须包含以下值之一。
  /// </summary>
  [Flags]
  private enum AllocationType : uint {
    /// <summary>
    /// 为指定的内存页在内存或磁盘上的分页文件中分配物理存储。
    /// 该函数将内存初始化为零。
    /// </summary>
    Commit = 0x1000,
    /// <summary>
    /// 在进程的虚拟地址空间中预留一个范围，但不向内存或
    /// 分页文件分配任何物理存储。
    /// </summary>
    Reserve = 0x20000,
    /// <summary>
    /// 表示由 `lpAddress` 和 `dwSize` 指定的内存范围数据不再感兴趣。
    /// 页面将不再从分页文件中读取或写入。然而，
    /// 内存块稍后将再次使用，因此不应取消提交。
    /// 值不能与任何其他值一起使用。
    /// </summary>
    Reset = 0x80000,
    /// <summary>
    /// 分配具有读写访问权限的物理内存。此值仅专门用于地址窗口扩展 (AWE) 内存。
    /// </summary>
    Physical = 0x400000,
    /// <summary>
    /// 在最高可能的地址分配内存。
    /// </summary>
    TopDown = 0x100000
}
}
```

## 第 23 章：平台互操作性与不安全代码

```csharp
/// <summary>
/// 待分配页区域的内存保护。
/// </summary>
[Flags]
private enum ProtectionOptions : uint
{
    /// <summary>
/// 允许对已提交的页区域进行执行访问。
/// 尝试对已提交区域进行读取或写入
/// 将导致访问违规。
    /// </summary>
    Execute = 0x10,
    /// <summary>
/// 允许对已提交的页区域进行执行和读取访问。
/// 尝试对已提交区域进行写入
/// 将导致访问违规。
    /// </summary>
    PageExecuteRead = 0x20,
    /// <summary>
/// 允许对已提交的页区域进行执行、读取和写入访问。
    /// </summary>
    PageExecuteWrite = 0x40,
    /// ...
}

/// <summary>
/// 释放操作类型。
/// </summary>
[Flags]
private enum MemoryFreeType : uint
{
    /// <summary>
/// 取消指定已提交页的提交。
/// 操作后，这些页将处于
/// 状态。
    /// </summary>
    Decommit = 0x4000,
    /// <summary>
/// 释放指定的页区域。在此操作后，
/// 页将处于空闲状态。
    /// </summary>
    Release = 0x0000
}

/// ...
```

枚举（`enums`）的优势在于它们将各种值组合在一起。此外，它们可以将范围限制为除这些值之外的任何内容。

## 使用包装器简化 API 调用

无论关注的是错误处理、结构体还是常量值，高效 API 开发者的一个目标是提供一个简化的托管 API，来封装底层的 Win32 API。例如，列表 23.9 通过公共版本重载了 `VirtualFreeEx()`，从而简化了调用。

### 列表 23.9：封装底层 API

```csharp
class VirtualMemoryManager
{
    // ...

    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool VirtualFreeEx(
        IntPtr hProcess, IntPtr lpAddress,
        IntPtr dwSize, IntPtr dwFreeType);
    public static bool VirtualFreeEx(
        IntPtr hProcess, IntPtr lpAddress,
        IntPtr dwSize)
    {
        bool result = VirtualFreeEx(
            hProcess, lpAddress,
            (IntPtr)MemoryFreeType.Decommit);
        if (!result)
        {
            throw new System.ComponentModel.Win32Exception();
        }
        return result;
    }
    public static bool VirtualFreeEx(
        IntPtr lpAddress, IntPtr dwSize)
    {
        return VirtualFreeEx(
            GetCurrentHandle(), lpAddress, dwSize);
    }

    [DllImport("kernel32", SetLastError = true)]
    static extern IntPtr VirtualAllocEx(
        IntPtr hProcess,
        IntPtr lpAddress,
        IntPtr dwSize,
        AllocationType flAllocationType,
        uint flProtect);

    // ...
}
```

## 函数指针映射到委托

与 P/Invoke 相关的最后一个关键点是，非托管代码中的函数指针映射到托管代码中的委托。例如，为了设置一个定时器，你需要提供一个函数指针，定时器在过期后可以回调该指针。具体来说，你需要传递一个与回调签名匹配的委托实例。

## 指南

鉴于 P/Invoke 的特殊性，有几条指南可以帮助编写此类代码的过程。

- **不要**不必要地复制已经执行非托管 API 功能的现有托管类。
- **应当**将 `extern` 方法声明为私有（`private`）或内部（`internal`）。
- **应当**提供公共包装方法，并使用托管约定，例如结构化异常处理、使用枚举（`enums`）处理特殊值等。
- **应当**通过为不必要的参数选择默认值来简化包装器方法。
- **应当**在 Windows 上使用 `SetLastErrorAttribute`，将使用 `SetLastError` 代码的 API 转换为抛出 `Win32Exception` 的方法。
- **应当**扩展 `SafeHandle` 或实现 `IDisposable` 以创建终结器，以确保非托管资源可以被有效清理。
- 当非托管 API 需要函数指针时，**应当**使用与目标方法签名匹配的委托类型。
- 可能的情况下，**应当**使用 `ref` 参数而不是指针类型。

## 指针与地址

有时，开发者可能想要直接访问和操作内存，以及指向内存位置的指针。这是必要的，例如对于某些操作系统的交互，以及对于某些类型的时间敏感型算法。C# 要求使用 `unsafe` 代码构造结构。

## 不安全代码

C# 的强大特性之一是它是强类型的，并且在整个运行时执行过程中支持类型检查。这一特性之所以特别有益，是因为可以绕过这种支持来直接操作内存和地址。当你处理内存和地址时就会这样做。与 P/Invoke 相关的最后一个关键点是，非托管代码中的函数指针映射到托管代码中的委托。例如，为了设置一个定时器，你需要提供一个函数指针，定时器在过期后可以回调该指针。具体来说，你需要传递一个与回调签名匹配的委托实例。

同样，该命令是无效的：

```
ServiceStatus* pStatus;
```

其中 `ServiceStatus` 的定义如列表 23.13 所示。问题再次在于 `ServiceStatus` 包含一个字符串字段。

### 列表 23.13：无效的引用类型示例

```
struct ServiceStatus
{
  int State;
  string Description; // Description 是引用类型
}
```

### 语言对比：C/C++——指针声明

在 C/C++ 中，同一条声明中的多个指针声明方式如下：

```
int *p1, *p2;
```

注意 `p2` 上的 `*`；这使得 `p2` 是 `int*` 类型而不是 `int`。相比之下，C# 始终将 `*` 与数据类型放在一起：

```
int* p1, p2;
```

结果是两个 `int*` 类型的变量。这种语法与在单个语句中声明多个数组的语法一致：

```
int[] array1, array2;
```

指针是一种全新的类型类别。与结构体、枚举和类不同，指针最终并不继承自 `System.Object`，甚至不能转换为 `System.Object`。相反，它们可以（显式地）转换为 `System.IntPtr`（该类型可以转换为 `System.Object`）。

除了仅包含非托管类型的自定义结构体外，有效的引用类型还包括枚举、预定义的值类型（`byte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`char`、`float`、`decimal` 和 `bool`）以及指针类型（如 `byte**`）。最后，有效的语法还包括 `void*` 指针，即指向未知类型的指针。

## 为指针赋值

一旦代码定义了指针，在访问它之前需要对其赋值。与引用类型一样，指针可以持有 `null` 值，这是它们的默认值。指针存储的值是某个位置的地址。因此，要为指针，必须首先获取数据的地址。

你可以显式地将 `int` 或 `long` 转换为指针，但如果没有在运行时确定特定数据值地址的方法，这种情况很少发生。相反，你需要使用地址运算符（`&`）来获取数据类型的地址：

```
byte* pData = &bytes[0]; // 编译错误
```

问题在于，在托管环境中，数据可能会移动，从而导致地址失效。结果性错误信息将是：“你只能在固定 语句初始化器内部对[未]固定的表达式取地址。” 在在这种情况下，被引用的 `byte` 出现在数组中，而数组是引用类型（可移动类型）。引用类型出现在堆上，并受垃圾回收或重定位的影响。当引用移动类型上的值类型字段时也会发生类似的问题：

```
int* a = &message.Length;
```

或者，为某些数据赋值需要满足以下条件：

- 数据必须被归类为变量。
- 数据必须是非托管类型。
- 变量需要被归类为固定（`fixed`），而不是可移动（`movable`）。

如果数据是非托管变量类型但不是固定的，请使用 `fixed` 语句来固定移动变量。

## 固定数据

为了获取移动数据项的地址，必须对数据进行固定或钉住（`pin`），如列表 23.14 所示。

### 列表 23.14：fixed 语句

```
byte[] bytes = new byte[24];
fixed (byte* pData = &bytes[0]) // 允许 pData = bytes
{
    // ...
}
```

在 `fixed` 语句的代码块内，被分配的数据不会移动。在这个示例中，`bytes` 将保持在相同的地址，至少直到 `fixed` 语句结束。

`fixed` 语句要求在其作用域内声明指针变量。这避免了在数据不再固定时在 `fixed` 语句之外访问该变量。然而，作为程序员，你有责任确保不会将指针赋值给另一个在 `fixed` 语句作用域之外的变量——例如在 API 调用中。不安全代码（`unsafe code`）之所以被称为“`unsafe`”是有原因的；你必须确保安全地使用指针，而不是依靠运行时为你强制执行安全。同样，使用 `ref` 或其他参数对于不会在方法调用后存活的数据将是有问题的。由于 `string` 是无效的 `ref` 类型，定义指向字符串的指针似乎是无效的。但在 C++ 内部，字符串是指向字符数组第一个字符的指针，可以使用 `char*` 声明指向字符串的指针。因此，C# 允许声明 `char*` 类型的指针并在 `fixed` 语句内将其赋值给字符串。`fixed` 语句防止了指针生命周期内字符串的移动。同样，在有 `fixed` 语句的情况下，它允许任何支持隐式转换为另一种类型指针的可移动类型。

你可以用简短的 `bytes` 替换冗长的 `&bytes[]` 赋值，如列表 23.15 所示。

### 列表 23.15：没有地址或数组索引器的 fixed 语句

```
byte[] bytes = new byte[24];
fixed (byte* pData = bytes)
{
    // ...
}
```

根据执行的频率和所需时间，`fixed` 语句可能会导致堆碎片，因为垃圾回收器无法紧凑固定对象。为了减少这个问题，最佳实践是在执行早期钉住内存块，并且钉住较少的大块而不是许多小块。不幸的是，这种偏好必须通过尽可能少地固定来平衡。

## 指针与地址

在这种情况下，你获取原始地址并使用预增运算符将其增加一个引用类型的大小（`sizeof(char)`）。接下来，你使用间接运算符（`indirection operator`）对该地址进行解引用，并在该位置分配一个不同的字符。同样地，在指针上使用 `+` 和 `--` 运算符会根据 *sizeof(T)* 操作数更改地址，其中 T 是引用类型。

比较运算符（`==`、`!=`、`<` `<=` 和 `>=`）也可以用于比较指针。因此，它们实际上等同于对地址值的比较。

解引用运算符（`dereferencing operator`）的一个限制是无法解引用 `void*`。`void*` 数据类型表示指向未知类型的指针。由于数据类型未知，无法对其进行解引用以产生变量。相反，要访问 `void*` 所引的数据，你必须将其转换为另一种指针类型，并对该类型进行解引用。

你可以使用索引运算符或间接运算符（参见列表 23.18）来实现与列表 23.17 中实现相同的行为。

### 列表 23.18：在不安全代码中使用索引运算符修改不可变字符串

```csharp
string text;
text = "52280ft";
Console.Write("{0} = ", text);
unsafe // 需要 /unsafe
{
    fixed (char* pText = text)
    {
        pText[1] = 'm';
        pText[2] = 'i';
        pText[3] = 'l';
        pText[4] = 'e';
        pText[5] = ' ';
        pText[6] = '\0';
    }
    Console.WriteLine(text);
```

列表 23.18 的结果出现在输出 23.4 中。

### 输出 23.4

Smileft = Smile

## 第 23 章：平台互操作性与不安全代码

像列表 23.17 和 23.18 中的此类修改会导致意外的行为。例如，如果在执行 `Console.WriteLine()` 语句后将 `text` 重新赋值为 "S5280ft" 并重新打印 `text`，输出仍然是 Smile，因为两个变量都指向相同的字符串字面量地址。尽管进行了不安全赋值，输出仍优化为由两者引用的同一个字符串字面量。

```csharp
text = "S5280ft";
```

在列表 23.17 的不安全代码之后，字符串赋值的内部是 "S5280ft" 位置的地址赋值，因此 `text` 永远不会被设置为预期值。

## 访问引用类型的成员
