
因此，`SP+4` 存储在 `R12` 寄存器中。
下一个指令 `STMIA R12, R0-R3` 将 `R0-R3` 的内容写入 `R12` 所向的内存。`STMIA` 是 Store Multiple Increment After（递增后存储）的缩写。Increment After 表示在写入每个寄存器值后，`R12` 增加 4。

- 通过栈传递 4：4 存储在 `R0` 中，此值通过 `STR R0, [#SP,0x18+var_18]` 指令保存到栈上。`var_18` 为 `-0x18`，因此偏移量为 0，从而将 `R0` 寄存器的值（4）写入 `SP` 所在的地址。
- 传递 1, 2 和 3 寄存器：前三个数字（a, b, c）的值（分别为 1, 2, 3）在调用 `printf()` 之前通过 `R1`、`R2` 和 `R3` 寄存器传递。
- 函数对尾部（Function ep）：

`ADD SP, SP, #0x14` 将 `SP` 指针恢复到原来的形式，使存储在栈上的所有内容消失。当然，存储在栈上的内容会保留，但在后续函数的执行期间，它们会被覆盖。
`LDR PC, [SP+4],#4` 指令将 `LR` 值从栈保存到 `PC` 中，导致函数退出。这里没有感叹号——实际上，`PC` 是从 `SP` 的第一个地址（`4+var_4=4+(-4)=0`）加载的，因此这条指令类似于 `LDR PC, [SP],#4`，然后 `SP` 增加 4。这被称为后索引⁷。为什么 IDA 显示的指令看起来是那样呢？因为它想说明布局，且该指令在某种程度上是为了在局部栈中保存 `LR` 值，类似于 x86 中的 `POP PC`¹¹。

## 优化 Keil 2013：Thumb 模式

```
.text:0000000C
.text:0000001C
.text:0000000C
.text:0000001C
.text:0000001C
.text:0000001C
.text:0000001C
.text:0000001C 00 B5
.text:0000001E 08 23
.text:00000020 05 B0
.text:00000022 04 93
.text:00000024 07 27
.text:00000026 06 21
.text:00000028 06 21
.text:0000002A 05 20
.text:0000002C 01 AB
printf_main2
    var_18 = -0x14
    var_14 = -0x14
    var_8 = -8
    PUSH {LR}
    MOVS R3, #8
    SUB SP, SP, #0x14
    STR R3, [#SP,0x18+var_18]
    MOVS R2, #7
    MOVS R1, #6
    MOVS R0, #5
    ADD R3, SP, #0x18+var_14
```

⁷ 更多信息：第 555 页的 1.39.2。
¹¹ 在 x86 中无法使用 `POP` 设置 `IP/RIP` 值，但无论如何，你已经理解这个类比了。尽管给我写信信（我的邮箱）。谢谢！

![](img/4590a0c34d3b5b6ca77b4202d4036d48_94_0.png)

```
.text:0000002C 07 C3 STMIA R3!, {R0-R2}
.text:0000002E 04 20 MOVS R0, #4
.text:00000030 00 23 STR R0, [SP,#0x18+var_1]
.text:00000032 02 23 MOVS R3, #3
.text:00000034 02 22 MOVS R2, #2
.text:00000036 01 21 MOVS R1
.text:00000038 A0 A0 ADR R0, =aABDCCDDEDDFDG ; "a=%d; b=%d; c=%d"
.text:0000003A 06 F9 08 BL _printf
.text:0000003E
.text:0000003E loc_3E ; CODE XREF:example13_f+16
.text:0000003E 05 B0 ADD SP, SP,#0x18
.text:00000040 00 BD POP (PC)
```

输出与之前的示例相似。然而，这是 Thumb 代码，且值在交替栈中打包的：8, 5, 6, 7 和 4。

## 优化 Xcode 4.6.3 (LLVM)：ARM 模式

```
.text:0000029C _printf2
.text:0000029C var_IC = -0xC
.text:0000029C var_C = -0xC
.text:0000029C 0B 40 2D A0 STMFD SP!,{R7,LR}
.text:00000210 00 70 A0 E3 MOV R7, SP
.text:00000214 10 4D A4 E2 SUB SP, SP,#0x14
.text:00000218 70 05 01 E3 MOV R0,#0x15
.text:0000021C 07 0C A0 E3 MOV R12, #7
.text:00000220 04 24 A0 E3 MOV R0, #0
.text:00000224 20 00 F8 E0 MOV R2, #4
.text:00000228 00 00 F8 E0 ADD R0, R0
.text:0000022C 06 30 A0 E3 MOV R3, #6
.text:00000230 08 10 A0 E3 MOV R1, #5
.text:00000234 20 80 D5 E5 STR R2, [SP,#0xC]
.text:00000238 0A 10 B0 E9 STMFFA,(R1,R3,R12)
.text:00000240 01 10 A0 E3 MOV R1, #1
.text:00000244 20 20 A0 E3 MOV R2, #2
.text:00000248 30 03 A0 E3 MOV R3, #3
.text:0000024C 10 90 B0 E8 _printf
.text:00000254 07 D0 A0 E1 MOV SP, R7
.text:00000258 00 80 B0 E8 MDL SP!,R7,PC}
```

与我们已经看到的几乎相同，除了 `STMFFA`（升序多寄存存储）。这条指令先增加 `SP` 的值，然后写入下一个寄存器，而不是相反的操作。如果你发现了错误或有任何建议，请尽管给我写信（我的邮箱）。谢谢！

另一个引起注意的是指令是随机排列的。例如，`R0` 寄存器的值在三个地方被操作（地址 `0x2918`、`0x2920` 和 `0x2928`），而可以在一点完成。然而，优化编译器可能有自己的理由来排序指令以获得更高的执行效率。通常，处理器尝试并行执行指令。例如，`MOV R0, #0` 和 `ADD R0, PC` 不能同时执行，因为它们都修改了 `R0` 寄存器。另一方面，`MOV R0, #0` 和 `MOV R2, #4` 可以同时执行，因为它们的执行效果互不冲突。假设编译器会在任何可能的地方尝试这样的代码。

## 优化 Xcode 4.6.3 (LLVM)：Thumb-2 模式

```
000002A0 _printf main
000002A0 var_IC = -0x1C
000002A0 var_18 = -0x18
000002A0 var_C = -0xC
000002A0
000002A0
000002A0
000002B0 80 05 PUSH {R7,LR}
000002B2 6F 46 MOV R0, SP
000002B4 85 00 SUB SP, SP, #0x14
000002B6 41 F3 08 20 MOVW R0, #0x12D8
000002B8 F6 07 0C MOVW R12, #7
000002B9 C0 F2 00 00 MOVW R0, #0
000002BA 02 04 MOVS R2, #4
000002BC 78 44 ADD R0, PC ; char *
000002BE 00 23 MOVS R3, #5
000002BF 05 21 MOVS R1, #5
000002C1 D4 01 04 ADD.W R1, SP, #0x1C+var_18
000002C3 00 92 STR R2, [SP,#0x1C+var_1C]
000002C5 F4 08 0E MOVW R0, #0
000002C7 E8 0A 10 STRIA.W {LR,R1,R3,R12}
000002C9 0C 21 MOVS R1, #1
000002CB 6A 22 MOVS R2, #2
000002CD 03 23 MOVS R3, #3
000002CF F8 10 90 STR W0
000002D1 07 D0 A0 E1 MOV SP, R7
000002D3 00 80 B0 E8 MDL SP!,R7,PC}
```

`$5...$7` (或 `$A1$...A3`)。这就是为什么寄存器以 `A-` 为前缀，这意味着它们用于传递函数参数。

## 列表 1.58：优化的 GCC 4.4.5 (汇编输出)

```
$LCO0:
    ascii a="%d; b=%d; c=%d\0000"
main:
    function prologue:
        lui     $28,$hi(  _gnu_local_gp)
        addiu   $28,$sp,-32
        addiu   $28,$lo(  gnu_local_gp)
        sw      $31,28($sp)
    load address of printf():
        lw      $25,$call16(printf)
    load address of the text string and set 1st argument of printf():
        lui     $4,$hi($LCO0)
        addiu   $4,$4,lo($LCO0)
    set 2nd argument of printf():
        li      $5,1             # 0x1
    set 3rd argument of printf():
        li      $6,2             # 0x2
    call printf():
        $25
        jalr    $25
    set 4th argument of printf(): (branch delay slot)
        li      $7,3             # 0x3
    function epilogue:
        lw      $31,28($sp)
    set return value to 0:
        move    $2,$0
    return:
        j       $31
        addiu   $sp,$sp,32      ; branch delay slot
```

## 列表 1.59：优化的 GCC 4.4.5 (IDA)

```
.text:00000000 main:
.text:00000000
.text:00000000 var_10    = -0x10
.text:00000000 var_4      = -4
.text:00000000
.function prologue:
.text:00000000    lui     $gp, (_gnu_local_gp) >> 16
.text:00000004    addiu   $sp,-0x20
.text:00000008    la      $sp, (_gnu_local_gp & 0xFFFF)
.text:0000000c    sw      $s7,$sp+20+var_4($sp)
.text:00000010    sw      $gp,$sp+20+var_10($sp)
.text:00000014 load address of printf():
.text:00000014    lw      $19, (printf & 0xFFFF)($gp)
.text:00000018 load address of the text string and set 1st argument of printf():
.text:0000001c    la      $a0,$LCO0      # #a="%d; b=%d; c="%d"
.text:00000020    li      $a1, 1
; set 3rd argument of printf:
.text:00000024    li      $a2, 2
; call printf():
.text:00000028    jalr    $t9
; set 4th argument of printf(branch delay slot):
.text:0000002c    li      $a3, 3
; function epilogue:
.text:00000030    lw      $ra, $0x20+var_4($sp)
; set return value to 0:
.text:00000034    move    $v0, zero
; return
.text:00000038    jr      $ra
.text:0000003c    addiu   $sp, $0x20 ; branch delay slot
```

IDA 将一对 `LUI` 和 `ADDI` 指令合并为了一条 `LA` 伪指令。这就是为什么在 `0x1c` 处没有指令的原因：因为 `LA` 占据了 8 字节。

## 未优化的 GCC 4.4.5

未优化的 GCC 更加冗长：

## 列表 1.6：未优化的 GCC 4.4.5 (汇编输出)

```
$L0$:    "a=%d; b=%d; c=%d\n000"
main:
; function prologue:
    addiu   $sp,-32
    sw      $sp,$28($sp)
    sw      $fp,$24($sp)
    move    $fp,$sp
    lui     $28,hi(gnu_local_gp)
    addiu   $20,$28,lo(gnu_local_gp)
; load address of the text string:
    lui     $2,hi($L0)
    addiu   $2,$2,lo($L0)
; set 1st argument of printf():
    move    $4,$2
; set 2nd argument of printf():
    li      $5,1              # 0x1
; set 3rd argument of printf():
    li      $6,2              # 0x2
; set 4th argument of printf():
    li      $7,$3              # 0x3
; get address of printf():
    lw      $2,%call16(printf))
    nop
; call printf():
    move    $25
    jalr    $25
    nop
; function epilogue:
  $28,16($fp)
  lw
; set return value to 0:
  move    $2,$0
  move    $sp,$fp
  move    $31,28($sp)
  lw    $fp,24($sp)
  addiu   $sp,$sp,32
; return:
  j
  nop
```

## 列表 1.61：未优化的 GCC 4.4.5 (IDA)

```
.text:00000000 main:
.text:00000000 var_10    = -0x10
.text:00000000 var_8      = -8
.text:00000000 var_4      = -4
.text:00000000
  function epilogue:
.text:00000000 addiu   $sp,-0x20
.text:00000004 sw      $ra,0x20+var_4($sp)
.text:00000008 sw      $fp,0x20+var_8($sp)
.text:0000000c move    $fp,$sp
.text:00000010 lw      $gp,gnu_local_gp
.text:00000018 sw      $ra,0x20+var_0($sp)
; load address of the text string:
.text:0000001c la      $v0,$a0 # "=%d;b=%d;c=%d"
set 1st argument of printf():
.text:00000024 move    $a0,$0
; set 2nd argument of printf():
.text:00000028 li      $a1,1
; set 3rd argument of printf():
.text:0000002c li      $a2,2
; set 4th argument of printf():
.text:00000030 li      $a3,3
```
