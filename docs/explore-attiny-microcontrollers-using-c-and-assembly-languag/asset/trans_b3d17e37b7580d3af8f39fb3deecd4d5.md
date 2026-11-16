

前一行 C 代码由 C 编译器转换为以下汇编语言行：

```
sbi DDRB, DDB4
```

这个特定的示例恰好从一行 C 代码转换为一行汇编语言代码。在其他情况下，一行 C 代码可能转换为多行汇编代码。在本节中，我们查看 C 编译器和链接器从 led_count.c 项目生成的汇编语言代码，以及实际加载到 AVR Flash 内存中的代码。虽然最终加载到 Flash 内存的是二进制机器码，但我们查看的是对这些机器码指令进行反汇编后的汇编语言代码。这是在 Microchip Studio 的调试器中完成的。使用“开始调试并中断”（Start Debugging and Break）启动调试器，可以使用实际硬件和硬件编程器/调试器，也可以使用模拟器。调试器启动后，从顶部菜单选择 Debug ▶ Windows ▶ Disassembly，或使用键盘快捷键 Alt + 8——第二个工具栏上也有一个 Disassembly 图标。打开反汇编窗口后，反汇编代码将在 Microchip Studio 中显示。以下列表显示了针对 ATtiny13(A) 的这部分反汇编代码的第一部分。

```
--- No source file ---
00000000 RJMP PC+0x000A Relative jump
00000001 RJMP PC+0x000F Relative jump
00000002 RJMP PC+0x000E Relative jump
00000003 RJMP PC+0x000D Relative jump
00000004 RJMP PC+0x000C Relative jump
00000005 RJMP PC+0x000B Relative jump
00000006 RJMP PC+0x000A Relative jump
00000007 RJMP PC+0x0009 Relative jump
00000008 RJMP PC+0x0008 Relative jump
00000009 RJMP PC+0x0007 Relative jump
0000000A RJMP PC+0x0006 Relative jump
--- /.../ : </crt1/gcrt1.S
0000000A CLR R1 Clear Register
0000000B OUT 0x3F,R1 Out to I/O location
0000000C LDI R28,0x9F Load immediate
0000000D OUT 0x3D,R28 Out to I/O location
0000000E RCALL PC+0x0003 Relative call subroutine
0000000F RJMP PC+0x00012 Relative jump
00000010 RJMP PC-0x0010 Relative jump
```

反汇编窗口显示来自 Flash 内存的反汇编代码。顶部是由 C 工具自动插入的中断向量表。我们在此不详细介绍中断。目前只需知道，中断向量表中的第一个条目是复位向量。该位置的指令只是导致跳转到 C 代码的入口点。当 AVR 上电或复位时，它首先运行此指令，这会导致程序跳过其余的向量表条目，并从头开始运行 C 代码。其他向量表条目也会导致程序跳转到复位向量，但首先是跳转到另一条跳转指令。代码列表显示了反汇编的前两个部分。请注意，此代码是为 ATtiny13(A) 构建的，它有一个较小的中断向量表，包含从地址 0 到地址 9 的 10 个条目。如果为 ATtiny25/45/85 构建相同的代码，您会注意到向量表有 15 个条目，从地址 0 到 14（0x000E）。每条汇编语言指令左侧是该指令在 Flash 程序内存中的地址。查看反汇编中的第一个条目，我们在地址 0 处有复位向量，旁边是一条 RJMP 指令，如下所示。

```
00000000 RJMP PC+0x000A Relative jump
```

可以看出，这条相对跳转指令跳转到 PC + 0x000A 处的地址，即当前程序计数器（PC）值加上 0x000A。复位时，PC 包含零，因此第一条跳转指令跳转到地址 0x000A。在反汇编列表中，CLR R1 位于 grc1.S 部分的地址 0x000A 处。中断向量表其余部分（从地址 0x0001 到 0x0009）也包含相对跳转指令，它们都跳转到地址 0x0010。在地址 0x0010 处，还有一条 RJMP 指令，它向后跳转 0x10 个地址，由地址旁边的负号指示，如下所示。

```
00000010 RJMP PC-0x0010 Relative jump
```

0x10 是十进制的 16，从当前地址 0x10 向后 16 个地址是 0，即向量表地址 0 处的复位向量。这意味着，如果触发任何中断，程序执行将简单地从地址 0 重新开始。在前面的反汇编列表中，代码的第二部分来自 grc1.S，如列表所示。此代码由 C 工具自动链接。在 grc1.S 名称中，crt 代表 C Runtime，即在调用 C main() 函数之前执行所需初始化的代码。C 运行时代码首先清除状态寄存器，即先清除 R1，然后将 R1 加载到地址 0x3F（即状态寄存器），如下所示。

```
0000000A CLR R1 Clear Register
0000000B OUT 0x3F,R1 Out to I/O location
```

在 ATtiny13(A) 和 ATtiny25/45/85 数据手册的 Register Summary 部分中，SREG（状态寄存器）位于表顶部的地址 0x3F 处。清除状态寄存器后，C 运行时代码将堆栈指针设置为指向 SRAM 数据内存的末尾。对于 ATtiny13(A)，这是 0x9F——内存映射请参阅第 5 章中的图 5.3。如以下代码所示，0x9F 被加载到寄存器 R28。然后将 R28 加载到地址 0x3D，即 SPL（堆栈指针低寄存器）。

```
0000000C LDI R28,0x9F      Load immediate
0000000D OUT 0x3D,R28      Out to I/O location
```

最后，使用 Relative Call to Subroutine RCALL 指令调用 main()，如下所示。

```
0000000E RCALL PC+0x0003   Relative call subroutine
```

这会跳转到地址 PC + 0x0003，即当前地址 0x000E + 3，换句话说是地址 0x0011。如以下反汇编列表的其余部分所示，地址 0x0011 是 main() 内的第一条指令。列表的其余部分显示了混合了转换为的汇编语言的 C 代码。

```
--- C: \ ... ... ... ./.../main.c
{
    uint8_t count = 0;        // Clear count

    // Set up pins PB0 to PB4 as output pins
    DDRB = 0b00011111;
00000011 LDI R24,0x1F         Load immediate
00000012 OUT 0x17,R24        Out to I/O location

    uint8_t count = 0;        // Clear count
00000013 LDI R24,0x00        Load immediate
00000014 PORTB = count;      // Display count on LEDs
00000014 OUT 0x18,R24        Out to I/O location
--- C: \ ... ... ... ./.../delay.h
--- builtin_avr_delay_cycles(__ticks__dc);
00000015 LDI R18,0xF7        Load immediate
00000016 LDI R19,0xA9        Load immediate
00000017 LDI R25,0x03        Load immediate
00000018 SUBI R18,0x01       Subtract immediate
00000019 SBCI R19,0x00       Subtract immediate with carry
0000001A SBCI R25,0x00       Subtract immediate with carry
0000001B BNE PC-0x03         Branch if not equal
0000001C RJMP PC+0x0001      Relative Jump
0000001D NOP                 No operation
--- C: \ ... ... ... ./.../main.c
count++;                     // Increment count
0000001E SUBI R24,0xFF       Subtract immediate
0000001F count &= 0b00011111; // Clear unused bits
0000001F ANDI R24,0x1F       Logical AND with immediate
00000020 RJMP PC-0x000C      Relative Jump
```

对上述列表进行顶层查看可发现，来自 delay.h 的延迟库函数代码被放置在 main.c 代码的中间。在反汇编代码的开头，可以看出该代码与 led_count_asm 项目代码相似。0x1F 被加载到 R24，然后使用 OUT 指令发送到地址 0x17，如下所示，C 代码行显示在其转换为的两行汇编语言之上。

```
DDRB = 0b00011111;
00000011 LDI R24,0x1F Load immediate
00000012 OUT 0x17,R24 Out to I/O location
```

0x17 是 DDRB 寄存器的地址，如数据手册的 Register Summary 部分所示。这两行代码执行与 led_count_asm 项目中前两行代码相同的功能，只不过上述代码使用 R24 和十六进制表示法，而 led_count_asm 项目使用 R16 和二进制表示法。

在地址 0x0013 处的下一行代码中，R24 用作 count 变量，并设置为初始值零，如下所示。

```
uint8_t count = 0; // Clear count
00000013 LDI R24,0x00 Load immediate
```

上述代码行是从显示在其上方的一行 C 代码转换而来。请注意，C 编译器将此行代码放在 DDRB 寄存器初始化之后。在原始 C 源代码中，count 变量在 DDRB 初始化之前声明并初始化。通过更改这些代码行的顺序，R24 首先用于初始化 DDRB，然后再次用作 count 变量。

在地址 0x0014 处，R24 中的 count 值被写入地址 0x18，即 PORTB 寄存器。再次，PORTB 的地址在数据手册的 Register Summary 部分中找到。此行代码将 0（R24 中的 count 值）写入 LED，将其关闭，并从显示在其上方的一行 C 代码转换而来。

```
PORTB = count; // Display count on LEDs
00000014 OUT 0x18,R24 Out to I/O location
```

接下来将运行地址 0x0015 到 0x001D 的代码，即 _delay_ms() 函数，它会创建延迟，使当前计数值在 LED 上显示一段时间。

Subtract Immediate (SUBI) 用于将计数寄存器 R24 加一。代码通过从 R24 减去 -1 来实现这一点，这等同于向 R24 加 1。这是通过从 R24 减去 -1 来完成的，-1 采用 2 的补码格式。-1 在两的补码中

