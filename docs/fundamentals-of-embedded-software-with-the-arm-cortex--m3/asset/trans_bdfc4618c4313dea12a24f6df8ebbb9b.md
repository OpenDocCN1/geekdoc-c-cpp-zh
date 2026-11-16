

| | 8-bit 目标 | 16-bit 目标 | 32-bit 目标 | 64-bit 目标 |
|---|---|---|---|---|
| 源为常数 5 | LDR<br>STRB<br>R0, =5<br>R0, dist8 | LDR<br>STRH<br>R0, =5<br>R0, dist16 | LDR<br>STR<br>R0, =5<br>R0, dist32 | LDR<br>LDR<sup>1</sup><br>STRD<br>R0, =5<br>R1, =0<br>R0, R1, dist64 |
| 8-bit 源 | LDRB<br>STRB<br>R0, src8<br>R0, dist8 | LDRB<br>STRH<br>R0, src8<br>R0, dist16 | LDRB<sup>2</sup><br>STR<br>R0, src8<br>R0, dist32 | LDRB<sup>2</sup><br>LDR<sup>4</sup><br>STRD<br>R1, =0<br>R0, R1, dist64 |
| 16-bit 源 | LDRB<br>STRB<br>R0, src16<br>R0, dist8 | LDRH<br>STRH<br>R0, src16<br>R0, dist16 | LDRH<sup>3</sup><br>STR<br>R0, src16<br>R0, dist32 | LDRH<sup>4</sup><br>LDR<sup>4</sup><br>STRD<br>R1, =0<br>R0, R1, dist64 |
| 32-bit 源 | LDRB<br>STRB<br>R0, src32<br>R0, dist8 | LDRH<br>STRH<br>R0, src32<br>R0, dist16 | LDR<br>STR<br>R0, src32<br>R0, dist32 | LDR<br>LDR<sup>4</sup><br>STRD<br>R0, =32<br>R1, =0<br>R0, R1, dist64 |
| 64-bit 源 | LDRB<br>STRB<br>R0, src64<br>R0, dist8 | LDRH<br>STRH<br>R0, src64<br>R0, dist16 | LDR<br>STR<br>R0, src64<br>R0, dist32 | LDRD<br>STRD<br>R0, R1, src64<br>R0, R1, dist64 |

<sup>1</sup>如果源操作数是负常数，则替换为 ASR R1, R0, #31。
<sup>2</sup>如果源操作数是有符号的，则替换为 LDRSB。
<sup>3</sup>如果源操作数是有符号的，则替换为 LDRSH。
<sup>4</sup>如果源操作数是有符号的，则替换为 ASR R1, R0, #31。

符号扩展完全由 LDRSB 或 LDRSH 指令处理。但是，当目标宽度为 64 位时，创建符号扩展的高 32 位需要对低半部分的副本执行 31 位算术右移；用于此目的的 ASR 指令将在本章后面介绍。

## 6.5 内存地址计算

在执行类似于“LDR R0, data;”的指令的执行阶段时，指令必须向内存提供内存操作数“data”的地址。如果将地址作为 32 位常数存储在指令本身的表示中，这意味着所有 LDR 和 STR 指令都将超过 32 位宽。为了节省内存空间和指令获取时间，这些指令仅指定如何从较少的位数计算地址。汇编器会自动将对变量“data”的引用转换为 PC-relative 引用，其中地址计算为程序计数器 (R15) 与指令中存储的小常数之和。该常数称为位移，其值是指令地址与数据地址之间的差值。位移仅 13 位宽，因此限制在 ±4,095 以内。

PC-relative 寻址是 ARM 寻址模式中称为“偏移寻址”的特例。它为计算地址提供了四个基本选项，如表 6-4 所示。这些选项的使用示例将在本节后面介绍。

| 语法 | 内存地址 | 示例 | 注释 |
| :--- | :--- | :--- | :--- |
| [Rn] | Rn | [R5] | |
| [Rn, #constant] | Rn + constant | [R5, #100] | |
| [Rn, Rm] | Rn + Rm | [R4, R5] | 与 LDRD 或 STRB 不可一起使用。这些指令只能使用寄存器 Rn。 |
| [Rn, Rm, LSL #constant] | Rn + (Rm << constant) | [R4, R5, LSL #3] | |

注意：“LDR R0, data”是 [Rn, #constant] 的一种特殊 PC-relative 情况。

![](img/f0b8aa873b11dc585ed698a10d04e7a7_126_0.png)

在编写汇编语言时，重要的是要记住，访问内存的指令的操作数字段仅限于使用值为常数的表达式（例如由变量名表示的地址），或表 6-4 中列出的四个选项之一。例如，汇编器会拒绝带下标的数组名（例如，LDR R0, data[k]）或在方括号括起来的地址规范中使用变量名（例如，LDR R0, [R0+k]）。

图 6-4 说明偏移寻址如何使用寄存器、移位器和小常数来生成指令操作数的地址。另外两种寻址模式只是偏移寻址的变体，它们在处理数组数据的循环中很有用。预索引寻址（在右方括号后跟一个感叹号来指定）仅在指令结束时将地址写回寄存器 Rn。后索引寻址（仅将 Rn 放在方括号中来指定）也执行相同操作，但使用 Rn 的先前内容作为指令操作数的地址。

## 6.6 内存寻址示例

当指令引用内存中的数据时，只有两种可能情况中的一种存在。要么数据的地址是常数，要么它是必须在运行时计算的值。在 C 语言中，地址为常数的唯一变量是那些全局声明（在所有函数之外）或在函数内部但使用 static 关键字声明的变量。通过指针访问的数据、所有函数参数以及在函数内部声明的任何非 static 变量都具有必须计算的地址。

### 6.6.1 将 C 指针表达式转换为汇编

在 C 语言中，指针用于保存内存中某个位置的地址。它们通常通过将“取地址”运算符 (&) 应用于另一个变量的结果来初始化：

```c
int8_t *ptr2byte; // 32-bit pointer holds address of an 8-bit byte
int8_t data;
ptr2byte = &data; // store address of data (a constant) in pointer
```

&data 的值是一个常数。在 ARM 汇编中，我们使用特殊的“ADR”指令来获取该常数：

```asm
ADR R0, data ;R0 ← &data
STR R0, ptr2byte ;ptr2byte ← R0
```

ADR 指令的源操作数字段可以使用与 LDR 和 STR 指令相同的任何内存引用表达式，但它并不实际引用内存——它仅计算地址而不导致内存读取或内存写入。在其最简单的形式中（如前所述），它类似于将常数加载到寄存器中的 LDR 指令，因为“data”的地址是一个常数。但是，这个地址实际上是通过将某个内容加到程序计数器的当前值上获得的。

当你解引用指针时，你使用其内容作为要引用的数据的地址。假设“ptr2byte”已用“data”的地址初始化，我们可以通过指针的间接引用将零存储到其中，如下所示：

```c
*ptr2byte = 0; // store a zero into the byte "data"
```

请注意，我们将零存储在由变量而非常数提供其地址的位置。因此，在 ARM 汇编中，我们必须将该变量的内容加载到寄存器中，然后在将零存储到内存时将其用在一对方括号内：

```asm
LDR R0, =0 ;get the constant zero
LDR R1, ptr2byte ;get the address held in "ptr2byte"
STRB R0, [R1] ;store the zero into a byte of memory
```

上述代码使用 STRB 指令是因为指针被声明为指向宽度为 8 位的数据。但是，指针本身是使用常规 LDR 指令加载的，因为地址始终是 32 位。

理解指针算术的工作原理也很重要。请考虑以下内容：

```c
int32_t array[100]; // an array of 32-bit words of 4 bytes each
int32_t *ptr2word; // a pointer to a 32-bit word
ptr2word = array; // initialize ptr2word with the address of array[0]
```

由于 ptr2word 包含 array[0] 的地址，我们知道 *ptr2word 是对 array[0] 内容的引用。同样，指针表达式 ptr2word + 1 是 array[1] 的地址，指针表达式 ptr2word + k 是 array[k] 的地址。重要的是要意识到数组的每个元素包含 4 个字节，因此如果 array[0] 的地址是 1000，则 array[1] 的地址将是 1004。这意味着当我们写 ptr2word + 1 时，我们实际上是在向地址添加 4 而不是 1。例如，C 赋值语句

```c
*(ptr2word + 5) = 0; // equivalent to: array[5] = 0;
```

将被转换为以下 ARM 汇编：

```asm
LDR R0, =0 ;get the constant zero
LDR R1, ptr2word ;get the address held in "ptr2word"
STR R0, [R1, #20] ;store zero at address 4*5 bytes higher in memory
```

如果我们用整数变量 k 替换常数 5，如下所示：

```c
*(ptr2word + k) = 0; // equivalent to: array[k] = 0;
```

那么 ARM 汇编代码变为：

```asm
LDR R0, =0 ;get the constant zero
LDR R1, ptr2word ;get the address held in "ptr2word"
LDR R2, k ;get the integer held in "k"
STR R0, [R1, R2, LSL #2] ;store at address 4k bytes beyond pointer
```

能够对地址计算中使用的寄存器内容进行左移，是乘以 2 的幂的简单方法，并且特别有用，因为我们通常处理宽度为 1、2、4 或 8 字节的数据。

还要记住，两个指针的差不是它们所持有的地址之差，而是对象之差。例如，请考虑以下声明：

```c
int32_t array[100]; // an array of 100 words of 4 bytes each
int32_t * p1 = &array[10];
int32_t * p2 = &array[20];
```

如果数组从地址 1000 开始，则 p1 将初始化为地址 1040，p2 初始化为 1080。但是，表达式 p2 - p1 的值不是 40（地址之差），而是 10（对象之差）。在汇编中计算此值需要先进行减法，然后除以 4：

```asm
LDR R0, p1 ;get the address held in p1
LDR R1, p2 ;get the address held in p2
SUB R2, R1, R0 ;R2 <- the difference in addresses
ASR R0, R2, #2 ;R0 <- R2, arithmetic shift right by 2 (divide by 4)
```

