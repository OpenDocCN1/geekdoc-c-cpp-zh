
### EMS 和 XMS

EMS 和 XMS 提供类似的功能，并且比堆分配更难检查。它们也比普通内存更复杂，因此我们更容易在它们上面出错。因此，必须尽可能彻底地检查对此类内存的调用。

随着时间的推移，EMS 和 XMS 变得越来越不重要。Windows 不使用它们。需要大量内存的 DOS 应用程序通常被编写为 DPMI 应用程序，它们使用 DPMI 服务器，而应用程序本身不进行任何 XMS 调用。

如果你不在乎 EMS 或 XMS，请阅读下面关于句柄跟踪的部分（也用于第 9 章“文件 I/O”），然后跳过该章节的其余部分。我在后续章节中包含的代码很少，仅足以传达基本概念。完整代码可以在配套磁盘上找到。

### 句柄跟踪

遗憾的是，你无法在 EMS/XMS 内存上像在堆上那样放置头文件和标题。然而，你仍然可以实现大部分在堆上可以进行的检查。

首先，对于每个 EMS/XMS 分配，我们都会分配一个类似于我们在堆上使用的头文件。但是，这段内存是通过普通内存中的 `malloc` 生成的。我们使用这段 `malloc` 内存来跟踪对 EMS 和 XMS 内存的使用（下一章将跟踪文件句柄）。

这些结构体持有 `malloc` 内存的句柄。由于每个句柄都是唯一的，所以你为 EMS 有一个链表，为 XMS 有另一个。这增加了少量的处理开销。对于堆内存，当你传递指针时，你知道结构体所在的位置。对于 EMS 和 XMS，你必须遍历相应的链表来找到传递给你的句柄。

为了做到这一点，我们创建了一组句柄调用。第一个创建一个链表。每个链表都有不同的数据大小，用于存储与给定句柄集关联的信息。这在与文件配合使用时变得很重要，因为你可能需要存储长达 74 字节的文件名。

### HdlCreate

下面的程序示例说明了为了配合句柄分配内存的用法。

```c
typedef struct S_HANDLE_NEXT
{
    struct S_HANDLE_NEXT *pNext;
    int iHdl;
} HANDLE_NEXT;

typedef struct S_HANDLE_HDR
{
    HANDLE_NEXT sHdlNext;
    unsigned uSize;
} HANDLE_HDR;

HANDLE_HDR *HdlCreate (unsigned uSize)
{
    HANDLE_HDR *phdl;
    if ((phdl = malloc(sizeof(HANDLE_HDR))) == NULL)
        return NULL;
    memset(phdl, 0, sizeof(HANDLE_HDR));
    phdl->uSize = uSize;
    return phdl;
}
```
*(注：原文示例代码中 `HdlCreate` 处存在语法错误如括号不匹配，根据要求代码块不翻译，此处保持逻辑或翻译结构)*
