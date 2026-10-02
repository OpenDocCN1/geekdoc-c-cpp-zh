
现在，如果我们实现的 `strlen()` 从地址 `0x008c1ff8` 开始一次性读取 16 字节，一直到 `0x008c2008`，那么就会抛出异常。当然，这种情况是需要避免的。

因此，我们只对对齐在 16 字节边界的地址进行操作，结合操作系统的页大小通常也对齐在 16 字节边界的知识，这为我们的函数不会从未分配的内存中读取提供了保证。

> 如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮件。谢谢！

让我们回到我们的函数。

`mmsetzero_si128()`——这是一个生成 `pxor xmm0, xmm0` 的宏——它只是清空 `XMM0` 寄存器。

`mmload_si128()`——是 `MOVDQA` 的宏，它只是从该地址加载 16 字节到 `XMM1` 寄存器中。

`mm_cmpeqb_ep18()`——是 `PCMEQB` 的宏，这是一条比较两个 `XMM` 寄存器的指令。

如果某个值等于另一个寄存器中的值，则结果中的该点为 `0xff`，否则为 `0`。

例如：

XMM1: 0x11223344556677888000000000000000

XMM0: 0x1ab32440078878811111111111111111

执行后，`XMM1` 寄存器包含：

XMM1: 0xff0000ff000ffff0000000000000000

在我们案例中，该指令将每个 16 字节块与一个 16 字节块进行比较，该块是通过 `pxor xmm0, xmm0` 设置在 `XMM0` 寄存器中的。

下一个关键是 `mm_movemask_ep18(1)`——即 `PMOVMSKB` 指令。

它与 `PCMEQB` 配合非常有用。

```
pmovmskb eax, xmm1
```

如果 `XMM1` 中第一个字节的最高位为 1，此指令会将 EAX 的第 1 位置1。换句话说，如果 `XMM1` 寄存器的第一个字节是 `0xff`，那么 `EAX` 的第一位也将设置为 1。

如果 `XMM1` 寄存器的第二个字节是 `0xff`，则 `EAX` 的第二位将设置为 1。换句话说，该指令回答问题“XMM1 中哪些字节的最高位大于 0x7f？”， 并在 `EAX` 中返回 16 位。`EAX` 中的其他位被清零。

顺便说，不要忘记我们算法的这个特性。输入中可能有 16 字节：

| 15 | 14 | 13 | 12 | 11 | 10 | 9 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|---|---|---|
| 'h' | 'e' | 'l' | 'l' | 'o' | | | | | | |

'hello' 字符串、终止零字节，以及一些随机噪声。如果我们将这 16 字节加载到 `XMM1` 并与清零的 `XMM0` 比较，我们将得到类似的结果：

```
XMM1: 0x0000ff0000000000ff000000
```

这意味着指令找到了两个零字节，这并不意外。

```
PMOVMSKB 在情况下会将 EAX 设置为 0b010000000010000
```

这里使用了从最高位 (MSB) 到最低位 (LSB) 的顺序。如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮件。谢谢！

显然，我们的函数必须只取第一个零并忽略其余。下一条指令是 `Bsf`。

```c
void s1 (
    DES_type a1,
    DES_type a2,
    DES_type a3,
    DES_type a4,
    DES_type a5,
    DES_type a6,
    DES_type *out1,
    DES_type *out2,
    DES_type *out3,
    DES_type *out4
) {
    DES x1, x2, x3, x4, x5, x6, x7, x8,
    x9, x10, x11, x12, x13, x14, x15, x16,
    x17, x18, x19, x20, x21, x22, x23, x24,
    x25, x26, x27, x28, x29, x30, x31, x32,
    x33, x34, x35, x36, x37, x38, x39, x40,
    x41, x42, x43, x44, x45, x46, x47, x48,
    x49, x50, x51, x52, x53, x54, x55, x56;

    x1 = a3 & -a5;
    x2 = x1 ^ -a4;
    x3 = a3 & -x4;
    x5 = a6 & x5;
    x6 = x2 ^ x4;
    x7 = a4 & -a5;
    x8 = x3 ^ a4;
    x9 = a6 & -x8;
    x10 = x7 ^ x9;
    x11 = a2 | x10;
    x12 = x6 ^ x11;
    x13 = a5 ^ x5;
    x14 = x13 & x8;
    x15 = a5 & -a4;
    x16 = x3 ^ x14;
    x17 = a6 | x16;
    x18 = x15 ^ x17;
    x19 = a2 | x18;
    x20 = x14 ^ x19;
    x21 = a1 & x20;
    x22 = x12 ^ -x21;
    *out2 = x1 | x5;
    x24 = x23 ^ x8;
    x25 = x18 & -x24;
    x26 = a2 & -x25;
    x27 = x24 ^ x26;
    x28 = x6 | x27;
    x29 = x28 ^ -x25;
    x30 = x9 ^ x24;
    x31 = x18 & -x30;
    x32 = a2 & x31;
    x33 = x29 ^ x32;
    x34 = a1 & x33;
    x35 = x27 ^ x34;
    *out4 = ~x35;
    x36 = a3 & x28;
    x37 = x18 & ~x36;
    x38 = a2 ^ x38;
    x39 = x37 ^ x38;
    x40 = a3 | x31;
    x41 = x24 & ~x37;
    x42 = x41 | x31;
    x43 = x42 & ~a2;
    x44 = x40 ^ x43;
    x45 = a1 & ~x44;
    *out1 = ~*out1 & ~x46;
    x47 = x33 & ~9;
    x48 = x47 ^ x39;
    x49 = x4 ^ x36;
    x50 = x49 & ~5;
    x51 = x45 & ~18;
    x52 = x51 | a5;
    x53 = a2 & ~x52;
    x54 = ~50 ^ a5;
    x55 = a1 | x54;
    x56 = x48 ^ ~55;
    *out3 = ~x56;
}
```

有很多局部变量。当然，并不是所有变量都进入了局部栈。让我们使用 MSVC 2008 /O2 选项进行编译：

# 列表 1.399: 优化后的 MSVC 2008

```asm
PUBLIC _s1
; 函数编译标志: /Otpy
TEXT SEGMENT
x65 = -20 : size = 4
x3s = -18 : Size = 4
x1$ = -12 : Size = 4
x8$ = -8 : Size = 4
x45 = -4 : Size = 4
a1$ = 8 : Size = 4
a2$ = 12 : Size = 4
a3$ = 16 : Size = 4
x33$ = 20 : Size = 4
x7s = -20 : Size = 4
a4$ = 20 : Size = 4
a5$ = 24 : Size = 4
x20$ = 28 : Size = 4
x36s = 28 : Size = 4
x28$ = 28 : Size = 4
a6$ = 28 : Size = 4
out1$ = 32 : Size = 4
x24$ = 36 : Size = 4
out2$ = 36 : Size = 4
out3$ = 40 : Size = 4
out4$ = 44 : Size = 4
s1 PROC
sub esp, 20
mov ebx, DWORD PTR a5$[esp+16]
push ebx
mov ebx, DWORD PTR a4$[esp+20]
push esi
mov ebx, DWORD PTR a3$[esp+28]
push edi
mov edi, DWORD PTR a1$[esp+32]
push e
mov ebx, DWORD PTR a2$[esp+32]
push ebp
push esi
mov DWORD PTR x3$[esp+36]
mov edi, DWORD PTR a3$[esp+32]
mov edi,mov PTR,movmov
,,2

mov,,

2

mov edi, DWORD PTR a2$[esp+32]
push ebp, DWORD PTR
mov,, PTR a1,esp+
2]
mov edi, DWORD PTR a1$[esp+32]
xor edi,,

, PTR PTR a1$[esp+32]
mov ebx, PTR
mov esp,, 2
```

（接上文）有32个有效位。但每当我使用指针时，它都消耗了我 64 位，并使我的数据结构大小增加了一倍。糟糕的是，它会进入缓存，导致我半数的缓存丢失，这非常耗钱——缓存是非常昂贵的。

所以我现在真的在尝试突破极限，我必须使用数组而不是指针。我编写了复杂的宏，使其看起来像是在使用指针，但实际上并没有。

（Donald Knuth 摘自《程序员工作实录：对编程技艺的反思》）

有些人会编写自己的内存分配器。了解 CryptoMiniSat¹⁷⁹ 的案例很有意思。这个程序很少使用超过 4GiB 的内存，但它大量使用了指针。因此，在 32 位架构上它需要的内存比 64 位架构上更少。为了解决这个问题，作者编写了自己的分配器（在 `classallocator.cpp` 文件中），它允许在 64 位指针中使用 32 位标识符来访问已分配的内存。

## 1.38 使用 SIMD 进行浮点数操作

当然，在添加 SIMD 扩展时，FPU 仍然保留在 x86 兼容处理器中。

SIMD 扩展（SSE2）提供了一种更简单的处理浮点数的方法。数值格式保持不变（IEEE 754）。

因此，现代编译器（包括为 x86-64 生成代码）通常使用 SIMD 指令而不是 FPU 单元。

可以说，使用这些指令操作起来更简单。我们将复用 FPU 部分的示例：第 275 页的示例 1.25。

### 1.38.1 简单示例

```c
#include <stdio.h>

double f (double a, double b)
{
    return a/3.14 + b*4.1;
}

int main()
{
    printf("%f\n", f(1.2, 3.4));
}
```

¹⁷⁹https://github.com/msoos/cryptominis/

如果你发现任何拼写错误、错误或有任何建议，请随时给我留言：我的邮箱。谢谢！

## 列表 1.400: 优化 MSVC 2012 x64

```assembly
real@4010066666666666r DQ 04010066666666666r : 4.1
real@40091eb851eb851f DQ 040091eb851eb85fr : 3.14
a = 8
b = 16
PROC
    divsd xmm0, QWORD PTR  real@40091eb851eb851f
    mulsd xmm1, QWORD PTR  real@40100666666666666
    addsd xmm0, xmm1
    ret
0
ENDP
```
