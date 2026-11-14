

```verilog
// Dataflow Level Model
// Gated SR Latch

module gsrLatch(q, qnot, sg, rg, clr, enab);
input sg, rg, clr, enab;
output q, qnot;

wire rL, sL;

wire q, qnot;

// Build the gating logic
assign rL = rg & clr & enab;
assign sL = sg & clr & enab;

// Build the basic RS latch
assign q = ~(rL | qnot);
assign qnot = ~(sL | q);

endmodule
// Use two SR Latches in
// a master slave configuration to build a flip-flop

module srmsff(q, qnot, s, r, clk, clr);
input s, r, clk, clr;
output q, qnot;

gsrLatch master(qm, qmnot, s, r, clk, clk);
gsrLatch slave(q, qnot, qm, qmnot, clr, ~clk);
endmodule
// Build a synchronous two bit binary up counter
// using master slave SR flip-flops
module TwoBitCntr(qA, qB, clr, clk);
input clr, clk;
output qA, qB;
wire sA, rA;
wire qA, qB;
assign sA = qAnot & qB;
assign rA = qA & qB;
srmsff FFB(qB, qBnot, qBnot, qB, clk, clr);
srmsff FFA(qA, qAnot, sA, rA, clk, clr);
endmodule
```

图 A.22 SR 锁存器、主从触发器和 2 位二进制递增计数器的数据流模型。

## A.4.3.1 ALWAYS 和 INITIAL 语句

initial 和 always 语句分离控制流。在行为级，Verilog 程序结构为 initial 和/或 always 块的集合。每个此类块表达一个独立的控制流，并且每个块的执行完成与其他任何块无关。一个模块可以定义多个 initial 和/或 always 块；但是，此类块不能嵌套。除了输入、输出语句和参数声明外，所有行为语句都必须包含在这些块之一中。

initial 块、begin、end。initial 块（由 begin 和 end 分隔）中包含的语句在仿真开始时只计算一次。always 块（由 begin 和 end 分隔）中包含的语句从仿真开始起持续计算。

always, initial。always 和 initial 语句是 Verilog 中允许向模块设置激励的众多关键字中的两个。initial 语句的语法如下：

```
Syntax
initial
begin
Initial statements
end
```

always 语句的语法是：

```
Syntax
always
begin
statements to always be executed
end
```

## A.4.3.2 过程赋值

行为模型中的赋值与门级模型或数据流模型中的赋值不同。在行为模型中，使用过程赋值语句来更新电路状态变量。在数据流模型中，连续赋值结构会持续更新左侧网络的值。相比之下，在行为模型中，值仅作为过程赋值语句执行的结果进行更新。

Verilog 支持两种过程赋值：阻塞和非阻塞，以及两种块：顺序块和并行块。顺序块（由 begin 和 end 分隔）中的语句按顺序执行。并行块（由 fork 和 join 分隔）中的语句并行执行。

阻塞赋值语句按其在顺序块中编写的顺序执行。它们会阻塞同一顺序块中后续语句的执行；但不会阻塞并行块中语句的执行。非阻塞赋值不会阻塞顺序块中的后续语句。

换句话说，阻塞赋值会依次计算顺序块中每个赋值语句的右侧，然后是左侧。非阻塞赋值会先计算所有右侧，然后计算顺序块中每个语句的所有左侧。

两种赋值的语法如下：

```
Syntax
Blocking
aVariable = aValue;
NonBlocking
aVariable <= aValue;
```

## A.4.3.3 延迟

### 语法

```
Blocking
aVariable = #d aValue;
#d aVariable = aValue;
NonBlocking
aVariable <= #d aValue;
#d aVariable <= aValue
```

每种情况的解释可能有点令人困惑。

### A.4.3.3.1 阻塞

第一个语句表示：
计算 aValue；然后阻塞 d 个时间单位，再将 aValue 赋给 aVariable。随后对 aVariable 的任何使用都将获得新值。

第二个语句表示：
在计算 aVariable = aValue 之前阻塞 d 个时间单位。变量 aVariable 将在 d 个时间单位后具有值 aValue。

### A.4.3.3.2 非阻塞

第一个语句表示：
计算 aValue；安排 d 个时间单位后更新 aVariable；但是，继续处理其他语句。在接下来的 d 个时间单位内，任何使用 aVariable 值的其他变量都将被赋予旧值。

第二个语句表示：
在计算 aVariable = aValue 之前等待 d 个时间单位。变量 aVariable 将在 d 个时间单位后具有值 aValue。

图 A.23 和 A.25 中的示例将说明在相同和不同的 initial 块中，这四种情况的行为。

### 示例 A.4

从图 A.23 中代码片段的执行来看，我们观察到图 A.24 给出的输出。

- 来自两个 initial 块的变量 a 和 g 在时间 10 时改变状态。变量 (b 和 c) 以及 (h 和 i) 类似地根据其指定的延迟，分别在 a 和 g 之后两个和四个时间单位跟随。
- 阻塞语句计算完成后，计算非阻塞语句。
- 变量 d 在第一个 initial 块中的阻塞语句之后 10 个时间单位被赋值为 1；表达式 j <= 1 在第二个 initial 块中的阻塞语句之后 10 个时间单位被计算。
- 变量 e 和 f 分别在第一个 initial 块中的阻塞语句之后两个和四个时间单位被计算。
- 最后，表达式 k <= 1 和 l <= 1 分别在第二个 initial 块中的阻塞语句之后两个和四个时间单位被计算。

### 示例 A.5

```
// Illustrate Procedural blocking and non-blocking assignment
// Separate initial block
module blockingNonblocking();
    //declare temp registers
    reg a,b,c,d,e,f,g,h,i,j,k,l;

    //initialize reg variables
    initial
    begin
        a = 0; b = 0; c = 0; d = 0; e = 0; f = 0;
        g = 0; h = 0; i = 0; j = 0; k = 0; l = 0;
    end

    initial
    begin // delay on right hand side
    // blocking
    a = #10 1;
    b = #2 1;
    c = #4 1;

    // non-blocking
    d <= #10 1;
    e <= #2 1;
    f <= #4 1;
    end

    // Illustrate Procedural blocking and non-blocking assignment
    // Separate initial block
    initial
    begin // delay on left hand side

    // blocking
    #10 g = 1;
    #2 h = 1;
    #4 i = 1;

    // non-blocking
    #10 j <= 1;
    #2 k <= 1;
    #4 l <= 1;
    end

    initial
    begin
    $display("time, va, vb, vc, vd, ve, vf, vg, vh, vi, vj, vk, vl");
    $monitor($time, "%b %b %b %b %b %b %b %b %b %b %b %b", a,b,c,d,e,f,g,h,i,j,k,l);
    #50 $finish(1);
    end
    endmodule
```

图 A.23 使用过程阻塞和非阻塞赋值。

| time | a | b | c | d | e | f | g | h | i | j | k | l |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 10 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 |
| 12 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |
| 16 | 1 | 1 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 0 | 0 |
| 18 | 1 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | 1 | 0 | 0 | 0 |
| 20 | 1 | 1 | 1 | 0 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 |
| 26 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 |
| 28 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 |
| 32 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |

图 A.24 图 A.23 中模块的系统输出。

### 示例 A.6

```
// Illustrate Procedural blocking and non-blocking assignment
// Single initial block
module blockingNonblocking();
  // declare temp registers
  reg a,b,c,d,e,f,g,h,i,j,k,l;
  // initialize reg variables
  initial
    begin
    a = 0; b = 0; c = 0; d = 0; e = 0; f = 0;
    g = 0; h = 0; i = 0; j = 0; k = 0; l = 0;
    end
  initial
    begin
    // delay on right hand side
    // blocking
    a = #10 1;
    b = #2 1;
    c = #4 1;
    // non-blocking
    d = #40 1;
    e <= #2 1;
    f <= #4 1;
    // blocking left hand side
    // blocking
    #10 g = 1;
    #2 h = 1;
    #4 i = 1;
    // non-blocking
    #10 j = 1;
    #2 k <= 1;
    #4 l <= 1;
    end
  initial
    begin
    $display("Time, a, b, c, d, e, f, g, h, i, j, k, l");
    $monitor($time, " %b %b %b %b %b %b %b %b %b %b %b %b",
             a,b,c,d,e,f,g,h,i,j,k,l);
    #50 $finish(1);
    end
endmodule
```

图 A.25 使用过程阻塞和非阻塞赋值。

