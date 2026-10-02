
很奇怪，但在 Windows 7 x86 上可以运行。

这在 shellcode 中很常见，因为很难从那里通过名称调用 DLL 函数。而 ASLR 是一项防御措施。

现在现实情况可能很奇怪，一些嵌入式 C 程序员可能熟悉这样的代码：

```c
int reset() {
  void (*foo)(void) = 0;
  foo();
}
```

谁会想调用地址 0 的函数呢？这是一个跳转到零地址的可移植方法。低成本微控制器也没有内存保护或 MMU，在重置后，它们从地址 0 开始执行代码，那里存储着某种初始化代码。跳转到地址 0 是一种自重置的方法。可以使用内联汇编，但如果不可用，可以使用这种可移植方法。

它在我 Linux x64 上的 GCC 4.8.4 上也能正确编译：

```assembly
reset:
  sub rsp, 8
  xor eax, eax
  call rax
  add rsp, 8
  ret
```

栈指针偏移并不是问题：微控制器中的初始化代码完全忽略寄存器和 RAM 状态，并从头开始启动。

当然，这在 *NIX 或 Windows 上会崩溃，因为有内存保护，即使在没有保护的情况下，地址 0 也没有代码。

GCC 有非标准扩展，允许跳转到特定地址而不是在该处调用函数：http://gcc.gnu.org/onlinedocs/gcc/Labels-as-Values.html。

> 39 地址空间布局随机化

如果你发现了拼写错误、错误或有任何建议，请随时给我发邮件：我的邮箱。谢谢！

## 3.2.5 作为函数参数的数组

有人可能会问，将函数参数类型声明为数组和指针有什么区别？似乎它们完全没有区别：

```c
void write_something1(int a[16]) {
  a[5]=0;
}

void write_something2(int *a) {
  a[5]=0;
}

int f() {
  int a[16];
  write_something1(a);
  write_something2(a);
}
```

GCC 4.8.4 优化：

```assembly
write_something1:
  mov DWORD PTR [rdi+20], 0
  ret

write_something2:
  mov DWORD PTR [rdi+20], 0
  ret
```

如果你发现了拼写错误、错误或有任何建议，请随时给我发邮件：我的邮箱。谢谢！

## 774

但如果数组的大小总是固定的，你仍然可以为了自文档化目的声明数组而不是指针。也许，某些静态分析工具可以警告你溢出。或者使用某些工具是可能的吗？

包括 Lin Torvalds 在内的人批评这种 C/C++ 特性：https://lkml.org/2015/9/428。

C99 标准（ISO/IEC 9899）也规定：
> 如果 static 关键字也出现在数组类型推导中，那么对于每次函数调用，相应的实际值应访问数组中至少数量的元素。

## 3.2.36 指向函数

C/C++ 中没有括号的函数名（如 `printf`）是指向函数的指针。让我们尝试读取函数的内容并修补它：

```c
#include <memory.h>
#include <stdio.h>

void print_something() {
    printf("we are %s\n", "s");
}

int main() {
    print_something();
    printf("first 3 bytes: %x %x %x...\n",
        *(unsigned char*)print_something,
        *(unsigned char*)print_something+1,
        *(unsigned char*)print_something+2);
    *(unsigned char*)print_something=0xC3; // RET 指令
    printf("going to call patched_something():\n");
    print_something();
    printf("it must exit at this point\n");
}
```

事实说明前三个字节是 55 e5（确实，这些操作是 PUSH EBP 和 MOV EBP, ESP）。但我们的程序会崩溃，因为段是只读的。重数我们的示例并使段可写：http://stackoverflow.com/questions/27581279/make-text-writable ![](img/4590ac34db5c6774d03d48.png)

如果你发现了拼写错误、错误或有任何建议，请随时给我发邮件：我的邮箱。谢谢！

```bash
gcc --static -g -W0 -o example.c
```

成功了！

```
we are in print_something()
first 3 bytes: 55 89 e5...
going to call patched_something():
it must exit at this point
```

## 3.2.7 指向函数：复制保护

软件破解可以找到一个返回真或假的保护函数。然后他将其 XOR EAX / MOV EAX, 1。你可以检查函数的完整性吗？结果证明，你可以这样做。根据 objdump，`check_protection()` 的前三个字节是 0x55 0x89 0xE5（考虑到这是非优化的）：

```c
#include <stdlib.h>
#include <stdio.h>

int check_protection() {
    // 做一些事情
    return 0;
    // return 1;
}

int main() {
    if (check_protection()) {
        printf("no protection installed\n");
        exit(0);
    }

    // ...这里有一个关键点...
    if ((*unsigned char*)check_protection)+0 != 0x55) {
        printf("1st byte has been altered\n");
        // 做一些事情，添加水印，等
    }

    if ((unsigned char*)check_protection)+1 != 0x89) {
        printf("2nd byte has been altered\n");
        // 做一些事情，添加水印，等
    }

    if ((*unsigned char*)check_protection)+2 != 0xe5) {
        printf("3rd byte has been altered\n");
        // 做一些事情，添加水印，等
    }
}
```

如果你发现了拼写错误、错误或有任何建议，请随时给我发邮件：我的邮箱。谢谢！

```assembly
0000054d <check_protection>:
  54d:   55                      push   %ebp
  54e:   89 e5                   mov    %esp,%ebp
  550:   e8 b7 07 00 00          call   60c <_x86_get_pc_thunk>
  555:   05 7f 1a 00 00          add    $1a7f,%eax
  55a:   b8 00 00 00 00          mov    $0,%eax
  55f:   5d                      pop    %ebp
  560:   c3                      ret
```

如果有人修补了 `check_function()` 的开头，你的程序可能会执行某些操作，也许突然退出。为了找到这种技巧，破解者可以在函数起始地址处设置内存断点（跟踪器有 BPMX 选项）。

## 3.2.8 指向函数：常见错误（或拼写错误）

一个臭名昭彰的错误：

```c
int expired() {
    // 检查许可证密钥、当前日期/时间等
}

int main() {
    if (expired) // 必须已过期
    {
        printf("expired\n");
        exit(0);
    } else {
        // 做一些事情
    }
}
```

由于仅仅通过函数名就会被解释为指针，`if (expired)` 必须为真。

## 3.2.9 作为对象标识符的指针

汇编语言和 C 没有 OOP 特性，但可以用 OOP 风格编写代码（将结构体视为对象）。有趣的是，有时指向对象（或其地址）被称为 ID（隐藏/封装意义）。

如果你发现了拼写错误、错误或有任何建议，请随时给我发邮件：我的邮箱。谢谢！

例如，`sqliteLibrary.LoadLibrary()` 根据 MSDN 返回“模块的句柄”。然后你将此“句柄”传递给 `GetProcAddress()` 等函数。但事实上，`LoadLibrary()` 返回的是映射到内存中的 DLL 指针。你可以读取 `LoadLibrary()` 返回的两个字节，它们是 "MZ"（Windows 任何 .EXE/.DLL 文件的两个字节）。显然，微软隐藏了这个事实以提供更好的兼容性。此外，`HMODULE` 和 `HINSTANCE` 在 16 位 Windows 中有另一种含义。

也许这就是为什么 `printf()` 有 `%p` 修饰符，它用于指针（32 位整数，64 位）的十六进制格式。结构化转储有助于在其他地方找到它。

这里是 SQLite 源码：

```c
struct Pager {
  sql3_vfs *vfs;      /* 用于 IO 的 OS 函数 */
  u8 exclusive;      /* 布尔值。如果 locking==EXCLUSIVE 则为真 */
  /* */
  u8 journalMode;     /* PAGER_JOURMODE 值之一 */
  u8 journal;       /* 在此文件上使用回滚日志 */
  u8 sync;           /* 如果为真不同同步日志 */
};

static int pagerLockDb(Pager *pPager, int elock) {
  int rc = SQLITE_OK;
  assert(elock==SHARED_LOCK || elock==RESERVED_LOCK || elock==
    EXCLUSIVE_LOCK);
  if (pPager->elock || pPager->elock==UNKNOWN_LOCK) {
    rc = sqlite3_oslock(pPager->fd, elock);
    if (rc==SQLITE_OK && pPager->elock!=UNKNOWN_LOCK && elock==
      EXCLUSIVE_LOCK) {
      pager->Lock = (u8)elock;
      OTRACE("Lock %s\n", pPager, elock);
    }
  }
  return rc;
}
```

## 3.23.10 Oracle RDBMS 和用于 C/C++ 的简单垃圾回收器

曾有段时间，这些文字的作者试图更多地了解 Oracle RDBMS，寻找漏洞等。这是一个巨大的软件，一个典型的函数可能会接收非常大的节点作为参数。我想要转储这些对象、树（或图）。

此外，我通过拦截内存分配/释放函数，跟踪了所有的内存分配/释放。当被拦截的函数获取内存块的指针时，我会在已分配的内存块列表中搜索该块。在 Windows 操作系统内核^{44} 中，我获取了该块的大小和短名称（例如“tagging”）。

给定一个内存块，我可以对其扫描 32 位的字（在 32 位操作系统上）或 64 位的字（在 64 位操作系统上）。每个字都可能是指向另一个块的指针。如果是如此（如果我在内存中找到了另一个），我就可以递归遍历。

并且，使用 GraphViz，我可以渲染出这样的图表：

```
cmd(dtcfvekallocLoadChild, size [480]
+0000: 0x04 0x00 0x00 0x00
+0004: 0x18 0x00 0x00 0x00
+0008: 0x1C 0x00 0x00 0x00
+000C: 0x00 0x00 0x00 0x00
+0010: 0x04 0x00 0x00 0x04
+0014: 0x1B 0x02 0x02 0x1A
+001C: 11C pr to [qscxt-kkmkgmc]
+0020: 13C pr to [kalloc-kscoc]
+0024: 21C pr to [qscxt-kkmkgmc]
+0028: 0x09 0x0B 0x0A 0x05
+002C: 34C pr to [qscxt-kkmkgmc]
+0030: 38C pr to [qscpath,qscaddSysPath]
```

```
cmd(qscxt, kkmkgmc, size [09]
+0004: pr to [qscxt, k
+0008: 0x02 0x00 0x00 0x00
+000C: 0x0C 0x50 0x05 0x00
```

```
cmd(qscxt, kkmkgmc, size [44]
+0004: 0x4A 0x02 0x0E
+0008: 0x3B pr to [qscxt, k
+000C: pr to [qscpath, k
```

```
cmd(kalloc-kscoc, size [28]
+0004: 0x01 0x13 0x00 0x00
+0008: 0x0D 0x01 0x00 0x00
+000C: 0x06 0x01 0x00 0x00
+0010: 0x05 0x0D 0x00 0x00
```

```
cmd(qscxt, kkmkgmc, size [22]
+0004: 0x24(1) 0x65 0xB2F
+0008: pr to [Typecheck h
```

```
cmd(qscpath, qscaddSys
+0000: pr to [qscpath, qcc
```

> 关于分配内存块中的注释：Dennis Yurichev, C/++ 语言笔记 http://yuriche.com/C-book.html。

如果你发现任何拼写错误、错误或有建议，请随时来邮件：我的邮箱！

### 更大的图片：1, 2.

这令人印象深刻，考虑到我并没有关于所有结构的信息。但我可以从中获取一些信息。

### 现在是用于 C/C++ 的垃圾回收器

如果你使用在内存中分配的块，它的地址必须在某个地方，作为另一个块中的指针、全局分配或局部变量。如果没有指向该块的指针，你可以称之为“孤立（orphan）”，这将导致内存泄漏。以及垃圾回收器（GC）做了什么（因为它保留了对所有分配内存的引用）。重要的是记住，它并不知道块中所有这些结构的类型——它只是扫描 32 位或 64 位的字，如果它们是指向另一个块的指针。它将块视为字数组，这些字可能是指针。如果你发现一个“孤立”的块，即该块无法被释放。此外，像 Boehm GC 一样（使用它，声明分配的块永远不会包含指向其他块的指针）。这可能是文本字符串或其他类型的数据。

### 循环优化

这是最简单的 `memcopy` 实现：

```c
void memcopy(unsigned char* dst, unsigned char* src, size_t cnt) {
    size_t i;
    for (i=0; i<cnt; i++)
        dst[i]=src[i];
}
```

至少从 1990 年代的 MSVC 6.0 到 MSVC 2013 可以产生非常奇怪的代码（这是由 MSVC 2013 x86 生成的）：

```
dst$ = 4
src$ = 12      ; size = 4
cnt$ = 16      ; size = 4

memcopy PROC
  mov edx, DWORD PTR cnt$[esp-4]
  test edx, edx
  je SHORT LN1@f
  mov eax, DWORD PTR _src[esp]
  sub esi, eax
  ; esi=src-dst, 即，指针

LL0@f:
  mov cl, BYTE PTR [esi+eax]
  mov BYTE PTR [eax], cl
  lea edx, DWORD PTR [eax+1] ; dst++
  dec edx
  jne SHORT LL0@f
  ; 减少计数直到结束
```

> 45 垃圾回收 https://www.boehm.info/gc/

如果你发现任何拼写错误、错误或有建议，请随时来邮件：我的邮箱！
