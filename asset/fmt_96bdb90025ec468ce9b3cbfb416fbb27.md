
列表 21.18 的结果显示在输出 21.4 中。

### 输出 21.4

> S$280ft = Smile

如列表 21.17 和列表 21.18 中的修改可能会导致意外行为。例如，如果在 `Console.WriteLine()` 语句之后将 `text` 重新赋值为 `"S$280ft"`，然后再次显示 `text`，输出仍然会是 `Smile`，因为两个相等字符串字面量的地址被优化为同一个字符串字面量，由两个变量引用。尽管表面上有赋值

```csharp
text = "S$280ft";
```

在列表 21.17 的 `unsafe` 代码之后，字符串赋值的内部操作是对修改后的 `"S$280ft"` 位置的地址赋值，因此 `text` 从未被设置为预期值。

## 访问被引用类型的成员

解引用指针会生成指针基础类型的变量。然后，你可以使用成员访问点运算符以通常方式访问基础类型的成员。然而，运算符优先级规则要求 `*x.y` 意味着 `*(x.y)`，这可能不是你想要的。如果 `x` 是指针，正确的代码是 `(*x).y`，这是一种令人不快的语法。为了更容易地访问已解引用指针的成员，C# 提供了一个特殊的成员访问运算符：`x->y` 是 `(*x).y` 的简写，如列表 21.19 所示。

### 列表 21.19：直接访问被引用类型的成员

```csharp
unsafe
{
    Angle angle = new Angle(30, 18, 0);
    Angle* pAngle = @angle;
    System.Console.WriteLine("{0}' {1}' {2}",
        pAngle->Hours, pAngle->Minutes, pAngle->Seconds);
}
```

列表 21.19 的结果显示在输出 21.5 中。

### 输出 21.5

`30° 18' 0`

## 通过委托执行 unsafe 代码

正如本章开头所承诺的，我们将以一个完整的可运行示例作为结尾，展示你在 C# 中可能做的最“不安全”的事情：获取内存块的指针，用机器代码字节填充它，创建一个引用新代码的委托，并执行它。在这个示例中，我们使用汇编代码来确定处理器 ID。如果在 Windows 机器上运行，它会打印处理器 ID。列表 21.20 展示了如何做到这一点。

### 列表 21.20：指定用于 unsafe 代码的块

```csharp
using System;
using System.Runtime.InteropServices;
using System.Text;
class Program
{
    public unsafe delegate void MethodInvoker(byte* buffer);
    public unsafe static int ChapterMain()
    {
        if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
        {
            unsafe
            {
                byte[] codeBytes = new byte[] {
                    0x49, 0x89, 0xd8, // mov %rbx,%r8
                    0x49, 0x89, 0xc9, // mov %rcx,%r9
                    0x48, 0x31, 0xc0, // xor %rax,%rax
                    0xf, 0xa2, // cpuid
                    0x4c, 0x89, 0xc8, // mov %r9,%rax
                    0x89, 0x18, // mov %ebx,0x0(%rax)
                    0x89, 0x50, 0x04, // mov %edx,0x4(%rax)
                    0x89, 0x48, 0x08, // mov %ecx,0x8(%rax)
                    0x4c, 0x89, 0xc3, // mov %r8,%rbx
                    0xc3 // retq
                };
                byte[] buffer = new byte[12];
                using (VirtualMemoryPtr codeBytesPtr =
                    new VirtualMemoryPtr(codeBytes.Length))
                {
                    Marshal.Copy(
                        codeBytes, 0,
                        codeBytesPtr, codeBytes.Length);
                    MethodInvoker method =
                        Marshal.GetDelegateForFunctionPointer<MethodInvoker>(codeBytesPtr);
                    fixed (byte* newBuffer = &buffer[0])
                    {
                        method(newBuffer);
                    }
                    Console.Write("Processor Id: ");
                    Console.WriteLine(ASCIIEncoding.ASCII.GetChars(buffer));
                } // unsafe
            }
        }
        else
        {
            Console.WriteLine("This sample is only valid for Windows");
        }
        return 0;
    }
}
```

列表 21.20 的结果显示在输出 21.6 中。

### 输出 21.6

```
Processor Id: GenuineIntel
```
