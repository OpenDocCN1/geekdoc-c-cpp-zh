
## ARM + 优化的 Keil (ARM 模式)

```asm
.text:000028C 03 7B LDRB R3, [R0#12] ; c
.text:000028E 01 79 LDRB R1, [R0#4] ; a
.text:0000290 59 A0 ADR R0, aADBDCDDD ; "a=%d; b=%d;"
.text:00000292 05 F0 AD FF BL 2printf
.text:00000296 02 E6 exit
```

正如我们所回忆的，这里传递的是一个结构体而不是一个，一旦 ARM 中的前 4 次函数调用通过寄存器传递，结构体的字段将通过 `R0–3` 传递。

`LDR` 通过内存加载一个字节并将其扩展为 32 位，同时考虑了其符号位。这在这里被用于从结构体中加载字段 `$a$` 和 `$c$`。

我们很容易发现的另一点是，这里没有函数尾部（epilogue），而是跳转到了另一个函数的尾部！确实，有一个完全不同的函数，与我们的函数毫无关系，但它具有完全相同的尾部（可能因为它也持有 5 个局部变量 (`sp = 4 + r1`)）。

它也位于附近（看一眼地址）。
事实上，执行哪一个尾部并不重要，只要它能按照我们需要的方式工作。
显然，Keil 决定重用另一个函数的部分内容以节省空间。
尾部通过跳转消耗了 4 字节—2。

## ARM + 优化的 Xcode 4.6.3 (LLVM) (Thumb-2 模式)

列表 1351：优化的 Xcode 4.6.3 (LLVM) (Thumb-2 模式)

```asm
var_C = -03xC

PUSH {R7,LR}

MOV  R7, SP

SUB  SP, SP, #4

MOV  R9, R1 ; b

MOV  R1, R0

MOVW R0, #0F10 ; "a=%d; b=%d; c=%d; d=%d\n"

STXB R0, R0

MOVT.w R0, #0

STR  R3, [SP#0xC+var_C] ; place d to stack for printf(\

ADD  R0, R0 ; format-string

STXB R3, R2 ; prepare c

MOV  R2, R9 ; b

BLX  printf

ADD  SP, SP, #4

POP  {R7,PC}
```

`SXTB`（有符号扩展字节）类似于 x86 中的 `MOVSX`。其余部分完全相同。

如果你发现了拼写错误、错误或有任何建议，请随时给我的邮件留言：我的邮箱。谢谢！

## MIPS

### 列表 1.352：优化的 Gcc 4.4.5 (IDA)

```asm
1 f:

2

3 var_10      = -0x18

4 var_10      = -0x10

5 var_4       = -4

6 arg_0       = 0

7 arg_4       = 4

8 arg_0       = 8

9 arg_c       = 0xC

10

11 $a0=s.a.

12 $a1=s.b.

13 $a2=s.c.

14 $a3=s.d.

15

16 lui       $gp, (gnu_local_gp >> 16)

17 addiu      $sp, -0x28

18 la        $gp, (gnu_local_gp & 0FFFF)

19 sra        $ra, 0x28+var_4($sp)

20 sw         $0x28-var_10($sp)

21 ; prepare a byte from 32-bit big-endian integer:

22 sra         $t0, $a0, 24

23 move       $v1, $a1

24 ; prepare a byte from 32-bit big-endian integer:

25 sra         $v0, $a2, 24

26 lw         $19, printf(&0FFFF)($sp)

27 $a0, 0x28+arg($sp), a="%d; b=%d; c=%d; d=%d\n"

28 lui       $a0, ($L0c < 16)

29 sw         $a3, 0x20-var_8($sp)

30 sw         $a1, 0x28+arg_4($sp)

31 sw         $a2, 0x28+arg_8($sp)

32 sw         $a3, 0x28+arg_c($sp)

33 $a0, ($L0c & 0xFFFF) # " "ascii=%d; b=%d; c=%d; d=%d\n"

34 la        $t1, $t0

35 move       $a2, $a1

36 jl         $a3 ; branch delay slot

37 lw         $a3, 0x28+var_4($sp)

38 or        $at, $zero ; load delay slot, nop

39 jr        $ra

40 addiu      $sp, 0x28
```

```c
printf("processor type=%d\n", tmp->processor_type);

printf("extended_model_id=%d\n", tmp->extended_model_id);

printf("extended_family_id=%d\n", tmp->extended_family_id);

return 0;

}
```

在 `CPUID` 填充 `EAX/EBX/ECX/EDX` 后，这些寄存器将被写入 `b[]` 数组。然后，我们有一个指向 `CPUID_1_EAX` 结构的指针，将其指向 `b[]` 数组中的 `EAX` 值。

换句话说，我们将一个 32 位整数视为一个结构体。然后从结构体中读取特定的位。

## MSVC

让我们在 MSVC 2008 中带 `/0x` 选项进行编译：

> 列表 1.354: 优化化的 MSVC 2008

```asm
b$ = -16 ; size = 16

main    PROC

    sub     esp, 16

    push    ebx

    xor     ecx, ecx

    mov     eax, 1

    cpuid

    push    esi

    lea     esi, DWORD PTR b$[esp+24]

    mov     DWORD PTR [esi], eax

    mov     DWORD PTR [esi+4], ebx

    mov     DWORD PTR [esi+8], ecx

    mov     DWORD PTR [esi+12], edx

    mov     esi, DWORD PTR b$[esp+24]

    mov     ecx, esi

    and     ecx, 15

    push    eax

    push    OFFSET $SG51435 ; 'stepping=%d', 0AH,00H

    call    _printf

    mov     ecx, esi

    shr     ecx, 4

    and     ecx, 15

    push    ecx

    push    OFFSET $SG51435 ; 'model=%d', 0AH,00H

    call    _printf

    mov     edx, esi

    shr     edx, 8

    and     edx, 15

    push    edx

    push    OFFSET $SG15437 ; 'family_id=%d', 0AH, 00H

    call    _printf

    mov     eax, esi

    shr     eax, 12

    and     eax, 3

    push    eax

    push    OFFSET $SG15438 ; 'processor_type=%d', 0AH, 00H

    call    _printf

    mov     ecx, esi

    shr     ecx, 15

    push    ecx

    push    ecx

    push    OFFSET $SG15439 ; 'extended_model_id=%d', 0AH, 00H

    call    _printf

    shr     esi, 20

    and     esi, 255

    push    esi

    push    OFFSET $SG15440 ; 'extended_family_id=%d', 0AH, 00H

    call    _printf

    add     esp, 48

    pop     esi

    xor     eax, eax

    pop     ebx

    add     esp, 16

    ret

main  ENDP
```

`SHR` 指令通过必须跳过的位数的来移位 `EAX` 中的值，例如，我们忽略了*右侧的*某些位。

`AND` 指令清除*左侧*不必要的位，换句话说，只保留 `EAX` 寄存器中我们需要的那些位。

# MSVC - OllyDbg

让我们将示例加载到 OllyDbg 中，查看在执行 `CPUID` 后 `EAX/EBX/ECX/EDX` 中设置了什么值。

![](img/4590a0c34d3b5b6ca77b420d4036d_487_0.png)

图 108: OllyDbg: CPUID 执行

`EAX` 为 `0x00002067000000001010100111` 的二进制形式。位按字段分布如下：

| field 字段 | binary form 二进制形式 | decimal form 十进制 |
|---|---|---|
| reserved | 0000 | 0 |
| extended_family_id | 00000000 | 0 |
| extended_model_id | 0010 | 2 |
| reserved | 0 | 0 |
| processor_id | 00 | 0 |
| family_id | 0110 | 6 |
| model | 1010 | 10 |
| stepping | 0111 | 7 |

列表 355: 控制台输出

```
stepping=7

model=10

family=6

processor_type=0

extended_model_id=2

extended_family_id=0
```

## GCC

让我们尝试带 `-03` 选项的 GCC 4.4.1。

列表 356: 优化化的 GCC 4.4.1

```asm
main    proc near ; XREF: start+17

push    ebp;

mov     ebp, esp

and     esp, 0FFF0h

push    esi

mov     esi, 1

push    ebx

mov     eax, esi

sub     esp, 18h

cpuid

mov     esi, eax

and     eax, 0F

mov     [esp+8], eax

mov     dword ptr [esp+4], offset aStepping ; "stepping=%d\n"

mov     [esp], 1

call   _printf

mov     eax, esi

shr     eax, 4

and     eax, 0F

mov     [esp+8], eax

mov     dword ptr [esp+4], offset aModel ; "model=%d\n"

mov     [esp], 1

call   _printf

mov     eax, esi

shr     eax, 8

and     eax, 0F

mov     [esp+8], eax

mov     dword ptr [esp+4], offset aFamilyID ; "family_id=%d\n"

mov     [esp], 1

call   _printf

mov     eax, esi

shr     eax, 10h

shr     eax, 14h

and     eax, 0F

mov     esi, FFh

mov     [esp+8], eax

mov     dword ptr [esp+4], offset aType ; "processor_type=%d\n"

mov     [esp], 1

call   _printf

mov     eax, esi

mov     dword ptr [esp+4], offset aExtended ; "extended_model_id=%d\n"

mov     [esp], 1

call   _printf

mov     [esp+8], esi

mov     dword ptr [esp+4], offset unk804d

mov     [esp], 1

call   _printf

add     esp, 18h

xor     eax, eax

pop     ebx

pop     esi

mov     esp, ebp

ret

main end
```

# 处理 float 类型

```c
#include <stdio.h>
#include <assert.h>
#include <stdlib.h>
#include <memory.h>

struct float_as_struct {
    unsigned int fraction = 23;
    unsigned int exponent = 8;
    unsigned int sign = 1;
};

float f(float in) {
    float in;
    struct float_as_struct t;
    assert(sizeof(struct float_as_struct) == sizeof(float));
    memcpy(&t, &in, sizeof(float));
    t.sign = 1; // 设置负号
    t.exponent = t.exponent + 2; // 乘以 2^n (这里 n 是 2)
    return f;
}

int main() {
    printf("%f\n", f(1.23));
}
```

`float_struct` 占用的内存量与 `float` 相同，即 4 字节或 32 位。现在我们也在输入值中设置了负号，通过给指数加 2，我们使整个数字乘以 $2^2$，即 4。

# 列表 1.357: 未优化的 MSVC 2008

```asm
tS = -8; size = 4

fs = -4; size = 4

inS = 8; size = 4

?@@YAM@Z PROC f

push
    ebp

mov    ebp, esp

sub    esp, 8

fld     WORD PTR inS[ebp]

fstp    WORD PTR _f[ebp]

push    4

lea     eax, DWORD PTR _t[ebp]

push    eax

lea     ecx, DWORD PTR _t[ebp]

push    ebx

push    ecx

call    memcpy

add     esp, 12

mov     edx, DWORD PTR _t[ebp]

or     edx, -2147483648 ; 0x8000000 - 设置负号

mov     dword ptr _t[ebp], edx

shr    eax, 23 ; 0x00017H - 丢掉小数部分

and     eax, 255 ; 只保留指数

add     eax, 2 ; 给它加 2

and     eax, 255 ; 0x000FFH

shl    eax, 23 ; 0x00H - 将结果移到 30:23 位

mov     ecx, DWORD PTR _t[ebp]

and     ecx, -213905041 ; 0xFFFFFF - 丢掉指数

; 带新指数的原始值：

or     ecx, eax

mov     dword ptr _t[ebp], ecx

push    4

lea     edx, DWORD PTR _t[ebp]

push    edx

lea     eax, DWORD PTR _f[ebp]

push    eax

call    memcpy

add     esp, 12

fld     DWORD PTR _f[ebp]

mov     esp, ebp

pop     ebp

ret     0

?@@YAM@Z ; f
```

冗余的，如果使用 `/0x` 标志编译，将没有 `memcpy()` 调用，直接使用变量 `f`。但查看未优化的版本更容易理解。

带 `-03` 选项的 GCC 4.4.1 会做什么？

# 列表 1.358: 化的 GCC 4.4.1

```asm
; f(float)

public Z1ff

Z1ff proc near

var_4 = dword ptr -4

arg_0 = dword ptr -8

push    ebp

mov     ebp, esp

sub     esp, 4

mov     eax, [ebp+arg_0] ; 设置负号

or     edx, eax

mov     edx, 0x8000000 ; 只保留符号位和小数部分在 EAX

mov     eax, 0x7FFFFFFF ; 准备指数

shr     edx, 23 ; 0x00017H - 丢掉小数部分

and     eax, 255 ; 只保留指数
```
