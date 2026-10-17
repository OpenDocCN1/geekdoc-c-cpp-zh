
在寄存器窗口中右键点击 `EAX` 并“在栈中跟踪”（Follow in stack）。添加了一个红色箭头，指向局部栈中的变量。此时，该位置包含包含一些垃圾数据（`0x6E494714`）。现在，借助 `PUSH` 指令，该栈元素将在下一个位置存储到同一个栈中。让我们用 `F8` 追踪直到 `scanf()` 执行完成。在 `scanf()` 执行期间，我们在控制台窗口输入了例如 123：

Enter X:

123

如果你发现任何拼写错误、错误或有任何建议，请随时给我留言：我的电子邮箱。谢谢！

## scanf() 已经完成了执行

![](img/4590a0c34d3b5b6ca77b4202d4036d48_112_0.png)

`scanf()` 在 `EAX` 中返回 1，这意味着它成功读取了一个值。我们再次查看与局部变量对应的栈元素，它现在包含 `0x7B` (123)。

如果你发现任何拼写错误、错误或有任何建议，请随时给我留言：我的电子邮箱。谢谢！

## 稍后，此值从栈复制到 ECX 寄存器并传递给 `printf()`

![](img/4590a0c34d3b5b6ca77b4202d4036d48_113_0.png)

图 1.15：OllyDbg：准备 `printf()` 的值

## GCC

让我们尝试在 Linux 下使用 GCC 4.4 编译这段代码：

```c
main() {
    var_20 = dwarf ptr -20h
    var_1C = dwarf ptr -1Ch
    var_4  = dwarf ptr -4h

    push    ebp
    mov     esp, esp
    and     esp, 0xFFh
    sub     esp, 20h
    call    [esp+20h], "X: "
    mov     edx, [esp+20h]
    lea     [esp+20h], edx
    mov     [esp, 4], eax
    mov     eax, 0
    leave
}
```

GCC 用 `puts()` 替换了 `printf()`。原因在第 28 页 (5.3)。

在 MSVC 示例中——参数放置在栈上。

这个简单的示例演示了编译器将 C/C++ 的表达式列表转换为顺序指令列表。C/C++ 中表达式之间没有内容，而在生成的机器码中，控制流跳转到下一个。

这里使用寄存器而不是栈来传递参数。

## MSVC

| DATA SEGMENT | |
|---|---|
| `$SG289` | `'Enter X:', 0AH, 00H` |
| `$SG291` | `'%d', 00H` |
| `$SG292` | `'You entered %d...', 0AH` |

```assembly
TEXT SEGMENT
x = 32
main
$3:
    sub     rsp, 56
    lea     rcx, OFFSET:$SG289; 'Enter X:'
    call    printf
    lea     rdx, DWORD PTR [rsp]
    lea     rcx, OFFSET:$SG291; '%d'
    call    scanf
    mov     edx, DWORD PTR [rsp]
    lea     rcx, OFFSET:$SG292; 'You entered %d...'
    call    printf

    return 0
    xor     eax, eax
    add     rsp, 56
    ret
END
```

## GCC

### 列表 1.73：优化的 GCC 4.4 x64

```
LC0:  string "Enter X:"
LC1:  string "%d"
LC2:  string "You entered %d..\n"

main:
    sub    rsp, 24
    mov    edi, OFFSET:.LC0 ; "Enter X:"
    call   puts
    lea    rdx, [rsp+12]
    mov    edi, OFFSET:.LC1 ; "%d"
    xor   eax, eax
    call   scanf
    mov    edx, DWORD PTR [rsp+12]
    mov    edi, OFFSET:.LC2 ; "You entered %d..\n"
    xor   eax, eax
    call   printf

    return 0
    xor   eax, eax
    add    rsp, 24
    ret
```

## ARM

### 优化的 Keil 6/2013 (Thumb模式)

```assembly
.text:00000042  scanf_main
.text:00000042
.text:00000042    var_8      = -8
.text:00000042  08 85    PUSH   (R3,LR)
.text:00000042  A9 A0    ADR    R0,aEnterX ; "Enter X:\n"
.text:00000046  F0 D3 F8 D0     BL     2printf
.text:0000004A  99 46    MOV    R1, SP       ; "%d"
.text:0000004A  A0 A0    ADR    R0, ad        ; "%d"
.text:0000004E  F0 F0 CB F8     BL     scanf
.text:00000052  00 99    LDR    R1, [SP,#var_8]
.text:00000059  A9 A0    ADR    R0, aEnteredD ; "You entered"
.text:00000056  F0 CB F8     BL     2printf
.text:0000005A  00 20    MOVS   R0, #0
```

`PUSH`/`POP` 在 ARM 中的行为与 x86 不同（相反的）。`PUSH` 先将一个值写入栈中，然后 `SP` 增加 4。`POP` 先从栈中读取一个值。因此，`PUSH` 之后，`SP` 指向一个未使用的空间并被 `scanf()` 和 `printf()` 读取。

`LDIA` 表示在每次传输后增加寄存器地址。`STDM` 在每次传输前增加多个寄存器地址。

稍后，借助 `LDR` 指令，此值从栈移动到 `R1` 寄存器以便传递给 `printf()`。

## ARM64

### 列表 1.74：非优化的 GCC 4.9.1 ARM64

```
LC0:      string "Enter X:"
LC1:      string "%d"
LC2:      string "You entered %d..\n"

main:
        sub    rsp, 32
        stp     x29, x30, [sp, -32]
        set stack frame (FP=SP)
        add      x29, sp, 0
        load pointer to the "Enter X:"
        adpr     x0, LC0
        add      x0, x0, :lo12:LC0
        X0;pointer to the "Enter X:" string
        printf:
        bl
        load pointer to the "%d" string:
        adpr     x0, LC1
        add      x0, x0, :lo12:LC1
        find a space in stack frame for "x" variable (XI=FP+28):
        add      x1, x29, 28
        XI;address of "x" variable
        pass the address to scanf() and call:
        bl
        _isoc99 scanf
        load 32-bit value from the variable in stack frame:
        ldr    w1, [x29, #28]
        mov    w0, w1
        load pointer to the "You entered %d..." string:
        adpr     x0, LC2
        add      x0, x0, :lo12:LC2
        X0;pointer to the "You entered %d..." string
        printf:
        bl

        return 0
        xor    w0, w0
        add    sp, 32
        pop     x29, x30, [sp]
        ret
```

| 行号 | 指令/注释 |
|---|---|
| 27 | `ldr w1,[x29,28]` |
| 28 | `w1=x` |
| 29 | load pointer to the "You entered %d..\n" string |
| 30 | `printf()` will take string from `X0` and "x" variable from `X1` (or `W1`) |
| 31 | `adpr x0,:LC2` |
| 32 | `add x0, x0,:lo12::LC2` |
| 33 | `bl printf` |
| 34 | return 0 |
| 35 | `mov w0, w0` |
| 36 | restore FP and LR, then add 32 to SP: |
| 37 | `ldp x29, x30,[sp], 32` |
| 38 | `ret` |

栈帧分配了 32 字节，这比需要的要大。也许是某种内存对齐问题？最有趣的发现是栈帧中为变量 `x` 留的空间（第 22 行）。为什么是 28？不知由于何，编译器决定将此变量放在栈帧末尾而不是开头。该地址传递给 `scanf()`，它只需将用户输入的值存储在该地址对应的内存中。这是一个 `int` 的 32 位值。该值在第 27 行被取出，然后传递给 `printf()`。

## MIPS

本地栈中为变量 `x` 分配了空间，其引用方式为 `$sp+24`。

它的地址传递给 `scanf()`，用户输入通过 `LW` ("Load Word") 指令加载，然后传递给 `printf()`。

> 列表 1.75：优化的 GCC 4.4 (汇编输出)

```assembly
$LC0:
  .ascii "Enter X:\000"

$LC1:
  .ascii "%d\000"

$LC2:
  .ascii "You entered %d..\012\000"

main:
  function prologue:
    lui $28,$hi(_gnu_local_gp)
    adddu $sp,$sp,-40
    adddu $28,$lo(_gnu_local_gp)
    sw $25,36($sp)

  call puts():
    lw $4,$hi($LC0)
    lui $25
    jalr $4,call16(puts)($28)
    adddu $4,$4,$lo($LC0); branch delay slot

  call scanf():
    lw $28,16($sp)
    lui $4,$hi($LC1)
    lw $25,4call16(isoc99_scanf)($28)
    set 2nd argument of scanf; $a1=$sp+24;
    addiu $5,$sp,24
    addiu $25
    jal $4,$4,lo($LC1) ; branch delay slot

; call printf();
lw      $28,16($sp)
; set 2nd argument of printf(),
; load word at address $sp+24:
lw      $5,24($sp)
lui     $25,call16(printf($28))
lui     $4,$hi($LC2)
jalr   $4,$4,lo($LC2) ; branch delay slot

; function eclipse:
lw      $31,36($sp)
; set return value to 0:
move   $2,$0
return:
j       $31
addiu  $sp,$sp,40    ; branch delay slot
```

IDA 显示的栈布局如下：

列表 1.76：优化的 GCC 4.4.5 (IDA)

```assembly
.text:00000000
.text:00000000
.text:00000000 var_18 = -0x18
.text:00000000 var_10 = -0x10
.text:00000000 var_4 = -4
.text:00000000
.text: function_ prologue:
.text:00000000 lui $gp, ( _gnu_local_gp >> 16)
               addiu  $sp, -0x28
.text:00000000 lw      $gp, ( _gnu_local_gp & 0xFFFF)
               sw      $ra, 0x28+4($sp)
.text:00000000 sw      $gp, 0x28+var_18($sp)
.text:00000000 ; call puts():
.text:00000014 lw      $19, (puts & 0xFFFF) # "Enter X:"
.text:00000018 lui     $a0, ($LC0 >> 16) # "Enter X:"
.text:0000001c jalr   $19
.text:00000020 la      $a0, ($LC0 & 0xFFFF) # "Enter X:" ; branch
.text:00000020 ; call scanf():
.text:00000024 lw      $gp, 0x22+var_18($sp)
.text:00000028 lui     $a0, ($LC1 >> 16) # "%d"
.text:0000002c lw      $19, (_isoc99_scanf & $sp))
.text:00000030 ; set 2nd argument of scanf; $a1=$sp+24;
addiu $5,$sp,24
.text:00000030 ; set 2nd argument of printf(),
; load word at address $sp+24:
addiu $s1,$sp,0x28+var_10
.text:00000034 jalr   $19    branch delay slot
.text:00000038 la      $a0, ($LC1 & 0FFFF) # "%d"
               call printf();
.text:0000003c lw      $gp, 0x28+var_18($sp)
.text:00000040 lw      $a1, 0x28+var_10($sp)
.text:00000044 lw      $t9, (printf & 0xFFFF)($gp)
.text:00000048 lui     $a0, ($LC2 >> 16) # "You entered %d..\n"
.text:0000004c jr      $19
.text:00000050 la      $a0, ($LC2 & 0xFFFF) # "You entered %d..\n"
; branch delay slot
; function prologue:
.text:00000054 lw      $ra, 0x28+var_4($sp)
; set return value to 0:
.text:00000058 move   $v0, zero
; return:
.text:0000005c jr      $ra
.text:00000060 addiu  $sp, 0x28; branch delay slot
```

## 1.1.2 经典错误

这是一个非常常见的错误（类型错误）：传递 `x` 的值而不是 `x` 的指针给 `scanf`：

```c
#include <stdio.h>

int main() {
    int x;
    printf("Enter X:\n");
    scanf("%d", x); // BUG
    printf("You entered %d..\n", x);
    return 0;
}
```
