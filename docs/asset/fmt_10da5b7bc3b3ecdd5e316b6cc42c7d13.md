
```csharp
public class VirtualMemoryManager {
    // ...

    // <summary>
    // 内存分配的类型。此参数必须
    // 包含以下值之一。
    // </summary>
    [Flags]
    private enum AllocationType : uint {
        // <summary>
        // 在内存或磁盘上的分页文件中为指定的预留
        // 内存页分配物理存储。该函数将内存初始化为零。
        // </summary>
        Commit = 0x1000,
        // <summary>
        // 预留进程虚拟地址空间范围，
        // 而不在内存或磁盘上的分页文件中
        // 分配任何实际物理存储。
        // </summary>
        Reserve = 0x2000,
        // <summary>
        // 表示由 lpAddress 和 dwSize 指定的
        // 内存范围的数据不再受关注。
        // 不应向分页文件读取或写入页。
        // 然而，内存块稍后将被使用，
        // 因此不应取消提交（decommitted）。
        // 值不能与任何其他值一起。
        // </summary>
        Reset = 0x80000,
        // <summary>
        // 分配具有读写访问权限的物理内存。
        // 此值专门用于地址窗口扩展
        //（AWE）内存。
        // </summary>
        Physical = 0x400000,
    }
}
```

```csharp
/// <summary>
/// 在最高可能的地址分配内存。
/// </summary>
TopDown = 0x100000,

/// <summary>
/// 要分配的页区域的内存保护。
/// </summary>
[Flags]
private enum ProtectionOptions : uint
{
/// <summary>
/// 为已提交的页区域启用执行权限。
/// 尝试读取或写入已提交区域
/// 将导致访问冲突。
/// </summary>
Execute = 0x10,
/// <summary>
/// 为已提交的页区域启用执行和读取权限。
/// 尝试写入已提交区域
/// 将导致访问冲突。
/// </summary>
PageExecuteRead = 0x20,
/// <summary>
/// 为已提交的页区域启用执行、读取和写入权限。
/// </summary>
PageExecuteReadWrite = 0x40,
/// ...

/// <summary>
/// 释放操作的类型。
/// </summary>
[Flags]
private enum MemoryType : uint
{
/// <summary>
/// 取消提交指定的已提交页区域。
/// 操作后，这些页将处于预留状态。
/// </summary>
Decommit = 0x4000,
/// <summary>
/// 释放指定的页区域。在此之后
```

```csharp
/// 操作后，页将处于空闲状态。
/// </summary>
Release = 0x8000
}

// ...
}
```

枚举的优点是它们将各种值组合在一起。此外，它们可以将范围限制为除这些值之外的任何其他内容。

# 使用包装器简化 API 调用

无论它们关注的是错误处理、结构体还是常量值，有效 API 的一个目标是提供一个封装底层 Win32 API 的简化版 API。例如，列表 23.9 使用常量值重载了 `VirtualFreeEx()`。

## 列表 23.9：封装底层 API

```csharp
public class VirtualMemoryManager
{
    //...

    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool VirtualFreeEx(
        IntPtr hProcess, IntPtr lpAddress,
        IntPtr dwSize, IntPtr dwType);
    public static bool VirtualFreeEx(
        IntPtr hProcess, IntPtr lpAddress,
        IntPtr dwSize)
    {
        bool result = VirtualFreeEx(
            hProcess, lpAddress, dwSize,
            (IntPtr)MemoryFreeType.Commit);
        if (!result)
        {
            throw new System.ComponentModel.Win32Exception();
        }
        return result;
    }
}
```

# 第23 章：平台互操作性与不安全代码

```cs
return VirtualFreeEx(
    GetCurrentProcessHandle(), lpAddress, dwSize);
}

[DllImport("kernel32", SetLastError = true)]
static extern IntPtr VirtualAlloc(
    IntPtr hProcess,
    IntPtr lpAddress,
    IntPtr dwSize,
    AllocationType flAllocationType,
    uint flProtect);

// ...
```

与 P/Invoke 相关的最后一个关键点是，未托管代码中的函数指针映射到托管代码中的委托。例如，使用定时器时，你需要提供一个函数指针，定时器到期后进行回调。具体来说，你传递一个与回调签名匹配委托实例。

C# 11 引入了用于存储函数指针的额外结构。函数指针比使用委托调用方法提供了性能改进。这些仅在不安全代码中可用，本文将在稍后介绍。

## 指南

考虑到 P/Invoke 的特殊性，有一些指南可以帮助编写代码过程。

> 指南

- 不要不必要的复制已经执行未托管 API 功能的现有托管类。
- 将 `extern` 方法声明为私有或内部。
- 提供使用托管习惯的公共包装方法，例如结构化异常处理、使用枚举处理特殊值等。

# 指针和地址

- 通过为不必要的参数选择默认值来简化包装方法。
- 在 Windows 上使用 `SetLastErrorAttribute` 将使用 `SetLastError` 错误代码的 API 转换为抛出 `Win32Exception` 的方法。
- 扩展 `SafeHandle` 或实现 `IDisposable` 并创建终结器，确保有效清理未托管资源。
- 当未托管 API 需要函数指针时，使用与所需方法匹配的委托类型。
- 尽可能使用 `ref` 参数而不是指针类型。

# 第 23 章：平台互操作性与不安全代码

## 列表 23.10：为不安全代码指定方法

```c
public class Program
{
    unsafe static int Main(string[] args)
    {
        // ...
    }
}
```

此外，C# 允许将 `unsafe` 作为语句来标记代码块以允许使用不安全代码（参见列表 23.11）。

## 列表 23.11：为不安全代码指定代码块

```c
public class Program
{
    static int Main(string[] args)
    unsafe
    {
        // ...
    }
}
```

`unsafe` 块内的代码可以包含指针等不安全构造结构。

> 注意
> 有必要显式地指示编译器支持不安全代码。

当你编写不安全代码时，你的代码将容易受到缓冲区溢出的影响，并可能暴露安全漏洞。因此，有必要显式通知编译器存在不安全代码。要实现这一点，请在你的 `.csproj` 文件中将 `AllowUnsafeBlocks` 设置为 `true`，如列表 23.12 所示。或者，你可以在运行 `dotnet build` 时在命令行传递该属性（参见输出 23.1）。或者，如果直接调用 C# 编译器，你需要使用 `/unsafe` 选项（参见输出 23.2）。

## 列表 23.12：无效引用类型示例

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.0</TargetFramework>
    <ProductName>Chapter20</ProductName>
    <WarningLevel>2</WarningLevel>
    <AllowUnsafeBlocks>True</AllowUnsafeBlocks>
  </PropertyGroup>
  <Import Project="..\Versioning.targets" />
  <ItemGroup>
    <ProjectReference Include="..\SharedCode\SharedCode.csproj" />
  </ItemGroup>
</Project>
```

## 输出 23.1

```bash
dotnet build /property:AllowUnsafeBlocks=True
```

## 输出 23.2

```bash
csc.exe /unsafe Program.cs
```

使用 Visual Studio，你可以通过勾选项目属性窗口中“生成”选项卡下的“允许不安全代码”复选框来激活此功能。

`/unsafe` 选项允许你直接操作内存并执行未管理的指令。因此，要求使用 `/unsafe` 意味着显式暴露此类代码可能引入的潜在安全漏洞。能力越大，责任越大。

# 指针声明

现在你已经将代码块标记为 `unsafe`，现在是时候看看如何编写不安全代码了。首先，不安全代码允许声明指针。考虑以下示例：

```csharp
byte* pData;
```

假设 `pData` 不为空，它的值值指向一个包含一个或多个连续字节的位置；`pData` 的值代表这些字节的内存地址。在 `*` 之前的类型是被引用类型——即指针值所指向位置的类型。在这个示例中，`pData` 是指针，而 `byte` 是被引用类型，如图 23.1 所示。

![](img/ffe0f34eac7523830420733690014d17_1130_0.png)

图 23.1：指针包含数据的地址

由于指针仅仅恰好引用内存地址的整数，因此它们不受垃圾回收的影响。C# 不允许除托管类型以外的引用类型（托管类型是指那些不是引用类型、不是泛型、且不包含引用类型的类型）。因此，以下命令是的：

```csharp
string* pMessage;
```

同样，该命令也是无效的：

```csharp
ServiceStatus* pStatus;
```

其中 `ServiceStatus` 的定义如列表 23.13 所示。问题再次在于 `ServiceStatus` 包含一个字符串字段。

## 列表 23.13：无效的被引用类型示例

```csharp
struct ServiceStatus
{
    int State;
    string Description; // Description 是引用类型
}
```

# 语言对比：C/C++——指针声明

在 C/C++ 中，同一条声明中的多个指针声明方式如下：

`int *p1, *p2;`

注意 `p2` 上的 `*`；这使得 `p2` 成为 `int*` 而不是 `int`。相比之下，C# 总是将 `*` 与数据类型放在一起：

`int* p1, p2;`

结果是两个 `int*` 类型的变量。这种语法与在单语句中声明多个数组的语法匹配：

```csharp
int[] array1, array2;
```

指针是一个全新的类型。与结构体、枚举和类不同，指针最终并不派生自 `System.Object`，甚至无法转换为 `System.Object`。相反，它们可以（显式地）转换为 `System.IntPtr`（该类型可以转换为 `System.Object`）。

除了仅包含托管类型的自定义结构体外，有效的指针还包括托管类型（非引用类型、int、float、double、decimal、bool、void）以及值类型（byte、ushort、int、uint、long、char）。

### 赋值

既然你已经将代码块标记为 `unsafe`，现在是时候看看如何编写不安全代码了。首先，不安全代码允许声明指针。考虑以下示例：

```csharp
byte* pData;
```

假设 `pData` 不为空，它的值指向一个包含一个或多个连续字节的位置；`pData` 的值代表这些字节的内存地址。在 `*` 之前的类型是被引用类型——即指针值所指向位置的类型。在这个示例中，`pData` 是指针，而 `byte` 是被引用类型，如图 23.1 所示。

![](img/ffe0f34eac7523830420733690014d17_1130_0.png)

图 23.1：指针包含数据的地址

由于指针仅仅恰好引用内存地址的整数，因此它们不受垃圾回收的影响。C# 不允许除托管类型以外的引用类型（托管类型是指那些不是引用类型、不是泛型、且不包含引用类型的类型）。因此，以下命令是无效的：

```csharp
string* pMessage;
```

同样，该命令也是无效的：

```csharp
ServiceStatus* pStatus;
```

其中 `ServiceStatus` 的定义如列表 23.13 所示。问题再次在于 `ServiceStatus` 包含一个字符串字段。

## 列表 23.13：无效的被引用类型示例

```csharp
struct ServiceStatus
{
    int State;
    string Description; // Description 是引用类型
}
```

# 第 23 章：平台互操作性与不安全代码

## 列表 23.10：为不安全代码指定方法

```c
public class Program
{
    unsafe static int Main(string[] args)
    {
        // ...
    }
}
```
