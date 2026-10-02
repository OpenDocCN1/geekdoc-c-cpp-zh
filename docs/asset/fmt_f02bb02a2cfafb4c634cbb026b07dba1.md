
## 汇编代码片段

```asm
.text:0000000078D24510 push    rbx
.text:0000000078D24515 sub     rsp, 50h
.text:0000000078D24516 cmp     rcx, 10000h
.text:0000000078D24517 jnb     loc_78D42FB4
.text:0000000078D24518 mov     [rsp+50h+var_38], rcx
.text:0000000078D24519 jmp     short -2h
.text:0000000078D2452A loc_78D4252A:
.text:0000000078D2452A mov     [rbx], eax
.text:0000000078D2452A BaseResourceIdA:1EAD0
.text:0000000078D2452B jmp     short +2h
.text:0000000078D2452C loc_78D4252C:
.text:0000000078D2452C mov     [rbx], loc_78D4252A
.text:0000000078D2452D BaseResourceIdA:1BB74
.text:0000000078D2452E mov     rax, rcx
.text:0000000078D2452F add     rsp, 50h
.text:0000000078D24530 pop     rbx
.text:0000000078D24531 ret
.text:0000000078D24532                                 78D4533
.text:0000000078D24534 align   20h
.text:0000000078D24535 BaseDllMapResourceId endp
.text:0000000078FB4  loc_78D42FB4:
.text:0000000078FB4  BaseResourceIdA+D
.text:0000000078FB5  cmp     byte ptr [rcx], '#'
.text:0000000078FB6  jnz     short loc_78D4305
.text:0000000078FB7  inc     rcx
.text:0000000078FBC  lea     r8, [rsp+50h+arg_8]
.text:0000000078FC1  mov     edx, 0Eh
```

如果你发现了拼写错误或有任何建议，请随时留言：我的邮箱。谢谢！

```asm
.text:0000000078DFC6 call    cs:RtlCharToInteger
.text:0000000078FCC  mov     ecx, [rsp+58h+var_8]
.text:0000000078FD0  mov     [rsp+58h+var_38], rcx
.text:0000000078FD5  test    eax, eax
.text:0000000078FD7  js      short loc_78DFE6
.text:0000000078FD9  test    rcx, 0xFFFFFF00h
.text:0000000078FE0  jz      loc_78D52A
```

如果输入指针中的值大于 `0x10000`，则发生字符串处理。否则，返回 `ptr` 的输入值。由于此处是 64 位代码，`0xFFFFFFFF` 仍然有效。

注意读者，如果字符串地址低于 `0x10000` 会怎样？这段代码依赖于在 Windows 中 0x1000 以下的地址没有任何内容，至少在 Win32 领域如此。

Raymond Chen 关于这一点：

> 构建如何工作？它将整数存储在指针的低 16 位，高位置零。这依赖于地址空间的前 64KB 永远映射到有效内存，这一约定在 Windows 7 中被强制执行。

简而言之，这是一个肮脏的黑客技巧（dirty hack），可能只有在真正需要时才使用。也许过去 `FindResource()` 函数参数是 `SHORT` 类型，微软添加了在那里传递字符串的方法，但必须支持旧代码。

现在这里有一个简短的示例：

```c
#include <stdio.h>
#include <stdint.h>

void f(char *a) {
    if ((uint64_t)a > 0x10000) {
        printf("Pointer to string has been passed: %s\n", a);
    } else
        printf("16-bit value has been passed: %d\n", (uint64_t)a);
}

int main() {
    f("Hello!"); // 传递字符串
    f((char*)1234); // 16 位值
}
```

它可以工作！

如果你发现了拼写错误、错误或有任何建议，请随时留言：我的邮箱。谢谢！

## Linux 内核中的指针滥用

正如 Hacker News 中提到的，Linux 内核也有类似的东西。

例如，这个函数可以同时返回错误代码和指针：

```c
struct kernfs_node *kernfs_create_link(struct kernfs_node *parent,
                                 const char *name,
                                 struct kernfs_node *target)
{
    struct kernfs_node *kn;
    int error;

    kn = kernfs_new_node(parent, name, S_IFLNK|S_IRWXUGO, KERNFS_LINK);
    if (!kn)
        return ERR_PTR(-ENOMEM);
    if (kernfs_ns_enabled(parent))
        kn->symlink.target = target->ns;
    kn->symlink.target = target;
    kernfs_get(target); /* ref owned by symlink */
    error = kernfs_add_one(kn);
    if (error)
        return kn;
    kernfs_put(kn);
    return ERR_PTR(error);
}
```

这些函数必须始终记住，在解引用指针之前，必须始终使用 `IS_ERR_VALUE` 检查返回值。

例如：

```c
fman->cam_offset = fman_muram_alloc(fman->muram, fman->cam_size);
if (IS_ERR_VALUE(fman->cam_offset)) {
    dev_err(fman->dev, "%s: MURAM alloc for DMA CAM failed\n", func);
    return -ENOMEM;
}
```

(https://github.com/torvalds/linux/blob/aa00ed1287a693eadcbc67a3d73555d969b35d/drivers/net/ethernet/freescale/fman.c#L826)

## UNIX 用户态中的指针

`mmap()` 在出错时会失败（返回 `MAP_FAILED`，等于 -1）。有些人说，在少数情况下，`mmap()` 可以在零地址映射内存，因此不能使用 0 或 `NULL` 作为代码错误代码。

### 空指针

#### MS-DOS 时代的“空指针赋值”错误

老派读者会记得 MS-DOS 时代一个奇怪的错误信息：“Null pointer assignment（空指针赋值）”。这意味着什么？

在 *NIX 和 Windows 操作系统*中，向零地址写入内存是不可能的，但在 MS-DOS 中由于完全没有内存保护，这是可能的。

因此，我从 20 世纪 90 年代初取出的 Turbo C++ 3.0（后来更名为 Borland C++），并尝试编译这段代码：

```c
#include <stdio.h>

int main() {
    int *ptr = NULL;
    *ptr = 1234;
    printf("%s let's read at NULL\n", ptr);
    printf("%d\n", *ptr);
}
```

难以置信，但它确实有效，尽管会报错：

```
C:\TC30\BIN1
Now let's read at NULL
1234
Null pointer assignment
C:\TC30\>
```

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

让我们深入研究 Borland C++ 3.1 的 CRT 源代码，文件 `c0.asm`：

```asm
; _checknull check for null pointer z copyright message
...
; Check for null pointers before exit
__checknull    PROC    DIST
               PUBLIC  EQ      __checknull
IF             LDATA   EQ      false
IFNDEF         TINY
               push    si
               push    di
               mov     es, DGROUP@@
               mov     ax, ax
               mov     si, ax
               mov     cx, Lg_CopyRight
ComputeChecksum label
               add     al, es:[si]
               adc
               inc     si
               ComputeChecksum
               sub     ax, CheckSum
               jz      @SumOK
               mov     cx, Lg_NullCheck
               mov     dx, offset DGROUP:NullCheck
               call    @SumOK
@@SumOK ErrorDisplay
               pop     di
               pop     si
ENDIF
__DATA           SEGMENT
; 调试信息用于定位数据段的魔法符号
DATASEG@; 在不改变空指针检查逻辑的情况下，绝对不能移动或更改版权字符串
CopyRight      db      4(dup())
               db      'Borland C++ - Copyright 1991 Borland Intl.',0
lgthCopyRight equ      $ - CopyRight
IF             LDATA   EQ      false
IFNDEF         TINY
CheckSum       equ      00D5CH
NullCheck      db      'Null pointer assignment', 13, 10
lgthNullCheck equ      $ - NullCheck
ENDIF
ENDIF
```

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

MS-DOS 的内存模型非常奇怪（见第 1264 页的 11.7），除非你是复古计算机或复古游戏的粉丝，否则可能不值得研究。我们必须记住的一点是，MS-DOS 中的内存段（包括数据段）是存储代码或数据的内存段，但与“严肃”的操作系统不同，它从地址 0 开始。

在 Borland C++ CRT 中，数据段以 4 个零字节和版权字符串“Borland C++ - Copyright 1991 Borland int.”开始。在退出时会检查这 4 个字节和文本字符串的完整性，如果被损坏，则会显示错误信息。

但为什么呢？向空指针写入是 C/C++ 中的常见错误，如果你在 *NIX 或 Windows 上这样做，你的应用程序将会崩溃。MS-DOS 没有保护，因此 CRT 必须在事后和退出时进行检查。如果你看到这条消息，意味着你的程序在某个时刻写入了地址 0。

我们的程序确实做了，所以这个 1234 被正确读取了：因为它被写入了前 4 个零字节的位置。退出时校验不正确（因为数字被留在了那里），所以显示了错误信息。

等等，那个节点。（其他解决方案只会更糟）。也许，你可能处于某些疯狂的环境中，需要在零地址处分配内存块。你将如何指示下一个节点的缺失？某种魔法数字？也许是 -1？或者可能使用额外的比特位？

在维基百科中，我们可以找到这些内容：

> 事实上，与零页最初的优先使用相反，某些现代操作系统（如 FreeBSD、Linux 和 Microsoft Windows[2]）使得零页不可访问，以捕获空指针的使用。

(https://en.wikipedia.org/wiki/Zero_page)

## 空指针函数

通过地址调用函数是可能的。例如，我用 MSVC 2010 编译了这段代码并在 Windows 7 上运行它：

```c
#include <windows.h>
#include <stdio.h>

int main() {
    printf("%0x%x\n", &MessageBoxA);
}
```

结果是 `0x7578feae`，并且在运行几次后没有发生变化，因为 `user32.dll`（`MessageBoxA` 函数所在的位置）总是加载到相同的地址。此外，还因为没有启用 ASLR（在这种情况下，结果每次都会不同）。

让我们尝试通过该地址调用 `MessageBoxA()`：

```c
#include <windows.h>
#include <stdio.h>

typedef int (*msgboxtype)(HWND hWnd, LPCTSTR lText, LPCTSTR lCaption, UINT uType);

int main() {
    msgboxtype msgboxaddr = 0x7578feae;
    // 强制将 DLL 加载到进程内存，
    // 因为我们的代码没有使用 user32.dll 中的任何函数，
    // 且 DLL 未被导入
    LoadLibrary("user32.dll");
    msgboxaddr(NULL, "Hello, world!", "hello", MB_OK);
}
```
