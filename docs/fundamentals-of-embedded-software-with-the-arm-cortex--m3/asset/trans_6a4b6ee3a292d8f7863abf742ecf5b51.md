

操作数；UMULL 和 UMLAL 对无符号操作数执行相同操作。有符号和无符号乘法仅在双长乘积的最高位半部分有所不同。MUL、MLA 和 MLS 指令仅生成单长乘积，因此这些指令可与有符号或无符号操作数一起使用。MLA、MLS、UMLAL 和 SMLAL 指令在级数近似中很有用，且 MLS 指令可用于计算除法后的余数（表 6-8）。

| 指令 | 操作 | [S] | 备注 |
|---|---|---|---|
| MUL | Rd <- Rn x Rm | NZ | 32 位乘积 |
| MLA | Rd <- (Rn x Rm) + Ra | | 32 位乘积 |
| MLS | Rd <- Ra - (Rn x Rm) | | 32 位乘积 |
| UMULL | RdHi,RdLo <- Rn x Rm | | 无符号 64 位乘积 |
| UMLAL | RdHi,RdLo <- Rn x Rm + RdHi,RdLo | | |
| SMLAL | RdHi,RdLo <- Rn x Rm + RdHi,RdLo | | 有符号 64 位乘积 |
| SMLALD | RdHi,RdLo <- Rn x Rm + RdHi,RdLo | | |
| UDIV | Rd <- Rn / Rm | | 无符号 32 位商；无余数 |
| SDIV | Rd <- Rn / Rm | | 有符号 32 位商；无余数 |

要计算除法的余数，必须从被除数中减去商与除数的乘积。例如，考虑以下 C 赋值语句：

```
remainder = dividend % divisor ;
```

假设所有变量均为 32 位无符号整数，则余数在汇编中计算如下：

```
LDR R0, dividend ;R0 <- dividend
LDR R1, divisor ;R1 <- divisor
UDIV R2,R0,R1 ;R2 <- quotient
MLS R0,R2,R1,R0 ;R0 <- dividend - divisor x quotient
STR R0, remainder
```

## 6.8.3 位操作指令

嵌入式应用程序经常处理打包信息，并需要一组有效的指令来操作位。Thumb-2 指令子集包括以下基本的按位 NOT、AND、OR 和异或操作（表 6-9）：

C 中熟悉的按位操作可以轻松翻译为等效的 ARM 汇编。例如，用于清除“x”第 5 位的 C 语句：

```
x &= ~(1 << 5) ; // clear bit n of x
```

| 指令 | 操作 | [S] | 备注 |
|---|---|---|---|
| AND Rd, Rn, <op2> | Rd <- Rn & <op2> | NZC | |
| ORR Rd, Rn, <op> | Rd <- Rn \| <op> | NZC | |
| EOR Rd, Rn, <op> | Rd <- Rn ^ <op> | NZC | "异或" |
| BIC Rd, Rn, <op> | Rd <- Rn & ~<op> | NZC | "位清除" |
| ORN Rd, Rn, <op> | Rd <- Rn \| ~<op> | NZC | "或非" |
| MVN Rd, Rn | Rd <- ~Rn | NZC | "移取反" |

将使用 BIC 指令编码，如下所示：

```
LDR R0, x ;get a copy of x
BIC R0, R0, #0x20 ;clear bit 5
STR R0, x ;store result back into x
```

## 6.8.4 移位指令

表 6-10 列出了 Thumb-2 移位指令。虽然许多其他指令（例如 ADD、ORR 等）可以包含对其一个操作数的移位，但移位量限制为常量。移位指令没有该限制。它们将操作数 (Rn) 的副本移位指定数量的比特位，该数量由常量或另一个寄存器的内容指定。在所有情况下，将字母“S”附加到指令助记符会导致进位标志 (C) 捕获从操作数移位“出”的比特；在多比特移位中，它捕获最后移位出的比特。

移位指令在用于填充操作数另一端空出的比特位方面有所不同，如图 6-7 所示。逻辑左移 (LSL) 和

| 指令 | 操作 | [S] | 备注 |
|---|---|---|---|
| LSL Rd, Rn, <shift> | Rd <- Rn << <shift> | NZC | |
| LSR Rd, Rn, <shift> | Rd <- Rn >> <shift> | NZC | 零填充 |
| ASR Rd, Rn, <shift> | Rd <- Rn >> <shift> | NZC | 符号扩展 |
| ROR Rd, Rn, <shift> | Rd <- Rn >> <shift> | NZC | 右旋转 |
| RRX Rd, Rn | Rd <- Rn >> 1 | NZC | 右移，用 C 填充 |

注意：“<shift>”可以是常量或寄存器，并指定要移位的比特位数。

6 此限制仅适用于 Cortex-M3 处理器的 Thumb-2 指令子集；更通用的 ARM 指令集允许移位量由寄存器的内容确定。

逻辑右移 (LSR) 指令始终插入 0。算术右移 (ASR) 指令复制最高有效位，使结果与原始操作数具有相同的符号。

![](img/f0b8aa873b11dc585ed698a10d04e7a7_135_0.png)

图 6-7 移位指令（附加“S”以修改进位标志）。

右旋转指令 (ROR) 执行 32 位旋转，因此用从位 0 移出的值填充位 31。注意，N 位的左旋转可以通过 32-N 位的右旋转来实现。扩展右旋转 (RRX) 执行 33 位旋转，进位标志 (C) 作为操作数的 1 位扩展；然后旋转所有 33 位，使位 31 填充进位标志的先前内容。

移位 64 位双长操作数需要三条指令。例如，要对双长操作数执行逻辑左移，先对高半部分执行逻辑左移。这会在其最低有效位留下一个 0，必须用低半部分的最高有效位替换它。一条指令可以同时将低半部分的副本右移 31 位，并按位或到高半部分。最后，只需对低半部分左移即可（图 6-8）。

| | | R1 | R0 |
|---|---|---|---|
| LDRD R0,R1,data64 | => | b63 ... b32 | b31 ... b0 |
| LSL R1,R1,#1 | => | b62 ... b32 0 | b31 ... b0 |
| ORR R1,R1,R0,LSR #31 | => | b62 ... b32 b31 | b31 ... b0 |
| LSL R0,R0,#1 | => | b62 | b31 b30 ... b0 0 |
| STRD R0,R1,data64 | => | | |

图 6-8 双长 64 位逻辑左移。

另一种解决方案是先对低半部分左移，并使用 LSLS 指令将位 31 捕获到进位标志中。然后，对高半部分左移。最后，使用以零作为第二个操作数的 ADC 指令，将保存在进位标志中的位 31 放入高半部分。但是请注意，虽然这种方法适用于双长左移，但不适用于相反方向。寻找双长左旋转的最优解留给读者作为练习。

## 6.8.5 位字段操作指令

使用 Thumb-2 指令可以轻松实现位置和宽度固定的位字段的提取和插入。一条指令可以将 0 插入寄存器的位字段中，将一个寄存器的最低有效位复制到另一个寄存器的位字段中，或从寄存器中提取位字段并将其扩展为 32 位有符号或无符号值。在每种情况下，位字段的最低有效位 (lsb) 位置和宽度均由指令的最后两个（常量）操作数指定（表 6-11）。

| 指令 | 操作 | [S] | 备注 |
|---|---|---|---|
| BFC | Rd<bits <- 0 | | |
| BFI | Rd<bits <- Rc<lsb> | | |
| SBFX | Rd <- Rc<bits> | | 符号扩展 |
| UBFX | Rd <- Rc<bits> | | 零扩展 |

例如，图 6-9 说明了如何轻松使用位字段操作指令从 16 位打包时间表示的中间提取 6 位无符号分钟，或将其替换为来自另一个寄存器的新值。

![](img/f0b8aa873b11dc585ed698a10d04e7a7_136_0.png)

图 6-9 位字段插入和提取指令。

## 6.8.6 其他位、字节和半字指令

除了位、移位和位字段指令外，以下指令偶尔用于特定情况，例如在小端和大端系统之间转换数据（处理以太网数据包中保存的数据时需要这样做）。这些指令不修改其操作数 (Rn) 或任何标志（表 6-12）。

| 指令 | 操作 | [S] | 备注 |
|---|---|---|---|
| CLZ Rd,Rn | Rd ← CountZeros(Rn) | | 前导零数 (0–32) |
| RBIT Rd,Rn | Rd ← RevBits(Rn) | | 反转位顺序 |
| REV Rd,Rn | Rd ← RevByteOrder(Rn) | | 反转字节顺序 |
| REV16 Rd,Rn | Rd ← RevHalfWords(Rn) | | 反转每个半字中的字节 |
| REVSH Rd,Rn | Rd ← RevLoHalf(Rn) | | 反转 2 个最低有效字节；符号扩展 |
| SXTB Rd,Rn | Rd ← SignedByte(Rn) | | 符号扩展；操作数可以是 Rn，或“Rn,ROR #n”，其中 n = 8、16 或 24 |
| SXTH Rd,Rn | Rd ← SignedHalf(Rn) | | 符号扩展；操作数可以是 Rn，或“Rn,ROR #n”，其中 n = 8、16 或 24 |
| UXTB Rd,Rn | Rd ← UnsignedByte(Rn) | | |
| UXTH Rd,Rn | Rd ← UnsignedHalf(Rn) | | |

## 处理大乘积

如果手动进行算术运算，将两个 n 位整数相乘会产生 2n 位的乘积。但是，C 中的乘法生成的乘积与操作数具有相同的数据类型（因此大小也相同）。考虑以下 C 代码行：

```
a = (b*c) / d ;
```

如果所有变量均为 16 位整数，则生成的汇编代码将类似于：

```
LDRSH R0, b
LDRSH R1, c
MUL R0, R0, R1
SXTH R0, R0 ;Force a 16-bit representation (short × short → short)
LDRSH R2, d
SDIV R0, R0, R2
STRH R0, a
```

现在，考虑当 b、c 和 d 各自包含像 +10,000 这样的大值时会发生什么。从数学上讲，最终结果也应该是 +10,000，但 32 位乘积太大，无法用 16 位表示，因此除法不会产生正确的结果。

7 这就是为什么 MUL、MLA 和 MLS 指令仅保留双长乘积的最低有效半部分。

