

```csharp
{
    return virtualMemoryPointer.AllocatedPointer;
}

// SafeHandle 抽象成员
public override bool IsInvalid
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
```

System.Runtime.InteropServices.SafeHandle 包含抽象成员 IsInvalid 和 ReleaseHandle()。你将清理代码放在后者中；前者指示这段代码是否已经执行。

使用 VirtualMemoryPtr，你只需实例化该类型并指定所需的内存分配，即可分配内存。

## 调用外部函数

一旦你声明了 P/Invoke 函数，就可以像调用任何其他类成员一样调用它们。然而，关键在于导入的 DLL 必须位于路径中，包括可执行目录，这样它才能被成功加载。清单 20.6 和清单 20.7 演示了这种方法。不过，它们依赖于一些常量。

由于 flAllocationType 和 flProtect 是标志，为它们提供常量或枚举是一种好的做法。封装建议你将这些常量或枚举作为 API 声明的一部分提供，而不是期望调用者来定义它们，如清单 20.8 所示。

### 清单 20.8：将 API 封装在一起

```csharp
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
        /// 为指定的保留内存页在内存中或磁盘上的
        /// 分页文件中分配物理存储。该函数将内存
        /// 初始化为零。
        /// </summary>
        Commit = 0x1000,

        /// <summary>
        /// 保留进程虚拟地址空间中的一段范围，
        /// 而不在内存中或磁盘上的分页文件中分配任何
        /// 实际的物理存储。
        /// </summary>
        Reserve = 0x2000,

        /// <summary>
        /// 表示由 lpAddress 和 dwSize 指定的内存范围中的数据
        /// 不再重要。不应从分页文件中读取或写入这些
        /// 页面。但是，该内存块稍后会被再次使用，
        /// 因此不应将其解除提交。此值
        /// 不能与任何其他值一起使用。
        /// </summary>
        Reset = 0x80000,

        /// <summary>
        /// 分配具有读写访问权限的物理内存。
        /// 此值仅用于地址窗口扩展 (AWE) 内存。
        /// </summary>
        Physical = 0x400000,

        /// <summary>
        /// 在尽可能最高的地址分配内存。
        /// </summary>
        TopDown = 0x100000,
    }

    /// <summary>
    /// 要分配的页面区域的内存保护。
    /// </summary>
    [Flags]
    private enum ProtectionOptions : uint
    {
        /// <summary>
        /// 启用对已提交页面区域的执行访问。
        /// 尝试读取或写入已提交区域会导致访问冲突。
        /// </summary>
        Execute = 0x10,
        /// <summary>
        /// 启用对已提交页面区域的执行和读取访问。
        /// 尝试写入已提交区域会导致访问冲突。
        /// </summary>
        PageExecuteRead = 0x20,
        /// <summary>
        /// 启用对已提交页面区域的执行、读取和写入访问。
        /// </summary>
        PageExecuteReadWrite = 0x40,
        // ...
    }

    /// <summary>
    /// 释放操作的类型
    /// </summary>
    [Flags]
    private enum MemoryFreeType : uint
    {
        /// <summary>
        /// 解除对指定已提交页面的提交。操作之后，
        /// 这些页面处于保留状态。
        /// </summary>
        Decommit = 0x4000,
        /// <summary>
        /// 释放指定的页面区域。此操作之后，
        /// 这些页面处于空闲状态。
        /// </summary>
        Release = 0x8000
    }

    // ...
}
```

枚举的优点是它们将各种值分组在一起。此外，它们可以将作用域限制为仅这些值。

### 使用包装器简化 API 调用

无论是错误处理、结构体还是常量值，高效 API 开发者的一个目标就是提供简化底层 Win32 API 的托管 API 包装。例如，清单 20.9 使用公共版本重载了 VirtualFreeEx()，从而简化了调用。

### 清单 20.9：包装底层 API

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

### 函数指针映射到委托

关于 P/Invoke 的最后一个关键点是，非托管代码中的函数指针映射到托管代码中的委托。例如，要设置一个 Microsoft Windows 计时器，你需要提供一个函数指针，计时器到期时可以回调该指针。具体来说，你需要传递一个与回调签名匹配的委托实例。

### 准则

鉴于 P/Invoke 的特殊性，有几条准则有助于编写此类代码。

- **不要**不必要地复制已经执行非托管 API 功能的现有托管类。
- **要**将 `extern` 方法声明为 private 或 internal。
- **要**提供使用托管约定的公共包装方法，例如结构化异常处理、对特殊值使用枚举等。
- **要**通过为不必要的参数选择默认值来简化包装方法。
- **要**使用 `SetLastErrorAttribute` 将使用 `SetLastError` 错误代码的 API 转换为抛出 `Win32Exception` 的方法。
- **要**扩展 `SafeHandle` 或实现 `IDisposable` 并创建终结器，以确保非托管资源能够被有效清理。
- **要**当非托管 API 需要函数指针时，使用与所需方法签名匹配的委托类型。
- **要**尽可能使用 `ref` 参数而不是指针类型。

## 指针和地址

有时，开发者可能希望直接访问和使用内存以及指向内存位置的指针。例如，某些操作系统交互以及某些类型的时间关键型算法需要这样做。为了支持这种能力，C# 要求使用不安全代码构造。

### 不安全代码

C# 的一大特性是它是强类型语言，并在整个运行时执行期间支持类型检查。使这一特性特别有益的是，可以绕过这种支持并直接操作内存和地址。在以下情况下你会这样做：

