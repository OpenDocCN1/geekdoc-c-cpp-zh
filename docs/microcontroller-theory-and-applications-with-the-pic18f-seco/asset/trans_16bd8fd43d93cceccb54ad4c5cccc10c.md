
- 考虑 TBLWT*- 指令。
    - 在执行 TBLWT* 指令前：[TBLPTR] = 0x000318，[TABLAT] = 0x24，[0x000318] = 0xF2。
    - 在执行 TBLWT* 指令后：[0x000318] = 0x24，[TBLPTR] = 0x000317，[TABLAT] = 0x24（保持不变）。
- 考虑 TBLWT+* 指令。
    - 在执行 TBLWT+* 指令前：[TBLPTR] = 0x000118，[TABLAT] = 0x24，[0x000119] = 0xF2。
    - 在执行 TBLWT+* 指令后：[0x000119] = 0x24，[TBLPTR] = 0x000119，[TABLAT] = 0x24（保持不变）。

## **示例 7.2** 在地址 0x100 处编写一个 PIC18F 汇编语言程序，将 BCD 数字 0 到 9 的 ASCII 码（从 30H 到 39H）从程序存储器中地址 0x200 开始的位置（地址 0x200 为 30H，地址 0x201 为 31H，依此类推）移动到数据存储器中地址 0x40 开始的位置（将 30H 存储在地址 0x40，将 31H 存储在地址 0x41，依此类推）。

## **解答**

```
INCLUDE <P18F4321.INC>  ORG 0x100 ;#1 程序的起始地址  COUNTER EQU 0x20  MOV LW UPPER_ADDR ;#2 将地址的高 5 位 (00H)  MOV WF TBLPTRU ;#3 移动到 TBLPTRU  MOV LW HIGH_ADDR ;#4 将地址的第 15-8 位 (02H)  MOV WF TBLPTRH ;#5 移动到 TBLPTRH  MOV LW LOW_ADDR ;#6 将地址的第 7-0 位 (00H)  MOV WF TBLPTRL ;#7 移动到 TBLPTRL  LFSR 0, 0x40 ;#8 将 FSR0 初始化为 0x40，用作 ; 数据存储器中的目标指针  MOV LW D'10' ;#9 将 COUNTER 初始化为 10  MOV WF COUNTER ;#10 将 [WREG] 移动到 COUNTER  LOOP TBLRD*+ ;#11 从程序存储器读取数据到 ; TABLAT，并将 TBLPTR 加 1  MOV F TABLAT, W ;#12 将 [TABLAT] 移动到 WREG  MOV WF POSTINC0 ;#13 将 W 移动到由 FSR0 指向的数据存储器地址，; 然后将 FSR0 加 1  DEC F COUNTER, F ;#14 COUNTER 减 1  BN Z LOOP ;#15 如果 Z = 0 则分支跳转，否则停止  FINISH BRA FINISH ; 停止  ORG 0x200 ; 在程序存储器中存储 ASCII 码  ADDR DB 30H, 31H, 32H, 33H, 34H, 35H, 36H, 37H, 38H, 39H  END
```

在上述程序中，# 符号及其行号放在注释之前，以便识别用于解释的具体行。请注意，程序末尾使用标签 ADDR 和指令 DB 将 BCD 数字的 ASCII 码存储在从地址 0x200 开始的程序存储器中。

## 表 7.4 PIC18F 子程序指令

| 指令 | 操作 |
| :--- | :--- |
| CALL k,s | 调用位于 2MB 程序存储器中地址 k 处的子程序。首先，返回地址 (PC + 4) 被压入返回堆栈。如果 's' = 1，WREG、STATUS 和 BSR 寄存器也会被压入其各自的影子寄存器（CPU 内部寄存器）WS、STATUSS 和 BSRs。如果 's' = 0，这些寄存器不受影响（默认情况）。然后，值 'k' 被加载到 PC 中。 |
| POP | 丢弃由 SP 指向的堆栈顶部，并将 STKPTR 减 1。 |
| PUSH | 将 PC 推入堆栈，并将 STKPTR 加 1。 |
| RETFIE | 从中断返回。堆栈弹出，堆栈顶部 (TOS) 被加载到 PC 中。通过设置高优先级或低优先级全局中断使能位来使能中断。该指令通常用于中断服务例程的末尾。 |
| RETLW k | 将 8 位立即数 'k' 加载到 WREG 中。程序计数器从硬件堆栈顶部（返回地址）加载。 |
| RETURN s | 从子程序返回。堆栈弹出，堆栈顶部 (TOS) 被加载到程序计数器中。如果 's' = 1，影子寄存器 WS、STATUSS 和 BSRs 的内容被加载到其对应的寄存器 WREG、STATUS 和 BSR 中。如果 's' = 0，这些寄存器不受影响（默认情况）。 |

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_176_0.png)

图 7.3 (a) PIC18F 硬件堆栈，执行 POP 指令前包含任意数据

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_176_1.png)

图 7.3 (b) PIC18F 硬件堆栈，执行 POP 指令后包含任意数据；假设地址 0x15 为空

第 1 行指定程序的起始地址为 0x000200。注意，程序员不需要定义 TABLAT 的地址 0xFF5。这是由 Microchip 预定义的地址（特殊功能寄存器）。MPLAB 汇编器在内部确定此地址。如前所述，TBLPTR 分为三个寄存器：TBLPTRU（预定义地址 0xF8）、TBLPTRH（预定义地址 0xF7）和 TBLPTRL（预定义地址 0xF6）。这些也是特殊功能寄存器。MPLAB 汇编器在内部确定这些地址。此外，MPLAB 汇编器将 TBLPTRU 识别为 UPPER，将 TBLPTRH 识别为 HIGH，将 TBLPTRL 识别为 LOW。第 2 行至第 7 行将 TBLPTR 初始化为 21 位地址 0x000200。

第 8 行将数据存储器指针 FSR0 初始化为 0x40。第 9 行和第 10 行将 COUNTER 初始化为 10。第 11 行从由 TBLPTR 寻址的程序存储器中读取一个字节到 TABLAT，然后将 TBLPTR 加 1。第 12 行将 TABLAT 的内容移动到 WREG。第 13 行将 [WREG] 移动到由 FSR0 指向的目标数据存储器地址，然后将 FSR0 加 1。第 14 行将 [COUNTER] 减 1。第 15 行的 BNZ 检查 Z 标志，如果 Z = 0，则执行 10 次 LOOP 循环，因此，ASCII 码 30H 到 39H 从程序存储器传输到数据存储器。

# 7.4 PIC18F 子程序指令

表 7.4 列出了 PIC18F 子程序指令。这些指令包括 PUSH/POP 和子程序 CALL/RETURN 指令。子程序指令自动使用制造商实现的“硬件堆栈”。如果需要存储局部变量，程序员可以创建“软件堆栈”。将在下一节中详细讨论“硬件堆栈”和“软件堆栈”。

- CALL 和 RETURN 指令需要两个周期执行。
- POP 和 PUSH 指令需要一个周期执行。
- 除 CALL 指令外，每条指令的大小为一个字；CALL 指令的大小为两个字。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_177_0.png)

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_177_1.png)

- POP 指令从返回堆栈中读取（弹出）堆栈顶部（TOS）值并将其丢弃；[STKPTR] 减 1。TOS 值变为之前压入返回堆栈的值。

作为一个例子，考虑带有数值的 POP 指令：
在执行 POP 之前：[STKPTR] = 0x15，[0x15] = TOS (堆栈顶部) = 0x000080，堆栈（下一层），[0x14] = 0x000150
在执行 POP 之后：[STKPTR] = 0x14，[0x14] = 0x000150
注意，尽管 0x000080 物理上是 0x15 的内容，但之前的 TOS (0x000080) 被丢弃，而之前的堆栈（下一层）变成了当前的 TOS。
图 7.3 (a) 和 (b) 描绘了这一点。

- PUSH 指令将 PC+2 写入（压入）返回堆栈顶部；[STKPTR] 加 1。之前的 TOS 值被压入堆栈的下一层。

作为一个例子，考虑带有数值的 PUSH 指令：
在执行 PUSH 之前：[STKPTR] = 0x14，[0x14] = TOS (堆栈顶部) = 0x00007C，[PC+ 2] = 0x0000A4；即 PUSH 指令存储在地址 0x0000A2。
在执行 PUSH 之后：[STKPTR] = 0x15，[0x15] = TOS = 0x0000A4，之前的 TOS (下一层)，[0x14] = 0x00007C。图 7.4 (a) 和 (b) 描绘了这一点。

- “CALL k, s” 指令当 s = 0 时（或 CALL k）是调用子程序的最简单方式；s = 0 是默认情况。例如，CALL START 指令自动将当前 PC 的内容压入堆栈，并将标签 START 的地址加载到 PC 中。注意，地址 START 包含子程序的起始地址。“RETURN s” 指令当 s = 0 时（或者 RETURN，因为 s = 0 是默认的）从 TOS 弹出返回地址（由 CALL START 指令压入堆栈的 PC），并将此地址加载到 PC 中。因此，控制权返回到主程序，程序执行继续执行 CALL START 后面的指令。
考虑以下 PIC18F 程序段：

## 表 7.5 PIC18F 系统控制指令

| 指令 | 操作 |
| :--- | :--- |
| CLRWDT | 清除看门狗定时器为 0。 |
| RESET | 将所有寄存器和标志位重置为它们的“硬件复位”值。硬件 RESET 在激活 PIC18F 输入引脚时执行。RESET 指令提供软件复位。 |
| SLEEP | PIC18F 进入睡眠模式，振荡器停止。 |
| NOP | 空操作 |

- 上述所有指令在一个周期内执行。
- 每条指令的大小为一个字。

