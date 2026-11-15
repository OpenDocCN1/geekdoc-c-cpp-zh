

## 参数数据类型

假设开发者已确定目标 DLL 和导出函数，最困难的步骤是识别或创建与外部函数中非托管类型对应的托管数据类型。清单 20.2 展示了一个更复杂的 API。

```
LISTING 20.2: The VirtualAllocEx() API

LPVOID VirtualAllocEx(
 HANDLE hProcess,
 // The handle to a process. The
 // function allocates memory within
 // the virtual address space of this
 // process.
 LPVOID lpAddress,
 // The pointer that specifies a
 // desired starting address for the
 // region of pages that you want to
 // allocate. If lpAddress is NULL,
 // the function determines where to
 // allocate the region.
 SIZE_T dwSize,
 // The size of the region of memory to
 // allocate, in bytes. If lpAddress
 // is NULL, the function rounds dwSize
 // up to the next page boundary.
 DWORD flAllocationType,
 // The type of memory allocation.
 DWORD flProtect); // The type of memory allocation.
```

VirtualAllocEx() 分配操作系统专门用于执行或数据的虚拟内存。要调用它，还需要在托管代码中为每个数据类型提供相应的定义；虽然在 Win32 编程中很常见，但 HANDLE、LPVOID、SIZE_T 和 DWORD 在 CLI 托管代码中未定义。因此，VirtualAllocEx() 在 C# 中的声明如清单 20.3 所示。

```
LISTING 20.3: Declaring the VirtualAllocEx() API in C#

using System;
using System.Runtime.InteropServices;
class VirtualMemoryManager
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

- 声明 Win32 API 特别有用的资源是 www.pinvoke.net。它为许多 API 提供了很好的起点，帮助避免从头开始编写外部 API 调用时可能出现的一些微妙问题。

## 使用 ref 而非指针

非托管代码经常使用指针来传递按引用的参数。在这些情况下，P/Invoke 不要求将数据类型映射到托管代码中的指针。相反，你将相应的参数映射到 ref（或 out），具体取决于参数是输入输出还是仅输出。在清单 20.4 中，数据类型为 PDWORD 的 lpflOldProtect 是一个示例，它返回“指向接收指定页面区域中第一页之前的访问保护的变量的指针”。

### 清单 20.4：使用 ref 和 out 而非指针

```
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

尽管 lpflOldProtect 被文档记录为 [out]（尽管签名并未强制执行），但描述继续说明该参数必须指向有效变量且不能为 NULL。这种不一致令人困惑，但很常见。准则是为 P/Invoke 类型参数使用 ref 而非 out，因为被调用方始终可以忽略通过 ref 传递的数据，但反之不一定会成功。

其他参数与 VirtualAllocEx() 几乎相同，只是 lpAddress 是从 VirtualAllocEx() 返回的地址。此外，flNewProtect 指定确切的内存保护类型：页面执行、页面只读等等。

## 使用 StructLayoutAttribute 实现顺序布局

某些 API 涉及没有相应托管类型的类型。要调用这些 API，需要在托管代码中重新声明该类型。例如，你在托管代码中声明非托管 COLORREF 结构体（请参阅清单 20.5）。

### 清单 20.5：从非托管结构体声明类型

```
[StructLayout(LayoutKind.Sequential)]
struct ColorRef
{
    public byte Red;
    public byte Green;
    public byte Blue;
    // Turn off warning about not accessing Unused.
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

各种 Microsoft Windows 颜色 API 使用 COLORREF 表示 RGB 颜色（红、绿、蓝级别）。

此声明的关键是 StructLayoutAttribute。默认情况下，托管代码可以优化类型的内存布局，因此字段之间的布局可能不是顺序的。要强制顺序布局，以便类型直接映射并可以在托管代码和非托管代码之间按位复制（blit），你需要添加带有 LayoutKind.Sequential 枚举值的 StructLayoutAttribute。（这在向文件流写入和读取数据时也很有用，因为可能需要顺序布局。）

由于非托管（C++）中 struct 的定义不映射到 C# 定义，因此非托管结构体与托管结构体之间没有直接映射。相反，开发者应遵循常规 C# 准则，判断类型应表现为值类型还是引用类型，以及大小是否较小（大约小于 16 字节）。

## 错误处理

Win32 API 编程的一个不便特点是，它经常以不一致的方式报告错误。例如，某些 API 返回值（0、1、false 等）以指示错误，而其他 API 则以某种方式设置输出参数。此外，要了解出了什么问题，需要额外调用 GetLastError() API，然后再调用 FormatMessage() 来检索与错误对应的错误消息。总之，非托管代码中的 Win32 错误报告很少通过异常发生。

幸运的是，P/Invoke 设计者提供了一种处理此问题的机制。要启用此功能，只要 DllImport 特性的 SetLastError 命名参数为 true，就可以实例化一个 System.ComponentModel.Win32Exception()，它会在 P/Invoke 调用后立即自动用 Win32 错误数据进行初始化（请参阅清单 20.6）。

### 清单 20.6：Win32 错误处理

```
class VirtualMemoryManager
{
    [DllImport("kernel32.dll", "", SetLastError = true)]
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
        (uint)(ProtectionOptions.PageExecuteReadWrite));
    if (codeBytesPtr == IntPtr.Zero)
    {
        throw new System.ComponentModel.Win32Exception();
    }

    uint lpflOldProtect = 0;
    if (!(VirtualProtectEx(
        hProcess, codeBytesPtr,
        (IntPtr)size,
        (uint)(ProtectionOptions.PageExecuteReadWrite),
        ref lpflOldProtect))
    {
        throw new System.ComponentModel.Win32Exception();
    }
}
