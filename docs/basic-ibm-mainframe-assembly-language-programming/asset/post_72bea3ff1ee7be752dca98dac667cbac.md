
## 12.6 Multiply

The original 32 bit binary integer multiply instructions are the M and MR. In both, the first operand specifies the even register of an even/odd pair of registers. In the original architecture these were 32 bit registers but in the current implementation only the low order 32 bits of the 64 bit general purpose registers participate. The high order bits are unchanged. The multiplicand is a 32 bit signed integer which resides in the odd register of the pair. The multiplier is a 32 bit signed integer which resides either in the register designated as the second operand (MR) or at the memory address specified (M). The contents of the even register are ignored.

| OpCode | Type | 1st Operand | 2nd Operand | Result |
|---|---|---|---|---|
| SL | RX | 32 bit register | 32 bit memory | 32 bit register |
| SLR | RR | 32 bit register | 32 bit register | 32 bit register |
| SLGR | RRE | 64 bit register | 64 bit register | 64 bit register |
| SLGFR | RRE | 64 bit register | 32 bit register | 64 bit register |
| SLY | RXY | 32 bit register | 32 bit memory | 32 bit register |
| SLG | RXY | 64 bit register | 64 bit memory | 64 bit register |
| SLGF | RXY | 64 bit register | 32 bit memory | 64 bit register |
| SLBR | RRE | 32 bit register | 32 bit register | 32 bit register |
| SLB | RXY | 32 bit register | 32 bit memory | 32 bit register |
| SLBGR | RRE | 64 bit register | 64 bit register | 64 bit register |
| SLBG | RXY | 64 bit register | 64 bit memory | 64 bit register |

Table 27 Logical Subtract Instructions

The result is a 64 bit signed binary number which is placed in the low order 32 bits of the even/odd register pair with the high order 32 bits of the result in the low order 32 bits of the even register and the low order 32 bits of the result placed in the low order 32 bits of the odd register. No overflow can take place and the Condition Code remains unchanged.

For example, If R5 contains 20₁₀ and R6 contains 3₁₀, we can multiply them with the instruction:

```
MR R4,R6
```

The result will be in R4 and R5. As the answer is 60₁₀, the result is effectively in R5. R6 will contain results only in the case when answers exceed 32 bits.

There is also an MH instruction where a 16 bit signed number from memory is multiplied by the 32 bit signed contents of the register specified as the first operand. The low order 32 bits of

In the current implementation only the low order 32 bits of the general purpose registers participate. The high order bits are unchanged. The low order portions of both registers are treated as one 64 bit signed binary integer with the high order part of the number in the even register. There is no halfword divide instruction.

| OpCode | Type | 1st Operand | 2nd Operand | Result |
|---|---|---|---|---|
| D | RX | 32 bit register | 32 bit memory | 32 bit register |
| DR | RR | 32 bit register | 32 bit register | 32 bit register |
| DSGR | RRE | 64 bit register | 64 bit register | 64 bit register |
| DSGFR | RRE | 64 bit register | 32 bit memory | 64 bit register |
| DSG | RXY | 64 bit register | 32 bit memory | 64 bit register |
| DSGF | RXY | 64 bit register | 64 bit memory | 64 bit register |

## Table 30 Signed Divide Instructions

The divisor is a 32 bit signed number located in the register specified as the second operand (DR) or at the memory location specified by the second operand address.

| OpCode | Type | 1st Operand | 2nd Operand | Result |
|---|---|---|---|---|
| DL | RXY | 32 bit register | 32 bit memory | 64 bit register |
| DLR | RXE | 32 bit register | 32 bit register | 64 bit register |
| DLGR | RXE | 64 bit register | 64 bit register | 128 bit register |
| DLG | RXY | 64 bit register | 64 bit memory | 128 bit register |

## Table 31 Unsigned Divide Instructions

The result consists of a remainder located in the even register of the first operand and the quotient located in the odd register. The sign of the quotient is determined by the rules of algebra and the remainder has the same sign as the dividend except that zero is always positive. A divide by zero will raise a fixed-point divide exception if enabled. The condition code is unchanged.

For example, if location VAR1 contains the 32 bit number 10, and location VAR2 contains the 32 bit number 3, you can divide the value at VAR1 by the value at VAR2 with the following:

```
L R2,VAR1
SRDA R2,32
D R2,VAR2
```

The results will be 1 in R2 (the remainder) and 3 in R3 (the quotient).

Only the low order 32 bits of the even/odd registers participate in the D and DR instructions and they are treated as a single 64 bit number.

We load the dividend into the even register and then do a shift double arithmetic to the right by 32. This has the effect of shifting the dividend from the even register to the odd register but propagating across the even register the sign bit.

The SRDA instruction shifts the low order 32 bits of each register as though they were one 64 bit register.

## 13. Character Instructions

## 13.1 Basic Character Instructions

The original architecture had instructions to manipulate strings of character data up to 256 bytes in length. In later versions of the architecture, these were extended to handle larger strings but we begin with the most basic.

## 13.1.1 Moving Characters (MVC)

```
MVC D1(L,B1),D2(B2)
```

The basic character move instruction is the MVC instruction. It is an SS instruction and copies up to 256 bytes beginning at the address given as the second operand to the address given as the first operand. The addresses may overlap.

In the machine language coding of an MVC (as is also the case with other SS character instructions), the length is expressed as an 8 bit field whose coded value is one less than the actual length to be moved. Thus, in the machine language format, a length value of 0 means move 1 byte and a length value of 255 means move 256 bytes, and so on. In the assembly language source code, however, the actual length is coded (one will be subtracted from this value by the assembler in constructing the machine language translation).

```
1  MVC L1,L2      * 20 bytes from L2 copied to L1
2  MVC L1(10),L2   * 10 bytes from L2 copied to L1
3
4  LA  R2,L1
5  LA  R3,L2
6
7  MVC 0(20,R2),0(R3) * 20 bytes from L2 copied to L1
8  MVC 10(10,R2),0(R3) * 10 bytes from L2 copied to L1
9  *              * beginning at position 10
10
11 MVC L1(1),=C' '  * blank copied to 1st byte.
12 MVC L1+1(19),L1  * overlapped move; L1 is made
13 *              * all blanks
14
15 L1 DS  CL20
16 L2 DC  C'ABCDEFGHIJKLMNOPQRST'
```

Figure 51 MVC Examples

In the case where no length is supplied, the implied length attribute of the first operand is used. The operands are specified

## 认知智能：从感知到理解的新范式

近年来，随着深度学习技术的快速发展，人工智能系统在感知任务上取得了显著进展。然而，单纯依靠大规模数据和计算能力堆叠的感知模型，在面对复杂推理、因果理解和常识判断等认知任务时仍存在明显不足。本文旨在探讨认知智能的发展路径及其与感知智能的本质区别。

### 一、感知与认知的本质差异

感知智能关注的是从原始数据中提取有效特征并进行模式识别，主要包括计算机视觉中的目标检测、图像分类，以及语音识别中的声学建模等任务。而认知智能则要求系统具备知识表示、逻辑推理、决策规划和语言理解等高层认知能力。两者之间的关系可以类比为人类视觉系统与大脑前额叶皮层的关系——前者负责将光信号转化为视觉信息，后者则负责对这些信息进行深层次的加工与利用。

### 二、认知智能的关键技术路线

当前，认知智能的研究呈现出多条技术路线并行发展的态势。知识图谱方法强调结构化知识的表示与推理，通过实体关系和逻辑规则构建可解释的推理链条；认知架构方法借鉴人类认知过程的信息加工模型，试图在人工智能系统中模拟注意、记忆、决策等认知功能；而以大语言模型为代表的联结主义路径，则试图通过参数规模的扩大和训练范式的创新，从海量文本中隐式地习得世界知识与推理模式。

![](img/4b7e9c58cac527296b19b501116daeb1_124_0.png)

上图展示了三种主要技术路线在研究目标、知识表示方式和推理机制上的差异。值得注意的是，不同研究路线之间并非互相排斥的关系，而是呈现出互补融合的趋势。

### 三、大语言模型的认知能力分析

以GPT系列和开源模型为代表的大语言模型，在各类认知基准测试中表现出令人惊讶的能力。它们在数学推理、代码生成、逻辑演绎等任务上展现出的水平，已经超越了此前所有人工智能系统所达到的高度。然而，研究者也发现这些系统存在系统性缺陷：它们在面对分布外样本时容易产生错误推理，在需要多步规划时可能出现逻辑断裂，更重要的是，它们缺乏真正的因果理解能力，往往依赖统计关联而非因果机制进行推断。

### 四、未来研究方向与展望

认知智能的未来发展，需要在以下几个方面实现突破：其一，将符号推理与神经表示有机融合，构建兼具灵活性与可解释性的混合推理框架；其二，引入因果推断方法，使模型能够从观测数据中识别真正的因果关系而非表面相关；其三，发展持续学习能力，让系统在不断变化的环境中积累知识而不遗忘已有技能；其四，建立更加完善的评估体系，从多维度衡量模型的认知水平而不局限于传统基准测试的表现。

总之，认知智能作为人工智能发展的下一个重要里程碑，承载着从工具性智能走向类人智能的期望。虽然当前在通往通用人工智能的道路上仍面临诸多挑战，但随着多学科的交叉融合与技术范式的持续演进，认知智能有望在未来十年取得突破性进展。
