
`newobj` IL 指令创建一个对象。许多语言（包括 C#、C++/CLI 和 Microsoft Visual Basic）提供 `new` 运算符，它会使编译器将 `newobj` 指令生成到方法的 IL 代码中。`newobj` 指令会使 CLR 执行以下步骤：

- 1. 计算该类型（及其所有基类型）的字段所需的字节数。
- 2. 加上对象开销所需的字节数。每个对象都有两个开销字段：类型对象指针和同步块索引。对于 32 位应用程序，这些字段各需要 32 位，因此每个对象要增加 8 字节。对于 64 位应用程序，每个字段为 64 位，因此每个对象要增加 16 字节。
- 3. 然后，CLR 检查保留区域中是否有分配该对象所需的字节可用（必要时提交存储）。如果托管堆中有足够的空闲空间，该对象将能放入，并从 `NextObjPtr` 指向的地址开始，这些字节会被清零。随后调用该类型的构造函数（将 `NextObjPtr` 作为 `this` 参数传入），而 `newobj` IL 指令（或 C# 的 `new` 运算符）返回该对象的地址。就在返回地址之前，`NextObjPtr` 会越过该对象向前移动，现在指向堆中下一个对象将被放置的地址。

图 21-1 展示了一个由三个对象组成的托管堆：A、B 和 C。如果要分配一个新对象，它将被放在 `NextObjPtr` 所指向的位置（紧跟在对象 C 之后）。

![](img/3c46ff5b170881db4209d365b1f7a808_539_0.png)

**图 21-1** 新初始化且其中构造了三个对象的托管堆

相比之下，我们来看看 C 运行时堆如何分配内存。在 C 运行时堆中，为对象分配内存需要遍历一个由数据结构组成的链表。一旦找到足够大的块，就会拆分该块，并修改链表节点中的指针以保持结构完整。对于托管堆，分配对象只是向指针加一个值——相比之下这快得惊人。事实上，从托管堆分配对象几乎与从线程栈分配内存一样快！此外，大多数堆（例如 C 运行时堆）会在找到空闲空间的地方分配对象。因此，如果我连续创建多个对象，这些对象很可能被数 MB 的地址空间分隔开。然而，在托管堆中，连续分配多个对象可确保这些对象在内存中连续。

在许多应用程序中，大约同时分配的对象往往彼此关系密切，并且经常在相近的时间被访问。例如，在创建 `BinaryWriter` 对象之前立即分配一个 `FileStream` 对象是非常常见的。然后，应用程序将使用 `BinaryWriter` 对象，而该对象在内部使用 `FileStream` 对象。在垃圾回收环境中，新对象在内存中连续分配，从而因引用局部性带来性能提升。具体来说，这意味着你的进程工作集将小于在非托管环境中运行的类似应用程序。你的代码正在使用的对象也很可能都能驻留在 CPU 缓存中。你的应用程序将以惊人的速度访问这些对象，因为 CPU 能够执行其大部分操作而不会发生缓存未命中，从而避免因访问 RAM 变慢。

到目前为止，听起来托管堆似乎因其实现简单和速度快而远优于 C 运行时堆。但在过于兴奋之前，你应该知道一个小细节。托管堆获得这些优势是因为它做了一个非常大的假设：地址空间和存储是无限的。显然，这个假设很荒谬，托管堆必须采用一种机制来支持它做出这个假设。这种机制就是垃圾回收器。它的工作方式如下：

当应用程序调用 `new` 运算符创建对象时，该区域中可能没有足够的剩余地址空间来分配给该对象。堆通过将对象所需的字节数加到 `NextObjPtr` 中的地址来检测空间不足。如果结果值超出地址空间区域的末尾，则堆已满，必须执行垃圾回收。

> **重要** 我刚才所说的过于简化了。实际上，垃圾回收在第 0 代已满时发生。有些垃圾回收器使用分代，这种机制的唯一目的就是提高性能。其思路是，新创建的对象属于年轻代，而在应用程序生命周期早期创建的对象属于老年代。第 0 代中的对象是最近分配且从未被垃圾回收算法检查过的对象。在一次回收中幸存下来的对象会被提升到另一代（例如第 1 代）。将对象分代后，垃圾回收器可以只回收特定代，而不是回收托管堆中的所有对象。我将在本章后面更详细地解释分代。在此之前，你最容易的理解是：堆满时就会发生垃圾回收。

## 垃圾回收算法

垃圾回收器会检查堆中是否有任何对象不再被应用程序使用。如果存在这样的对象，就可以回收这些对象占用的内存。（如果垃圾回收后堆中不再有可用内存，`new` 会抛出 `OutOfMemoryException`。）垃圾回收器如何知道应用程序是否正在使用某个对象？可以想象，这不是一个简单的问题。

每个应用程序都有一组 `roots`。单个根是一个存储位置，其中包含指向引用类型对象的内存指针。这个指针要么引用托管堆中的对象，要么被设置为 `null`。例如，静态字段（在某个类型中定义）被视为根。此外，任何方法参数或局部变量都被视为根。只有引用类型的变量才被视为根；值类型变量绝不会被视为根。现在，让我们从一个具体示例开始，先看下面的类定义：

```csharp
internal sealed class SomeType {
    private TextWriter m_textWriter;

    public SomeType(TextWriter tw) {
        m_textWriter = tw;
    }

    public void WriteBytes(Byte[] bytes) {
        for (Int32 x = 0; x < bytes.Length; x++) {
            m_textWriter.Write(bytes[x]);
        }
    }
}
```

第一次调用 WriteBytes 方法时，即时（JIT）编译器会将该方法的 IL 代码转换为本机 CPU 指令。假设 CLR 正在 x86 CPU 上运行，并且 JIT 编译器将 WriteBytes 方法编译为图 21-2 所示的 CPU 指令。（我在右侧添加了注释，以帮助你理解本机代码如何映射回原始源代码。）

```asm
00000000 push    edi                          // Prolog
00000001 push    esi
00000002 push    ebx

EBX ─────── 00000003 mov     ebx, ecx                    // ebx = this  (argument)
            00000005 mov     esi, edx                    // esi = bytes array (argument)
ESI ─────── 00000007 xor     edi, edi                    // edi = x
            00000009 cmp     dword ptr [esi+4],0         // compare bytes.Length with 0
            0000000d jle     0000002A                    // if bytes.Length <=0, go to 2a

ECX ─────── 0000000f mov     ecx,dword ptr [ebx+4]       // ecx = m_textWriter (field)
            00000012 cmp     edi,dword ptr [esi+4]       // compare x with bytes.Length
            00000015 jae     0000002E                    // if x >= bytes.Length, go to 2e

            00000017 movzx   edx,byte ptr [esi+edi+8]   // edx = bytes[x]
            0000001c mov     eax,dword ptr [ecx]         // eax = m_textWriter's type object
            0000001e call    dword ptr [eax+000000BCh]   // call m_textWriter's Write method

            00000024 inc     edi                         // x++
            00000025 cmp     edi,dword ptr [esi+4]       // compare bytes.Length with x
            00000028 jg      0000000F                    // if bytes.Length > x, go to f

            0000002a pop     ebx                         // Epilog
            0000002b pop     esi
            0000002c pop     edi
            0000002e ret                                 // return to caller

            0000002e call    7686E337                    // Throw IndexOutOfRangeException
            00000033 int     3                           // Break in debugger
```

**图 21-2** JIT 编译器生成的本机代码，并显示了根的范围
