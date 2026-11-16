

2,147,484 并将其代入 Cr 公式，我们得到的值为 4,294,967,999，这比 2^32 - 1 大 704。因此，我们可以在 wait_ms 子程序中使用 20MHz 和 2,147,483 毫秒的值，但如果使用 20MHz 和 2,147,484 或更大的值，我们的 wait_ms 子程序将会失败。

## 在汇编语言中设置值限制

在汇编语言代码中对固定值设置限制的常见方法是使用汇编器指令来检测限制，并在超出范围时生成错误或警告。添加到 wait_ms_asm 项目的 wait_ms.asm 文件顶部的以下代码展示了此操作。

```
wait_ms.asm : wait_ms.asm - top part of code
; Millisecond delay subroutine - time set by MS_TIME_DEL
.equ WAIT_MS_CYCLES = (((F_CPU * MS_TIME_DEL) / 1000) - 10) / 10
.if (WAIT_MS_CYCLES > (exp2(32) - 1))
    .error "F_CPU MS_TIME_DEL combination out of range in wait_ms subroutine."
.endif
wait_ms:
ldi R16, low (WAIT_MS_CYCLES)
ldi R17, byte2(WAIT_MS_CYCLES)
ldi R18, byte3(WAIT_MS_CYCLES)
ldi R19, byte4(WAIT_MS_CYCLES)
...
...
```

对 wait_ms.asm 代码顶部所做的第一个修改是为计算 wait_ms 函数生成周期数的公式命名。该名称为 WAIT_MS_CYCLES，并在代码顶部如下等式定义。

```
.equ WAIT_MS_CYCLES = (((F_CPU * MS_TIME_DEL) / 1000) - 10) / 10
```

这仅仅意味着每当使用 WAIT_MS_CYCLES 时，都会替换公式的结果。因此，WAIT_MS_CYCLES 被放置在 wait_ms 子程序顶部的每个先前放置公式的位置，如下所示。

```
wait_ms:
ldi R16, low (WAIT_MS_CYCLES)
ldi R17, byte2(WAIT_MS_CYCLES)
ldi R18, byte3(WAIT_MS_CYCLES)
ldi R19, byte4(WAIT_MS_CYCLES)
```

既然公式结果可以轻松地作为 WAIT_MS_CYCLES 使用，汇编器指令就用于检测该值是否超出范围。这是通过以下代码完成的。

```
.if (WAIT_MS_CYCLES > (exp2(32) - 1))
    .error "F_CPU MS_TIME_DEL combination out of range in wait_ms subroutine."
.endif
```

在上述代码中，.if 指令用于确定由公式计算并等同于 WAIT_MS_CYCLES 的 32 位值是否在范围内。我们知道，32 位数字可以具有的最大值是 2^32 - 1。AVR 汇编器程序支持一个名为 exp2() 的函数，用于计算传递给它的数字的 2 次幂。在代码中，exp2() 用于通过传递 32 来计算最大 32 位值。然后从结果中减去 1，这给出了 32 位数字可以容纳的最高数字。换句话说，以下代码计算 2^32 - 1。

```
(exp2(32) - 1)
```

在 .if 指令后的括号中，使用大于运算符 (>) 来确定 WAIT_MS_CYCLES 的值是否大于上述计算的结果，如下所示。

```
.if (WAIT_MS_CYCLES > (exp2(32) - 1))
```

在上述代码行中，如果 WAIT_MS_CYCLES 小于 2^32 - 1，则 .if 指令和关闭的 .endif 指令之间的代码将被忽略。另一方面，如果 WAIT_MS_CYCLES 的值大于 2^32 - 1，则 .if 指令和 .endif 指令之间的代码将被执行。此代码包含 .error 指令，后跟一个文本字符串。.error 指令在 Microchip Studio 中标记错误，并打印紧随 .error 指令之后的文本字符串。此消息是我们自己的消息，用于描述问题所在。可以看出，该消息指出 wait_ms 子程序中的 F_CPU MS_TIME_DEL 组合超出范围，这对问题进行了很好的描述。我们可以使用计算出的限制来测试此代码。为避免任何混淆，wait_ms_asm 项目的完整修改代码如下。

### wait_ms_asm : main.asm

```
.equ  F_CPU       = 20000000
.equ  MS_TIME_DEL = 2147483   ; upper limit
.equ MS_TIME_DEL = 2147484   ; upper limit + 1

start:
    sbi   DDRB, DDB4        ; Set pin PB4 as output
loop:
    sbi   PORTB, PORTB4     ; Set LED pin high
    rcall wait_ms           ; LED on delay
    cbi   PORTB, PORTB4     ; Clear LED pin low
    rcall wait_ms           ; LED off delay
    rjmp  loop

.include "wait_ms.asm"
```

### wait_ms_asm : wait_ms.asm

```
; Millisecond delay subroutine - time set by MS_TIME_DEL
.equ  WAIT_MS_CYCLES = (((F_CPU * MS_TIME_DEL) / 1000) - 10) / 10
.if (WAIT_MS_CYCLES > (exp2(32) - 1))
.error "F_CPU MS_TIME_DEL combination out of range in wait_ms subroutine."
.endif

wait_ms:
    ldi   R16, low (WAIT_MS_CYCLES)
    ldi   R17, byte2(WAIT_MS_CYCLES)
    ldi   R18, byte3(WAIT_MS_CYCLES)
    ldi   R19, byte4(WAIT_MS_CYCLES)

wait_ms_loop:
    subi  R16, 1
    sbci  R17, 0
    sbci  R18, 0
    sbci  R19, 0
    mov   R20, R16
    or    R20, R17
    or    R20, R18
    or    R20, R19
    brbc  SREG_Z, wait_ms_loop
    nop
    nop
    nop
    ret
```

main.asm 代码已设置为为 F_CPU 使用 20MHz 的值，并且 MS_TIME_DEL 的最大值设置为我们计算出的最大值 2,147,483。使用这些值时，我们预期 wait_ms.asm 文件中的 .if 指令将评估为 false，并且不会打印错误消息。按照前面的清单修改 wait_ms.asm 项目中的代码后，构建项目，Microchip Studio 中不应出现错误消息。

当 MS_TIME_DEL 的值递增到 2,147,483 以上（例如 2,147,484）时，我们预期在构建项目时会在 Microchip Studio 中看到错误。将 main.asm 顶部中 MS_TIME_DEL 等于 2,147,483 的第一个实例注释掉，并取消注释下方将其等于 2,147,484（比最大限制大 1）的第二个 MS_TIME_DEL 实例。保存更改并构建项目。Microchip Studio 现在会标记错误，因为 .if 指令评估为 true，并且 .error 指令标记错误。双击 Microchip Studio 底部的错误消息将打开 wait_ms.asm 文件，并将光标置于包含 .error 指令和消息的行上。

## 汇编器程序中的数字大小限制

有了前面的解释，在理想世界中，用于在代码中为超出限制的值标记错误的机制似乎直观且可靠。在现实世界中，值受到限制，因此使用超过我们迄今所用基本测试值的值彻底测试所有实际代码非常重要。对前面代码的进一步测试表明，当某些值被赋给 MS_TIME_DEL 时，.if 指令处的错误消息不会在应该触发时触发。例如，将 WAIT_MS_CYCLES 设置为 3221225 会导致错误消息按预期触发。将 3221226（比前一个值大 1）赋给 WAIT_MS_CYCLES，在构建代码时不会触发错误消息。事实证明，此问题的原因是 AVRASM2 汇编器程序中的整数大小限制。导致上述问题的限制不止一个。首先，如果 exp2() 函数传递值 32，则无法正常工作。我们预期 exp2(32)（即 2^32）将结果为 0x100000000，但它实际上结果为 1，如以下代码所示。

```
.if (1 == exp2(32))
.warning "Numbers are equal: 1 == exp2(32)."
.endif
```

将上述代码添加到项目的源代码中会在构建项目时生成警告消息，证明 exp2(32) 评估为 1。代码中的 == 运算符与 C 中的工作方式相同，用于测试左侧的值是否等于右侧的值，如果相等，则打印警告消息。

除上述内容外，使用 .equ 或 #define 指令时，整数（整数）值将被截断为 32 位，如以下代码所示。

```
.equ NUM1 = 0x0000000F    ; 32-bit number (15)
.equ NUM2 = 0x100000000   ; 33-bit number (4,294,967,296)

.if (NUM1 > NUM2)
.warning "NUM1 is greater than NUM2."
.endif
```

在上述代码中，使用 .equ 为 NUM1 赋予一个小值，并以同样的方式为 NUM2 赋予一个非常大的值，注释中显示了十进制值。.if 指令处的比较永远不应该评估为 true，因为 NUM2 大于 NUM1，而不是反过来。比较之所以评估为 true，是因为 NUM2 被截断为 32 位数字，这意味着它丢失了最高有效位。这导致其值为 0（零）。15 大于 0，这就是表达式评估为 true 的原因。我们可以使用以下代码证明 NUM2 被截断为 0。

```
.if (NUM2 == 0)
.warning "NUM2 is equal to 0."
.endif
```

在上述代码中，NUM2 被赋予与前面代码中相同的值，.if 指令处的表达式评估为 true，导致在构建项目时打印警告消息。这证明 NUM2 被截断为 32 位，结果值等于 0。

使用与前面代码相同的值，但将值直接放在比较中，而不是使用 .equ 或 #define 分配名称，比较将按预期工作。在以下代码中直接比较分配给 NUM1 和 NUM2 的值会产生预期的 false 结果，并且不会触发警告消息。

```
.if (0x0000000F > 0x100000000)
.warning "0x0000000F is greater than 0x100000000."
.endif
```

