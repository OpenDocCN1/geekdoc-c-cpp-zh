
基本设计可以扩展，将使能作为额外的控制级别。逻辑图和 Verilog 实现（使用 srLatch）如图 A.14 所示。

![](img/679b8d2d47f1bf86e17aca48f596f5cc_1025_0.png)

```
// Gate Level Model
// Gated SR Latch with clear
module gsrLatch(q, qnot, sg, rg, clr, enab);
    input sg, rg, clr, enab;
    output q, qnot;
    parameter delay0 = 2;

    // Build the gating logic
    not n0(nclr, clr);
    and n0d(rl, rg, clr, enab);
    and n1(sl, sg, clr, enab);

    // Build the basic RS latch
    nor #delay0 N0(q, rl, nclr, qnot);
    nor #delay0 N1(qnot, sl, q);
endmodule
```

图 A.14 扩展带有相应结构 Verilog 模块的 SR 锁存器。

使用门控锁存器的主从式实现如图 A.15 所示。

![](img/679b8d2d47f1bf86e17aca48f596f5cc_1025_1.png)

```
// Use two SR Latches
// in a master slave configuration to build a flip-flop
module srmsff(q, qnot, s, r, clr, clk);
    input s, r, clr, clk;
    output q, qnot;

    not n0(nclk, clk);
    gsrLatch master(qm, qnotm, s, r, clr, clk);
    gsrLatch slave(q, qnot, qm, qnotm, clr, nclk);
endmodule
```

图 A.15 带有相应结构 Verilog 模块的主从式 SR 锁存器。

现在可以使用 SR 触发器构建一个简单的 2 位同步二进制递增计数器。逻辑图和 Verilog 模型如图 A.16 所示。

![](img/679b8d2d47f1bf86e17aca48f596f5cc_1026_0.png)

```
// Build a two bit binary up counter
// using master slave SR flip-flops
module TwoBitCntr(qA, qB, clr, clk);
    input clr, clk;
    output qA, qB;
    and a1(sA, qAnot, qB);
    and a2(rA, qA, qB);
    srmsff FFB(qB, qBnot, qBnot, qB, clr, clk);
    srmsff FFA(qA, qAnot, sA, rA, clr, clk);
endmodule
```

图 A.16 使用主从式 SR 锁存器的 2 位二进制递增计数器及其相应结构 Verilog 模块。

## A.4.2 数据流模型

门级建模是处理较小问题的一种有效方法。这种方法直接遵循典型的详细逻辑图，从而简化了从设计到模型和仿真的过程。嵌入式应用的复杂性在不断增加。昨天的 SSI 和 MSI 模块正在被 ASIC、FPGA 和微处理器所取代。在门级开发完整设计已不再可行。在门级工作类似于尝试用汇编语言编写复杂的应用程序。虽然可以这样做，但这种方法不切实际。

然而，在更高层次上开发也并非没有问题。一个人越是远离底层细节并越依赖工具来生成这些细节，工具生成非最优设计的风险就越大。推动设计和技术极限的能力来自多年的经验和对问题的理解。工具可以帮助我们解决大多数设计问题。它们还不够先进，无法完全自主地解决所有问题。

- 数据流建模
- RTL，寄存器传输级
- 逻辑综合

数据流建模顾名思义，从数据在系统中从源到目的地移动的角度来看待设计。在数字世界中，这种观点通常被称为 RTL 或寄存器传输级设计。当代工具能够接受数据流模型作为输入，并通过称为逻辑综合的过程生成低级逻辑门实现。

## A.4.2.1 连续赋值

在数据流级别，设计被建模为模块之间数据的移动，以实现应用。该数据通过网络移动。因此，这种建模的一个基本元素是能够将值从源模块驱动到互连网络上的目标模块。在 Verilog 中，这种能力通过连续赋值来表达。连续赋值语句使用以下语法指定。

- 连续赋值

```
Syntax
assign destination net = source net expression
```

连续赋值的左侧必须是标量或向量（多行）网络。表达式的右侧可以是网络、寄存器或函数调用返回值，并且必须与左侧大小相同。例如，不能将标量赋值给向量，反之亦然。

连续赋值始终处于活动状态。右侧的变化会强制对左侧进行求值，并将右侧值赋给左侧网络。

## A.4.2.1.1 组合逻辑

我们使用之前设计的 AndOr 电路来说明组合数据流模型。该模型使用连续赋值，如图 A.17 所示。

```
// continuous assignment
module AndOr(AandB, AorB, A, B);
output AandB, AorB;
input A, B;

wire AandB, AorB;
parameter delay0 = 10;

assign AandB = A&B;
assign AorB = A|B;
endmodule
```

图 A.17 使用数据流 Verilog 模型的组合逻辑模块。

使用按位 AND 和 OR 运算符实现该函数应该与之前使用其 C 语言对应物的工作相似。

## A.4.2.2 延迟

从门级上升一层抽象并不排除对电路行为现实世界影响建模的需求。数据流级别的 Verilog 延迟模型自然源自门级模型。

语法如下：

```
Syntax
assign #delay net
```

## 示例 A.2

之前设计的 AndOr 电路模型可以包含延迟，如图 A.18 所示。

```
// continuous assignment
module AndOr(AandB, AorB, A, B);
output AandB, AorB;
input A, B;
wire AandB, AorB;
parameter delay0 = 10;
assign #delay0 AandB = A&B;
assign #delay0 AorB = A|B;
endmodule
```

图 A.18 使用数据流 Verilog 模型的带门延迟的组合逻辑模块。

系统输出现在将在输入信号中的任何一个变化后 10 个时间单位发生变化，如图 A.19 所示。

| 时间 | A | B | AandB | AorB |
|---|---|---|---|---|
| 0 | 1 | 1 | x | x |
| 10 | 0 | 1 | 1 | 1 |
| 20 | 0 | 0 | 0 | 1 |
| 30 | 0 | 1 | 0 | 0 |
| 40 | 0 | 1 | 0 | 1 |

图 A.19 图 A.18 电路模块的系统输出。

上升和下降时间延迟以类似方式纳入。所有三者的语法如下：

```
Syntax
assign # (rise time, fall time, delay) net;
```

## 示例 A.3

之前设计的 AndOr 电路模型可以包含所有三种延迟，如图 A.20 所示。

```
// Compute the logical AND and OR of inputs A and B.
module AndOr(AandB, AorB, A, B);
output AandB, AorB;
input A, B;
wire AandB, AorB;
parameter delay0 = 10;
parameter rise = 5;
parameter fall = 7;
assign #(rise, fall, delay0) AandB = A&B;
assign #(rise, fall, delay0) AorB = A|B;
endmodule
```

图 A.20 使用数据流 Verilog 模型的带所有延迟的组合逻辑模块。

系统输出现在将在输入信号中的任何一个变化后 10 个时间单位发生变化，并反映上升和下降时间，如图 A.21 所示。

| 时间 | A | B | AandB | AorB |
|---|---|---|---|---|
| 0 | 1 | 1 | x | x |
| 5 | 1 | 1 | 1 | 1 |
| 10 | 0 | 1 | 1 | 1 |
| 17 | 0 | 1 | 0 | 1 |
| 20 | 0 | 0 | 0 | 1 |
| 30 | 0 | 1 | 0 | 0 |

图 A.21 图 A.20 电路模块的系统输出。

## A.4.2.3 运算符

数据流级别 Verilog 中使用的语法和运算符与 C 语言非常接近。表 A.2 列出了最常用的运算符。

| 运算符 | 符号 | 操作 | 运算符 | 符号 | 操作 |
|---|---|---|---|---|---|
| 算术 | + | 加 | 相等 | == | 等于 |
| | - | 减 | | != | 不等于 |
| | / | 除 | 逻辑 | ! | 逻辑非 |
| | * | 乘 | | && | 逻辑 AND |
| | % | 取模 | | || | 逻辑 OR |
| 关系 | > | 大于 | 按位 | ~ | 按位非 |
| | < | 小于 | | & | 按位 AND |
| | >= | 大于或等于 | | | 按位 OR |
| | <= | 小于或等于 | 移位 | << | 左移 |
| | | | | >> | 右移 |

## A.4.2.3.1 时序逻辑

图 A.22 中的以下三个代码模块演进了之前在门级设计的门控 SR 锁存器、主从式 SR 触发器和 2 位二进制计数器的数据流实现。

## A.4.3 行为级模型

行为级模型又提高了一层设计抽象级别。我们对设计的思考现在超越了系统内部数据流的考虑，转而关注表达系统行为的算法。在行为级别，模型开始更像 C 或 C++ 程序，而非数字电路。系统中的控制流使用熟悉的循环和分支结构来表达，而不是逻辑门。

## A.4.3.1 程序结构

在行为级别，C 或 C++ 等语言之间的一个主要区别变得清晰。与 C 或 C++ 不同，在 C 或 C++ 中控制流通常是顺序的，而在 Verilog 中控制流是并发的。C 或 C++ 中的语句串行执行；Verilog 中的语句并行执行。

顺序 并发
