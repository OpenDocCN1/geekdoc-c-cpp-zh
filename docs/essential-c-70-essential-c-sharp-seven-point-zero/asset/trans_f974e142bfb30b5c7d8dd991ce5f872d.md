
代码不同，内存指针会根据处理器的不同而变化。因此，对于像 `HANDLE` 和 `LPVOID` 这样的类型，不要简单地将它们映射到 `int`，而是需要将其映射到 `System.IntPtr`，其大小将随处理器的内存布局而变化。本示例还使用了 `AllocationType` 枚举，我们将在本章后面“使用封装简化 API 调用”一节中讨论该枚举。

关于列表 21.3 有一个有趣的点是，`IntPtr` 不仅对指针有用，也就是说，它对数量等其他内容也有用。`IntPtr` 并不意味着仅指“存储在整数中的指针”，它还意味着“大小与指针相同的整数”。一个 `IntPtr` 不必包含指针，只需包含与指针大小相同的内容即可。许多东西的大小与指针相同，但它们并不是指针。

### 使用 ref 而非指针

经常有非托管代码使用指针作为引用传递参数。在这种情况下，P/Invoke 并不要求你在托管代码中将数据类型映射为指针。相反，你需要将相应的参数映射为 `ref`（或者 `out`，具体取决于参数是 in/out 还是仅为 out）。在列表 21.4 中，数据类型为 `PDWORD` 的 `lpflOldProtect` 是一个示例，它返回“指向接收指定页面区域中第一页先前访问保护的变量的指针”²。

**列表 21.4：使用 ref 和 out 而非指针**

```csharp
class VirtualMemoryManager
{
    // ...
    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool VirtualProtectEx(
        IntPtr hProcess, IntPtr lpAddress,
        IntPtr dwSize, uint flNewProtect,
        ref uint lpflOldProtect);
}
```

尽管 `lpflOldProtect` 被文档标记为 [out]（尽管签名并未强制执行这一点），但描述继续提到该参数必须指向一个有效变量，而不是 NULL。这种不一致性令人困惑，但很常见。指南是对于 P/Invoke 类型参数，应使用 `ref` 而不是 `out`，因为被调用方始终可以忽略通过 `ref` 传递的数据，但反之则不一定成功。

² MSDN 文档。

其他参数几乎与 `VirtualAllocEx()` 相同，除了 `lpAddress` 是来自 `VirtualAllocEx()` 的地址。此外，`flNewProtect` 指定了确切的内存保护类型：页执行、页只读等。

### 使用 StructLayoutAttribute 进行顺序布局

一些 API 涉及没有对应托管类型的类型。调用这些类型需要重新声明托管代码中的类型。例如，你在托管代码中声明非托管的 `COLORREF` 结构体（见列表 21.5）。

**列表 21.5：从非托管结构体声明类型**

```csharp
[StructLayout(LayoutKind.Sequential)]
struct ColorRef
{
public byte Red;
public byte Green;
public byte Blue;
// Turn off warning about not accessing Unused
#pragma warning disable 414
private byte Unused;
#pragma warning restore 414

public ColorRef(byte red, byte green, byte blue)
{
Blue = blue;
Green = green;
Red = red;
Unused = 0;
}
}
```

各种 Microsoft Windows 颜色 API 使用 `COLORREF` 来表示 RGB 颜色（即红色、绿色和蓝色的水平）。

此声明的关键是 `StructLayoutAttribute`。默认情况下，托管代码可以优化类型的内存布局，因此从一个字段到下一个字段的布局可能不是顺序的。为了强制顺序布局，使类型能够直接映射，并可以从托管代码逐位复制（blit）到非托管代码，反之亦然，你需要添加带有 `LayoutKind.Sequential` 枚举值的 `StructLayoutAttribute`。（这在向文件流写入和读取数据时也很有用，因为那时可能期望顺序布局。）

由于非托管（C++）的结构体定义并不映射到 C# 定义，因此非托管结构体到托管结构体没有直接的映射。相反，开发人员应遵循关于类型应表现为值类型还是引用类型，以及大小是否较小（大约小于 16 字节）的常见 C# 指南。

## 错误处理

Win32 API 编程的一个不便方面是 API 经常以不一致的方式报告错误。例如，一些 API 返回一个值（0、1、false 等）来表示错误，而另一些则以某种方式设置输出参数。此外，了解出错详情的额外调用需要 `GetLastError()` API，然后再调用 `FormatMessage()` 来获取对应于该错误的错误消息。总之，非托管代码中的 Win32 错误报告很少通过异常发生。

幸运的是，P/Invoke 设计者提供了一种错误处理机制。要启用它，如果 `DllImport` 属性的 `SetLastError` 命名参数为 `true`，则可以实例化 `System.ComponentModel.Win32Exception()`，它会自动用紧随 P/Invoke 调用之后的 Win32 错误数据进行初始化（见列表 21.6）。

**列表 21.6：Win32 错误处理**

```csharp
class VirtualMemoryManager
{
  [DllImport("kernel32.dll", SetLastError = true)]
  private static extern IntPtr VirtualAllocEx(
    IntPtr hProcess,
    IntPtr lpAddress,
    IntPtr dwSize,
    AllocationType flAllocationType,
    uint flProtect);

  // ...

  [DllImport("kernel32.dll", SetLastError = true)]
  static extern bool VirtualProtectEx(
    IntPtr hProcess, IntPtr lpAddress,
    IntPtr dwSize, uint flNewProtect,
    ref uint lpflOldProtect);
}
```

```csharp
[Flags]
private enum AllocationType : uint
{
    // ...
}

[Flags]
private enum ProtectionOptions
{
    // ...
}

[Flags]
private enum MemoryFreeType
{
    // ...
}

public static IntPtr AllocExecutionBlock(
    int size, IntPtr hProcess)
{
    IntPtr codeBytesPtr;
    codeBytesPtr = VirtualAllocEx(
        hProcess, IntPtr.Zero,
        (IntPtr)size,
        AllocationType.Reserve | AllocationType.Commit,
        (uint)ProtectionOptions.PageExecuteReadWrite);

    if (codeBytesPtr == IntPtr.Zero)
    {
        throw new System.ComponentModel.Win32Exception();
    }

    uint lpfOldProtect = 0;
    if (!VirtualProtectEx(
        hProcess, codeBytesPtr,
        (IntPtr)size,
        (uint)ProtectionOptions.PageExecuteReadWrite,
        ref lpfOldProtect))
    {
        throw new System.ComponentModel.Win32Exception();
    }
    return codeBytesPtr;
}

public static IntPtr AllocExecutionBlock(int size)
{
    return AllocExecutionBlock(
        size, GetCurrentProcessHandle());
}
```

此代码使开发人员能够按照每个 API 使用的特定错误检查提供自定义检查，同时以标准方式报告错误。

列表 21.1 和 21.3 将 P/Invoke 方法声明为 `internal` 或 `private`。除了最简单的 API 之外，将方法封装在公共包装器中，以减少 P/Invoke API 调用的复杂性，是一个提高 API 可用性并朝着面向对象类型结构发展的良好准则。列表 21.6 中 `AllocExecutionBlock()` 的声明提供了这种方法的一个良好示例。

> **指南**
>
> **要（DO）** 创建公共托管包装器来包装使用托管代码惯例的非托管方法，例如结构化异常处理。

## 使用 SafeHandle

P/Invoke 经常涉及资源，例如句柄，代码在使用后需要清理。而不是要求开发人员记住这一步骤是必要的并在每次手动编码，提供一个实现了 `IDisposable` 和终结器的类是很有帮助的。例如，在列表 21.7 中，`VirtualAllocEx()` 和 `VirtualProtectEx()` 返回后的地址需要后续调用 `VirtualFreeEx()`。为了提供对此过程的内置支持，你定义一个继承自 `System.Runtime.InteropServices.SafeHandle` 的 `VirtualMemoryPtr` 类。

**列表 21.7：使用 SafeHandle 的托管资源**

```csharp
public class VirtualMemoryPtr : System.Runtime.InteropServices.SafeHandle
{
    public VirtualMemoryPtr(int memorySize) :
        base(IntPtr.Zero, true)
    {
        ProcessHandle = VirtualMemoryManager.GetCurrentProcessHandle();
        MemorySize = (IntPtr) memorySize;
        AllocatedPointer = VirtualMemoryManager.AllocExecutionBlock(
                          memorySize, ProcessHandle);
        Disposed = false;
    }
}
```

