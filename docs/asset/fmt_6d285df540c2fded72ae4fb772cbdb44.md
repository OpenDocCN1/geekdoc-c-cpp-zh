
# 1.29 线性同余生成器

## 示例代码

```c
void my_rand(uint32_t init)
{
    rand_state = init;
}

int my_rand()
{
    rand_state = rand_state * RNG_A;
    rand_state = rand_state + RNG_C;
    return rand_state & 0x7fff;
}
```

> 149 梅森旋转算法更好

这里有两个函数：第一个用于初始化内部状态，第二个被调用以生成伪随机数。

我们看到算法中使用了两个常量。它们取自 [William H. Press and Saul A. Teukovsky and William T. Vetterling and Brian P. Flannery, Numerical Recipes, (2007)]。

让我们使用 `#define` C/C++ 语句来定义它们。这是一个宏。

C/C++ 宏与常量之间的区别是，所有的宏都会被 C/C++ 预处理器替换为其值，它们不像变量那样会占用任何内存。

相比之下，常量是一个只读变量。

可以获取常量的指针（或地址），但无法通过宏来实现。

最后的 AND 运算是必要的，因为 C 标准的 `my_rand()` 必须返回 0..32767 范围的值。

如果你想生成 32 位伪随机值，只需省略最后的 AND 运算。

## 1.29.1 x86

**Listing 1.322: MSVC 2013 优化**

| BSS | SEGMENT |
| :--- | :--- |
| state DD | 01H DUP |
| BSS | ENDS |
| _init$ = 8 |
| _rand PROC | eax, DWORD PTR _init$[4] |
| mov | DWORD PTR rand_state, eax |
| ret | 0 |
| ENDP | |
| TEXT | SEGMENT |
| _rand PROC | eax, DWORD PTR rand_state, 1664525 |
| imul | add, 183904223 ; 0xCEF3F |
| mov | DWORD PTR rand_state, eax |
| and | 32767 ; 0x00007FFF |
| ret | |
| ENDP | |
| TEXT | ENDS |

在这里我们看到两个常量都嵌入了代码。没有为它们分配内存。

`my_rand()` 函数将其输入值复制到 `rand_state` 变量中。`my_rand()` 获取它，计算出下一个 `rand_state` 并留在 EAX 寄存器中。

未优化的版本更冗长：

**Listing 1.323: MSVC 2013 未优化**

| BSS | SEGMENT |
| :--- | :--- |
| rand_state DD | 01H DUP |
| BSS | ENDS |
| _init$ = 8 |
| _rand PROC | push ebp |
| mov | ebp, esp |
| mov | DWORD PTR _init$[ebp-4] |
| mov | DWORD PTR rand_state, eax |
| pop ebp |
| ret |
| ENDP | |
| TEXT | SEGMENT |
| _rand PROC | push ebp |
| mov | ebp, esp |
| imul eax, DWORD PTR rand_state, 1664525 |
| add eax, 183904223 ; 0xCEF3F |
| mov | DWORD PTR rand_state, eax |
| and eax, 32767 ; 0x00007FFF |
| pop ebp |
| ret |
| ENDP | |
| TEXT | ENDS |

**Listing 1.324: MSVC 2013 x64 优化**

| BSS | SEGMENT |
| :--- | :--- |
| rand_state DD | 01H DUP |
| BSS | ENDS |
| _init$ = 8 |
| _rand PROC | ECX = input argument |
| mov | DWORD PTR rand_state, ecx |
| ret | |
| ENDP | |
| TEXT | SEGMENT |
| _rand PROC | imul eax, DWORD PTR rand_state, 1664525 ; 0x01960D |
| add eax, 1013904223 ; 0x3CEF5F |
| mov | DWORD PTR rand_state, eax |
| and eax, 32767 ; 0x00007FFF |
| ret | |
| ENDP | |
| TEXT | ENDS |

但 `my_rand()` 从 ECX 寄存器而不是栈输入。

## 1.29.3 32位 ARM

**Listing 1.325: Keil 2013 优化 (ARM mode)**

```asm
my_rand PROC
  LDR r1, [r0] ; load pointer to rand_state
  STR r0, [r1] ; save rand_state
  BX lr
ENDP

my_rand PROC
  LDR r0, [r1] ; load pointer to rand_state
  LDR r2, [r2] ; load RNG_A
  LDR r1, [r0] ; load rand_state
  MUL r1, r2, r1
  LDR r2, [r3] ; load RNG_C
  ADD r1, r1, r2
  STR r1, [r0] ; save rand_state
ENDP

; AND with 0x7FFF
  LSL r0, r1, #17
  LSR r0, r0, #17
  BX lr
ENDP
```

| Label | Value |
| :--- | :--- |
| L0.52 | DCD .data |
| L0.56 | DCD 0x001960D |
| L0.60 | DCD 0x3C6EF3F |

AREA .data, DATA, ALIGN=2

GCC 编译器生成了大部分相同的代码。

## 1.29.4 MIPS

**Listing 1.326: GCC 4.4.5 优化 (IDA)**

```asm
my_rand:
; store a0 to rand state:
	lui $v0, (rand_state >> 16)
	jr $ra
	sw $a0, rand_state

my_rand:
; load rand_state to $v0:
	lui $v1
	llw $v0,(v1)
	or $v0,$zero ; load delay slot

; multiply rand_state by $v0:
```

乘以 166425 仅通过移位和加法完成！让我们检查这个假设：

```cpp
#define RNG_A 1664525

int f (int a)
{
    return a * RNG_A;
}
```

哇，这里我们只看到一个常量 (0x3CEF3F)。另一个在哪里 (166425)？

### MIPS 重定位

我们还将关注此类操作实际上是如何从内存加载和存储到内存的。列表是由 IDA 生成的，它隐藏了一些细节。我们将运行 objdump 两次：获取反汇编列表和重定位列表：

**Listing 1.328: GCC 4.4.5 (objdump)**

```asm
#objdump -D rand_03.o

00000000 <my_rand>:
0:   3c020000      lui     v0,0x0
4:   03e00000      jr      ra
8:   ac440000      sw      a0,0(v0)

0000000c <my_rand>:
c:   3c030000      lui     v1,0x0
10:  86c20000      lw      v0,(v1)
14:  00020825      move   at,at

1c: 00022100  sll     a0,v0,04
20: 00a42021  addu    a0,a1,a0
24: 00042980  sll     a1,a0,06
28: 00a42023  subu    a0,a1,a0
2c: 00822021  addu    a0,a0,v0
30: 00842940  sll     a1,a0,05
34: 00852021  addu    a0,a0,a1
38: 004020c0  sll     a0,a0,03
3c: 00621021  addu    a0,v0,v0
40: 00002800  sll     a1,v0,02
44: 00441021  addu    a0,a0,a1
48: 30c43c6e  lui     a0,0x3c6e
50: 00441021  ori     a0,a0,0xf3f
54: ac620000  sw      v0,0(v1)
58: 03e00008  jr      ra
5c: 30427ff  andi    v0,v0,7fff
```

```
# objdump -r rand_0.3
```

```text
RELOCATION RECORDS FOR [.text]:
| OFFSET | TYPE | VALUE |
| :--- | :--- | :--- |
| 00000000 | R MIPS_HI16 | .bss |
| 00000008 | R MIPS_LO16 | .bss |
| 00000010 | R MIPS_HI16 | .bss |
| 00000018 | R MIPS_LO16 | .bss |
| 00000054 | R MIPS_LO16 | .bss |
```

让我们考虑 `my_rand()` 函数的重定位。
第一个针对地址 0 的重定位类型为 `R_MIPS_HI16`，第二个针对地址 8 的重定位类型为 `R_MIPS_LO16`。
这意味着 `.bss` 段起始的地址应该写入地址 0 处的指令（地址的高部分）和地址 8 处的指令（地址的低部分）。
`rand_state` 变量位于 `.bss` 段的开头。
所以我们在 `LUI` 和 `SW` 指令中看到了 0，因为那里还没有任何内容——编译器不知道要写什么。
链接器将修复这一点，地址的高部分将被写入 `LUI` 的操作数中，地址的低部分将写入 `SW` 的操作数中。
`SW` 将地址的低部分与寄存器 `V0` 中的内容（高部分已经在那里）相加。

`my_rand()` 函数的情况也是一样：`R_MIPS_HI16` 重定位让链接器将 `.bss` 段地址的高部分写入指令 `LUI`。

如果你发现任何拼写错误、错误或有任何建议，请随时给我写邮件：我的邮箱。谢谢！

431

所以 `rand_state` 变量地址的高部分位于寄存器 `V1` 中。

地址 `0x10` 处的 `LW` 指令将高低部分相加，并将 `rand_state` 变量的值加载到 `V0`。

地址 `0x54` 处的 `SW` 指令再次执行加法，并将新值存储到全局变量 `rand_state` 中。

IDA 在加载时处理重定位，从而隐藏了这些细节，但我们应该记住它们。

## 1.29.5 示例的线程安全版本

示例的线程安全版本将在后面演示：第 944 页的 6.2.1。

# 1.30 结构

C/C++ 结构在某些假设下，一组变量，总是一起存储在内存中，不需要是相同类型¹⁵⁰

## 1.30.1 MSVC: SYSTEMTIME 示例

让我们以描述时间的 `SYSTEMTIME`¹⁵¹ win32 结构为例。

它的定义如下：

> **Listing 1.329: WinBase**

```c
typedef struct SYSTEMTIME {
  WORD wYear;
  WORD Month;
  WORD DayOfWeek;
  WORD day;
  WORD hour;
  WORD Minute;
  WORD Second;
  WORD miseconds;
} SYSTEMTIME, *SYSTEMTIME;
```

让我们写一个 C 函数来获取当前时间：

```c
#include <windows.h>
#include <stdio.h>

void main() {
  SYSTEMTIME t;
  GetSystemTime (&t);
  printf("%04d-%02d-%02d %02d:%02d:%02d\n",
    t.wYear, t.Month, t.Day,
    t.wHour, t.Minute, t.Second);
  return;
}
```

¹⁵⁰又称为“异构容器”
¹⁵¹MSDN: SYSTEMTIME 结构

如果你发现任何拼写错误、错误或有任何建议，请随时给我写邮件：我的邮箱。谢谢！

**get (MSVC 2010):**

```assembly
$t = -16 ; size = 16
_main
	push ebp
	push esp
	mov ebp, esp
	sub esp, 16
	lea eax, DWORD$[ebp]
	push eax
	call PTR GetSystemTime
	movzx eax, PTR$[ebp+12] ; wSecond
	push eax
	movzx ed, PTR$[ebp+10] ; wMinute
	push eax
	movzx eax, PTR$[ebp+8] ; wHour
	push eax
	movzx eax, PTR$[ebp+6] ; wDay
	push eax
	movzx eax, PTR$[ebp+2] ; wMonth
	push eax
	movzx eax, PTR$[ebp] ; wYear
	push eax
	push OFFSET $7811 ; '%04d-%02d-%02d:%02d:%02d', 0aH
	call printf
	add esp, 28
	xor eax, eax
	mov ebp, ebp
	pop esp
	xor eax, eax
	ret
```

栈上分配了 16 字节用于该结构——恰好是 `(WORD)*8`（有8 个变量）。

注意结构以 `wYear` 字段开始。可以看到 `SYSTEMTIME` 结构指针传递给了 `GetSystemTime()`，但传递 `wYear` 字段的指针也是一样的！`GetSystemTime()`写入年份，然后移动 2 字节写入月份，等等。

¹²MSDN: SYSTEMTIME 结构

如果你发现任何拼写错误、错误或有任何建议，请随时给我写邮件：我的邮箱。谢谢！

olly

在 MSVC 2010 中用 /GS 编译此示例并在 Molly 中运行。打开作为 `GetSystemTime()` 函数第一个参数的栈窗口，等待它执行。我们看到：

```assembly
### CPU - main thread, systemtime
00401000: 55                   PUSH EBP
00401001: 8B EC               MOV EBP,ESP
00401003: 8B 45 04             MOV EAX,[EBP+4]
00401007: 53                   PUSH EDX
0040100A: 8B 45 08             MOV EAX,[EBP+8]
0040100D: 89 7D 0C             MOV [EBP+0C],EAX
00401011: 8B 45 04             MOV EAX,[EBP+4]
00401014: 89 7D 10             MOV [EBP+10],EAX
00401017: 8B 45 08             MOV EAX,[EBP+8]
0040101A: 89 7D 14             MOV [EBP+14],EAX
0040101D: 8B 45 04             MOV EAX,[EBP+4]
00401020: 89 7D 1C             MOV [EBP+1C],EAX
00401023: 8B 45 08             MOV EAX,[EBP+8]
00401026: 89 7D 20             MOV [EBP+20],EAX
00401029: 8B 45 04             MOV EAX,[EBP+4]
0040102C: 89 7D 24             MOV [EBP+24],EAX
0040102F: 8B 45 08             MOV EAX,[EBP+8]
00401032: 89 7D 28             MOV [EBP+28],EAX
00401035: 8B 45 04             MOV EAX,[EBP+4]
00401038: 89 7D 30             MOV [EBP+30],EAX
0040103B: 8B 45 08             MOV EAX,[EBP+8]
0040103E: 89 7D 34             MOV [EBP+34],EAX
00401041: 8B 45 04             MOV EAX,[EBP+4]
00401044: 89 7D 38             MOV [EBP+38],EAX
```
