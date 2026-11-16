

## 10.2.2 更好的软件延迟子程序

下面的清单中包含了一个改进的软件延迟子程序，作为 led_blink_asm 代码的一部分。这个新程序现在称为 wait_1s_asm，包含一个名为 wait_1s 的子程序，用于精确延迟一秒。在清单顶部，必须将代码将要运行的 AVR 频率分配给 F_CPU。可以看到，提供了两个频率，其中一个被注释掉了。这些当然分别对应 ATtiny25/45/85 和 ATtiny13(A) 的默认频率 1MHz 和 1.2MHz。当代码顶部正确设置频率时，连接到引脚 PB4 的 LED 在主循环中的代码运行时会保持亮起 1 秒。

```
wait_1s.asm : main.asm

; .equ F_CPU = 1000000
.equ F_CPU = 1200000

start:
    sbi DDRB, DDB4    ; Set pin PB4 as output

loop:
    sbi PORTB, PORTB4 ; Set LED pin high
    rcall wait_1s     ; LED on delay
    cbi PORTB, PORTB4 ; Clear LED pin low
    rcall wait_1s     ; LED off delay
    rjmp loop

; 1 second delay subroutine
wait_1s:
    ldi R16, low ((F_CPU - 10) / 10) ; Load number of loop cycles
    ldi R17, byte2((F_CPU - 10) / 10) ; to registers R16 to R19
    ldi R18, byte3((F_CPU - 10) / 10)
    ldi R19, byte4((F_CPU - 10) / 10)

wait_1s_loop:
    subi R16, 1    ; Perform decrement on 32-bit
    sbci R17, 0    ; number in R16 to R19
    sbci R18, 0
    sbci R19, 0
    mov R20, R16   ; Determine if 32-bit number is
    or R20, R17    ; zero using OR and BRBC
    or R20, R18
    or R20, R19
    brbc SREG_Z, wait_1s_loop ; Balance BRBC to 2 clock cycles
    nop            ; Balance instructions outside of
    nop            ; loop to 10 clock cycles
    ret
```

### 10.2.2.1 工作原理

wait_1s 子程序的工作原理是递减一个 32 位数字直到其为零，以浪费足够的时间来产生所需的 1 秒延迟。如果微控制器运行的频率为 1MHz，则子程序必须消耗一百万个时钟周期来创建 1 秒的时间延迟。这是因为 1MHz 是每秒一百万个周期，意味着在此频率下，一百万个周期需要一秒钟才能完成。

本书中使用的一些 ATtiny 微控制器的最高时钟频率可达 20MHz。由于频率以赫兹（Hz）为单位进行测量，即每秒的时钟周期数，而 wait_1s 子程序用于延迟 1 秒，因此 1 秒延迟所需消耗的时钟周期数等于微控制器运行的频率。对于最高频率 20MHz，必须完成 2000 万个时钟周期才能消耗 1 秒。如果微控制器以 1.2MHz 运行，则必须完成 120 万个周期才能消耗一秒钟，以此类推，适用于所使用的任何频率。代码顶部的 F_CPU 必须更改为微控制器运行的频率，以便 wait_1s 子程序能正确延迟 1 秒。

### 10.2.2.2 使用 8 位寄存器进行 32 位减法

为了在 8 位处理器上对 32 位数字进行减法运算，需要四个 8 位寄存器来存储该 32 位数字。在 wait_1s 子程序中，寄存器 R16、R17、R18 和 R19 用于存储要减去的 32 位数字。如果减法过程只需要一个时钟周期，那么我们只需将微控制器运行的频率值加载到这些寄存器中，如下所示。

```
ldi   R16, low (F_CPU)
ldi   R17, byte2(F_CPU)
ldi   R18, byte3(F_CPU)
ldi   R19, byte4(F_CPU)
```

在上述代码中，我们有熟悉的 low() 汇编函数，用于获取 F_CPU 值的低字节。此代码中新增的是 byte2()、byte3() 和 byte4()，它们的工作方式与 low() 相同，但用于获取 32 位数字的第二、第三和第四个字节。这些函数在 AVR 汇编器文档中。因此，上述代码的作用是按顺序将 F_CPU 的值逐字节加载到 R16、R17、R18 和 R19 中，从最低有效字节开始，一直到最高有效字节。事实证明，减法过程需要多个时钟周期。因此，wait_1s.asm 清单中的代码并不直接将 F_CPU 的值加载到寄存器中，而是进行一些数学补偿，这将在下一节中解释。

实际减法由一条 SUBI（立即数减法）指令和三条 SBCI（带进位的立即数减法）指令执行，如下面的代码所示。

```
subi R16, 1    ; Perform decrement on 32-bit
sbci R17, 0    ; number in R16 to R19
sbci R18, 0
sbci R19, 0
```

上述代码是第 7 章第 7.2.2 节中加法的对应版本，其中使用一条 ADD（不带进位加法）指令和一条 ADC（带进位加法）指令来相加两个 16 位数字并考虑进位。在上面所示的此代码的负数版本中，减法只是扩展到对四个寄存器进行操作。在此代码中，SUBI 指令从 R16（即最低有效字节 LSB）中减去 1。然后使用 SBCI 指令从 R17、R18 和 R19 中减去 0。由于该指令会考虑减法产生的任何进位，因此只有在发生进位时，R17、R18 和 R19 才会递减。这有效地允许分布在四个寄存器上的 32 位数字在每次循环中递减 1。

循环中代码的最后部分用于确定 R16 到 R19 中的 32 位数字是否为零。这是通过使用逻辑 OR 操作来完成的，该操作将 R16、R17、R18 和 R19 进行 OR 运算，如下面的清单所示。如果这些寄存器中有任何一个包含非零数字，则 OR 运算的结果不为零，这会导致 BRBC 指令跳回到循环顶部并执行另一次递减。

```
mov R20, R16    ; Determine if 32-bit number is
or R20, R17     ; zero using OR and BRBC
or R20, R18
or R20, R19
brbc SREG_Z, wait_1s_loop
```

由于 AVR OR 指令具有破坏性，即它将 OR 运算的结果放入第一个寄存器并覆盖其内容，因此需要一个额外的寄存器来存储 OR 运算的结果。R20 是上述代码中用于存储 OR 运算结果的寄存器。首先，使用 MOV（复制寄存器）指令将 R16 中的值复制到 R20。之后，R17、R18 和 R19 依次与 R20 进行 OR 运算，R20 保存 OR 运算的累积结果。由于 R20 用于存储每个结果，R16 到 R19 中的值从未被修改或覆盖。在一系列 OR 运算完成后，只有当 R16 到 R19 全部包含零时，状态寄存器中的零位才会被置位。这会导致程序执行继续在 BRBC 指令下方进行。如果这些寄存器中有任何一个不包含零，BRBC 将跳转到循环顶部。

### 10.2.2.3 代码时序

现在我们了解了 wait_1s 子程序的基本工作原理，可以检查该子程序中使用的指令的时序。下面重复了代码，显示每条指令使用的时钟周期数。

```
wait_1s:
ldi    R16, low  ((F_CPU - 10) / 10)   ; 1 clock cycle
ldi    R17, byte2((F_CPU - 10) / 10)   ; 1 clock cycle
ldi    R18, byte3((F_CPU - 10) / 10)   ; 1 clock cycle
ldi    R19, byte4((F_CPU - 10) / 10)   ; 1 clock cycle

wait_1s_loop:
subi   R16, 1                          ; 1 clock cycle
sbci   R17, 0                          ; 1 clock cycle
sbci   R18, 0                          ; 1 clock cycle
sbci   R19, 0                          ; 1 clock cycle
mov    R20, R16                        ; 1 clock cycle
or     R20, R17                        ; 1 clock cycle
or     R20, R18                        ; 1 clock cycle
or     R20, R19                        ; 1 clock cycle
brbc   SREG_Z, wait_1s_loop            ; 1 clock cycle
nop                                  ; 1 clock cycle
nop                                  ; 1 clock cycle
nop                                  ; 1 clock cycle
ret                                  ; 4 clock cycles
```

如代码所示，每条指令只需要一个时钟周期，除了 BRBC 指令和 RET 指令。如我们所知，当 BRBC 指令分支到循环顶部时需要两个时钟周期，而不分支时只需要一个时钟周期。为了有效地使此指令始终消耗两个时钟周期，在其下方放置了一条 NOP 指令。这意味着当 BRBC 不分支时，它会执行下方的 NOP 指令，从而有效地消耗两个时钟周期而不是一个。

循环中的指令（在上述清单中以粗体显示）总共需要 10 个时钟周期。BRBC 下方的 NOP 指令包含在此总数中，因为它有效地导致 BRBC 的最终执行仍然消耗两个时钟周期。在将 F_CPU 加载到子程序顶部的 R16 到 R19 之前，必须先将其除以这 10 个时钟周期。这是因为循环中的减法过程消耗了这 10 个时钟周期，如果不补偿这 10 个时钟周期，子程序将花费 10 倍的时间。

除了循环中使用的时钟周期外，循环前后还使用了时钟周期。wait_1s 开头的 LDI 指令使用了四个时钟周期。

