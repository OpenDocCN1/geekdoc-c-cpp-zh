
public readonly IntPtr AllocatedPointer;
readonly IntPtr ProcessHandle;
readonly IntPtr MemorySize;
bool Disposed;
public static implicit operator IntPtr(
VirtualMemoryPtr virtualMemoryPointer)
{
return virtualMemoryPointer.AllocatedPointer;
}
// SafeHandle 抽象成员
public override bool IsValid
{
get
{
return Disposed;
}
}
// SafeHandle 抽象成员
protected override bool ReleaseHandle()
{
if (!Disposed)
{
Disposed = true;
GC.SuppressFinalize(this);
VirtualMemoryManager.VirtualFreeEx(ProcessHandle,
AllocatedPointer, MemorySize);
}
return true;
}

`System.Runtime.InteropServices.SafeHandle` 包含抽象成员 `IsValid` 和 `ReleaseHandle()`。您在后者中放置清理代码；前者指示该代码是否已经执行。使用 `VirtualMemoryPtr`，您只需实例化该类型并指定所需的内存分配即可简单地分配内存。

## 调用外部函数

一旦您声明了 P/Invoke 函数，您就可以像调用任何其他类成员一样调用它们。然而，关键在于，导入的 DLL 必须位于路径中（包括可执行文件目录），以便其能够成功加载。清单 21.6 和 21.7 演示了这种方法。但是，它们依赖于一些常量。

由于 `flAllocationType` 和 `flProtect` 是标志，因此为每个标志提供常量或枚举是一种良好的做法。相反，如果期望调用者定义这些常量或枚举，封装建议您将它们作为 API 声明的一部分提供，如清单 21.8 所示。

### 清单 21.8：一起封装 API

```
class VirtualMemoryManager
{
// ...
/// <summary>
/// 内存分配的类型。此参数必须
/// 包含以下值之一。
/// </summary>
[Flags]
private enum AllocationType : uint
{
/// <summary>
/// 为指定的保留内存页分配物理
/// 存储空间在内存或磁盘上的分页文件中。该函数将内存
/// 初始化为零。
/// </summary>
Commit = 0x1000,
/// <summary>
/// 保留进程虚拟地址
/// 空间范围，而不分配任何实际物理
/// 存储到内存或磁盘上的分页文件中
/// </summary>
Reserve = 0x2000,
/// <summary>
/// 表示 lpAddress 和 dwSize 指定的内存范围中的数据不再感兴趣。
/// 不应该从分页文件中读取或写入
/// 这些页。但是，内存块稍后
/// 将再次使用，因此不应取消提交。此
/// 值不能与其他任何值一起使用。
/// </summary>
Reset = 0x80000,
/// <summary>
/// 分配具有读写访问权限的物理内存。
/// 此值仅用于地址窗口扩展（AWE）内存。
/// </summary>
Physical = 0x400000,
/// <summary>
/// 在最高可能的地址处分配内存
/// </summary>
TopDown = 0x100000,
}
```

```
/// <summary>
/// 要分配的页面区域的内存保护
/// </summary>
[Flags]
private enum ProtectionOptions : uint
{
    /// <summary>
    /// 对已提交的页面区域启用执行访问权限。尝试读取或写入已提交
    /// 区域会导致访问冲突。
    /// </summary>
    Execute = 0x10,

    /// <summary>
    /// 对已提交的页面区域启用执行和读取访问权限。尝试写入
    /// 已提交区域会导致访问冲突。
    /// </summary>
    PageExecuteRead = 0x20,

    /// <summary>
    /// 对已提交的页面区域启用执行、读取和写入访问权限
    /// </summary>
    PageExecuteReadWrite = 0x40,

    /// ...
}
```

```
/// <summary>
/// 释放操作的类型
/// </summary>
[Flags]
private enum MemoryFreeType : uint
{
    /// <summary>
    /// 取消提交指定的已提交页面区域。
    /// 操作之后，页面处于保留
    /// 状态。
    /// </summary>
    DeCommit = 0x4000,

    /// <summary>
    /// 释放指定的页面区域。在此
    /// 操作之后，页面处于释放状态。
    /// </summary>
    Release = 0x8000

    /// ...
}
```

枚举的优势在于它们将各种值分组在一起。此外，它们可以将作用域限制为除这些值以外的其他任何内容。

## 使用封装简化 API 调用

无论是错误处理、结构体还是常量值，有效的 API 开发者的一个目标都是提供一个简化的托管 API 来包装底层的 Win32 API。例如，清单 21.9 通过提供简化调用的公共版本对 `VirtualFreeEx()` 进行了重载。

### 清单 21.9：包装底层 API

```
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
         hProcess, lpAddress, dwSize,
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
         GetCurrentProcessHandle(), lpAddress, dwSize);
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

与 P/Invoke 相关的最后一个关键点是，非托管代码中的函数指针映射到托管代码中的委托。例如，为了设置定时器，您需要提供一个函数指针，以便定时器过期时可以回调它。具体来说，您需要传递一个与回调签名匹配的委托实例。

## 指南

鉴于 P/Invoke 的特殊性，有几项指南可以帮助编写此类代码的过程。

![](img/ef6a8a417630b222bfb3f3b949facff0_946_0.png)

## 指针和地址

在某些情况下，开发人员可能希望直接访问和操作内存以及对内存位置的指针。这对于某些操作系统交互以及某些类型的实时关键算法是必需的。为了支持此功能，C# 要求使用 `unsafe` 代码结构。

## 非安全代码

C# 的一大优势在于它是强类型的，并且在整个运行时执行期间支持类型检查。使此功能特别有益的一点是，可以绕过这种支持并直接操作内存和地址。例如，当处理内存映射设备时，或者如果您想要实现实时关键算法时，您需要这样做。关键在于将代码的一部分指定为 *不安全*。

非安全代码是一个显式的代码块和编译选项，如清单 21.10 所示。*unsafe* 修饰符对生成的 CIL 代码本身没有影响，但它只是向编译器发出的指令，允许在 *unsafe* 块内进行指针和地址操作。此外，*unsafe* 并不意味着 *unmanaged*。

### 清单 21.10：指定非安全代码的方法

```csharp
class Program
{
    unsafe static int Main(string[] args)
    {
        // ...
    }
}
```

您可以将 *unsafe* 作为类型的修饰符，或作为类型内特定成员的修饰符。

此外，C# 允许将 *unsafe* 作为语句来标记代码块以允许非安全代码（参见清单 21.11）。

### 清单 21.11：指定非安全代码的代码块

```csharp
class Program
{
    static int Main(string[] args)
    {
        unsafe
        {
            // ...
        }
    }
}
```

*unsafe* 块内的代码可以包含非安全结构，例如指针。

