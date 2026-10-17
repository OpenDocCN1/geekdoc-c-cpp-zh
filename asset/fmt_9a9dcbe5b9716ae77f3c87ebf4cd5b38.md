
## 1.16 指针

### 1.16.1 返回值

指针经常用于从函数返回值（回想 `scf()` (第 87 页 1.12)）。

例如，当一个函数需要返回两个值时。

#### 全局变量示例

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：[我的电子邮箱]。谢谢！

### 列表 1.103: 优化 MSVC2010 (/Ob0)

```asm
COMM    product:DWORD
COMM    sum:DWORD
$SG2803 DB  'sum=%d, product=%d', 0aH, 00H

_x = 8          ; size = 4
_y = 12         ; size = 4
_sums = 16      ; size = 4
_product = 20   ; size = 4
f1      PROC
        mov     ecx, DWORD PTR y$[esp-4]
        mov     eax, DWORD PTR x$[esp-4]
        lea     edx, DWORD PTR [eax+ecx]
        imul    ecx, eax
        mov     ecx, DWORD PTR _product$[esp-4]
        push    esi
        mov     esi, DWORD PTR _sum$[esp]
        mov     DWORD PTR [esi], edx
        mov     DWORD PTR [ecx], eax
        pop     esi
        ret
        0
f1      ENDP

main    PROC
        push    OFFSET _product
        push    OFFSET _sum
        push    456             ; 000001C8
        push    123             ; 0000007B
        push    f1
        call    eax, DWORD PTR _product
        mov     eax, DWORD PTR _sum
        push
        eax
        push
        ecx
        push
        push    OFFSET $SG2803
        call    DWORD PTR _imp_printf
        add     esp, 28
        xor     eax, eax
        ret
        0
main    ENDP
```

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：[我的电子邮箱]。谢谢！

让我们在 OllyDbg 中查看这个：

#### CPU - 主线程，模块全局变量

![](img/4590a0c34d3b5b6ca77b4202d4036d48_163_0.png)

图 1.24: OllyDbg: 全局变量被传递给 f1()

首先，全局变量被传递给 f1()。我们可以点击“跟随至 (Follow in)”来查看栈中的 f1()。

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：[我的电子邮箱]。谢谢！

f1() 开始。到目前，栈 `0x2EF854` 和 `0x2EF858` 处只有垃圾数据：

![](img/4590a0c34d3b5b6ca77b4202d4036d48_170_0.png)

如果你发现拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

#### f1() 完成：

151

![](img/4590a0c34d3b5b6ca77b4202d4036d48_171_0.png)

图 1.31: OllyDbg: f1() 完成执行

我们在地址 `0x2EF854` 和 `0x2EF858` 处发现了 `0xDB18` 和 `0x243`。这些值就是结果：

#### 结论

f1() 可以返回内存中任何位置的指针，位于任何地方。

这本质上就是指针的有用之处。

顺便提一下，C++ 用的的工作方式完全相同。阅读更多关于它们的内容：第 705 页 (3.21)。

### 1.16.2 交换输入值

这将完成工作：

```c
#include <memory.h>
#include <stdio.h>

void swap_bytes(unsigned char* first, unsigned char* second) {
    unsigned char tmp1;
    unsigned char tmp2;

    tmp1=first;
    tmp2=second;

    *first=tmp2;
```

如果你发现拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

152

```c
*second=tmp;

int main() {
    // 将字符串拷贝到堆，这样我们就可以修改它
    char *s=strdup("string");
    // 交换第 2 和第 3 个字符
    swap_bytes(s+1, s+2);
    printf("%s\n", s);
}
```

我们可以看到，字节通过 `MOVZX` 加载到 `ECX` 和 `EBX` 的低 8 位（因此这些寄存器的高位将被清零），然后交换写入字节。

### 列表 1.106: 优化 GCC 5.4

| | |
|---|---|
| push | ebx |
| mov | DWORD PTR [esp8] |
| mov | DWORD PTR [esp+12] |
| movzx | ecx, BYTE PTR [edx] |
| movzx | ebx, BYTE PTR [eax] |
| mov | BYTE PTR [idx], bl |
| mov | BYTE PTR [idx], cl |
| pop | ebx |
| ret | |

两个字节的地址都是从参数获取的，并在函数执行过程中位于 `EDX` 和 `EBX` 中。

所以我们使用了指针；没有指针，没有更好的方法完成这项任务。

## 1.17 GOTO 操作符

GOTO 操作符通常被认为是反模式，参见 [Edgar Dijkstra, Statement Considered Harmful (1968)]89。尽管如此，它可以被合理使用，参见 [Donald E. Knuth, Structured Programming with go to Statements (1974)]90 91。

这里有一个简单的例子：

```c
#include <stdio.h>

int main() {
    printf("begin\n");
}
```

> 89 http://yuriche.com/mirrors/Dijkstra68.pdf
> 90 http://yuriche.com/mirrors/KnuthStructuredProgrammingGoTo.pdf
> 91 [Dennis Yuriche, C++ programming language notes] 也有一些示例。

如果你发现拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

```c
goto exit:

printf("skip me!\n");

printf("end\n");
```

这是我们在 MSVC 2012 中得到的：

### 列表 1.107: MSVC 2012

```asm
$5G2934 DB      'begin', 0AH, 00H
$5G2936 DB      'skip me!', 0AH, 00H
$5G2937 DB      'end', 0AH, 00H

main   PROC
       push      ebp
       mov       ebp, esp
       push
       call      OFFSET $5G2934 ; 'begin'
       add       esp, 4
       call      .printf
       jmp       SHORT exit3
       push
       call      OFFSET $5G2936 ; 'skip me!'
       call      .printf
       add       esp, 4
$exit3:
       push      OFFSET $5G2937 ; 'end'
       call      .printf
       add       esp, 4
       xor       eax, eax
       pop       ebp
       ret
main   ENDP
```

`goto` 语句被简单替换为 `JMP` 指令，其效果相同：无条件跳转到另一个地方。第二个 `printf()` 只有通过人工干预（使用调试器或补丁代码）才能执行。

如果你发现拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

这也可以作为简单的补丁非常有用。让我们在 Hiew 中打开生成的执行文件：

```
Hiew: goto.exe
C:\goto.exe             F                 a32 PE
00401000: 5B               push           ebp
00401001: 8BC               mov             esp
00401003: 68000400      push           00;'begin'
00401008: FF15020400call            printf
0040100E: 83C404         add             esp,4
00401011: E800000      call            printf;'skip me!'--E3
00401015: FF15020400call            printf
00401018: 5B               push           ebp
0040101E: 83C404         add             esp,4
00401021: 68000400      push           0031--E4
00401027: 25               call            printf
0040102C: 83C404         add             esp,4
0040102F: 3C              xor             eax,eax
00401031: 5D               pop             ebp
00401032: C3
```

图 32: Hiew

将光标置于 `JMP` (0x410)，按两次 F3 (编辑)，操作码变为 `EB:00`：

![](img/4590a0c34d3b5b6ca77b4202d4036d48_175_0.png)

图 33: Hiew

`JMP` 的第二个字节表示跳转的相对量，`00` 表示当前指令之后。

现在 `JMP` 跳过了第二个 `printf()` 调用。

按 F9 (保存) 并编辑。如果我们运行执行文件将会看到：

### 列表 08: 补丁执行文件

| | |
|---|---|
| C:\goto.exe | |
| begin | |
| skip me! | |
| end | |

通过 2 个 `NOP` 指令替换 `JMP` 指令可以实现相同的结果。

`NOP` 的操作码为 `0x90`，长度为 1 字节，所以我们需要 2 个指令作为 `JMP`（大小为 2 字节）。

#### 1.17.1 死代码

第二个 `printf()` 调用在编译器术语中被称为“死代码”。

这意味着代码永远不会执行。当你使用优化编译它时，编译器会移除“死代码”，不留痕迹：

如果你发现拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

### 列表 109: 优化 MSVC 2012

| | |
|---|---|
| $5G2981 DB | 'begin', 0AH, 00H |
| $5G2983 DB | 'skip me!', 0AH, 00H |
| $5G2984 DB | 'end', 0AH, 00H |

```asm
main
    push    OFFSET $5G2981 ; 'begin'
    call    printf
    push    OFFSET $5G2984 ; 'end'
$exit4:
    call    .printf
    add     esp, 8
    xor     eax, eax
    ret
main
ENDP
```

然而，编译器忘记移除 "skip me!" 字符串。

#### 1.17.2 练习

尝试使用你喜欢的编译器和调试器实现相同的结果。

## 1.18 条件跳转

### 1.18.1 简单示例 <stdio.h>

```c
#include <stdio.h>

void f_signed(int a, int b)
{
    if (a>b)
        printf("a>b\n");
    if (a==b)
        printf("a==b\n");
    if (a<b)
        printf("a<b\n");
}

void f_unsigned(unsigned int a, unsigned b)
{
    if (a>b)
        printf("a>b\n");
    if (a==b)
        printf("a==b\n");
    if (a<b)
        printf("a<b\n");
}

int main()
{
```

```c
f_signed(1, 2);
f_unsigned(1, 2);
return 0;
}
```

如果你发现拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

### x86

### x86 + MSVC

这里是 `f_signed()` 函数的样式：

#### 列表 1.110: 未优化的 MSVC 2012

```asm
a$ = 8
b$ = 12
f_signed PROC
       push      ebp
       mov       ebp, esp
       mov       eax, DWORD PTR a+[ebp]
       cmp       eax, DWORD PTR b+[ebp]
       jle       SHORT exit3 ; 'a'-'b'
       push      esp
       call      .printf
       add       esp, 4
$LN3f_signed:
       mov       ecx, DWORD PTR a+[ebp]
       cmp       ecx, DWORD PTR b+[ebp]
       jne       SHORT LN4f_signed ; 'a'<b'
       push      OFFSET $5G739
       call      .printf
       add       esp, 4
$LN2f_signed:
       mov       edx, DWORD PTR a+[ebp]
       mov       edx, DWORD PTR b+[ebp]
       jge       SHORT $5G741 ; 'a'<b
       push      OFFSET $5G741
       call      .printf
       add       esp, 4
$LN4f_signed:
       xor       eax, eax
       pop       ebp
       ret
f_signed ENDP
```

无论如何，所有的 `printf()` 调用都不会执行。在没有特殊干预的情况下，这是可能的。现在让我们来看 `f_unsigned()` 函数。`f_unsigned()` 函数与 `f_signed` 相同，不同之处在于使用了 `JBE` 和 `JAE` 指令代替了 `JGE` 和 `JGE`，如下：

### 列表 1.111: GCC
