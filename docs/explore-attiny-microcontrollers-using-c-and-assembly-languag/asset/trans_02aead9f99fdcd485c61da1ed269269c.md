

wait_ms.asm : wait_ms.asm

```asm
; Millisecond delay subroutine - delay time set by MS_TIME_DEL
; F_CPU must be set to the frequency that the AVR is operating at

.if (F_CPU > 20000000)
.error "F_CPU too high for wait_ms subroutine. Maximum 20MHz"
.elif (F_CPU < 210000)
.error "F_CPU too low for wait_ms subroutine. Minimum 210kHz"
.elif (MS_TIME_DEL < 1)
.error "MS_TIME_DEL too low for wait_ms subroutine. Minimum 1ms"
.elif (((((MS_TIME_DEL * 1000) - 10) / 10) > 0xFFFFFFF)
// Maximum MS_TIME_DEL is 2,147,483s @ 20MHz and 204,522,525 @ 210kHz
// Maximum MS_TIME_DEL calculated by: (10,000 * 2^32) / F_CPU
.error "MS_TIME_DEL too big for wait_ms subroutine."
.endif

.equ WAIT_MS_CYCLES = ((((F_CPU * MS_TIME_DEL) / 1000) - 10) / 10)

wait_ms:
ldi R16, low (WAIT_MS_CYCLES)
ldi R17, byte2(WAIT_MS_CYCLES)
ldi R18, byte3(WAIT_MS_CYCLES)
ldi R19, byte4(WAIT_MS_CYCLES)

wait_ms_loop:
subi R16, 1
sbci R17, 0
sbci R18, 0
sbci R19, 0
mov R20, R16
or R20, R17
or R20, R18
or R20, R19
brbc SREG_Z, wait_ms_loop
nop
nop
ret
```

在上述代码中，使用 .if 指令对上下限进行测试，后面跟着若干个 .elif 指令。.elif 指令的意思是“否则如果”。从代码顶部开始，测试内容为：1) 如果 F_CPU 大于 20MHz，则标记错误；2) 否则如果 F_CPU 小于 210kHz，则标记错误；3) 否则如果 MS_TIME_DEL 小于 1ms，则标记错误；4) 否则如果 WAIT_MS_CYCLES 计算结果过大，则标记错误。由于 .elif 指令的使用方式，发现的第一个错误将停止构建过程。修复错误后，程序员可以再次构建项目。如果还有其他错误，将在项目第二次构建时被捕获，依此类推，直到所有限制错误都被纠正。

可以使用 wait_ms.asm 文件中的 wait_ms 子程序，结合项目 main.asm 中的以下代码进行测试。代码中放置了一些测试值，通过取消这些值的注释来测试上下限。最大和最小 F_CPU 值可以与各种 MS_TIME_DEL 值配合使用。每次只能取消一种类型值的注释，因此在测试新值时，请务必注释掉当前值。

```asm
main.asm : main.asm

.equ  F_CPU   = 20000000  ; Maximum frequency
.equ  F_CPU   = 20000001  ; Above maximum frequency
.equ  F_CPU   = 210000    ; Minimum frequency
.equ  F_CPU   = 209999    ; Below minimum frequency
.equ  MS_TIME_DEL = 1     ; Below minimum millisecond value
.equ  MS_TIME_DEL = 0     ; Millisecond value
.equ  MS_TIME_DEL = 2147483 ; Upper millisecond limit @ 20MHz
.equ  MS_TIME_DEL = 2147484 ; Upper millisecond limit + 1 @ 20MHz
.equ  MS_TIME_DEL = 20452252 ; Upper millisecond limit @ 210kHz
.equ  MS_TIME_DEL = 20452253 ; Upper millisecond limit + 1 @ 210kHz
.equ  MS_TIME_DEL = 0x4522523 ; Highest positive value in ms
.equ  MS_TIME_DEL = 0x7FFFFFFF ; Highest positive value in ms
.equ  MS_TIME_DEL = 0x80000000 ; Negative value after 1 added to above
.equ  MS_TIME_DEL = 0xFFFFFFFF ; -1

start:
sbi   DDRB, DDB4   ; Set pin PB4 as output

loop:
sbi   PORTB, PORTB4 ; Set LED pin high
rcall wait_ms       ; LED on delay
cbi   PORTB, PORTB4 ; Clear LED pin low
rcall wait_ms       ; LED off delay
rjmp  loop

.include "wait_ms.asm"
```

使用上述列表顶部的值测试代码，也可以尝试一些自己的值。记住在修改后保存文件，然后构建项目，以确保在预期时会标记错误，在不预期时不会标记错误。将 MS_TIME_DEL 设为 0 并测试 F_CPU 的上下限值，两种情况都会出现错误，符合预期。使用高于 20MHz 或低于 210kHz 的 F_CPU 值也会标记错误。在 F_CPU 为 20MHz 时，使用 20MHz 的最大 MS_TIME_DEL 加 1 会导致错误，但使用相同的 MS_TIME_DEL 值配合 20kHz 的 F_CPU 则不会导致错误，因为在较低频率下时间延迟可以大得多。你会注意到代码中我们计算出的上限 MS_TIME_DEL 测试值，以及一旦超过 0x7FFFFFFF 就会变为负值的值。

## 10.2.4 向子程序传递值

前一节开发的 wait_ms 子程序比之前的固定 1 秒子程序更有用，但仍有局限性。一旦设置，其延迟时间在代码中是固定的。每次在代码中使用它时，都会延迟相同的时间段。

修改 wait_ms 子程序代码，使其能够接收一个毫秒延迟值并据此延迟，所需精力不大。每次在代码中使用它时，都可以传递不同的值，并据此延迟相应的时间。

### 10.2.4.1 传递值的最简单方法

向子程序传递值的机制是将要传递的值放在已知位置，可以是内存或寄存器中。下面给出了 wait_ms_asm 项目的一个修改版，名为 wait_pass_val.asm，演示了向子程序传递值的最简单方法。

```asm
wait_pass_val.asm : wait_pass_val.asm

wait_pass_val:
  subi  R16, 1
  sbci  R17, 0
  sbci  R18, 0
  sbci  R19, 0
  mov   R20, R16
  or    R20, R17
  or    R20, R18
  or    R20, R19
  brbc  SREG_Z, wait_pass_val
  nop
  nop
  nop
  ret
```

在上述代码中，wait_ms 子程序已被修改。首先，它被重命名为 wait_pass_val。为了清晰起见，之前添加的用于测试子程序所用值上下限的代码已被移除，因为我们正在研究向此子程序传递值的方法。之前，子程序顶部会将包含子程序中要消耗的周期数的寄存器加载上值，但现在这些代码已被移除。移除寄存器后，只需要一个标签作为跳转目标，该标签恰好也是子程序的入口点。从子程序中移除寄存器加载的想法是：在调用子程序之前，在代码中加载这些值。这样，每次调用子程序时都可以传递一个新值。下面展示了 wait_pass_val_asm 项目中 main.asm 的列表。

```asm
wait_pass_val.asm : main.asm

.equ	F_CPU		 = 1000000
.equ	MS_DELAY_1	 = (((F_CPU * 200) / 1000) - 10) / 10 ; 200ms
.equ	MS_DELAY_2	 = (((F_CPU * 500) / 1000) - 10) / 10 ; 500ms

start:	sbi	DDRB, DDB4		 ; Set pin PB4 as output

loop:	sbi	PORTB, PORTB4		 ; Set LED pin high
	ldi	R16, low (MS_DELAY_1)	 ; Pass 32-bit value
	ldi	R17, byte2(MS_DELAY_1)	 ; to the wait_pass_val
	ldi	R18, byte3(MS_DELAY_1)	 ; subroutine
	ldi	R19, byte4(MS_DELAY_1)	 ;
	rcall	wait_pass_val		 ; LED on delay
	cbi	PORTB, PORTB4		 ; Clear LED pin low
	ldi	R16, low (MS_DELAY_2)	 ; Pass 32-bit value
	ldi	R17, byte2(MS_DELAY_2)	 ; to the wait_pass_val
	ldi	R18, byte3(MS_DELAY_2)	 ; subroutine
	ldi	R19, byte4(MS_DELAY_2)	 ;
	rcall	wait_pass_val		 ; LED off delay
	rjmp	loop

.include "wait_pass_val.asm"
```

代码顶部，两个名称被赋予了使用我们现在熟悉的公式计算出的值。第一个值计算子程序产生 200ms 延迟所需的周期数，第二个值计算产生 500ms 延迟所需的周期数。在调用 wait_pass_val 之前，这些值被加载到寄存器 R16 到 R19 中。这样一来，值就被传递给了 wait_pass_val 子程序，因为子程序使用这些值来生成时间延迟。

请注意，在上述代码中，如果在模拟器中测量子程序使用的周期数，必须从 32 位数的第一部分加载到 R16 的地方开始测量。原因是用于计算生成周期数的公式尚未修改以移除传递值给子程序所用的周期数。无论如何，这可能是我们偏好的行为，因为这些指令仍然消耗周期，可被视为我们生成的延迟的一部分。请注意，由于 RCALL 指令现在，总数中额外增加了 3 个周期。

