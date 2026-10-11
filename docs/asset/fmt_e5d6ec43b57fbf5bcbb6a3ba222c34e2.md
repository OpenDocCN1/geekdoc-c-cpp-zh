
在这种情况下，类是 `VirtualMemoryManager`，因为它将包含与内存管理相关的函数。（此特定函数可以直接从 `System.Diagnostics.Processor` 类获取，因此没有需要……

# 列表 23.1：声明外部方法

```
using System;
using System.Runtime.InteropServices;
public class VirtualMemoryManager
{
    [DllImport("kernel32.dll", EntryPoint = "GetCurrentProcess")]
    internal static extern IntPtr GetCurrentProcessHandle();
}
```

在实际代码中声明它。）注意，该方法返回一个 `IntPtr`；这种类型将在下一节中解释。

`extern` 方法从不包含任何体，并且（几乎）总是静态的（`static`）。代替方法体，伴随方法声明的 `DllImport` 特性指向了实现。至少，该属性需要定义该函数的 DLL 名称。运行时根据方法名确定函数名，尽管你可以通过使用名为 `EntryPoint` 的命名参数提供函数名来覆盖此默认值。（.NET 框架将自动尝试调用 Unicode `...W` 或 ASCII `...A` 版本的 API。）

在这种情况下，外部函数 `GetCurrentProcess()` 获取当前进程的伪句（pseudohandle），你将在虚拟内存分配调用中使用它。以下是非托管的声明：

```
HANDLE GetCurrentProcess();
```

## 参数数据类型

假设开发者已经识别了目标 DLL 和导出函数，最困难的一步是识别或创建与外部函数中非托管类型对应的托管数据类型。列表 23.2 显示了一个更复杂的 API。

### 列表 23.2：VirtualAllocEx() API

```
LPVOID VirtualAllocEx(
    // 进程的句柄。
    HANDLE hProcess,
    // 期望的起始地址
    LPVOID lpAddress,
    // 要分配区域的大小。
    SIZE_T dwSize,
    // 内存分配类型
    DWORD flAllocationType,
    // 内存保护类型
    DWORD flProtect);
```

`VirtualAllocEx()` 分配操作系统专门指定用于执行或数据的虚拟内存。要调用它，你需要在托管代码中有相应的定义；`HANDLE`、`LPVOID`、`SIZE_T` 和 `DWORD` 在托管代码中是未定义的。因此，`VirtualAllocEx()` 的 C# 代码在列表 23.3 中。

托管代码的一个显著特征是，像 `int` 的原始类型不会根据处理器改变其大小。无论处理器是 32 位还是 64 位，`int` 始终是 32 位。在非托管代码中，1. 声明 Win32 API 的一个非常有用的资源是 `https://github.com/microsoft/CsWin32`。它为许多 API 提供了一个很好的起点，帮助你规避从零开始编写外部调用时出现的一些细微问题。

### 列表 23.3：在 C# 中声明 VirtualAllocEx() API

```csharp
using System;
using System.Runtime.InteropServices;
public class VirtualMemoryManager
{
    [DllImport("kernel32.dll")]
    internal static extern IntPtr GetCurrentProcess();

    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern IntPtr VirtualAllocEx(
        IntPtr hProcess,
        IntPtr lpAddress,
        IntPtr dwSize,
        AllocationType flAllocationType,
        uint flProtect);
}
```

在列表 23.3 中一个值得注意的点是，`IntPtr` 不仅对指针有用——也就是说，它对数量等其他事物用。`IntPtr` 并不仅仅意味着“存储在整数中的指针”，它还意味着“与指针大小相同的整数”。`IntPtr` 不需要包含指针，只需要包含与指针大小相同的内容。

要将 `HANDLE` 和 `LPVOID` 简单地映射为 `int`，你需要映射到 `System.IntPtr`，其大小将根据处理器内存布局而异。此示例还使用了 `AllocationType` 枚举，我们将在本章稍后的“使用封装器简化 API 调用”部分讨论它。

#### 原生大小整数

C# 9.0 引入了新的上下文关键字 `nint` 和 `nuint`，它们代表原生机器大小的整数。这些都是根据运行进程可能是 32 位或 64 位的整数。在内部，`nint` 和 `nuint` 使用 `System.IntPtr` 和 `System.UIntPtr` 实现。在 C# 11 中，这些被更新为其所代表的类型的简单别名。

# 使用 ref 代替指针

通常，非托管代码使用指针作为引用传递的参数。在这些情况下，P/Invoke并不要求你将数据类型映射到托管情况中的指针。相反，请使用相应的参数进行 `ref`（或直接使用 `out`）。在列表 23.4 中，`lpProtect` 的数据类型为 `PDWORD`，它返回“指向接收指定区域第一页之前保护属性的变量的指针”。

### 列表 23.4：使用 ref 和 out 代替指针

```csharp
public class VirtualMemoryManager
{
    // ...
    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool VirtualProtectEx(
        IntPtr hProcess,
        IntPtr lpAddress,
        uint dwSize,
        uint flNewProtect,
        ref uint lpProtect);
}
```

尽管 `lpProtect` 被记录为 `out`（尽管签名并没有强制执行），但描述也提到该参数必须指向一个有效变量而不是 `NULL`。这种不一致性令人困惑但很常见。指南是对于 P/Invoke 参数使用 `ref` 而不是 `out`，因为调用者始终可以忽略通过 `ref` 传递的数据，但反之则不会成功。其他参数与 `VirtualAllocEx()` 基本相同，`lpAddress` 是 `VirtualAllocEx()` 返回的地址。此外，`flNewProtect` 指定内存保护的具体类型：执行、只读等。MSDN 文档。

# 使用 StructLayoutAttribute 进行顺序布局

某些 API 调用没有对应名称的类型。调用这些类型需要在托管代码中声明非托管结构体（参见列表 23.5）。

### 列表 23.5：从非托管结构体声明类型

```csharp
[StructLayout(LayoutKind.Sequential)]
struct ColorRef
{
    public byte Red;
    public byte Green;
    public byte Blue;
    // 关闭未使用的警告
    private byte Unused;

    public ColorRef(byte red, byte green, byte blue)
    {
        Blue = blue;
        Green = green;
        Red = red;
        Unused = 0;
    }
}
```

各种 Windows API 使用 `COLORREF` 来表示 RGB（即红、绿、蓝的级别）。列表 23.5 中的关键是 `StructLayoutAttribute`。默认情况下，托管代码可以优化类型的内存布局，为了使布局从一个字段到下一个字段是顺序的，你需要添加带有 `LayoutKind.Sequential` 枚举的 `StructLayoutAttribute`。这在对流读写数据时也有用。由于非托管 (C++) 定义没有映射到 C# 定义，开发者应该遵循指南，判断类型应该表现像值类型还是引用类型，以及大小是否较小（小于 16 字节）。

# 第 23 章：平台互操作与不安全代码

## 内联数组

将结构体声明为缓冲区是有帮助的。在 C# 12.0 中，结构体可以装饰为固定大小。内联数组可以隐式转换为 `Span<T>` 或 `ReadOnlySpan<T>`，作为与内联数组交互的简单方法。你也可以通过索引器访问内联数组中的元素，包括读取和写入索引。要创建一个内联数组，声明一个带有单个字段并使用 `System.Runtime.CompilerServices.InlineArrayAttribute` 的结构体。

## 跳过局部变量初始化

自 C# 1.0 以来，局部变量被初始化为零值。然而，在某些高性能情况下，这些零初始化值会被覆盖。C# 9.0 引入了新的 `SkipLocalsInit`。此属性将导致编译器输出 `localsinit` 标记。结果是局部变量可能未初始化。

## 错误处理

Win32 API 编程的一个不方面是 API 经常以不一致的方式报告错误。例如，某些 API 返回值（0、1、false 等）来指示错误，而另一些通过某种方式设置 `out` 参数。此外，错误的细节需要调用 `GetLastError()` API 然后调用 `FormatMessage()` 来获取错误消息。总之，非托管代码中的 Win32 错误很少通过异常发生。

幸运的是，P/Invoke 设计者提供了错误处理机制。如果 `DllImport` 属性的 `SetLastError` 参数为 `true`，则可以在 P/Invoke 调用后立即实例化带有错误数据的 `System.ComponentModel.Win32Exception()`（参见列表 23.6）。

### 列表 23.6：Win32 错误处理

```csharp
public class VirtualMemoryManager
{
    [DllImport("kernel32.dll", SetLastError = true)]
    private static IntPtr VirtualAllocEx(
        IntPtr hProcess,
        IntPtr lpAddress,
        uint dwSize,
        AllocationType fAllocationType,
        uint lProtect);
    // ...
    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool VirtualProtectEx(
        IntPtr hProcess,
        IntPtr lpAddress,
        uint dwSize,
        uint flNewProtect,
        ref uint lpProtect);

    public enum AllocationType
    {
        Reserve,
        Commit
    }

    public enum ProtectionOptions
    {
        PageExecute,
        PageReadOnly,
        PageReadWrite
    }

    public static IntPtr AllocExecutionBlock(int size, IntPtr hProcess)
    {
        uint lpOldProtect = 0;
        IntPtr codeBytesPtr = VirtualAllocEx(
            hProcess,
            IntPtr.Zero,
            (uint)size,
            AllocationType.Reserve | AllocationType.Commit,
            ref lpOldProtect);

        if (codeBytesPtr == IntPtr.Zero)
        {
            throw new System.ComponentModel.Win32Exception();
        }
        return codeBytesPtr;
    }

    internal static IntPtr GetCurrentHandle()
    {
        // 实现细节
        return IntPtr.Zero;
    }
}
```

### 指南

- 要为非托管方法创建公共托管包装器，使用托管代码的约定，例如结构化异常处理。

# 使用 SafeHandle

通常，P/Invoke 调用一个资源（例如句柄），代码在使用后需要清理。与其要求开发者记住这一步是必要的并每次手动编写代码，不如提供一个实现 `Disposable` 和析构函数的类是有帮助的。在列表 23.7 中，例如 `VirtualAllocEx()` 和 `VirtualProtectEx()` 返回的地址需要后续调用 `VirtualFreeEx()`。为此过程提供内置支持，你定义了一个派自 `System.Runtime.InteropServices.SafeHandle` 的 `VirtualMemoryPtr` 类。

### 列表 23.7：使用 SafeHandle 的托管资源

```csharp
public class VirtualMemoryPtr :
    System.Runtime.InteropServices.SafeHandle
{
    public VirtualMemoryPtr(int memorySize) :
        base(IntPtr.Zero, true)
    {
        _ProcessHandle = VirtualMemoryManager.GetCurrentHandle();
        _MemorySize = (IntPtr)memorySize;
        _AllocatedPointer = VirtualMemoryManager.AllocExecutionBlock(
            memorySize, _ProcessHandle);
        _Disposed = false;
    }

    public readonly IntPtr _AllocatedPointer;
    private readonly IntPtr _ProcessHandle;
    private readonly IntPtr _MemorySize;
    private bool _Disposed;

    public static implicit operator IntPtr(
        VirtualMemoryPtr virtualMemoryPointer)
```

# 第23 章：平台互操作性与不安全代码

```cs
{
    return virtualMemoryPointer.AllocatedPointer;
}

// SafeHandle 抽象成员
public override bool IsInvalid
{
    get {
        return _Disposed;
    }
}

// SafeHandle 抽象成员
protected override bool ReleaseHandle()
{
    if (!Disposed)
    {
        _Disposed = true;
        GC.SuppressFinalize(this);
        VirtualMemoryManager.VirtualFree(_ProcessHandle, _AllocatedPointer, _MemorySize);
    }
    return true;
}
```

`System.Runtime.InteropServices.SafeHandle` 包含抽象成员 `IsInvalid` 和 `ReleaseHandle()`。你将清理代码放置在后者中；前者指示该代码是否已执行。

通过 `VirtualMemoryPtr`，你可以通过通过实例化该类型并指定所需的内存分配来分配内存。

# 调用外部函数

一旦声明了 P/Invoke 函数，你就可以像调用其他类成员一样调用它们。然而，关键在于被导入的 DLL 必须在路径中（包括可执行文件目录），这样才能成功加载。列表 23.6 和列表 23.7 演示了这种方法。但是，它们依赖于某些常量。

由于存在 `flAllocationType` 和 `flProtect` 标志，为每个标志提供常量或枚举是一种良好的做法。与其期望调用者定义这些常量或枚举，不如封装建议你将它们作为 API 声明的一部分提供出来，如列表 23.8 所示。

# 列表 23.8：将 API 封装
