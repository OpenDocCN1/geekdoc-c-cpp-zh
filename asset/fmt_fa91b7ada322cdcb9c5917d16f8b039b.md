
```c
uRtn = write (hFil, pBuf, uNum);
#if DEBUG
 ((uRtn != uNum) || (errno))
    pHdlFil = HdlFind (pHdrHdlFile, hFil);
    DebugMessageBox("File: %s, Module %s, Line %d\nWrite %d,%p,%d) = %d\nError: %#X",
    pHdlFil->sName, pHdlFil->pModule, pHdlFil->iLine,
    hFil, pBuf, uNum, uRtn, errno);
}
#endif

return (uRtn);
}
```

### Close

`Close`非常简单但非常重要。`Close`会检查传入的句柄是否合法。然后它会关闭文件。关闭文件后，`close`必须从`Hdl`链表中移除该文件关联的信息。

### Close

下面的程序示例说明了如何关闭文件。

```c
void Close (int hFil)
{
#if DEBUG
 if (HdlFind (pHdrHdlFile, hFil) == NULL)
    DebugMessageBox("Close %d\nUnknown Handle", hFil);
#endif

close (hFil);
#if DEBUG
 // Close 可以返回错误！
if (errno)
{
    pHdlFil = HdlFind(pHdrHdlFile, hFile);
    DebugMessage("File: %s, Module %s, Line %d\n" 
               Close(%d)\nError: %#X", pHdlFil->sName,
               pHdlFil->pModule, pHdlFil->iLine, hFile, errno);
}

// 从链表中移除我们
HdlDelete(pHdrHdlFile, hFile);
#endif
}
```

请确保你已经关闭了所有文件。虽然打开的文件并不太危险（`DOS`会关闭它），但它可能会指出某些你认为已经执行但实际上没有执行的代码。此外，已处理的文件是有限资源，所以当你完成后应该关闭它们以释放资源。一旦文件被关闭，它的缓冲区就会刷新，大小也会更新，这样即使在程序结束前机器重启，文件也将是完全安全的。

简而言之，退出时留下文件是懒惰、粗心的的，并且可能对你的程序造成破坏（从技术上说——这不是一个好主意）。幸运的是，你维护的打开文件链表允许我们仍然通过名称识别文件。这使得确定哪些文件已打开变得简单。

### FilesDone

下面的程序示例说明了在文件退出时列出仍然打开的文件。

```c
// 程序退出时调用，以确定哪些文件
// 仍然打开。你需要同时检查我们自己的和其他文件。
void FilesDone(void)
{
    HDL_FILE *pHdlFile;

    // 查看哪些文件仍开启，然后消除存储
    for (pHdlFile = HdlNext(pHdrHdlFile, NULL); pHdlFile != NULL;
        pHdlFile = HdlNext(pHdrHdlFile, pHdlFile))
        DebugPrint(0, "%s is opened in %s at line %d still open",
                   pHdlFile->sFileName, pHdlFile->pFile, pHdlFile->iLine);

    // 查找列表中没有的打开文件
    for (iNum=5; iNum<256; iNum++)
      if (lseek(iNum, 0L, 0) != -1L)
        if (! HdlFind (pHdHdrFile, iNum)
          DebugPrint(0, "File open. %d", iNum);

    // 你需要释放存储，以便当你查找
    // 未释放的内存时，它不会显示我们的链表
    HdlClose (pHdHdrFile);
}
```

## 第 10 章

### C++ 的特殊技巧

到目前为止，所有的示例都是用 `c` 语言提供的（部分堆栈代码使用了汇编 `asm`）。然而，我们现在进入了 `c++` 的奇妙世界。像 `PC` 社区的几乎所有人一样，我在过去的 2 年里才开始玩 `c++`。而且直到最近 6 个月内，编译器才变得足够好到可以在商业代码（这确实让这本书看起来很老旧了）。

因此，本章是对 `c++` 下调试技巧的首次尝试。与任何其他语言一样，我们并没有在 `c++` 下执行不同的技巧。相反，我们有独特的方法来实现之前列出的技巧。然而，`C++` 确实让实现之前提到的某些技巧变得更容易了。

### 覆盖全局 new 和 delete

我们希望对 `new` 和 `delete` 使用堆分配技巧。我们将重新定义 `new` 和 `delete` 为我们自己的函数。这些函数可以像在第 8 章“监控堆分配”中讨论的 `Alloc` 和 `Free` 调用一样工作。

我们希望这些调用与第 8 章使用的 `Alloc` 和 `Free` 隔离开。全局变量在程序结束时确实不会被销毁（这不是 `bug`）。我们还希望 `Alloc` 调用 `malloc`，而我们希望我们的 `new` 调用原始的 `new`。

在调试模式下，你不应该重新定义 `new` 和 `delete`。直接调用它们要高效得多。在 `C++` 中，你只需要将重定义代码放在 `#if DEBUG` 内部，其他部分保持不变。

重新定义 `new` 最有用的理由是填充

### New 和 Delete

下面的程序示例说明了 `new` 和 `delete`。

```c
#if DEBUG
void* operator new (size_t size)
{
    void *pBuf = malloc(size);
    if (!pBuf)
        DebugMessageBox("new %d failed\n", size);
    memset(pBuf, FILL_CHAR, size);
    return pBuf;
}

void operator delete (void *pBuf, size_t size)
{
    if (pBuf)
    {
        if ((unsigned *)pBuf) != MEM_1)
            DebugMessageBox("delete %d underwritten\n%X-%#X", size, *(unsigned *)pBuf);
        free(pBuf);
    }
}
#endif
```

### 108 无 Bug

```c
if (errno)
{
    pHdlFil = HdlFind(pHdrHdlFile, hFile);
    DebugMessage("File: %s, Module %s, Line %d\n" 
               Close(%d)\nError: %#X", pHdlFil->sName,
               pHdlFil->pModule, pHdlFil->iLine, hFile, errno);
}

// 从链表中移除我们
HdlDelete(pHdrHdlFile, hFile);
```

### 构造函数和析构函数

在构造函数中，记得执行以下操作。通过这些操作，`c++` 自动化了我们在 `c` 语言中必须显式执行的结构设置。

- 1. 将所有变量设置为 `FILL_CHAR`。小心，因为类中的数据并不总是连续的。虚函数地址可能会潜伏在变量之间（通常当变量是一个类时）——如果你覆盖了它们，你是在制造 `bug` 而不是发现 `bug`。解决这个问题的简单方法是将所有数据放在一个结构中。你可以直接访问元素（大多数编译器也支持匿名结构），然后用 `FILL_CHAR` 填充结构。

- 2. 在调试模式下，为每个类添加一个 `ID` 字节或字）。在构造函数中，将 `ID` 设置为已知值（每个类不同）。由于 `C++` 自动调用构造函数，你就可以保证已经设置了 `ID` 元素。

### string 构造函数

下面的程序示例说明了字符串构造函数的用法。

```c
#define STRING_ID 0x13
class string
{
private:
    struct s_string
    {
        char str[20];
        char len;
    } vars;
#if DEBUG
    char ID;
#endif
    :

string :: string ()
{
#if DEBUG
    memset(&vars, FILL_CHAR, sizeof(s_string));
    ID = STRING_ID;
#endif

// 初始化变量
len = 0;
}
};
```

### 字符串析构函数

作用域内，你现在正在检查每一个变量。这是一个强大的工具。

其次，你用 `FILL_CHAR` 填充数据结构。然后，如果你在变量被销毁后访问它，你将获得垃圾数据。你还会重写 `ID`，导致 `ID` 错误。你特意重写了 `ID`，以确保 `memset` 实例的 `FILL_CHAR` 等于正确的 `ID` 值。

下面的程序示例说明了字符串析构函数的使用。

```cpp
// note - 在非调试模式不需要析构函数
#if DEBUG
string() : ::string ()
{
    // 确保 ID 是正确的
    if (ID != STRING_ID)
        DebugBox("Bad String ID returned");

    memset(&vars, FILL_CHAR, sizeof(s_string));
    ID = ~STRING_ID;
}
#endif
```

通过在构造函数和析构函数中使用上述实践，你就可以从我们所有的类中消除以下类型的错误。如果你使用了未初始化的变量，将得到一个坏值（`FILL_CHAR`）。如果你得到了一个错误的指针，在销毁错误的指针时，你会收到一条消息。最后，如果你覆盖了数据，也会收到一条消息。如果你尝试在变量超出作用域后访问它，将得到坏数据。

仅仅通过在每个构造函数和析构函数中放置少量代码，我们就获得了所有这些强大的功能。而且性能影响微乎其微。

### 基类断言

大多数 `C++` 程序员使用一个所有类都派生的基类。仅在调试模式下，为基类添加两个方法。第一个是 `Assert` 函数。你只需调用 `inst.Assert()` 对类的任何实例进行断言。在非调试模式下，`Assert` 应该定义为空空函数，这样就不会为断言调用生成代码。

这把断言放在了它应该，作为类定义的一部分。随着类的变化，它的断言也会之变化。它也使得断言任何实例变得非常简单。

### 基断言

下面的程序示例说明了 `Assert` 的定义。

```cpp
class base
{
...

#if DEBUG
  void Assert (void);
  void Dump (void);
#else
  void Assert (void) {};
  void Dump (void) {};
#endif

#if DEBUG
void base::Assert (void)
{
  // 这个函数不应该被调用
  DebugMessageBox ("No Assert for this class - OhOh");
}
#endif
```

你应该添加的第二个方法是 `Dump`。`Dump` 将输出调试监控器的内容。有了 `Assert`，它把 `Dump` 放在了它应该，与类在一起。它也使得导出类实例的内容变得容易。

### 基转储

```cpp
#if DEBUG
void base::Dump(void)
{
    // 这个函数不应该被调用
    DebugPrintf(0, "No Dump for this class - OhOh.. ");
}
#endif
```

对于每个类，你都在调试模式下定义这两个函数。在非调试模式下，将使用基类的空定义。如果一个人设计了一个类，另一个开发者可以在不了解类本身的情况下对其进行断言或转储。

这把一些调试功能带入了面向对象的世界。仅仅因为我正在销毁一个类的实例，并不意味着我想知道它是如何工作的。我只是想知道它是什么时候被销毁的。

我们可以让断言简单如检查 `ID` 字节，也可以复杂如对类中的所有数据进行一致性检查。重要的是为每个类准备一个断言，至少会检查 `ID`。这将捕捉到你没有指向你认为正在指向的变量类型的地方。

下面的字符串类绝不是建议的实现方法。相反，它是为了说明上述讨论的技巧。

### 字符串断言与转储

下面的程序示例说明了字符串的 `Assert` 和 `Dump` 方法。

```cpp
#if DEBUG
void string::Assert(char *pFile=__FILE__, int iLine=__LINE__)
{
    // 你真的指向一个字符串吗？
    if (ID != STRING_ID)
    {
        DebugMessageBox("string has wrong ID\nFile: %s, Line: %d",
        pFile, iLine);
        return;
    }

    // 检查长度
    if ((len < 0) || (len > 20))
        DebugMessageBox("string has len:%d (>20)\nFile:%s, Line:%d",
        len, pFile, iLine);

    // 你可以在这里检查字符串的内容
    // 如果这样做，在 iLen 错误时返回。
}

void string::Dump (void)
{
    char sBuf[22];

    // 你需要拷贝 str 以供 printf
    memcpy(sBuf, str, 20);
    sBuf[len] = 0;

    DebugPrintf(0, "string %d: %s", len, sBuf);
}
#endif
```

### 调试类

当我第一次决定写这本书时，我强烈考虑用 `C++` 而不是 `C` 编写所有的代码示例。它不仅是未来的语言，而且极大地帮助消除某类错误。遗憾的是，它不是现在的语言，但这本书使用 `C` 来介绍这些概念。

我也想使用 `C++`，因为书中的许多概念属于一个调试类。

我们可以通过在入口处保留所有寄存器并在出口处检查它们来核对这些寄存器。以下宏使用 `pusha` 以保持代码示例简短。它们也没有检查段寄存器；在没有远端指针（`far pointers`）的小模型程序中，不需要这种检查。

入口（`Entry`）必须是每个函数的第一个调用。如果你访问栈上的变量，在确定参数的偏移量时，需要考虑 `pusha`。可以简单地将 `equate STACK_OFF` 添加到每个偏移量上。

在 `RegCheck` 调用之后，唯一的调用应该是 `ret`。你可能想将 `ret` 包含在 `RegCheck` 中。但我倾向于单独使用。没有 `ret` 的函数看起来很奇怪。`RegCheck` 使用 `add sp, 16` 是因为你无法恢复那些已经改变的寄存器。你与 `pushed` 的寄存器进行对比，但随后会将它们丢弃。

这些宏不仅可以发现你是否没有保留某个寄存器——还能发现你是否正确清理了栈。如果你没有将 `SP` 恢复到之前的值，那么所有检查都不应该通过。先测试 `SP` 确保它失败，这样你就会考虑到栈帧（`stack frame`）。

### 检查寄存器

下面的程序示例演示了 `CHECK_STACK`。

```
if DEBUG
STACK_OFF      EQU     16
else
STACK_OFF      EQU     0
endif
```

```
CHECK_STACK      STRUCT
    csFlags        dw
    csBPret        dw
    csDI           dw
    csSI           dw
    csBP           dw
```

```
csSP    dw
csBX    dw
csDX    dw
csCX    dw
csAX    dw
CHECK_STACK  ENDS
```

```
RegEntry  MACRO
if DEBUG
    pusha
endif
endm
```

```
RegCheck  MACRO  r
if DEBUG
    pushf
    push bp
    mov    bp, sp
    irp    reg, <r>
ifidni  <reg>, <sp>
    cmp    sp, [bp + csBP]
    TrapNe
else
```

```
; bp 是特殊的 - 你必须使用栈上的值
ifidni  <reg>, <ax>
    push    ax
    mov     ax, [bp + csBPRet]
    cmp     ax, [bp + csBP]
    pop     ax
    TrapNe
else
```

```
; 处理其余寄存器
; 包括 al, ah, ..., dh
endif
endm
```

```
pop     bp
popf
add     sp, 16
endif
endm
```

### 123 无 Bug

```
func    proc near
               RegEntry

               ; 获取传入的参数
               mov     bp, sp
               mov     ax, [bp + STACK_OFF + 2]
               ...
               RegCheck <di,si,bp>
               ret
               end
```
