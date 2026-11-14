

从图 A.25 中代码片段的执行结果如图 A.26 所示。

| 时间 | a | b | c | d | e | f | g | h | i | j | k | l |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 10 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 12 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 16 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 18 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 20 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| 26 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| 28 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 |
| 32 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 |
| 42 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 |
| 44 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 |
| 48 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |

图 A.26 图 A.25 中模块的系统输出。

两种实现之间的主要区别体现在变量 d、e、f、g、h 和 i 的求值时间上。

## A.4.3.3.3 组合逻辑

图 A.27 中的下一个示例使用行为模型实现了前面的 NandNor 组合逻辑电路，并利用带有右侧和左侧延迟的阻塞和非阻塞赋值。

```
module blocking_nonblocking();
reg a, b, d, AandB, AorB, AandNAndB, AorNAndB;
reg e, f, EnforEf, EforF, EorF;
// Blocking Assignment
initial
begin
a = b = 1;
// Delay on the right hand side
AandB = #10 a & b;
// Delay on the left hand side
#10 d = a & b;
#10 AorB = a|b;
#11 AandNAndB = ~AorB;
end
// Non-Blocking Assignment
initial
begin
e = f = 1;
// Delay on the right hand side
// Delay on the left hand side
EnforEf <= #11 e&f;
// Delay on the left hand side
#12 EforF <= e & f;
#13 EorF <= e | f;
end
initial
begin
$display("time a b, \tAandB, \tAorB, \tAandNAndB, \tAorNAndB, \tEnforEf, \tEforF");
$monitor($time, " (%b) (%b) (%b) (%b) (%b) (%b) (%b) (%b) (%b) (%b) (%b)", a, b, AandB, AorB, AandNAndB, AorNAndB, e, f, EnforEf, EforF, EorF);
#50 $finish(1);
end
endmodule
```

图 A.27 使用带有阻塞和非阻塞赋值的行为 Verilog 模型的组合逻辑模块。

## 示例 A.7

图 A.27 中每种情况的电路输出如图 A.28 所示。

| 时间 | a | b | AnandB | AnorB | e | f | EnandF | EnorF |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 1 | 1 | x | x | 1 | 1 | x | x |
| 21 | 1 | 1 | 0 | x | 1 | 1 | x | x |
| 25 | 1 | 1 | 0 | x | 1 | 1 | x | 0 |
| 42 | 1 | 1 | 0 | 0 | 1 | 1 | x | 0 |

图 A.28 图 A.27 中模块的系统输出。

请注意，基于非阻塞赋值的求值顺序，NAND 操作数永远不会被赋予有效值。

## A.4.3.4 控制流

行为 Verilog 模型支持许多熟悉的控制流结构，例如分支、开关和循环。此外，该语言还提供对基于事件的控制的支持。

## A.4.3.4.1 事件

Verilog 支持四种不同的基于事件的控制。如下所示：

- 常规事件
- 命名事件
- OR 事件
- 电平。

基于事件的控制

每种都由事件控制符 @ 标识。Verilog 将事件解释为网线或寄存器值的变化。这种变化可用于触发单个语句或语句块的求值。

每种的语法如下。

```
Syntax
Regular Event
@(signal = action
variable = @( signal) action
signal may be clock, posedge clock, negedge clock for example
Named Event
event anEvent;
always @(anEvent) action // event is a keyword
OR Event
always @( signal1 or signal2 or signal3..) action
Level
always wait( signal) action // wait is a keyword
```

## A.4.3.4.2 分支

### *if, if else*

与 C 和 C++ 语言一样，Verilog 使用 if 和 if else 结构根据条件变量的值选择备用执行路径。允许的组合遵循 C 和 C++ 语法。

```
Syntax
if (condition)
    statement;
if (condition)
    statement1;
else
    statement2;
if (condition1)
    statement1;
else if (condition2)
    statement2;
else
    statement 3;
If statement comprises a block of statements, the block must be delimited by the begin-end pair.
```

如果 if 语句包含一个语句块，则该块必须由 begin-end 对界定。

## A.4.3.4.3 case 语句

Verilog 中的 switch 或 case 语句使用 Pascal 而非 C 语言语法，如所示。

```
Syntax
case (expression)
    label0:    statement0;
    label1:    statement1;
    .
    .
    .
    labeln-1:  statementn-1;
    default:   defaultStatement;
endcase
If statement comprises a block of statements, the block must be delimited by the begin-end pair.
```

如果语句包含一个语句块，则该块必须由 begin-end 对界定。

与 C 的 switch 不同，一旦求值了某个语句或语句块，控制流就会离开 case，而不是继续执行其余备选项。

## A.4.3.4.4 循环

Verilog 语言支持四种常见的循环结构：

- while
- repeat
- for
- forever。

前三种应该从 C 或 C++ 语言中很熟悉；forever 是 Verilog 所独有的。每种的语法如下。

```
**Syntax**
while(test)
begin
    loop body
end

repeat(repeatcount)
begin
    loop body
end

for(init; test; action)
begin
    loop body
end
init and action are usually assignments.

forever
begin
    loop body
end
```

## A.4.3.4.5 时序逻辑

图 A.29 中的三个代码模块演进了之前在门级和数据流级设计的门控 SR 锁存器、主从式 SR 触发器和 2 位二进制计数器的行为实现。

```
// Behavioral Level Model
// Gated SR Latch
module gated_sr_latch(q, qnot, s, r, clr, enab);
reg q, qnot;
always @(~clr or enab)
begin
if (~clr)
begin
q = 1'b0;
qnot = 1'b1;
end
end
else
begin
if(s & ~r)
begin
q <= s;
qnot <= r;
end
else if(~s & r)
begin
q <= s;
qnot <= r;
end
end
endmodule

// Use two SR Latches in a master slave
// configuration to build a flip-flop
module srmffs(q, qnot, s, r, clk, clr);
input s, clk, clr;
output q, qnot;
gated_sr_latch master(qm, qmnot, qnot, s, r, clk, clr);
gated_sr_latch slave(q, qnot, qm, qmnot, clr, ~clk);
endmodule

// Build a synchronous two bit binary up counter
// using master slave SR flip-flops
module TwoBitCounter(qA, qB, clk, clr);
input clk, clr;
output qA, qB;
reg sA, sR;
wire qA, qnotB, qB;
always @(posedge clk)
begin
qA = qA & qnot & qB;
sR = ~qA & qB;
end
srmffs FFB(qB, qBnot, sB, rB, clk, clr);
srmffs FFA(qA, qAnot, sA, sR, clk, clr);
endmodule
```

图 A.29 SR 锁存器、主从式触发器和 2 位二进制递增计数器的行为模型。

图 A.30 中的下一个代码模块说明了一种更常用的建模计数、定时或寄存器类型设计的方法。该设计不是使用单个触发器，而是采用算法方法。

```
// Build a synchronous two bit binary up counter
module TwoBitCntr(state, clr, clk);
    input clr, clk;
    output[1:0] state;

    reg[1:0] state;

// Name the states
parameter state0 = 2'b00;
parameter state1 = 2'b01;
parameter state2 = 2'b10;
parameter state3 = 2'b11;

// Build a synchronous two bit binary up counter
always @(~clr or negedge clk)
begin
    if (~clr)
    begin
        state = state0;
    end

    else case(state)
    state0:
        state = state1;
    state1:
        state = state2;
    state2:
        state = state3;
    state3:
        state = state0;
    endcase
end
endmodule
```

图 A.30 使用 case 语句的 2 位二进制递增计数器行为模型。

## A.5 测试和验证电路

一旦电路在 Verilog 中设计并建模完成，我们就进入下一阶段。首先需要验证模型功能是否正常。下一步是将其用于预定目的。为此，我们通过模型对设计执行任何我们认为必要的功能、参数和压力测试，以在提交硬件之前确认设计。

