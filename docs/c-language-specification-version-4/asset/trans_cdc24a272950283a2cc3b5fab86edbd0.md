
```
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize) {
        int len = s.Length;
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }

    unsafe static void Main()
    {
        Font f;
        f.size = 10;
        PutString("Times New Roman", f.name, 32);
    }
}
```

## 18.7.3 确定性赋值检查

固定大小缓冲区不受确定性赋值检查 (§5.3) 的约束，并且在对结构体类型变量进行确定性赋值检查时，固定大小缓冲区成员会被忽略。

当固定大小缓冲区成员的最外层包含的结构体变量是静态变量、类实例的实例变量或数组元素时，固定大小缓冲区的元素会自动初始化为其默认值 (§5.2)。在所有其他情况下，固定大小缓冲区的初始内容是未定义的。

## 18.8 栈分配

在不安全上下文中，局部变量声明 (§8.5.1) 可以包含栈分配初始化器，该初始化器从调用栈分配内存。

```
local-variable-initializer:
    ...
    stackalloc-initializer

stackalloc-initializer:
    stackalloc unmanaged-type [ expression ]
```

unmanaged-type 表示将存储在新分配位置中的项目的类型，而 expression 表示这些项目的数量。两者合在一起指定了所需的分配大小。由于栈分配的大小不能为负，因此将项目数量指定为求值为负值的常量表达式是编译时错误。

形式为 stackalloc T[E] 的栈分配初始化器要求 T 为非托管类型 (§18.2)，E 为类型为 int 的表达式。该构造从调用栈分配 E * sizeof(T) 字节，并返回指向新分配块的指针，其类型为 T*。如果 E 为负值，则行为未定义。如果 E 为零，则不进行分配，且返回的指针由实现定义。如果没有足够的内存来分配给定大小的块，则会抛出 System.StackOverflowException。

新分配内存的内容是未定义的。

栈分配初始化器不允许在 catch 或 finally 块 (§8.10) 中使用。

分配的内存会在方法返回时自动丢弃。这对应于 alloca 函数，这是在 C 和 C++ 实现中常见的扩展。

在示例中

```csharp
using System;
class Test
{
    static string IntToString(int value) {
        int n = value >= 0? value: -value;
        unsafe {
            char* buffer = stackalloc char[16];
            char* p = buffer + 16;
            do {
                *--p = (char)(n % 10 + '0');
                n /= 10;
            } while (n != 0);
            if (value < 0) *--p = '-';
            return new string(p, 0, (int)(buffer + 16 - p));
        }
    }
    static void Main() {
        Console.WriteLine(IntToString(12345));
        Console.WriteLine(IntToString(-999));
    }
}
```

栈分配初始化器在 IntToString 方法中用于在栈上分配一个 16 个字符的缓冲区。缓冲区会在方法返回时自动丢弃。

## 18.9 动态内存分配

除 stackalloc 运算符外，C# 未提供用于管理非垃圾回收内存的预定义结构。此类服务通常由支持的类库提供，或直接从底层操作系统导入。例如，下面的 Memory 类说明了如何从 C# 访问底层操作系统的堆函数：

```csharp
using System;
using System.Runtime.InteropServices;
public unsafe class Memory
{
    // Handle for the process heap. This handle is used in all calls to the
    // HeapXXX APIs in the methods below.
    static int ph = GetProcessHeap();
    // Private instance constructor to prevent instantiation.
    private Memory() {}
    // Allocates a memory block of the given size. The allocated memory is
    // automatically initialized to zero.
    public static void* Alloc(int size) {
        void* result = HeapAlloc(ph, HEAP_ZERO_MEMORY, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }
    // Copies count bytes from src to dst. The source and destination
    // blocks are permitted to overlap.
    public static void Copy(void* src, void* dst, int count) {
        byte* ps = (byte*)src;
        byte* pd = (byte*)dst;
        if (ps > pd) {
            for (; count != 0; count--) *pd++ = *ps++;
        }
        else if (ps < pd) {
            for (ps += count, pd += count; count != 0; count--) *--pd = *--ps;
        }
    }
    // Frees a memory block.
    public static void Free(void* block) {
        if (!HeapFree(ph, 0, block)) throw new InvalidOperationException();
    }
    // Re-allocates a memory block. If the reallocation request is for a
    // larger size, the additional region of memory is automatically
    // initialized to zero.
    public static void* ReAlloc(void* block, int size) {
        void* result = HeapReAlloc(ph, HEAP_ZERO_MEMORY, block, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }
    // Returns the size of a memory block.
    public static int SizeOf(void* block) {
        int result = HeapSize(ph, 0, block);
        if (result == -1) throw new InvalidOperationException();
        return result;
    }
    // Heap flags
    const int HEAP_ZERO_MEMORY = 0x00000008;
    // Heap API functions
    [DllImport("kernel32")]
    static extern int GetProcessHeap();
    [DllImport("kernel32")]
    static extern void* HeapAlloc(int hHeap, int flags, int size);
    [DllImport("kernel32")]
    static extern bool HeapFree(int hHeap, int flags, void* block);
    [DllImport("kernel32")]
    static extern void* HeapReAlloc(int hHeap, int flags,
        void* block, int size);
    [DllImport("kernel32")]
    static extern int HeapSize(int hHeap, int flags, void* block);
}
```

使用 Memory 类的示例如下所示：

```
class Test
{
    static void Main() {
        unsafe {
            byte* buffer = (byte*)Memory.Alloc(256);
            try {
                for (int i = 0; i < 256; i++) buffer[i] = (byte)i;
                byte[] array = new byte[256];
                fixed (byte* p = array) Memory.Copy(buffer, p, 256);
            }
            finally {
                Memory.Free(buffer);
            }
        }
        for (int i = 0; i < 256; i++) Console.WriteLine(array[i]);
    }
}
```

该示例通过 Memory.Alloc 分配 256 字节的内存，并使用从 0 到 255 递增的值初始化内存块。然后它分配一个包含 256 个元素的字节数组，并使用 Memory.Copy 将内存块的内容复制到字节数组中。最后，使用 Memory.Free 释放内存块，并将字节数组的内容输出到控制台。

## A. 文档注释

C# 为程序员提供了一种机制，使用包含 XML 文本的特殊注释语法来记录代码。在源代码文件中，具有特定形式的注释可用于指示工具从这些注释和它们前面的源代码元素生成 XML。使用此类语法的注释称为文档注释。它们必须立即位于用户定义的类型（如类、委托或接口）或成员（如字段、事件、属性或方法）之前。XML 生成工具称为文档生成器。（该生成器可以是，但不必是 C# 编译器本身。）文档生成器产生的输出称为文档文件。文档文件用作文档查看器的输入，文档查看器是一种旨在以某种方式可视化显示类型信息及其相关文档的工具。

本规范建议了一组可在文档注释中使用的标签，但使用这些标签不是必需的，如果需要，也可以使用其他标签，只要遵循良好的 XML 规则即可。

### A.1 引言

具有特殊形式的注释可用于指示工具从这些注释和它们前面的源代码元素生成 XML。此类注释是单行注释，以三个斜杠 (///) 开头，或定界注释，以斜杠和两个星号 (/**) 开头。它们必须立即位于它们注释的用户定义的类型（如类、委托或接口）或成员（如字段、事件、属性或方法）之前。属性部分 (§17.2) 被视为声明的一部分，因此文档注释必须位于应用于类型或成员的属性之前。

语法：

```
single-line-doc-comment:
    /// input-characters_opt

delimited-doc-comment:
    /** delimited-comment-text_opt */
```

在单行文档注释中，如果在当前单行文档注释相邻的每个单行文档注释的 /// 字符后都有一个空白字符，则该空白字符不会包含在 XML 输出中。

在定界文档注释中，如果第二行的第一个非空白字符是星号，并且在定界文档注释内的每一行开头都重复相同的可选空白字符和星号字符的模式，则重复模式的字符不会包含在 XML 输出中。该模式可能在星号字符之前以及之后包含空白字符。

示例：

```
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>
public class Point
{
    /// <summary>method <c>draw</c> renders the point.</summary>
    void draw() {...}
}
```
