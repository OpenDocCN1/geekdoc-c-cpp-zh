
29 PARM DS F * PARM LIST
30 N1 DS F * DATA
32 FACT CSECT
33 STM R14,R12,12(R13) * SAVE REGS
34 BALR R12,R0 * EST BASE REG
35 USING *,R12 * EST BASE REG
37 LR R3,R1 * PRESERVE R1
38 * * ADDR OF PARM LIST
39 * * GETMAIN WILL ALTER R1
41 GETMAIN RU,LV=80 * GET 80 BYTES
42 * * ALTERS R1 AND R0
43 ST R1,8(R13) * PARENT -> US
44 ST R13,4(R1) * WE -> PARENT SAVE AREA
45 LR R13,R1 * ALLOC AREA NOW OUR SAVE
46 USING AUTO,R13 * POINT DSECT AT ALLOC MEM
47 LR R1,R3 * RESTORE R1
49 L R5,0(0,R1)
50 L R5,0(0,R5) * 1ST PARM -> R5
51 XDECO R5,0T1 MSG1,L'OT1+L'MS
52 XPRNT G1
53 C R5,=F'1' * END OF RECURSION?
54 BNE RECURS * NO
55 L R2,0(0,R1) * ADDR 1ST PARM -> R2
56 ST R5,0(0,R2) * STORE 1 in 1ST PARM
58 EXIT LR R1,R13 * ADDR ALLOC MEM
59 L R13,4(R13) * ADD SAVE AREA ABOVE
60 FREEMAIN RU,A=(1),LV=80 * RELEASE MEM
61 LM R14,R12,12(R13) * RESTORE REGS
62 BR 14 * RETURN
64 RECURS LR R6,R5 * COPY PARM -> R6
65 S R6,=F'1' * DECREMENT
66 ST R6,N1 * STORE AS OUR PARM
67 LA R7,N1 * ADDR OF PARM
68 ST R7,PARM * STORE ADDR TO PARM LIST
69 LR R3,R1 * PRESERVE PARENT PARM
70 LA R1,PARM * R1 -> PARM LIST

## 19.3.2 基于系统堆栈的链接

原始的 IBM 360 既没有硬件堆栈支持，也没有独立的指令和数据地址空间。在较新的版本中，这些功能在一定程度上被添加了。

链接堆栈于 1989 年引入，是系统提供的一种保存寄存器和其他系统状态信息的方式。使用链接堆栈的指令如 图 69 所示。

链接堆栈必须用于 AR（访问寄存器）地址空间控制（ASC）程序。在主模式下，CPU 使用通用寄存器计算地址，而在 AR 模式下，则使用访问寄存器的内容以及通用寄存器。本文仅涉及主 ASC 模式编程。AR 模式用于多个地址空间。对于非 AR（主）ASC 程序，它是可选的。

当分支并堆栈（BAKR）和程序调用（PC）指令执行时，它们会将所需的寄存器和状态保存到系统堆栈上。当程序返回（PR）执行时，它会恢复寄存器和状态。BAKR 除其他操作外，还会存储通用寄存器 2 到 14，而 PR 指令则恢复它们并分支到返回地址。

| 指令 | 助记符 | 类型 |
|---|---|---|
| 分支并堆栈 | BAKR | RSE |
| 提取堆栈寄存器 | EREG/EREGG | RRE |
| 提取堆栈状态 | ESTA | RRE |
| 修改堆栈状态 | MSTA | RRE |
| 程序调用 | PC | S |
| 程序返回 | PR | E |
| 测试访问 | TAR | RRE |

图 69 堆栈链接指令

### 19.3.2.1 系统堆栈链接示例

图 70 显示了使用系统堆栈计算的阶乘程序。用于访问堆栈的指令是分支并堆栈寄存器（BAKR）和程序返回（PR）。

BAKR 指令将通用寄存器和访问寄存器（当程序处于 AR 模式时用于访问替代虚拟内存数据空间）存储在链接堆栈上。第一个操作数包含返回地址。除非第二个操作数为零，否则会分支到第二个操作数。

PR 指令恢复调用程序的访问寄存器和通用寄存器 2 - 14，从链接堆栈中移除条目，并将控制权返回给调用程序。请注意，仅恢复通用寄存器和访问寄存器 2 到 14。

图 70 中的程序功能与图 69 中的非常相似，只是所有中间结果和最终结果都存储在寄存器中，而不是内存中。因此，该程序是可重入的。由于使用了系统堆栈，它也是递归的。

要计算阶乘的数字（5）在第 8 行加载到 R5 中，并在第 10 行和第 11 行调用 FACT 子程序。返回后，R1 中的值，即答案，被打印出来。FACT 在 R5 中接收其参数，并在 R1 中返回结果。

进入时，FACT 执行分支并堆栈寄存器，从而保存调用程序的寄存器。它建立一个基址寄存器并测试 R5 中传递的值是否为 1。如果不是，则分支到 RECURS。如果是，则将 R5（1）的内容复制到 R1 并执行程序返回（PR）指令。请注意，PR 不会改变 R1。

 1        PRINT     NOGEN
 2        EQU       
 3        MAIN      CSECT
 4        BAKR      R14,0                 * STACK CALLERS REGS
 5        BASR      R12,0                 * GET ABS ADDR
 6        USING     *,R12                 * EST BASE REG
 7
 8        L         R5,=F'5'              * FACTORIAL TO CALC
 9
10        L         R15,=V(FACT)           * CALL FCN
11        BASR      R14,R15               * CALL FCN
12
13        XDECO     R1,OUT
14        XPRNT     MSG,L'MSG'+L'OUT'
15        SR        R15,R15               * RETURN CODE ZERO
16        PR
17
18        LTORG
19 MSG    DC        C' FACTORIAL = '
20 OUT    DS        CL12
21
22 FACT   CSECT
23        BAKR      R14,0                 * STACK CALLERS REGS
24        BASR      R12,0                 * GET ABS ADDR
25        USING     *,R12                 * EST BASE REG
26
27        C         R5,=F'1'              * DONE?
28        BNE       RECURS                * NO
29        LR        R1,R5                 * ANS --> R1
30          PR
31
32 RECURS
    LR      R6,R5          * SAVE CRNT FACTOR
33    S       R5,=F'1'       * DECR FOR NEXT LEVEL
34    L       R15,=V(FACT)   * RECURSE
35    BASR    R14,R15
36
37    SR      R4,R4          * GET READY TO MULT
38    LR      R5,R6          * MULTIPLICAND
39    MR      R4,R1          * R1 RETRND FROM FCN
40    LR      R1,R5          * COPY ANS TO R1 FOR RETRN
41    PR                  * RESTORE REGS AND RETURN
42
43    LTORG
    END

输出:
5 FACTORIAL =          120

图 70 基于系统堆栈的链接

在 RECURS 处，程序将 R5 的输入值保存到 R6，递减 R5 并调用自身。返回后（第 36 行至第 40 行），它将 R4/R5 的内容乘以 R1（返回的值），将结果复制到 R1 并返回。

## 20. 调试 (XDUMP, SNAP)

转储是机器在某一瞬间状态相关的内存、寄存器、PSW 和其他信息的快照，通常以十六进制表示。转储显示的内存区域可以是当前正在运行的程序的，也可以更大。在计算的早期，转储是打印在纸上，可能长达数千页。现在它们被写入文件。

通常在程序遇到运行时异常或中断时产生转储。或者，程序员可以使用 ASSIST XDUMP 宏或系统宏 SNAP 显式请求转储。

在因错误而产生的转储情况下，程序会终止。当程序员请求转储时，通常出于诊断原因，程序是否终止由程序员自行决定。

例如，如果将图 47 中的程序修改为包含如 图 71 所示的 XDUMP，则结果是如 图 72 所示的文本（长行已截断）。

转储的内容包含以下一项或多项：

- 1. 16 个 64 位通用寄存器 R0 到 RF（R0 到 R15）的内容；
- 2. 16 个 64 位浮点寄存器 F0 到 FF（F0 到 F15）的内容；
- 3. 从地址 00000000₁₆ 到地址 000FFFFF₁₆ 的内存内容。
- 4. PSW。
- 5. 保存区回溯。

通用寄存器和浮点寄存器的内容以 16 位十六进制数字显示（对应 8 字节）。通常，每行显示四个寄存器。例如，通用寄存器的第一行显示 R0、R1、R2 和 R3，而最后一行显示寄存器 RC（R12）、RD（R13）、RE（R14）和 RF（R15）的内容。浮点寄存器（F0 到 FF）也显示类似的模式。

z390 模拟器预先将每个寄存器的每个字节初始化为 F4₁₆，因此如果程序仅使用 32 位指令，寄存器的高 32 位可能为 F4₁₆。寄存器的低 32 位在程序运行过程中未使用寄存器时将为 F4₁₆。
