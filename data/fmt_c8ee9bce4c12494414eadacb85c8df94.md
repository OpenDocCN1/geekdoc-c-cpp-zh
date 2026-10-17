
```
CPU - main thread, module_2
00431010  CC          INT3
00431011  CC          INT3
00431012  CC          INT3
00431013  CC          INT3
00431014  53 0000000  PUSH ESI
00431018  55 DFFFFFFF  PUSH EBP
0043101C  8B 75 00  MOV ESI,loops_2.0031000
00431020  89 75 04  MOV [EBP+4],ESI
00431024  73 F7 0B  J SHORT loops_2.0031026
00431027  83 C7 04  CMP ESI,4
0043102A  75 F8  JNE -8
0043102D  53 0000000  PUSH ESI
00431031  C3          RET
00431032  E8 6143200  CALL loops_2.0031406
00431039  C3          RET
ESP=0042FD
```

Registers (FPU)

EDX:00000000  OFFSET M

EAX:00000000  MSUCRI

ECX:000002F8

EDX:000002F8

ESP:0043F010

EIP:00431020

ESI:00433579  loops_

EDI:00431020  loops_

EBX:004322B 32bit

ECX:004322B 32bit

ESI:004322B 32bit

EDI:004322B 32bit

EBP:004322B 32bit

FS:004322B 32bit

GS:004322B 32bit

```

正如我们所看到的，在调试器中手动跟踪是不方便的，这就是我们使用 `tracer` 的原因。我们在 IDA 中打开编译后的示例，`PUSH ESI` 指令（向 `f` 传递唯一参数）的地址在这种情况下为 `0x41026`，然后运行 `tracer`：

```
tracer.exe -l:loops_2.exe bp=loops_2.exe!0041026
```

BP 在该地址设置断点，`tracer` 然后将打印寄存器的状态。

在 `tracer` 的日志中，我们看到：

```
PID=12684|New process loops_2.exe

(0) loops_2.exe:0041026

EAX=0x003A328C EBX=0x00000000 ECX=0x6f0f4714 EDX=0x00000000

ESI=0x00000002 EDI=0x00333378 EBP=0x00024fbc ESP=0x00024fbb8

EIP=0x00310266

FLAGS=0x20 IF

(0) loops_2.exe:0041026

EAX=0x0000000B EBX=0x00000000 ECX=0x6f0a5617 EDX=0x00001ee88

ESI=0x00000003 EDI=0x00333378 EBP=0x00024fbc ESP=0x00024fbb8

EIP=0x00310260

FLAGS=0xCF AF SF

(0) loops_2.exe:0041026

EAX=0x00000005 EBX=0x00000000 ECX=0x6f0a5617 EDX=0x00001ee88

ESI=0x00000005 EDI=0x00333378 EBP=0x00024fbc ESP=0x00024fbb8

EIP=0x00310260
```

9 是最后一个循环值。这就是为什么在增加后 JL 不会触发，函数将结束：

239

```
FLAGS=CF AF SF IF

(0) loops_2_exe!0x401026

EAX=0x00000005 EBX=0x00000000 ECX=0x6f0a5617 EDX=0x0000ee18

ESI=0x00000006 EDI=0x00333378 EBP=0x00024fbc ESP=0x00024fbb8

EIP=0x0331026

FLAGS=CF PF AF SF IF

(0) loops_2_exe!0x401026

EAX=0x00000005 EBX=0x00000000 ECX=0x6f0a5617 EDX=0x0000ee18

ESI=0x00000007 EDI=0x00333378 EBP=0x00024fbc ESP=0x00024fbb8

EIP=0x0331026

FLAGS=CF PF AF SF IF

(0) loops_2_exe!0x401026

EAX=0x00000005 EBX=0x00000000 ECX=0x6f0a5617 EDX=0x0000ee18

ESI=0x00000009 EDI=0x00333378 EBP=0x00024fbc ESP=0x00024fbb8

EIP=0x0331026

FLAGS=CF PF AF SF IF

PID=1284|Process loops_2_exe exited. ExitCode=0 (0x0)
```

不仅如此，追踪器（`tracer`）还可以收集函数内所有地址的寄存器值。这被称为全跟踪（trace every）。每条指令都会被跟踪，所有感兴趣寄存器值都会被记录。

然后，会生成一个 IDA-idc 脚本来添加注释。因此，在 IDA 中我们了解到 `main()` 函数的地址是 `0x00401020`，并运行：

```
tracer.exe -l:loops_2_exe .bpf=loops_2_exe!0x00401020,trace:cc
```

BPF 代表函数断点（breakpoint on function）。

结果是，我们得到了 `loops_2_exe.idc` 和 `loops_2_exe_clear.idc` 脚本。

如果你发现了任何拼写错误、错误或有任何建议，请随时给我留言：我的电子邮箱。谢谢！

我们在 IDA 中加载 `loops_2_exe.idc` 并看到：

```
.text:0x010200 = SUBROUTINE

.text:0x010200 inc

.text:0x010201 int _cdecl main(int argc, const char **argv, const char **envp)

.text:0x010203 main : CODE XREF: mainStart+110jpj

.text:0x010204 prec near

.text:0x010205 argc = dword ptr 4

.text:0x010206 argv = dword ptr 8

.text:0x010207 envp = OCH

.text:0x010208 push esi : ESI:1

.text:0x010209 mov esi, 2

.text:0x0102a : CODE XREF: _Main+19jj

.text:0x01020b loc_041026: : ESI:2..9

.text:0x01020c tracing nested maximum level (1) reached,

.text:0x01020d call sub_041026

.text:0x01020e and esi = 0xf3fcbc

.text:0x01020f cmp esi, 08h

.text:0x010210 jl short loc_041026 : ESI:3..0xa

.text:0x010211 max eax, esi

.text:0x010212 pop esi

.text:0x010213 ret : EAX=0

.text:0x010214 _main : endp
```

图 1.57：加载了 id-script 的 IDA

我们看到在循环开始时，ESI 可以从 2 到 9，从 3 到 0xA (10) 递增。我们还可以看到 `main()` 结束时 EAX 值为 0。`tracer` 生成了 `2_exe.txt`，其中其中包含了关于每条指令执行次数和寄存器值的信息：

列表 1.173：loops_2_exe.txt

- 0x041020 (.text+0x20), e=1 [PUSH ESI] ESI=1
- 0x041021 (.text+0x21), e=1 [MOV ESI, 2]

# 245

```
move $fp, $sp

; 将计数器初始化为2并将此值存储在局部栈

li $v0, 2

sw $v0, 0x28+i($fp)

pseudoinruction: $BEQ $v0, $ZERO, loc_9C there in fact:

b loc_9C

or $at, $zero ; branch delay slot, NOP
```

```
loc_80: # 代码交叉引用: main+48

; 从局部栈加载计数器值并调用 printing_function()

lw $v0, 0x28+i($fp)

jal printing_function

or $at, $zero ; branch delay slot, NOP

; 加载计数器，递增并存回:

lw $v0, 0x28+i($fp)

or $at, $zero ; NOP

addiu $v0, 1

sw $v0, 0x28+i($fp)
```

```
loc_9C: # 代码交叉引用: main+18

; 检查计数器，它是否不是10?

lw $v0, 0x28+i($fp)

or $at, $zero

slti $v0, $A

; 如果小于10，跳转到 loc_80 (循环体)

bnez $v0, loc_80

or $at, $zero ; branch delay slot, NOP
```

```
finishing; return: 0

move $v0, $zero

function epilogue:

move $sp, $sp

lw $ra, 0x28+saved_RA($sp)

lw $fp, 0x28+saved_FP($sp)

addiu $sp, 0x28

jr $ra

or $at, $zero ; branch delay slot, NOP
```

指令紧随我们的 B 实际上是伪指令 (`BEQ`)。

# 还有一点

在生成的代码中我们可以看到：在初始化 i 之后，循环体将不会执行，因为 i 的条件会先被检查，只有在检查之后才能执行循环体。这是正确的。

因为，如果循环条件在开始时不满足，则必须不执行循环体。这在以下情况下是可能可能的：

```c
for (i=0; total_entries_to_process; i++)
  loop_body;
```

如果 `total_entries_to_process` 为 0，则循环体将完全不会执行。

如果你发现了任何拼写错误或有任何建议，请随时给我留言：我的电子邮箱。谢谢！

246

这就是为什么在执行之前会检查条件。
然而，一个优化过的编译器可能会交换条件检查和循环体，前提是它确定这里描述的情况是不可能发生的（例如我们这个非常简单的例子的情况，以及使用如 Keil、Xcode (LLVM)、优化模式下的 MSVC 等编译器时）。

# 1.22.2 内存块复制例程

真实世界的复制程序在每次迭代中可能会复制 4 或 8 字节，使用 SIMD¹⁰ 向量化等。但为了简单起见，这是最简单的。

```c
#include <stdio.h>

void memcopy(unsigned char* dst, unsigned char* src, size_t cnt)
{
    size_t i;
    for (i=0; i<cnt; i++)
        dst[i]=src[i];
}
```

# 直接的实现

列表 1.177: GCC 4.9 x64 针对大小优化 (-Os)

我的 memcopy:
```assembly
;RDI = 目标地址
;RSI = 源地址
;RDX = 块的大小
; 将计数器 (i) 为 0
.L2:
xor eax, eax
```
