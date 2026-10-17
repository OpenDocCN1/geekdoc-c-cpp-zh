
# SPARK 入门指南

**Claire Dross 和 Yannick Moy**

## 1 SPARK 概述

### 1.1 什么是 SPARK？

SPARK 指两个含义：

- 一种面向功能规范和静态验证的编程语言；
- 一套开发和验证工具。

SPARK 语言基于 Ada 的一个子集。Ada 特别适用于关键软件，因为它是为了形式化验证而设计的。Ada 2012 版本引入了方面属性（aspects）。

### 1.2 这些工具是做什么的？

我们首先回顾程序的静态验证，即在不编译或执行代码的情况下对源代码进行的验证。验证使用执行静态分析的工具。这些工具可以有多种形式。它们包括检查类型和强制执行可见性规则的工具（如编译器），以及执行更复杂推理的工具（例如像 CodePeer 等工具所使用的抽象解释）。SPARK 附带的工具执行不同形式的静态分析：

- 流分析（flow analysis）是最快的分析形式。它检查变量的初始化，并查看程序输入输出之间的数据依赖。它还能发现未使用的赋值和未初始变量。
- 证明检查（proof checks）用于确保没有运行时错误，以及程序是否符合其规范。

### 1.3 关键工具

用于 SPARK 语言形式化验证的工具是`GNATprove`。它检查是否符合 SPARK 子集，并对源代码进行流分析和证明。其他工具也使用 SPARK 语言，包括 GNAT 编译器和 GNAT Studio 集成开发环境。

### 1.4 一个简单的示例

我们从一个简单的 Ada 子程序开始，该程序使用 SPARK 方面属性来指定子程序合约。该子程序名为`Increment`，功能将其参数`X`的值加 1：

```ada
procedure Increment
X : in out Integer
with
  Global
    Depends => (X => X),
    Pre      => X = Integer,
    Post     => X = X'Old + 1;
```

```ada
procedure Increment
X : in out Integer
begin
  X := X + 1;
end Increment;
```

```text
Phase 1 of 2: generation of Global contracts ...
Phase 2 of 2: flow analysis and proof ...
increment.ads:5:10: info: overflow check proved
increment.ads:4:03: info: data dependencies proved
increment.ads:5:03: info: flow dependencies proved
increment.ads:7:14: info: postcondition proved
increment.ads:7:24: info: overflow check proved
```

这些契约使用 Ada 的 aspect（特性）功能编写，展示了该子程序的几个属性：

- SPARK Global aspect 对于安全至关重要：它表示参数`X`的值仅取决于`X`的（之前的）值。
- SPARK Depend aspect 表示`Increment`不读取或写入任何全局变量。
- Ada 的 Pre（前置）和 Post（后置）aspect 显示了`Increment`的特定属性：
  - 只有在调用之前`X`的值小于 Integer Last 时才允许调用`Increment`。这确保了子程序体中执行的操作不会发生溢出。
  - `Increment`没有对`X`进行递增：调用后`X`的值大于其调用之前的值。

`GNATprove`可以验证所有这些契约。此外，它还验证了在执行`Increment`体运行时不会抛出任何错误。

## 1.5 编程语言

理解为什么 SPARK 和 Ada 语言之间存在差异很重要。设计 Ada 的 SPARK 子集的目标是创建一个可能的、且便于进行规范和稳健验证的 Ada 子集。

Ada 最显著的限制与异常（exceptions）和访问类型（access types）有关，众所周知这两者都会显著增加完全支持所需的用户编写的注释量。向后`goto`语句和受控类型（controlled types）也不受支持，因为它们引入了非平凡的控制流。剩下的两个限制与表达式中的副作用和名称别名（aliasing）有关，我们现在将详细介绍。

## 1.6 局限性

### 1.6.1 表达式中没有副作用

SPARK 语言不允许表达式中存在副作用。换句话说，评估一个 SPARK 表达式不能更新任何对象。这一限制是为了避免依赖于求值顺序、参数传递机制或编译器优化的不可预测行为。下面`Dummy`的表达式由于两次调用`F`的求值顺序是非确定性的。因此，它不是合法的 SPARK。

Listing 3: `show_illegal_ada_code.adb`

```ada
procedure Show_Illegal_Ada_Code is
function F (X : in Integer) return Integer is
Tmp : constant Integer := X;
begin
X := X + 1;
return Tmp;
end F;

Dummy : Integer := 0;

begin
Dummy := F (Dummy) - F (Dummy); -- ??
end Illegal_Ada_Code;
```

#### 构建输出

```text
show_illegal_ada.code:13:20- error: value may be affected by call to "F" because order of evaluation is arbitrary

gprbuild: compilation phase failed
```

#### 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

show_illegal_ada.code:13:28- error: value may be affected by call to "F" because order of evaluation is arbitrary

gnatprove: error during generation of Global contracts
```

事实上，上面的代码并不是非法的 Ada，因此 GNAT 编译器生成相同的顺序。当`GNATProve`对以下被 Ada 编译器接受的等代码产生错误时，SPARK 就会受到影响：

> Listing 4: `show_illegal_spark_code.adb`

```ada
procedure Show_Illegal_SPARK_Code is

Dummy : Integer := 0;

function F return Integer is
Tmp : constant Integer := Dummy;
begin
Dummy := Dummy + 1;
return Tmp;
end F;

begin
Dummy := F - F; -- ??
end_Illegal_SPARK_Code;
```

#### 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow

show_illegal_spark.code:5:13- error: function with output output global "Dummy" is not allowed in SPARK

gnatprove: error during analysis of data and information flow
```

SPARK 通过禁止函数中的副作用来强制表达式无副作用，这包括对参数或全局变量的操作。因此，SPARK 禁止带有`out`或`in out`参数的函数，同时也禁止修改全局变量的函数。下面的函数`F`在 SPARK 中是非法的，而函数`Incr`如果不修改任何全局变量则可能是合法的，如果函数`Incr_Log`修改了全局变量来执行记录，则可能是非法的。

```ada
function F (X : in Integer) return Integer; -- 非法
```

```ada
function Incr (X : Integer) return Integer; -- OK?
```

```ada
function Incr_And_Log (X : Integer) return Integer; -- OK?
```

在许多情况下，你可以轻松用带有返回计算值的`out`参数的过程来替换这些函数。

在函数体方面，GNAT 证明了这些函数没有副作用。例如，函数`Incr`和`Incr_And_Log`具有相同的签名，但只有`Incr`在 SPARK 中：`Incr_And_Log`不是：它尝试更新全局变量`Call_Count`。

Listing 5: `side_effects.ads`

```ada
package Side_Effects is
function Incr (X : Integer) return Integer; -- OK
function Incr_And_Log (X : Integer) return Integer; -- 非法
end Side_Effects;
```

Listing 6: `side_effects.sp`

```ada
package body Side_Effects is
function Incr (X : Integer) return Integer is
begin
  return X;
end Incr;

function Incr_And_Log (X : Integer) return Integer is
begin
  Call_Count := Call_Count + 1;
  return X;
end Incr_And_Log;
```

### 1.6.2 名称别名

SPARK 施加的另一个限制涉及名称别名。如果两个名称指向同一个对象，我们就称它们为别名。SPARK 禁止使用别名的原因如下：

- 这会变得非常困难，因为必须考虑不同名称实际上更新了同一个对象的情况。
- 结果从用户的角度来看可能是出乎意料的。程序的输出可能取决于编译器的特定属性，例如参数传递机制，当……

别名也可以发生在过程调用的一部分。当调用过程时，SPARK 会验证`out`参数与过程体中修改的另一个参数是否存在别名。使用访问类型（指针）也可能产生别名。这些在 SPARK 中是被限制的，以便只允许良性的别名，即当两个名称都用于读取数据时。

> 5 https://en.wikipedia.org/wiki/Aliasing

## SPARK 简介

具体而言，访问对象之间的赋值操作了一个所有权的转移，源对象失去对其读取或写入底层分配内存的权限。

过程`Ownership_Transfer`是在 Ada 中合法但在 SPARK 中由于别名（aliasing）被拒绝的代码示例：

Listing 8: `ownership_transfer.adb`

```ada
procedure Ownership_Transfer is
  type IntPtr is access Integer;
  X : IntPtr;
  Y : IntPtr;
  Dummy : Integer;
begin
  X := new Integer'(1);
  X.all := X.all + 1;
  Y := X;
  Y.all := Y.all + 1;      illegal
  X.all := X.all + 1;      illegal
  X.all := 1;              illegal
  Dummy := X.all;         illegal
end Ownership_Transfer;
```

#### 输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

ship_transfer.adb:11:06: error: dereference from "X" is not writable

ship_transfer.adb:11:06: error was moved at line 9

ship_transfer.adb:11:15: error: dereference from "X" is not readable

ship_transfer.adb:11:15: error was moved at line 9

ship_transfer.adb:12:06: error: dereference from "X" is not writable

ship_transfer.adb:12:06: error was moved at line 9

ship_transfer.adb:13:15: error: dereference from "X" is not readable

ship_transfer.adb:13:15: error was moved at line 9

gnatprove: error during analysis of data and information flow
```

在`X`和`Y`赋值后，变量`X`无法用于读取或写入底层分配的内存。

> **注意：** 有关这些限制的更多细节，请参阅 SPARK 用户指南。

## 1.7 指定 SPARK 代码

SPARK 语言被限制为易于指定和验证的结构，有时你无法或不愿在整个代码库中遵守这些限制。因此，SPARK 工具只检查你标识为 SPARK 的 SPARK 子集代码。

你通过名为`SPARK_Mode`的属性（aspect）来实现这一点。如果没有显式指定，则 SPARK Mode 为关闭，这意味着你可以在代码中使用完整的 Ada 功能，并且它不应被`Gnatprove`识别。你可以选择性地（在某些单元或子程序上）或全局性（使用配置 pr，这是我们在教程中所做的）更改此默认设置。为了简单地重用现有的 Ada 库，导入单元中声明的没有显式 SPARK Mode 的实体可以在 SPARK 代码中使用。工具仅对 SPARK 代码中实际使用的实体声明进行 SPARK 合规性检查。

这里是使用`SPARK_Mode`属性的一个常见用法：

```ada
package P
with SPARK_Mode => On
is
  -- 包规范属于 SPARK，因此可以被 SPARK 客户端使用
end P;
package body P
with SPARK_Mode => Off
is
  -- 体不属于 SPARK，因此被 GNATprove 忽略
end P;
```

包 P 只定义了属于 SPARK 子集的规范。然而，它希望在体中使用所有的 Ada 特性。因此，该体不应被分析，并且其`SPARK_Mode`属性应设置为`Off`。

你可以按单元为单位细粒度地指定`SPARK_Mode`。一个 Ada 包包含四个部分：规范的可见部分和私有部分，以及体的声明部分和语句部分。你可以在这些任何部分上将`SPARK_Mode`设置为`On`或`Off`。同样，一个子程序（subparagraph）有两个部分：它的规范和它的体。

SPARK 中的一条通用规则是：一旦 Mode 设置为`Off`，在包或子程序的同一部分中永远无法切换回`On`。这防止了在之前设置为`SPARK_Mode Off`的单元中将`SPARK_Mode`切回`On`。

> **注意：** 有关`SPARK Mode`使用的更多细节，请参阅 SPARK 用户指南。

## 1.8 代码示例 / 陷阱

### 1.8.1 示例 1

这是一个定义 Element 对象的抽象栈类型的包，它提供了栈的通常功能。该包被标记为属于 SPARK 子集。

Listing 9: `stack_package`

```ada
package Stack_Package
with SPARK_Mode => On
is
  type Element is new Natural;
  type Stack is private;
  function Empty return Stack;
  procedure Push (S : in out Stack; E : Element);
  function Pop (S : in out Stack) return Element;
private
  type Stack is record
    Top : Integer;
end record;
end Stack_Package;
```

#### 证明输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

stack_package.ads:9:13: error: "in out" parameter is not allowed in SPARK

stack_package.ads:9:13: error: violation of SPARK Mode at line 2

gnatprove: error during data and information flow
```

SPARK 不允许副作用。因此，`Pop`不允许修改参数`S`。

### 1.8.2 示例 2

让我们转换为抽象状态机栈，提供单个栈实例。栈的内容（全局变量`Content`和`Pop`）对客户端不可见。在简化版本中，只有`Pop`函数对客户端可用。包的规范和体被标记为属于 SPARK。

> Listing 10: `global_stack`



```ada
package Global_Stack
with SPARK_Mode => On
type Element is new Integer;
function Pop return Element;
end Global_Stack;
```

> Listing 11: `global_stack.adb`

```ada
package body Global_Stack
with SPARK_Mode => On
Max : constant Natural := 100;
type Element_Array is array (1 .. Max) of Element;
Content : Element_Array;
Top : Natural;
function Pop return Element is
E : constant Element := Content(Top);
begin
Top := Top - 1;
return E;
end Pop;
end Global_Stack;
```

# 证明输出

Phase 1 of 2: generation of Global contracts

Phase 2 of 2: analysis of data and information flow

`global_stack.adb:7:04`: warning: variable "Content" is read but never assigned [-gnatw]

`global_stack.adb:6:13`: error: function with output "Top" is not allowed in SPARK

`gnatprove`: error analysis of data and information flow

如上，函数应该没有副作用。在这里，`Pop` 更新全局变量 `Top`，这是不允许的。

### 1.8.3 示例 3

我们现在考虑两个过程：`Permute` 和 `Swap`。`Permute` 对 `X` 和 `Y` 的值应用循环排列。

> Listing 12: `p.ads`

```ada
package P
with SPARK_Mode => On
is
  procedure Permute (X, Y, Z : in out Positive);
  procedure Swap (X, Y : in out Positive);
end P;
```

> Listing 13: `p.adb`

```ada
package body P
with SPARK_Mode => On
is
  procedure Permute (X, Y, Z : in out Positive) is
    Tmp : constant Positive := X;
  begin
    X := Y;
    Y := Z;
    Z := Tmp;
  end Permute;

  procedure Swap (X, Y : in out Positive) is
  begin
    Permute (X, Y);
  end Swap;
end P;
```

> Listing 14: `test_swap.adb`

```ada
with P; use P;
procedure Test_Swap
with SPARK_Mode => On
is
  A : Integer := 1;
  B : Integer := 2;
begin
  Swap (A, B);
end Test_Swap;
```

# 构建输出

`p.adb:14:19`: error: writable actual for "Y" overlaps with actual "Z"

`gprbuild`: *** compilation failed

# 证明输出

Phase 1 of 2: generation of Global contracts

`p.adb:14:19`: error: writable actual for "Y" overlaps with actual "Z"

`gnatprove`: error during generation of Global contracts

在这里，`Y` 和 `Z` 的值被别名以调用 `Permute`，这在 SPARK 中是不允许的。事实上，在特定情况下，这违反了 Ada 规则，因此 Ada 编译器也发出了相同的错误。

在这个例子中，我们看到了为什么 SPARK 不允许别名的原因：因为 `Y` 和 `Z` 是 `Positive` 类型，它们是通过复制传递的，调用 `Permute` 的结果取决于它们在调用后被复制的顺序。

这段代码是正确的。对 `Swap` 的调用是安全的：同一个记录的两个不同组件不能引用同一个对象。

### 1.8.5 示例 #5

这里是对上一个示例的微调，使用数组代替记录：`Swap_Indexes` 在存储在数组 `A` 中的值上调用 `Swap`。

> Listing 17: `pads`

```ada
package P
with SPARK_Mode => On
is
  type P_Array is Array (Natural range <>) of Positive;
  procedure Swap_Indexes (A : in out P_Array; J : Natural);
  procedure Swap (X, Y : in out Positive);
end P;
```

> Listing 18: `pdb`

```ada
package body P
with SPARK_Mode => On
is
  procedure Swap (X, Y : in out Positive) is
  begin
    Tmp : Constant := X;
    X := Y;
    Y := Tmp;
  end Swap;

  procedure Swap_Indexes (A : in out P_Array; I, J : Natural) is
  begin
    Swap (A (I), A (J));
  end Swap_Indexes;
end P;
```

## 证明器输出

阶段 1 的 2: 生成全局契约

阶段 2 的 2: 分析数据和信息流 ...

`p.adb:13:13`: medium: 形式参数 "X" 和 "Y" 可能存在别名 (SPARK RM 6.4.-2)

`gnatprove`: 未证明的消息被视为错误

GNATprove 会探测到可能的别名情况。与之前的示例不同，当我们调用 `Swap` 时，它无法获知两个元素 `A (I)` 和 `A (J)` 实际上是不同的。GNATprove 会发布一条检查消息而不是错误，这允许在审查后对该消息进行证明（这意味着你已经手动验证了这种情况实际上不会发生）。

14

### 1.8.6 示例 #6

我们现在考虑一个声明了 `Dictionary` 类型的包，该类型是一个包含每个字母一个单词的数组。`Store` 过程允许我们在字典的正确索引处插入单词。

> Listing 19: `p.ads`

```ada
with Ada.Finalization;

package P
with SPARK_Mode => On
is
  subtype Letter is Character range 'a' .. 'z';
  type String_Access is new Ada.Finalization.Controlled with record
    Ptr : Access String;
  end record;
  type Dictionary is array (Letter) of String_Access;

  procedure Store (D : in out Dictionary; W : String);
end P;
```

> Listing 20: `p.adb`

```ada
package body P
with SPARK_Mode => On
is
  procedure Store (D : in out Dictionary; W : String)
    First Letter : constant Letter := W(W'First);
  begin
    D (First).Ptr := new String(W);
  end Store;
end P;
```

## 证明器输出

阶段 1 的 2: 生成全局契约 ...

阶段 2 的 2: 分析数据和信息流 ...

`pads.7:07`: error: "StringAccess" 不允许在 SPARK 中（由于 controlled_types）违反了第 2 行的 SPARK Mode 属性，该表达式在 SPARK 中是不允许 (SPARK Mode 3.10(3))

`pads.7:31`: error: 违反了不允许在 SPARK 中的属性（由于 controlled_types），对象或表达式部分在第 2n 行的 SPARK Mode 中是不允许

`pads.7:09`: error: "controlled" 不允许在 SPARK 中（由于 controlled_types）

`pads.7:09`: error: 违反了第 4 行的 SPARK Mode 属性

`pads.10:04`: error: "StringAccess" 不允许在 SPARK 中（由于 controlled_types）

`pads.10:04`: error: 违反了第 4 行的 SPARK Mode 属性

`gatprove`: 在分析数据和信息流期间出错

这段代码是不正确的：控制类型（controlled types）不是 SPARK 子集的一部分。解决方案是使用 `SPARK.Mode` 以细粒度将 `String_Access` 的定义与代码的其他部分分离。

### 1.8.7 示例 #7

这是上一个示例的新版本，我们对其进行了修改，将控制类型隐藏在包 `P` 的私有部分，并在私有部分的开头使用 `pragma SPARK_Mode (Off)`。

> Listing 21: `p.ads`

```ada
with Ada.Finalization;
package P
  with SPARK_Mode => On
is
  subtype Letter is Character range 'a' .. 'z';
  type String_Access is private;
  type Dictionary is array (Letter) of String_Access;
  function New_Access (W : String) return String_Access;
  procedure Store (D : in Dictionary; W : String);
private
  pragma SPARK_Mode (Off);
  type String_Access is new Ada.Finalization.Controlled with record
    Ptr : access String;
  end record;
  function New_Access (W : String) return String_Access
  (Ada.Finalization.Controlled with Ptr => new String(W));
end P;
```

## 教程输出

- 阶段 1 的 2: 生成全局契约 ...

- 阶段 2 的 2: 分析数据和信息流 ...

由于控制类型的定义和使用是 GNATprove 生成的代码的一部分，这段代码是正确的。

### 1.8.8 示例 #8

我们将包 `P` 的规范与之前的实现体结合起来。

> Listing 22: `p.ads`

```ada
with Ada.Finalization;
package P
  with SPARK_Mode => On
is
  subtype Letter is Character range 'a' .. 'z';
  type String_Access is private;
  type Dictionary is array (Letter) of String_Access;
  function New_Access (W : String) return String_Access;
  procedure Store (D : in Dictionary; W : String);
private
```

（继续下一页）

（接上页）

```ada
  pragma SPARK_Mode (Off);

  type String_Access is new Ada.Finalization.Controlled with record
    Ptr : access String;
  end record;
  function New_Access (W : String) return String_Access
(Ada.Finalization.Controlled with Ptr => new String(W));
end P;
```

> Listing 23: `p.adb`

```ada
package body P
with SPARK_Mode => On
is
  procedure Store (D : in Dictionary; W : String)

First Letter : constant Letter := W(W'First);
  begin
    D (First).Ptr := new String(W);
  end Store;
end P;
```

阶段 1 的 2: 生成全局契约 ...

```text
p.adb:13:13: medium: 形式参数 "X" 和 "Y" 可能存在别名 (SPARK RM 6.4.-2)
```

阶段 2 的 2:

阶段 2 的 2: 分析数据和信息流 ...

`gnatprove`: 未证明的消息被视为错误

`gnatprove`: 在分析数据和信息流期间出错

`Store` 的实现体没有使用任何不在 SPARK 子集的构造，但我们仍然无法将 SPARK Mode 开启。

### 1.8.9 示例 #9

接下来，我们将 `Store` 过程的声明移动到另一个名为 `Q` 的包。

> Listing 24: `p.ads`

```ada
with Ada.Finalization;

package P
with SPARK_Mode => On
is
  subtype Letter is Character range 'a' .. 'z';
  type String_Access is private;
  type Dictionary is array (Letter) of String_Access;

  function New_Access (W : String) return String_Access;

private
  pragma SPARK_Mode (Off);

  type String_Access is new Ada.Finalization.Controlled with record
    Ptr : access String;
  end record;
```

（继续下一页）

（接上页）

```ada
function New_Access (W : String) return String_Access
(Ada.Finalization.Controlled with Ptr => new String(W));
end P;
```

> Listing 25: `q.ads`

```ada
with P; use P;
package Q
with SPARK_Mode => On
is
  procedure Store (D : in out Dictionary; W : String);
end Q;
```

> Listing 26: `q.adb`

```ada
package body Q
with SPARK_Mode => On
is
  procedure Store (D : in out Dictionary; W : String) is
    First_Letter : constant Letter := W (W'First);
  begin
    D (First_Letter) := New_String_Access (W);
  end Store;
end Q;
```

## 证明器输出

阶段 1 的 2: 生成全局契约 ...

阶段 2 的 2: 分析数据和信息流 ...

一切正常：我们成功保留了控制类型的使用，同时让大部分代码处于 SPARK 子集中，因此 GNATprove 能够进行分析。

### 1.8.10 示例 #10

我们的最后一个示例是一个包含两个函数的包，用于在数组 `A` 中搜索值 `0`。第一个函数在 `A` 中未找到 0 时抛出异常，另一个在情况下简单的返回 0。

> Listing 27: `p.ads`

```ada
package P
with SPARK_Mode => On
is
  type N_Array is (Positive range <>) of Natural;
  Not_Found : exception;
  function Search_Zero_P (A : N_Array) return Positive;
  function Search_Zero_N (A : N_Array) return Natural;
end P;
```

> Listing 28: `p.adb`

```ada
package body P
with SPARK_Mode => On
is
```




```ada
function Search_Zero_P (A : N_Array) return Positive is
begin
  for I in A'Range loop
    if A (I) = 0 then
      return I;
    end if;
  end loop;
  raise Not_Found;
end Search_Zero_P;

function Search_Zero_N (A : N_Array) return Natural is
with SPARK Mode => Off is
begin
  return Search_Zero_P (A);
exception
  when Not Found => return 0;
end Search_Zero_N;
end P;
```

## Prover 输出

Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: flow analysis and proof ...

`p.adb:11:07: medium: exception might be considered as errors`

`gnatprove: unproved check messages considered as errors`

这段代码是完全正确的，尽管使用了异常处理，因为我们仔细地隔离了这一非 SPARK 特性，将其放在一个标记为 `SPARK Mode => Off` 的函数体中，因此 `GNATprove` 忽略了它。然而，`GNATprove` 试图证明 `Not_Found` 在 `Search_Zero_P` 中从未被抛出，从而产生了一条关于可能抛出异常的消息。查看 `Search_Zero_N`，确实在某些情况下可能会抛出异常，这意味着你需要使用其他方法（如同行评审或测试）来验证 `Not_Found` 是否仅在适当的情况下被抛出。

## 1.8 代码示例 / 陷阱

# 流分析

在本节中，我们将介绍由 `GNATprove` 工具提供的流分析能力，这是使用 SPARK 的一项关键工具。

## 2.1 流分析是做什么的？

流分析主要集中在变量上。它模拟了信息在子程序执行期间如何在变量之间流转，将变量的最终值与其初始值连接起来。它分析了在库级别定义的全局变量、局部变量以及子程序的形式参数。

子程序的嵌套创建了我们所谓的“作用域变量”：在包含单元中局部声明的变量。从嵌套子程序的角度来看，作用域变量看起来非常像全局变量。

流分析通常很快，速度大约与编译相当。它能检测各种类型的错误和对某些 SPARK 合法性规则的违反，例如缺少别名以及表达式不受副作用影响的规则。我们在 SPARK 概述（第 3 页）中讨论过这些规则。

流分析是完备的：如果它没有检测到它应该检测的任何类型错误，我们就知道不存在此类错误。

## 2.2 检测到的错误

### 2.2.1 未初始化变量

我们现在介绍流分析检测到的每一类错误。第一种是读取未初始化的变量。这始终是一个错误：它引入了非确定性并破坏了系统，因为未初始化变量的值可能超出其子类型的范围。由于某些原因，SPARK 要求每个变量在使用之前必须进行初始化。

流分析负责确保 SPARK 代码满足所有要求。例如，对于所示的 `Max_Array` 函数，我们忘记了在进入循环之前初始化变量 `Max`。结果，`if` 语句条件读取的值可能是未初始化的。流分析会检测并报告这一错误。

列表 1：`show_uninitialized.ads`

```ada
package Show_Uninitialized is
  type Array_Of_Naturals is array (Integer range =>) of Natural;
  function Max_Array (A : Array_Of_Naturals) return Natural;
```

（接上页）

```ada
end Show_Uninitialized;
```

列表 2：`show_uninitialized.adb`

```ada
package Show_Uninitialized is

  function Max_Array (A : Array_Of_Naturals) return Natural is
    Max : Natural;
  begin
    for I in A'Range loop
      if A (I) > Max then -- Max 可能未初始化
        Max := A (I);
    end loop;
    return Max;
  end Max_Array;

end Show_Uninitialized;
```

## Prover 输出

Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

`show_uninitialized.adb:7:21: warning: "Max" may be referenced before it has been initialized [enabled by default]`

`show_uninitialized.adb:7:22: medium: "Max" might not be initialized`

`show_uninitialized.adb:11:14: medium: "Max" might not be initialized`

`gnatprove: unproved check messages considered as errors`

> 注意：关于流分析如何验证初始化的细节，请参阅《SPARK 用户指南》。

### 2.2.2 无效语句

无效语句与死代码（dead code）不同：它们会被执行，并且通常会修改变量的值，但对子程序的任何可见输出（参数、全局变量或函数结果）没有影响。应该避免无效语句，因为它们会让代码的可读性降低并难以维护。

更重要的是，它们通常是由程序中的错误引起的：该语句可能是为了某些目的编写的，但没有被使用。这类错误在他人代码中很难检测。例如，`Swap1` 和 `Swap2` 没有正确地使用它们的参数 `X` 和 `Y`。这个错误导致一条语句变得无效。该无效语句本身并不是错误，但流分析会产生警告，因为这可能是错误的征象，在此处确实如此。

列表 3：`show_ineffective_statements.ads`

```ada
package Show_Ineffective_Statements is
  type T is Integer; (接下页)
```

> 9 <https://docs.ada.dev/live/spark/2014/html/spark2014_ug/language_restrictions.html#initialization-policy>

（接上页）

```ada
procedure Swap1 (X, Y : out T);
procedure Swap2 (X, Y : out T);
end Show_Ineffective_Statements;
```

列表 4：`show_ineffective_statements.adb`

```ada
package Show_Ineffective_Statements is

  procedure Swap1 (X, Y : out T) is
    Tmp : T;
  begin
    Tmp := X; -- 这条语句是无效的
    X := Y;
    Y := X;
  end Swap1;

  procedure Swap2 (X, Y : out T) is
    Tmp : T := 0; -- 这个变量未使用
  begin
    X := Y;
    Y := Tmp;
  end Swap2;
  
end Show_Ineffective_Statements;
```

### 2.2.3 作用域变量

流分析主要集中在变量上。它模拟了信息在子程序执行期间如何在变量之间流转，将变量的最终值与其初始值连接起来。它分析了在库级别定义的全局变量、局部变量以及子程序的形式参数。

子程序的嵌套创建了我们所说的作用域变量：在包含单元中局部声明的变量。从嵌套子程序的角度来看，作用域变量看起来非常像全局变量。

流分析通常很快，速度大约与编译相当。它能检测各种类型的错误和对某些 SPARK 合法性规则的违反，例如缺少别名以及表达式不受副作用影响的规则。我们在 SPARK 概述（第 3 页）中讨论过这些规则。

流分析是完备的：如果它没有检测到它应该检测的任何类型错误，我们就知道不存在此类错误。

## 第 2 章：流分析

# SPARK 简介




这段代码是完全正确的，尽管使用了异常处理，因为我们仔细地隔离了这一非 SPARK 特性，将其放在一个标记为 SPARK Mode 为 Off 的函数体中，因此 GNATprove 忽略了它。然而，GNATprove 试图证明 `Not_Found` 在 `Search_Zero_P` 中从未被抛出，从而产生了一条关于可能抛出异常的消息。查看 `Search_Zero_N`，确实在某些情况下可能会抛出异常，这意味着你需要使用其他方法（如同行评审或测试）来验证 `Not_Found` 是否仅在适当的情况下被抛出。

## 1.8 代码示例 / 陷阱

# 第二章 流分析

在本节中，我们将介绍由 GNATprove 工具提供的流分析能力，这是使用 SPARK 的一项关键工具。

## 2.1 流分析是做什么的？

流分析主要集中在变量上。它模拟了信息在子程序执行期间如何在变量之间流转，将变量的最终值与其初始值连接起来。它分析了在库级别定义的全局变量、局部变量以及子程序形式参数。

子程序的嵌套创建了我们所说的“作用域变量”：在包含单元中局部声明的变量。从嵌套子程序的角度来看，作用域变量看起来非常像全局变量。

流分析通常很快，速度大约与编译相当。它能检测各种类型的错误和对某些 SPARK 合法性规则的违反，例如缺少别名以及表达式不受副作用影响的规则。我们在 SPARK 概述（第 3 页）中讨论过这些规则。

流分析是完备的：如果它没有检测到它应该检测的任何类型错误，我们就知道不存在此类错误。

## 2.2 检测到的错误

### 2.2.1 未初始化变量

我们现在介绍流分析检测到的每一类错误。第一种是读取未初始化的变量。这始终是一个错误：它引入了非确定性并破坏了系统，因为未初始化变量的值可能超出其子类型的范围。由于某些原因，SPARK 要求每个变量在使用之前必须进行初始化。

流分析负责确保 SPARK 代码满足所有要求。例如，对于所示的 `Max Array` 函数，我们忘记了在进入循环之前初始化变量 `Max`。结果，`if` 语句条件读取的值可能是未初始化的。流分析会检测并报告这一错误。

列表 1：`show_uninitialized.ads`

```ada
package Show_Uninitialized is
  type Array_Of_Naturals is array (Integer range =>) of Natural;
  function Max_Array (A : Array_Of_Naturals) return Natural;
```

# SPARK 简介

（接上页）

```ada
end Show_Uninitialized;
```

列表 2：`show_uninitialized.adb`

```ada
package Show_Uninitialized is

  function Max_Array (A : Array_Of_Naturals) return Natural is
    Max : Natural;
  begin
    for I in A'Range loop
      if A (I) > Max then -- Max可能未初始化
        Max := A (I);
    end loop;
    return Max;
  end Max_Array;

end Show_Uninitialized;
```

### Prover 输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

show_uninitialized.adb:7:21: warning: "Max" may be referenced before it has been initialized [enabled by default]

show_uninitialized.adb:7:22: medium: "Max" might not be initialized

show_uninitialized.adb:11:14: medium: "Max" might not be initialized

gnatprove: unproved check messages considered as errors
```

> 注意：关于流分析如何验证初始化的细节，请参阅《SPARK 用户指南》。

### 2.2.2 无效语句

无效语句与死代码不同：它们会被执行，并且通常会修改变量的值，但对子程序的任何可见输出（参数、全局变量或函数结果）没有影响。应该避免无效语句，因为它们会让代码的可读性降低并难以维护。

更重要的是，它们通常是由程序中的错误引起的：该语句可能是为了某些目的编写的，但没有被使用。这类错误在他人代码中很难检测。例如示例，`Swap1` 和 `Swap2` 没有正确地使用它们的参数 `X` 和 `Y`。这个错误导致一条语句变得无效。该无效语句本身并不是错误，但流分析会产生警告，因为这可能是错误的征象，在此处如此。

列表 3：`show_ineffective_statements.adb`

```ada
package Show_Ineffective_Statements is
  type T is Integer; (接下页)
```

> 9 <https://docs.ada.dev/live/spark/2014/html/spark2014_ug/language_restrictions.html#initialization-policy>

## 第 2 章 流分析

# SPARK 简介

（接上页）

```ada
procedure Swap1 (X, Y : out T);
procedure Swap2 (X, Y : out T);
end Show_Ineffective_Statements;
```

列表 4：`show_ineffective_statements.adb`

```ada
package Show_Ineffective_Statements is

  procedure Swap1 (X, Y : out T) is
    Tmp : T;
  begin
    Tmp := X; -- 这条语句是无效的
    X := Y;
    Y := X;
  end Swap1;

  procedure Swap2 (X, Y : out T) is
    Tmp : T := 0; -- 这个变量未未使用
  begin
    X := Y;
    Y := Tmp;
  end Swap2;
  
end Show_Ineffective_Statements;
```

### Prover 输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

show_uninitialized.adb:7:21: warning: "Max" may be referenced before it has been initialized [enabled by default]

show_uninitialized.adb:7:22: medium: "Max" might not be initialized

show_uninitialized.adb:11:14: medium: "Max" might not be initialized

gnatprove: unproved check messages considered as errors
```

# SPARK 简介

全局变量 `X` 的值且不访问任何其他全局变量。如果我们通过注释执行此操作（正如在其他语言中通常这样做），GNATprove 无法验证代码是否按照此规范编译：

```ada
package Show_Global_Contracts is

X : Natural := 0;

function Get_Of_X return Natural;
  -- Get_Of_X 读取全局变量 X 的值
end Show_Global_Contracts;
```

你可以在子程序规范中编写全局合约（global contracts）。除了在流分析中的价值外，它们还为子程序的用户提供了有用的信息。你为 `Global` 属性指定的值是全局变量的聚合列表，根据它们的类型进行分组。

在示例中，`Set_X_To_Y_Plus` 过程读取 `Y` 和 `Z`。我们通过将它们指定为 `Input` 的值来指示这一点。它读取 `X`，我们使用 `Output` 来指定它。由于 `Set_X_To_Y_Plus` 写入 `X` 及其初始值，因此 `X` 的模式是 `In_Out`。像参数一样，全局属性中没有指定模式，默认为 `Input`。在 `Get_Of_X` 的声明中也是如此。最后，如果子程序（如 `Incr_Parameter_X`）没有引用任何全局变量，你将全局合约的值设置为 `null`。

列表 7：`show_global_contracts.ads`

```ada
package Show_Global_Contracts is

X, Y, Z : Natural := 0;

procedure Set_X To_Y_Plus with
  Global = (Input => (Y, Z),   -- 读取 Y 和 Z 的值
  Output = X);               -- 修改 X 的值

procedure Set_X To_X_Plus with
  Global = (Input => Y,       -- 读取 Y 的值
  In_Out = X);               -- 修改 X 的值
                             -- 读取其初始值

function Get_Of_X return Natural with
  Global = X;               -- 读取全局变量 X 的值

procedure Incr_Parameter_X (X : in out Natural) with
  Global = null;            -- 不引用任何全局变量

end Show_Global_Contracts;
```

# 证明器输出

- 第 1 阶段（共 2 阶段）：生成全局合约...
- 第 2 阶段（共 2 阶段）：分析数据和信息流 ...

> 注意：有关全局合约的更多信息，请参阅 SPARK 用户指南10。

10 <https://docs.adaore.com/live/wave/spark2014/html/spark2014_ug/en/source/subprogram_contracts.html#ndata-dependencies>

## 2.3 其他验证

# SPARK 简介

### 2.3.2 依赖合约（Depends Contracts）

你也可以为子程序提供合约，以指定输入和输出之间的依赖关系。这些依赖关系不仅包括作为参数的全局变量以及的结果。当你为子程序提供 `Depends` 合约时，流分析将显示它是正确的，也就是说，对于每个依赖项，变量依赖于列出的变量，而不依赖于其他。

例如，你可能想表示下所示 `Swap` 的每个参数的值仅依赖于参数的初始值，而 `Set_X_Zero` 返回后 `X` 的值依赖于全局变量。如果你像其他语言一样通过注释指示这一点，GNATprove 将验证这确实如此。

```ada
package Show_Depends_Contracts is
```

```ada
type T is Integer;

procedure Swap (X, Y : in out T);
  -- 调用后 X（相应 Y） 的值仅依赖于
  -- 调用前的 Y（相应 X） 的值

X : Natural;
procedure Set_X_Zero;
  -- 调用后 X 的值不依赖于任何输入

procedure Show_Depends_Contracts;
```

像 `Global` 属性一样，你可以在子程序声明中使用属性（aspect）指定 `Depends` 合约。它的值是子程序输出和输入之间的一个或多个依赖关系列表。每个关系由两个用箭头分隔的变量列表表示。每个箭头的左侧是变量，其最终值依赖于右侧变量列表的初始值。

例如，我们指示 `Swap` 的每个参数的最终值仅依赖于另一个参数的初始值。如果子程序是一个函数，我们将其列为输出，使用 `Result` 属性，正如我们对 `Get_Value_Of_X` 所做的那样。

列表 8：`show_depends_contracts.ads`

```ada
package Show_Depends_Contracts is
type T is Integer;
X, Y, Z : T := 0;

procedure Swap (X, Y : in out T) with
  Depends => (X = Y);
  -- X 依赖于 Y 的初始值
  Y := X;
  -- Y 依赖于 X 的初始值

function Get_Value_Of_X return T with
  Depends => (Get_Value_Of_X.Result => X);
  -- 结果依赖于 X 的初始值

procedure Set_X_To_Plus_Z with
  Depends => (X = (Y, Z));
  -- X 依赖于 Y 和 Z 的值

procedure Set_X_To_Plus_Y with
  Depends => (X = Y);
  -- X 依赖于 Y 的初始值

procedure Set_X_To_X_Plus with
  Depends => (In_Out = X);
  -- X 依赖于 X 的初始值
  -- 读取其初始值

procedure Do_Nothing (X : T) with
  Depends => (null);
  -- 不依赖任何全局变量

end Show_Depends_Contracts;
```

（注：原文此处有 continued from previous page）

```ada
package Show_Depends_Contracts is
type T is Integer;
X, Y, Z : T := 0;

procedure Swap (X, Y : in out T) with
  Depends => (X = Y);
  -- X 依赖于 Y 的初始值
  Y := X;
  -- Y 依赖于 X 的初始值

function Get_Value_Of_X return T with
  Depends => (Get_Value_Of_X.Result => X);
  -- 结果依赖于 X 的初始值

procedure Set_X_To_Plus_Z with
  Depends => (X = (Y, Z));
  -- X 依赖于 Y 和 Z 的值

procedure Set_X_To_Plus_Y with
  Depends => (X = Y);
  -- X 依赖于 Y 的初始值

procedure Set_X_To_X_Plus with
  Depends => (In_Out = X);
  -- X 依赖于 X 的初始值
  -- 读取其初始值

procedure Do_Nothing (X : T) with
  Depends => (null);
  -- 不依赖任何全局变量

end Show_Depends_Contracts;
```

# 证明器输出

- 第 1 阶段（共 2 阶段）：生成全局合约...
- 第 2 阶段（共 2 阶段）：分析数据和信息流

通常，`Global` 属性的值是全局变量的聚合列表，根据它们的类型进行分组。

在示例中，`Set_X_To_Y_Plus` 过程读取 `Y` 和 `Z`。我们通过将它们指定为 `Input` 的值来指示这一点。它读取 `X`，我们使用 `Output` 来指定它。由于 `Set_X_To_Y_Plus` 写入 `X` 及其初始值，因此 `X` 的模式是 `In_Out`。像参数一样，全局属性中没有指定模式，默认为 `Input`。在 `Get_Of_X` 的声明中也是如此。最后，如果子程序（如 `Incr_Parameter_X`）没有引用任何全局变量，你将全局合约的值设置为 `null`。

列表 7：`show_global_contracts.ads`

```ada
package Show_Global_Contracts is

X, Y, Z : Natural := 0;

procedure Set_X To_Y_Plus with
  Global = (Input => (Y, Z),   -- 读取 Y 和 Z 的值
  Output = X);               -- 修改 X 的值

procedure Set_X To_X_Plus with
  Global = (Input => Y,       -- 读取 Y 的值
  In_Out = X);               -- 修改 X 的值
                             -- 读取其初始值

function Get_Of_X return Natural with
  Global = X;               -- 读取全局变量 X 的值

procedure Incr_Parameter_X (X : in out Natural) with
  Global = null;            -- 不引用任何全局变量

end Show_Global_Contracts;
```

# 证明器输出

第 1 阶段（共 2 阶段）：生成全局合约...

第 2 阶段（共 2 阶段）：分析数据和信息流 ...

> 注意：有关全局合约的更多信息，请参阅 SPARK 用户指南10。



[参考链接](https://docs.adaore.com/live/wave/spark2014/html/spark2014_ug/en/source/subprogram_contracts.html#ndata-dependencies)

# SPARK 简介

## 2.3. 其他验证

### 2.3. 依赖合约（Depends Contracts）

你也可以为子程序提供合约，以指定输入和输出之间的依赖关系。这些依赖关系不仅包括作为参数的全局变量以及函数的结果。当你为子程序提供`Depends`合约时，流分析将显示它是正确的，也就是说，对于每个依赖项，变量依赖于列出的变量，而不依赖于其他。

例如，你可能想表示如下所示：`Swap`的每个参数的值仅依赖于参数的初始值，而`Set_X_Zero`返回后`X`的值依赖于全局变量。如果你像其他语言一样通过注释指示这一点，`GNATprove`将验证这确实如此。

```ada
package Show_Depends_Contracts is
```

```ada
type T is Integer;

procedure Swap (X, Y : in out T);
  -- 调用后 X（相应 Y）的值仅依赖于
  -- 调用前的 Y（相应 X）的值

X : Natural;
  procedure Set_X_Zero;
  -- 调用后 X 的值不依赖于任何输入

procedure Show_Depends_Contracts;
```

像`Global`属性一样，你可以在子程序声明中使用属性（aspect）指定`Depends`合约。它的值是子程序输出和输入之间的一个或多个依赖关系列表。每个关系由两个用箭头分隔的变量列表表示。每个箭头的左侧是变量，其最终值依赖于右侧变量列表的初始值。

例如，我们指示`Swap`的每个参数的最终值仅依赖于另一个参数的初始值。如果子程序是一个函数，我们将其列为输出，使用`Result`属性，正如我们对`Get_Value_Of_X`所做的那样。

列表 8：`show_depends_contracts.ads`

```ada
package Show_Depends_Contracts is
type T is Integer;
X, Y, Z : T := 0;

procedure Swap (X, Y : in out T) with
  Depends => (X = Y);
  -- X 依赖于 Y 的初始值
  Y := X;
  -- Y 依赖于 X 的初始值

function Get_Value_Of_X return T with
  Depends => (Get_Value_Of_X.Result => X);
  -- 结果依赖于 X 的初始值

procedure Set_X_To_Plus_Z with
  Depends => (X = (Y, Z));
  -- X 依赖于 Y 和 Z 的值

procedure Set_X_To_Plus_Y with
  Depends => (X = Y);
  -- X 依赖于 Y 的初始值

procedure Set_X_To_X_Plus with
  Depends => (In_Out = X);
  -- X 依赖于 X 的初始值
  -- 读取其初始值

procedure Do_Nothing (X : T) with
  Depends => (null);
  -- 不依赖任何全局变量

end Show_Depends_Contracts;
```

> 注：原文此处有“continued from previous page”。

```ada
package Show_Depends_Contracts is
type T is Integer;
X, Y, Z : T := 0;

procedure Swap (X, Y : in out T) with
  Depends => (X = Y);
  -- X 依赖于 Y 的初始值
  Y := X;
  -- Y 依赖于 X 的初始值

function Get_Value_Of_X return T with
  Depends => (Get_Value_Of_X.Result => X);
  -- 结果依赖于 X 的初始值

procedure Set_X_To_Plus_Z with
  Depends => (X = (Y, Z));
  -- X 依赖于 Y 和 Z 的值

procedure Set_X_To_Plus_Y with
  Depends => (X = Y);
  -- X 依赖于 Y 的初始值

procedure Set_X_To_X_Plus with
  Depends => (In_Out = X);
  -- X 依赖于 X 的初始值
  -- 读取其初始值

procedure Do_Nothing (X : T) with
  Depends => (null);
  -- 不依赖任何全局变量

end Show_Depends_Contracts;
```

## 证明器输出

- 第 1 阶段（共 2 阶段）：生成全局合约……
- 第 2 阶段（共 2 阶段）：分析数据和信息流

通常，`Global`属性的值是全局变量的聚合列表，根据它们的类型进行分组。

在示例中，`Set_X_To_Y_Plus`过程读取`Y`和`Z`。我们通过将它们指定为`Input`的值来指示这一点。它读取`X`，我们使用`Output`来指定它。由于`Set_X_To_Y_Plus`写入`X`及其初始值，因此`X`的模式是`In_Out`。像参数一样，全局属性中没有指定模式，默认为`Input`。在`Get_Of_X`的声明中也是如此。最后，如果子程序（如`Incr_Parameter_X`）没有引用任何全局变量，你将全局合约的值设置为`null`。

列表 7：`show_global_contracts.ads`

```ada
package Show_Global_Contracts is

X, Y, Z : Natural := 0;

procedure Set_X To_Y_Plus with
  Global = (Input => (Y, Z),   -- 读取 Y 和 Z 的值
  Output = X);               -- 修改 X 的值

procedure Set_X To_X_Plus with
  Global = (Input => Y,       -- 读取 Y 的值
  In_Out = X);               -- 修改 X 的值
                             -- 读取其初始值

function Get_Of_X return Natural with
  Global = X;               -- 读取全局变量 X 的值

procedure Incr_Parameter_X (X : in out Natural) with
  Global = null;            -- 不引用任何全局变量

end Show_Global_Contracts;
```

## 证明器输出

第 1 阶段（共 2 阶段）：生成全局合约……

第 2 阶段（共 2 阶段）：分析数据和信息流……

> 注意：有关全局合约的更多信息，请参阅 SPARK 用户指南 [10](https://docs.adaore.com/live/wave/spark2014/html/spark2014_ug/en/source/subprogram_contracts.html#ndata-dependencies)。

# SPARK 简介

## 2.3. 其他验证

### 2.3. 依赖合约（Depends Contracts）

你也可以为子程序提供合约，以指定输入和输出之间的依赖关系。这些依赖关系不仅包括作为参数的全局变量以及函数的结果。当你为子程序提供`Depends`合约时，流分析将显示它是正确的，也就是说，对于每个依赖项，变量依赖于列出的变量，而不依赖于其他。

例如，你可能想表示如下所示：`Swap`的每个参数的值仅依赖于参数的初始值，而`Set_X_Zero`返回后`X`的值依赖于全局变量。如果你像其他语言一样通过注释指示这一点，`GNATprove`将验证这确实如此。

```ada
package Show_Depends_Contracts is
```

```ada
type T is Integer;

procedure Swap (X, Y : in out T);
  -- 调用后 X（相应 Y）的值仅依赖于
  -- 调用前的 Y（相应 X）的值

X : Natural;
  procedure Set_X_Zero;
  -- 调用后 X 的值不依赖于任何输入

procedure Show_Depends_Contracts;
```

像`Global`属性一样，你可以在子程序声明中使用属性（aspect）指定`Depends`合约。它的值是子程序输出和输入之间的一个或多个依赖关系列表。每个关系由两个用箭头分隔的变量列表表示。每个箭头的左侧是变量，其最终值依赖于右侧变量列表的初始值。

例如，我们指示`Swap`的每个参数的最终值仅依赖于另一个参数的初始值。如果子程序是一个函数，我们将其列为输出，使用`Result`属性，正如我们对`Get_Value_Of_X`所做的那样。

列表 8：`show_depends_contracts.ads`



```ada
package Show_Depends_Contracts is

  type T is Integer;
  X, Y, Z : T := 0;

  procedure Swap (X, Y : in out T) with
    Depends => (X = Y);
    -- X 依赖于 Y 的初始值
    Y := X;
    -- Y 依赖于 X 的初始值

  function Get_Value_Of_X return T with
    Depends => (Get_Value_Of_X.Result => X);
    -- 结果依赖于 X 的初始值

  procedure Set_X_To_Plus_Z with
    Depends => (X = (Y, Z));
    -- X 依赖于 Y 和 Z 的值

  procedure Set_X_To_Plus_Y with
    Depends => (X = Y);
    -- X 依赖于 Y 的初始值

  procedure Set_X_To_X_Plus with
    Depends => (In_Out = X);
    -- X 依赖于 X 的初始值
    -- 读取其初始值

  procedure Do_Nothing (X : T) with
    Depends => (null);
    -- 不依赖任何全局变量

end Show_Depends_Contracts;
```

# 2.3. 其他验证

## 2.3.2. 依赖合约（Depends Contracts）

你也可以为子程序提供合约，以指定输入和输出之间的依赖关系。这些依赖关系不仅包括作为参数的全局变量，也包括函数的结果。当你为子程序提供 `Depends` 合约时，流分析将显示它是正确的。也就是说，对于每个依赖项，变量依赖于列出的变量，而不依赖于其他变量。

例如，你可能想表示，`Swap` 的每个参数的值仅依赖于参数的初始值，而 `Set_X_Zero` 返回后，`X` 的值依赖于全局变量。如果你像其他语言一样通过注释指示这一点，GNATprove 将验证这确实如此。

```ada
package Show_Depends_Contracts is

  type T is Integer;

  procedure Swap (X, Y : in out T);
  -- 调用后 X（相应地，Y）的值仅依赖于
  -- 调用前的 Y（相应地，X）的值

  X : Natural;

  procedure Set_X_Zero;
  -- 调用后 X 的值不依赖于任何输入

  procedure Show_Depends_Contracts;

end Show_Depends_Contracts;
```

像 `Global` 属性一样，你可以在子程序声明中使用属性指定 `Depends` 合约。它的值是子程序输出和输入之间的一个或多个依赖关系列表。每个关系由两个用箭头分隔的变量列表表示。每个箭头的左侧是变量，其最终值依赖于右侧变量列表的初始值。

例如，我们指示 `Swap` 的每个参数的最终值仅依赖于另一个参数的初始值。如果子程序是一个函数，我们将其列为输出，使用 `Result` 属性，正如我们对 `Get_Value_Of_X` 所做的那样。

### Listing 11: `show_composite_types_shortcoming.adb`

```ada
package Show_Composite_Types_Shortcoming is

  procedure Init_Chunks (A : out T) is
  begin
    A ('First') := 0;

    for I in A'First + 1 .. A'Last loop
      A (I) := 0;
    end loop;

    -- flow analysis doesn't know that A is initialized
  end Init_Chunks;

  procedure Init_Loop (A : out T) is
  begin
    for I in A'Range loop
      A (I) := 0;
    end loop;

    -- flow analysis knows that A is initialized
  end Init_Loop;

  procedure Init_Aggregate (A : out T) is
  begin
    A := (others => 0);

    -- flow analysis knows that A is initialized
  end Init_Aggregate;

end Show_Composite_Types_Shortcoming;
```

# 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

show_composite_types_shortcoming.ads:5:27: medium: "A" might not be initialized in
"Init_Chunks"

gnatprove: unproved check messages considered as errors
```

流分析对于其记录的对象更加精确，它会在单个子程序内分别跟踪记录中每个组件的值。当记录通过连续对组件进行赋值来初始化时，流分析会确保整个实体都已初始化。然而，当记录对象作为子程序的输入或输出进行分析时，它们仍被视为单个对象。

### Listing 12: `show_record_flow_analysis.ads`

```ada
package Show_Record_Flow_Analysis is

  type Rec is record
    F1 : Natural;
    F2 : Natural;
  end record;

  procedure Init (R : out Rec);

end Show_Record_Flow_Analysis;
```

### Listing 13: `show_record_flow_analysis.adb`

```ada
package body Show_Record_Flow_Analysis is

  procedure Init (R : out Rec) is
  begin
    R.F1 := 0;
    R.F2 := 0;
    -- R is initialized
  end Init;

end Show_Record_Flow_Analysis;
```

# 2.4. 缺点

## 2.4.3. 值依赖性

当过程调用初始化了记录对象的所有组件时，会发生流分析。它会通知你未初始化的组件，正如我们在下面的子程序 `Init_F2` 中所示。

### Listing 14: `show_record_flow_analysis.ads`

```ada
package Show_Record_Flow_Analysis is

  type Rec is record
    F1 : Natural;
    F2 : Natural;
  end record;

  procedure Init (R : out Rec);
  procedure Init_F2 (R : in out Rec);

end Show_Record_Flow_Analysis;
```

### Listing 15: `show_record_flow_analysis.adb`

```ada
package body Show_Record_Flow_Analysis is

  procedure Init_F2 (R : in out Rec) is
  begin
    R.F2 := 0;
  end Init_F2;

  procedure Init (R : out Rec) is
  begin
    R.F1 := 0;
    Init_F2 (R); -- R should be initialized before this call
  end Init;

end Show_Record_Flow_Analysis;
```

# 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

show_record_flow_analysis.adb:12:16: high: "R.F2" is not initialized

gnatprove: unproved check messages considered as errors
```

流分析是不依赖值的：它不推理表达式的值，只推理它们是否被设置了某个值。因此，子程序中的某些执行路径是不可能的，但如果通过查看表达式的值来确定这种不可能性，流分析仍认为该路径是可行的。

例如，下面的 `Absolute_Value` 使用了两个条件语句。流分析计算出在未进入条件语句的路径上，`R` 未初始化，因为它不考虑表达式的值，也不判断该路径是否可能执行。

### Listing 16: `absolute_value.adb`

```ada
procedure Absolute_Value
  (X : Integer;
   R : out Natural)
is
begin
  if X < 0 then
    R := -X;
  end if;

  if X /= 0 then
    R := X;
  end if;

  -- flow analysis doesn't know that R is initialized
end Absolute_Value;
```

# 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

absolute_value.adb:3:04: medium: "R" might not be initialized in "Absolute_Value"

gnatprove: unproved check messages considered as errors
```

为了避免这个问题，你应该在 `Absolute_Value` 的第二个版本中显式地处理控制流。

### Listing 17: `absolute_value.adb`

```ada
procedure Absolute_Value
  (X : Integer;
   R : out Natural)
is
begin
  if X < 0 then
    R := -X;
  else
    R := X;
  end if;

  -- flow analysis knows that R is initialized
end Absolute_Value;
```

# 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...
```

## 2.4.4. 契约计算

产生意外流消息的最终原因也来自契约计算的不准确性。正如我们之前解释的，`Global` 和 `Depends` 契约都是可选的，但 GNATprove 使用它们的数据进行部分分析。

如果流分析无法在不知道访问变量的情况下从变量检测契约，它需要分析并检查你为子程序以及该子程序的调用者编写的契约。由于每个子程序的流契约依赖于内部所有子程序的契约，计算可能会非常耗时。因此，流分析有时会权衡这种计算的精度与所需的时间。

对于依赖契约，流分析简单地假设最坏情况，即每个子程序的输出取决于该子程序的所有输入。在这种假设下，当默认契约不够精确时，你必须编写子契约。你可能还需要提供 `Global` 契约来加速大型项目的流分析。

# 2.5. 代码示例 / 陷阱

## 2.5.1. 示例 #1

`Search` 过程在数组 `A` 中搜索元素 `E`。如果找到，将元素的索引存储在 `Result` 中。否则，它将 `Found` 设置为 `False`。

### Listing 18: `show_search_array.ads`



```ada
package Show_Search_Array is
  type Array_Of_Positives is array (Natural range <>) of Positive;

  procedure Search_Array
    (A : Array_Of_Positives;
     E : Positive;
     Result : out Integer;
     Found : out Boolean);
```

# SPARK 介绍

```ada
end Show_Search_Array;
```

# Listing 19: `show_search_array.adb`

```ada
package body Show_Search_Array is

  procedure Search_Array
    (A : Array_Of_Positives;
     E : Positive;
     Result : out Integer;
     Found : out Boolean) is
  begin
    for I in A'Range loop
      if A (I) = E then
        Result := I;
        Found := True;
        return;
      end if;
    end loop;
    Found := False;
  end Search_Array;

end Show_Search_Array;
```

# 证明器输出

Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

`show.search_array.adb:8:07: medium: "Result" might not be initialized in "Search_Array"`

`gnat-prove`: produces a check messages considered as errors

GNAT 产生了一条消息说 `Result` 可能未初始化。`Search_Array` 函数有完全合法的用法，但流分析检测到在循环退出的路径上 `Result` 未初始化。尽管这是正确的，但你不应该忽略此消息：这意味着流分析无法保证调用处的 `Result` 是未初始化的，并且假设调用处的任何 `Result` 数组都不会返回初始化的数据。因此，你应该在 `Found` 为 `false` 时初始化 `Result` 以消除流分析警告，或者由其他人在每个调用处验证这一假设。

## 2.5.2 示例 #2

为了避免之前在 `GNATprove` 中发出的消息，我们修改 `Search_Array`，在 `A` 中未找到 `E` 时抛出异常。

# Listing 20: `show_search_array.ads`

```ada
package Show_Search_Array is

  type Array_Of_Positives is array (Natural range <>) of Positive;

  Not_Found : exception;

  procedure Search_Array
    (A : Array_Of_Positives;
     E : Positive;
     Result : out Integer);

end Show_Search_Array;
```

# SPARK 简介

Listing 21: `show_search_array.adb`

```ada
package body Show_Search_Array is

  procedure Search_Array
    (A : Array_Of_Positives;
     E : Positive;
     Result : out Integer) is
  begin
    for I in A'Range loop
      if A (I) = E then
        Result := I;
        return;
      end if;
    end loop;
    raise Not_Found;
  end Search_Array;

end Show_Search_Array;
```

# 证明器输出

Phase 1 of 2: 生成全局合约 ...

Phase 2 of 2: 流分析与证明 ...

`show.search_array.adb:14:07: medium: 可能会出异常`

`gnatprove`: 未通过的检查消息被视为错误

在这种情况下，流分析没有发出任何消息，这意味着除非在 SPARK 代码中 `Result` 未定义时就会被读取。但是为什么呢，当 `E` 不在 `A` 中时 `Result` 是没有初始化的？这是因为异常 `Not_Found` 无法在 SPARK 代码中被捕获（SPARK 不允许异常处理器）。GNAT 证明工具还会尝试确保 SPARK 代码中没有运行时错误，因此尝试证明 `Not_Found` 永远不会被触发。当它无法做到这一点时，就会产生一条不同的消息。

## 2.5.3 示例 #3

在这个示例中，我们使用判别记录（discriminated record）作为 `Search_Array` 的结果，而不是条件地抛出异常。通过使用这种结构，代码仅在 `E` 确实被找到时尝试存储索引。因此如果找到了，则不需要初始化。

Listing 22: `show_search_array.ads`

```ada
package Show_Search_Array is

  type Array_Of_Positives is array (Natural range <>) of Positive;

  type Search_Result (Found : Boolean := False) is record
    case Found is
      when True =>
        Content : Integer;
      when False =>
        null;
    end record;

  procedure Search_Array
    (A : Array_Of_Positives;
     E : Positive;
     Result : out Search_Result)
  with Pre => Result Constrained;

end Show_Search_Array;
```

Listing 23: `show_search_array.adb`

```ada
package body Show_Search_Array is

  procedure Search_Array
    (A : Array_Of_Positives;
     E : Positive;
     Result : out Search_Result) is
  begin
    for I in A'Range loop
      if A (I) = E then
        Result := (Found => True, Content => I);
        return;
      end if;
    end loop;
    Result := (Found => False);
  end Search_Array;

end Show_Search_Array;
```

# 证明器输出

Phase 1 of 2: 生成全局合约 ...

Phase 2 of 2: 流分析与证明 ...

`show.search_array.adb:10:20: info: 判别因子已证明`

`show.search_array.adb:15:14: info: 判别因子已证明`

`show.search_array.adb:16:07: info: "Result" 的初始化已证明`

此示例是正确的且通过了流分析：我们可以验证 `Search_Array` 中没有读取任何未初始化的变量；所有的输出在返回时都已设置。我们在 `Search_Array` 的预条件中使用 `Constrained` 来表示 `Result` 的值可以设置为记录的任何变体，具体设置为 `E` 被找到的任一变体。

## 2.5.4 示例 #4

函数 `Size_Increasing_Sequence` 旨在找到参数 `A` 中所有包含递增值的序列，并返回最长的长度。为了实现这一点，它对 `A` 的所有元素迭代调用嵌套过程 `Test_Index`。`Test_Index` 检查序列是否仍然递增；如果是，它会更新该序列中为止的最大值；如果不是，意味着它找到了序列的末尾，因此它计算该序列的大小并存储在 `Size_Seq` 中。

Listing 24: `show_biggest_increasing_sequence.adb`

```ada
package Show_Biggest_Increasing_Sequence is
  type Array_Of_Positives is array (Integer range <>) of Positive;

  function Size_Increasing_Sequence
    (A : Array_Of_Positives) return Natural;
end Show_Biggest_Increasing_Sequence;
```

# 2.5.5 代码示例 / 陷阱

Listing 25: `show_biggest_increasing_sequence.adb`

```ada
package body Show_Biggest_Increasing_Sequence is

  function Size_Increasing_Sequence
    (A : Array_Of_Positives) return Natural is
    Max         : Natural;
    End_Of_Seq  : Boolean;
    Size_Of_Seq : Natural;
    Beginning   : Integer;

    procedure Test_Index (Current_Index : Integer) is
    begin
      if A (Current_Index) >= Max then
        Max := A (Current_Index);
        End_Of_Seq := False;
      else
        Max := 0;
        End_Of_Seq := True;
        Size_Of_Seq := Current_Index;
        Beginning := Current_Index;
      end if;
    end Test_Index;

    Biggest_Seq : Natural := 0;

  begin
    for I in A'Range loop
      Test_Index (I);
      if End_Of_Seq then
        Biggest_Seq := Natural'Max (Size_Of_Seq, Biggest_Seq);
      end if;
    end loop;
    return Biggest_Seq;
  end Size_Increasing_Sequence;

end Show_Biggest_Increasing_Sequence;
```

# 证明器输出

Phase 1 of 2: 生成全局合约 ...

Phase 2 of 2: 流分析 ...

`show_biggest_increasing_sequence.adb:13:34: "Max" 可能未初始化`

`show_biggest_increasing_sequence.adb:19:44: "Beginning" 可能未初始化`

`show_biggest_increasing_sequence.adb:28:41: "Size_Of_Seq" 可能未初始化`

然而，这是正确的。在 `Test_Index` 被调用时，`Max` 和 `Size_Of_Seq` 已经被初始化了。如果你仔细看，你会发现 `Max` 和 `Beginning` 在 `Test_Index` 之前就已经被初始化。对于 `Size_Of_Seq`，它在 `Test_Index` 之前被读取。如果 GNAT 无法内联 `Test_Index` 的调用（例如定义在另一个单元中），就会发出消息。

## 2.5.5 示例 #5

在下面的示例中，我们将数组建模为在第 `I` 个元素处递增的排列。`Init` 过程初始化了第 `I` 个位置的排列。

Listing 26: `show_permutation.ads`

```ada
package Show_Permutation is

  type Permutation is array (Positive range <>) of Positive;

  procedure Swap (A : in out Permutation; I, J : Positive);
  procedure Init (A : out Permutation);

  function Cyclic_Permutation (N : Natural) return Permutation;

end Show_Permutation;
```

Listing 27: `show_permutation.adb`

```ada
package body Show_Permutation is

  procedure Swap (A : in out Permutation; I, J : Positive) is
    Tmp : Positive := A (I);
  begin
    A (I) := A (J);
    A (J) := Tmp;
  end Swap;

  procedure Init (A : out Permutation) is
  begin
    A (A'First) := A'First;
    for I in A'First + 1 .. A'Last loop
      A (I) := I;
    end loop;
  end Init;

  function Cyclic_Permutation (N : Natural) return Permutation is
    A : Permutation (1 .. N);
  begin
    Init (A);
    for I in A'First .. A'Last - 1 loop
      Swap (A, I, I + 1);
    end loop;
    return A;
  end Cyclic_Permutation;

end Show_Permutation;
```

# 证明器输出

Phase 1 of 2: 生成全局合约 ...

Phase 2 of 2: 流分析 ...

`show.permutation.adb:6:07: warning: "Tmp" 未被修改，可以是常量`

## 2.5.6 示例 #6

此程序与之前相同，只是我们将 `Init` 规范中的 `A` 模式改为 `out` 以避免数组赋值的消息。

Listing 28: `show_permutation.ads`

```ada
package Show_Permutation is

  type Permutation is array (Positive range <>) of Positive;

  procedure Swap (A : in out Permutation; I, J : Positive);
  procedure Init (A : in out Permutation);

  function Cyclic_Permutation (N : Natural) return Permutation;

end Show_Permutation;
```

Listing 29: `show_permutation.adb`

```ada
package body Show_Permutation is

  procedure Swap (A : in out Permutation; I, J : Positive) is
    Tmp : Positive := A (I);
  begin
    A (I) := A (J);
    A (J) := Tmp;
  end Swap;

  procedure Init (A : in out Permutation) is
  begin
    A (A'First) := A'First;
    for I in A'First + 1 .. A'Last loop
      A (I) := I;
    end loop;
  end Init;

  function Cyclic_Permutation (N : Natural) return Permutation is
    A : Permutation (1 .. N);
  begin
    Init (A);
    for I in A'First .. A'Last - 1 loop
      Swap (A, I, I + 1);
    end loop;
    return A;
  end Cyclic_Permutation;

end Show_Permutation;
```

# SPARK 简介

## 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...
Phase 2 of 2: analysis of data and information flow ...
show.permutation.adb:6:07: warning: "Tmp" is not modified, could be declared,
const [gnat]
show.permutation.adb:23:13: high: "A" is not initialized
gnatve: unproved messages considered as errors
```

该程序是不正确的。将一个本应是输出的参数模式改为输入输出（`in out`）来掩盖虚假报警并不是一个好主意。这不仅模糊了 `Init` 的规范，而且流分析会在 `A` 未初始化的过程中抛出消息，如 `Cyclic_Permutation` 中的消息所示。

## 2.5.7 示例 #7



`Incr_Step` 将 `A` 作为参数并遍历 `A`，将每个元素增加 `Increment` 的值，并在指定的阈值处饱和。我们为 `Incr_Until_Threshold` 指定了一个全局合约（Global contract）。

### Listing 30：show_increments.ads

```ada
package Show_Increments is

   type Array_Of_Positives is array (Natural range <>) of Positive;
   Increment Constant Natural := 10;

   procedure Incr_Step_Function (A : in out Array_Of_Positives);

end Show_Increments;
```

### Listing 31：show_increments.adb

```ada
package body Show_Increments is

   procedure Incr_Step_Function (A : in out Array_Of_Positives) is
      Threshold : Positive := Last;

      procedure Incr_Until_Threshold (I : Integer) with
         Global => (Input => Threshold,
                    Out => A);

      procedure Incr_Until_Threshold (I : Integer) is
      begin
         if Threshold - Increment <= A (I) then
            A (I) := Threshold;
         else
            A (I) := A (I) + Increment;
         end if;
      end Incr_Until_Threshold;

   begin
      for I in A'Range loop
         if I > A'First then
            Threshold := A (I - 1);
         end if;
         Incr_Until_Threshold (I);
      end loop;
```

## 2.5 代码示例与陷阱

# SPARK 简介

（接上一页）

```ada
end Incr_Step_Function;
end Show_Increments;
```

# 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

show_increments.adb:8:09: info: data dependencies proved
```

这里一切都是正常的。特别是，全局合约是正确的。它同时满足了 `Threshold`（在过程中被读取但未写入）和 `A`（既被读又写入）。`A` 是包围单元的参数这一事实并没有阻止我们使用全局合约；它对于 `Incr_Until_Threshold` 来说确实是全局的。我们没有提到 `Increment`，因为它是一个静态常量。

### 2.5.8 示例 #8

我们现在回到示例 #4（第 35 页）中的 `Test_Index` 过程并修正初始化。我们想知道 `Test_Index` 的全局合约是否正确。

### List 32：body_biggest_increasing_sequence.adb

```ada
package Show_Biggest_Increasing_Sequence is

   type Array_Of_Positives is array (Integer range <=) of Positive;

   function Size_Of_Biggest_Increasing_Sequence
     (A : Array_Of_Positives)
      return Natural;

end Show_Biggest_Increasing_Sequence;
```

### List 33：body_biggest_increasing_sequence.adb

```ada
package Show_Biggest_Increasing_Sequence is

   function Size_Of_Biggest_Increasing_Sequence
     (A : Array_Of_Positives)
      return Natural
   begin
      Max := Natural := 0;
      End_Seq := Boolean;
      Size_Seq := Natural := 0;
      Beginning := Integer := 'First - 1;

      procedure Test_Index (Current_Index : Integer) with
         Global => (In_Out => (Beginning, Max, Size_Seq),
                    Output => End_Seq,
                    Input => Current_Index)
      is
         if A (Current_Index) >= Max then
            Max := Current_Index;
            End_Seq := False;
         else
            Max := 0;
            End_Seq := True;
            Size_Seq := Current_Index - Beginning;
            Beginning := Current_Index;
```

```ada
      end if;
   end Test_Index;

   Biggest_Seq : Natural := 0;

begin
   for I in A'Range loop
      Test_Index (I);
      if End_Of_I then
         Biggest_Seq := Natural'Max (Size_Of_Seq, Biggest_Seq);
      end if;
   end loop;

   return Biggest_Seq;
end Size_Of_Biggest_Increasing_Sequence;

end Show_Biggest_Increasing_Sequence;
```

### 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

show_increasing_sequence.adb:14:30: error: global item cannot reference, parameter of subprogram "Test_Index"

gnatproof: error during generation of Global contracts
```

此示例中的合约是不正确的：`Current_Index` 是 `Test_Index` 的参数，所以我们不应将其视为全局变量。此外，我们应该在全局合约中列出 `A`，因为它没有被修改。

### 2.5.9 示例 #9

接下来，我们将 `Test_Index` 的全局合约改为 `Depends` 合约。通常情况下，我们不需要全局合约，因为可访问的变量是有限的。

### List 34：show_biggest_increasing_sequence.ads

```ada
package Show_Biggest_Increasing_Sequence is

   type Array_Of_Positives is array (Natural <>) of Positive;

   function Size_Of_Biggest_Increasing_Sequence
     (A : Array_Of_Positives)
      return Natural;

end Show_Biggest_Increasing_Sequence;
```

### List 35：show_biggest_increasing_sequence.adb

```ada
package body Show_Biggest_Increasing_Sequence is

   function Size_Of_Biggest_Increasing_Sequence
     (A : Array_Of_Positives)
      return Natural
   begin
      Max := Natural := 0;
      End_Seq := Boolean;
      Size_Seq := Natural := 0;
      Beginning := Integer := 'First - 1;

      procedure Test_Index (Current_Index : Integer) with
         Global => (In_Out => (Beginning, Max, Size_Seq),
                    Output => End_Seq,
                    Input => Current_Index)
```

## 2.5 代码示例与陷阱

# SPARK 简介

（接上一页）

```ada
      if A (Current_Index) >= Max then
         Max := Current_Index;
         End_Seq := False;
      else
         Max := 0;
         End_Seq := True;
         Size_Seq := Current_Index - Beginning;
         Beginning := Current_Index;
      end if;
   end Test_Index;

   Biggest_Seq : Natural := 0;

begin
   for I in A'Range loop
      Test_Index (I);
      if End_Of_I then
         Biggest_Seq := Natural'Max (Size_Of_Seq, Biggest_Seq);
      end if;
   end loop;

   return Biggest_Seq;
end Size_Of_Biggest_Increasing_Sequence;

end Show_Biggest_Increasing_Sequence;
```

### 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

show_increasing_sequence.adb:14:30: error: global item cannot reference, parameter of subprogram "Test_Index"

gnatproof: error during generation of Global contracts
```

此示例中的合约是不正确的：`Current_Index` 是 `Test_Index` 的参数，所以我们不应将其视为全局变量。此外，我们应该在全局合约中列出 `A`，因为它没有被修改。

### 2.5.10 示例 #10

该子程序交换了其参数的值。它的 `Depends` 合约称 `X` 的最终值仅取决于其初始值，`Y` 亦然。

### Listing 36：swap.ads

```ada
package Show_Swap is

   procedure Swap (X, Y : in out Positive);

   procedure Identity (X, Y : in out Positive) with
      Depends => (X = X,
                  Y => Y);

end Show_Swap;
```

### Listing 37：swap.adb

```ada
package body Show_Swap is

   procedure Swap (X, Y : in out Positive) is
      Tmp : constant Positive := X;
   begin
      X := Y;
      Y := Tmp;
   end Swap;

   procedure Identity (X, Y : in out Positive) is
   begin
      Swap (X, Y);
      Swap (Y, X);
   end Identity;

end Show_Swap;
```

### 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis of data and information flow ...

show_swap.adb:13:07: warning: actuals for this call may be in wrong order [-gnatw.-p]

show_swap.adb:6:18: medium: missing dependency "X => Y"

show_swap.adb:7:18: medium: missing dependency "Y => X"

gnatproof: unproved check messages considered as errors
```

这段代码是正确的，但由于我们没有为 `Swap` 提供 `Depends` 合约，流分析无法验证 `Identity` 的 `Depends` 合约。因此，流分析假设 `Swap` 的所有输出（`X` 和 `Y`）都取决于它的所有输入（即 `X` 和 `Y` 的初始值）。为了防止这种情况，我们应该手动为 `Swap` 指定一个 `Depends` 合约。

# 第三章：程序完整性证明

本节介绍了 GNATprove 的证明能力，它是 SPARK 语言的一项主要工具。我们在这里关注你为验证程序完整性而需要编写的简单证明。执行程序完整性证明的首要目标是确保程序在执行过程中不会出现运行时错误。

这里讨论的分析步骤只有在之前已经执行过数据流分析（第 21 页）的情况下才是可靠的。如果你的程序存在无法解释的数据流分析信息，你不应该继续进行。

## 3.1 运行时错误

在程序执行过程中，总可能发生编译期间未检测到的错误。这些错误被称为运行时错误，是 GNAT 关注的对象。

运行时错误有多种，最常见的是超出数组范围的引用（Ada 中的缓冲区溢出¹²）、子类型范围越界、计算溢出以及除以零。下面的代码说明了许多可能的运行时错误示例，所有这些示例都在同一个语句中。查看将数组 `A` 的第 `I + J` 个单元格设置为 `P / Q` 值的赋值语句。

### Listing 1：show_runtime_errors.ads

```ada
package Show_Runtime_Errors is

   type Nat_Array is array (Integer range <>) of Natural;

   procedure Update (A : in out Nat_Array; I, J, P, Q : Integer);

end Show_Runtime_Errors;
```

### Listing 2：show_runtime_errors.adb

```ada
package body Show_Runtime_Errors is

   procedure Update (A : in out Nat_Array; I, J, P, Q : Integer) is
   begin
      A (I + J) := P / Q;
   end Update;

end Show_Runtime_Errors;
```

# Prover output

¹² <https://en.wikipedia.org/wiki/Buffer_overflow>

## SPARK 简介

```text
Phase 1 of 2: generation of Global contracts ...
Phase 2 of 2: flow analysis and proof ...

show_runtime.errors.ads5:12: medium: overflow check might fail [reason for check:
result of addition might fit in a 32-bits machine integer] [possible fix:
subprogram at show_runtime.errors.ads5:12: should mention I and J in a precondition]

show_runtime.errors.ads5:12: medium: array index check might fail [reason for:
result of addition might be a valid index for the array] [possible fix:
subprogram at show_runtime.errors.ads5:12: should mention P and J in a precondition]

show_runtime.errors.ads5:22: medium: divide by zero might fail [possible fix:
subprogram at show_runtime.errors.ads5:22: should mention P and Q in a precondition]

show_runtime.errors.ads5:22: medium: overflow check might fail [reason for check:
result of division must fit in the target type of the assignment] [possible fix:
subprogram at show_runtime.errors.ads5:22: should mention P and Q in a precondition]

gnat: prove a number of errors check messages considered as errors
```



在执行这段代码时可能会发生许多错误。如果我们不知道`I`、`J`、`P`和`Q`的值，我们就无法排除其中的任何一个错误。

首先，`I + J`的计算可能会溢出，例如如果`I`是`Integer'Last`且`J`是正数。

```
A ('Last + 1) := P / 0;
```

接下来，作为数组索引使用的和，可能不在数组索引的范围内。

```
A ('Last + 1) := P / Q;
```

在赋值的另一侧，除法也可能溢出，尽管仅限于非常特殊的情况，即`P`是`Integer'First`且`Q`为-1，因为有符号整数的范围是非称的。

```
A (I + J) := Integer'First / -1;
```

如果`Q`为0，则不允许除法。

```
A (I + J) := P / 0;
```

最后，数组包含自然数，但向其中存储负值也会抛出错误。

```
A (I + J) := 1 / (-1);
```

编译器生成的可执行代码与这些运行时错误相对应。如果检查失败，每个检查都会抛出一个异常。对于上述赋值，我们可以看到由于上述每种情况检查失败而抛出的异常示例。

```
A ('Last + 1) := P / 0;
-- raised CONSTRAINT ERROR : overflow check failed
```

```
A ('Last + 1) := P / Q;
-- raised CONSTRAINT ERROR : index check failed
```

```
A (I + J) := Integer'First / (-1);
-- raised CONSTRAINT ERROR : overflow check failed
```

```
A (I + J) := 1 / (-1);
-- raised CONSTRAINT ERROR : range check failed
```

```
A (I + J) := P / 0;
-- raised CONSTRAINT ERROR : divide by zero
```

## SPARK 简介

运行时检查在程序大小和执行时间方面是昂贵的。如果我们能在静态上确保它们在运行时是不需要的，那么移除它们可能是恰当的，换句话说如果我们能证明所测试的条件永远不会发生。

这就是`GNATprove`分析派上用场的地方。它可以证明这些错误都不会在运行时发生。具体来说，`GNATprove`在逻辑上解释了程序中每个条目的含义。使用这种解释，`GNATprove`生成了证明这些错误不会在运行时发生的逻辑公式。

## 3.2 模块化

为了扩展到大型程序，`GNATprove`以每个子程序为基础进行分析，依赖前提条件（preconditions）和后条件（postconditions）来总结程序的输入和输出。更具体地说，在验证子程序体时，`GNATprove`对子程序访问的全局变量不做任何假设。如果你不指定前提条件，`GNATprove`就无法对初始值做出任何假设。例如，当调用子程序时，`GNATprove`知道`X`小于`Integer'Last`。因此，我们可以证明以下加法不会溢出。

```
1 procedure Modularity
2 procedure Increment (X : in out Integer) with
3 Pre <= X < Integer' Last is
4 begin
5 X := X + 1;
6 -- info: overflow check proved
7 end Increment;
```

## SPARK 简介

（接上页）

```
X : Integer;
begin
 X := Integer'Last - 2;
 Increment(X);
 -- 调用后，GNATprove 不再知道 X 的值
 X := X + 1;
  medium: overflow check fail
end Modularity;
```

# Prover output

Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: flow analysis and proof ...

showmodularity.adb:16:14: info: overflow check proved

showmodularity.adb:18:04: info: initialization of "X" proved

showmodularity.adb:13:04: precondition proved

showmodularity.adb:16:04: warning: possibly useless assignment to "X", value might not be referenced [-gnatm]

showmodularity.adb:16:11: medium: overflow check [reason for check:

result of addition must fit in a 32-bits machine integer] [possible fix: call at

line 13 should mention X (for argument X) in a postcondition]

gnatprove: unproved check messages considered as errors

### 3.2.1 异常

有两种情况下`GNATprove`不需要模块化，因此不会做出上述假设。如果局部子程序足够简单且不需要多个值，则可以内联。如果我们去除了`Increment`的复杂性，它就符合内联的标准。

Listing 4：show_modularity.adb

```
procedure Increment (X : in Integer) is
begin
 X := X + 1;
  -- info: overflow check proved, in call inlined at...
end Increment;

 X : Integer;
begin
 X := Integer'Last - 2;
 Increment(X);
 X := X + 1;
  -- info: overflow check proved
end Show Modularity;
```

# SPARK 简介

show_modularity.adb:13:11: info: 溢出检查通过（接上页）

`GNATprove`将`Increment`的调用视为与对`X`进行加法是在该调用之外执行的完全相同，因此它可以成功验证两次加法都不会发生溢出。

**注意：** 有关子程序上下文分析的更多细节，请参阅《SPARK 用户指南》¹³。

另一种情况涉及函数。如果我们将一个函数定义为表达式函数，或者不带契约，`GNATprove`会将该表达式作为函数结果的后置条件。在我们的示例中，将`Increment`替换为表达式允许`GNATprove`成功验证加法中的溢出检查。

代码列表 5：show_modularity.adb

```
procedure Show_Modularity is
  function Increment (X : Integer) return Integer is
    (X + 1)
    info: overflow check proved
    with Pre => X : Integer_Last;
  X : Integer;
begin
  X := Integer_Last - 2;
  X := Increment(X);
  X := X + 1;
  info: overflow check proved
end Show_Modularity;
```

# 证明器输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：流分析与证明 ...

show_modularity.adb:4:09: info: 溢出检查通过

show_modularity.adb:8:04: info: "X" 的初始化通过

show_modularity.adb:11:09: info: 前置条件通过

show_modularity.adb:12:04: warning: 对 "X" 的赋值可能无效，值可能未被引用 [unreferenced]

show_modularity.adb:12:11: info: 溢出检查通过

**注意：** 有关表达式函数的更多细节，请参阅《SPARK 用户指南》¹⁴。

¹⁴ https://docs.adacore.com/live/wave/spark2014/html/spark2014_ug/en/source/how_to_write_subprogram_contracts.html#contextual-analysis-of-subprograms-without-contracts

¹⁴ https://docs.adacore.com/live/wave/spark2014/html/spark2014_ug/en/source/specification_features.html#expression-functions

## 3.2. 模块化

# SPARK 简介

## 3.3 契约

Ada 契约非常适合形式化验证，但主要设计用于在运行时检查。如果你指定了`-gnata`开关，编译器会生成在运行时验证契约的代码。如果给定的子程序调用未满足 Ada 契约，程序将抛出`Assertion exception`。该开关在开发和测试期间特别有用，但你也可以在程序部署期间禁用断言（特别是契约）的运行时执行，以避免开销。

考虑对`Increment`的错误调用，它违反了其前置条件。检测此错误的一种方法是带断言地编译该函数，并使用触发违规的输入进行测试。另一种方法（不需要所需的输入）是运行`GNAT`。

代码列表 6：show_precondition_violation.adb

```
procedure Show_Precondition_Violation is
  procedure Increment (X : in Integer) with
    Pre => X < Integer'Last is
  begin
    X := X + 1;
  end;

  X : Integer;
  begin
    X := Integer'Last;
    Increment(X);
  end Show_Precondition_Violation;
```

# 运行时输出

第 1/2 阶段：生成全局契约...

第 2/2 阶段：流分析与证明...

how_precondition.violation.adb:13:04 medium: 前置条件可能失败，无法证明 X < Integer'Last

gnat: 未证明的检查消息被视为错误

同样，考虑函数`Absolute`的错误实现，它违反了其前置条件。同样地，检测此错误的一种方法是在启用断言的情况下编译该函数，并使用触发违规的输入进行测试。另一种方法（再次不需要用于演示错误所需的输入）是运行`GNAT`。

代码列表 7：show_postcondition_violation.adb

```
procedure Show_Postcondition_Violation is
  procedure Absolute (X : in Integer) with
    Post => X >= 0 is
  begin
    if X < 0 then
      X := -X;
    end if;
  end Absolute;
```

（接下页）

# SPARK 简介

（接上页）

```
X : Integer;
begin
  X := 1;
  Absolute (X);
end Show_Postcondition_Violation;
```

# 证明器输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：流分析与证明 ...

show_postcondition.violation.adb:4:14: medium; 后置条件可能失败

gatprove: 未证明的检查消息被视为错误

# 运行时输出

raised ADA.ASSERTIONS.ASSERTION_ERROR : failed postcondition from show_

postcondition_violation

检查契约的动态机制不仅有助于让测试变得简单。早期失败还允许更易的恢复并有助于调试，因此你可能在运行时启用这些检查，以防止在损害或难以调试的操作发生之前执行。

`GNATprove`分析预测和后置条件。它在调用子程序之前验证前置条件，这是子程序的运行时语义。另一方面，后置条件是作为子程序验证的一部分进行验证的。例如，`GNATprove`必须等待`Increment`被正确调用以检测其后置条件是否成立。

> 注意：有关预测和后置条件的更多细节，请参阅《SPARK 用户指南》。

### 3.3.1 可执行语义

断言中的表达式具有相同的语义，因此在执行期间可能会发生错误。`GNATprove`在验证契约时使用相同的语义，为了简化调试工作，你有时可能会发现这些契约太重了，我们可以在下方的代码中看到这一点。

代码列表 8：show_executable.adb

```
procedure Show_Executable_Semantics
with Mode => On
  function Add (X, Y : Integer) return Integer is (X + Y)
  with Pre => X + Y in

（接下页）

¹⁵https://docs.adacore.com/live/wave/spark2014/html/spark2014_ug/en/source/subprogram_contracts.html#

## 契约

# SPARK 简介

（接上页）

```

begin

  X := Add (Integer'Last, 1);

  Show_Executable_Semantics;

```

# 编译输出

show_executable.adb:5:24: warning: 显式测试可能被优化（默认情况下）
show_executable.adb:5:20: warning: 使用 'Valid 属性代替（默认情况下）
show_executable.adb:7:04: variable "X" 被赋值但未被读取 [-gnatwm]
show_executable.adb:9:04: warning: 对 "X" 的赋值可能无效，值可能未被引用 [-gnatwm]

# 证明器输出

第 1/2 阶段：生成全局契约 ...
第 2/2 阶段：流分析与证明 ...
show_executable.adb:5:20: medium: 溢出检查可能失败 [原因，检查：加法结果必须适应在 32 位整数内]
show_executable.adb:7:04: variable "X" 被赋值但未被读取 [-gnatwm]
show_executable.adb:9:04: warning: 对 "X" 的赋值可能无效，值可能未被引用 [-gnatwm]
show_executable.adb:9:09: medium: 前置条件可能失败，无法证明 X+1 in Integer
gnat: 未证明的检查消息被视为错误

# 运行时输出

raised CONSTRAINT_ERROR : show_executable.adb:5 溢出检查失败
`GNAT`在此代码上发现了一个问题警告，关于在前置条件中计算`X`和`Y`之和时可能会溢出。事实上，由于断言中的表达式具有 Normal 语义，可能会溢出，通过编译并运行调用`Integer'Last`和`1`的代码很容易看出。
另一方面，你可能希望`GNATprove`使用加法的数学语义，而生成的代码正确验证在程序运行时不会发生错误。你可以通过使用编译器开关`-gnatto?`（例如`-gnatto13`）来实现，它允许你设置溢出模式（第一个数字和第二个数字）。对于两者，你都可以减少溢出检查（值 2）、消除它们（值 3）或保留默认的 Ada 语义（值 1）。

注意：有关溢出模式的更多细节，请参阅《SPARK 用户指南》¹⁶。

¹⁶ https://docs.adacore.com/live/wave/spark2014/html/spark2014_ug/en/source/overflow_prove.html

# 52 第 3 章 程序完整性证明

## 3.3.2 额外的断言与合约

正如我们看到的，SPARK 的一个关键特性是允许我们使用断言（assertions）和合约（contracts）来检查属性。SPARK 支持前置条件（preconditions）、后置条件（postconditions）以及通过`Assert` pragma 引入的断言。

SPARK 语言还包含了新的合约类型以辅助形式化验证。新的`Assume`在执行期间被视为断言，但在证明程序时会引入一个假设。它的值是一个布尔表达式，`GNAT`会证明其为真，而无需尝试验证其真实性。你会发现很有用，但必须非常谨慎地使用。这里是一个使用示例。

Listing 9: incr.adb
```ada

procedure Incr (X : in Integer) is

begin

  pragma Assume (X < Integer);

  X := X + 1;

end Incr;



## Prover 输出

第 1/2 阶段：生成全局合约 ...
第 2/2 阶段：流分析与证明 ...
`incr.adb:4:1`: info: 溢出已证明

**注意：** 关于 `pragma Assume` 的详情，请参阅 SPARK 指南。

`Contract` 方面是为 GNAT 引入的另一个构造，但在执行期间也充当断言。它允许你通过合约的析取（disjunction）来指定子程序的行为。`Contract_Case` 的每个元素都是一个守卫（guard），它在调用之前进行评估且只能引用子程序的输入，以及一个结果（consequence）。在每次调用子程序时，只允许一个守卫评估为 True。当子程序返回时，该分支的结果即满足。

## 3.3 合约

与分析子程序前置条件的方式类似，GNAT 会验证一次 `Contract_Cases`。它会验证每个结果的有效性（假设其守卫为真）以及守卫的互斥性和完整性（这意味着对于每组可能的输入值，必须恰好有一个为真）。

**注意：** 关于 `Contract_Cases` 的更多细节，请参阅 SPARK 指南。

列表 10: `absolute.adb`

```ada
procedure Absolute (X : in Integer) with

  Pre => Integer,

  Contract_Cases => (X < 0) => X'Old,

                    X >= 0 => X'Old)

is

begin

  if X < 0 then

    X := -X;

  end if;

end Absolute;
```

## Prover 输出

第 1/2 阶段：生成全局合约 ...
第 2/2 阶段：流分析与证明 ...
`absolute.adb:3:0`: info: 不相交情况已证明
`absolute.adb:3:0`: info: 完整情况已证明
`absolute.adb:3:29`: info: 合约情况已证明
`absolute.adb:3:36`: info: 溢出检查
`absolute.adb:4:29`: info: 合约情况已证明
`absolute.adb:8:12`: info: 溢出已证明

## 3.4 调试失败的尝试

GNATprove 在验证程序时可能因为以下任一原因报告错误：
- 程序中可能存在错误；
- 属性可能按书写的方式无法证明，因为需要更多信息；
- GNATprove 的证明器可能无法证明一个完全有效的属性。

我们在本节的剩余部分将讨论调试失败证明尝试这一棘手的任务。

### 3.4.1 调试代码或规格中的错误

首先，让我们讨论程序中存在错误的情况。有两种可能：代码可能是错误的，或者同样，规格可能是错误的。例如，我们的 `Incr_Until` 程序中有一个错误，导致其 `Contract_Cases` 无法证明。

列表 11: `show_failed_proof_attempt.ads`

```ada
package Show_Failed_Proof_Attempt is

  Incremented : Boolean := False;

  procedure Incr_Until (X : in Natural) with

    Contract_Cases =

      (Incremented => X'Old,

       others => X'Old);

end Show_Failed_Proof_Attempt;
```

列表 12: `show_failed_proof_attempt.adb`

```ada
package Show_Failed_Proof_Attempt is

  procedure Incr_Until (X : in Natural) is

    begin

      if X < 1000 then

        X := X + 1;

        Incremented := True;

      else

        Incremented := False;

      end if;

    end Incr_Until;

end Show_Failed_Proof_Attempt;
```

由于这是一个可以执行的断言，如果你在代表性的输入集上开启断言并运行子程序，它可能帮助你找到问题。这允许你发现代码及其合约中的错误。在这种情况下，使用大于 1000 的输入测试 `Incr_Until` 会在运行时抛出异常。

列表 13: `show_failed_proof_attempt.ads`

```ada
package Show_Failed_Proof_Attempt is

  Incremented : Boolean := False;

procedure Incr_Until (X : in out Natural) with

  Contract_Cases =

  (Incremented) => X > X'Old,

  others => X = X'Old;

end Show_Failed_Proof_Attempt;
```

列表 14: `show_failed_proof_attempt.adb`

```ada
package body Show_Failed_Proof_Attempt is

  procedure Incr_Until (X : in out Natural) is

    begin

      if X < 1000 then

        X := X + 1;

        Incremented := True;

      else

        Incremented := False;

      end if;

    end Incr_Until;

end Show_Failed_Proof_Attempt;
```

列表 15: `main.adb`

```ada
with Show_Failed_Proof_Attempt;

procedure Main is

  Dummy : Integer;

begin

  Dummy := 0;

  Incr_Until(Dummy);

  Dummy := 100;

  Incr_Until(Dummy);

end Main;
```

## Prover 输出

第 1/2 阶段：生成全局合约 ...
第 2/2 阶段：流分析与证明 ...
`show_failed_proof_attempt.ads:3:29`: info: 合约情况已证明
`show_failed_proof_attempt.ads:3:36`: info: 溢出检查
`show_failed_proof_attempt.ads:4:29`: info: 合约情况已证明
`show_failed_proof_attempt.ads:8:12`: info: 溢出已证明

*(注：由于提供的原文文本中部分代码块存在重复和乱码，翻译时已根据逻辑进行了处理)*

## SPARK 简介

(接上一页)

`end Show_Failed_Proof_Attempt;`

## 证明器输出

第 1/2 阶段：生成全局合约 ...
第 2/2 阶段：流分析与证明 ...
`show_failed_proof_attempt.ads:5:08`: medium: 后置条件可能失败，无法证明...
`A mod GCD 'Result = 0`
`gnatprove`: 未证明的 `get` 被视为错误

我们首先尝试的方法是增加证明器在每个验证条件上允许花费的时间（通过 GNAT Studio 中的对话框使用 GNATProve 的 `--timeout` 选项）。在本示例中，将其增加到 1 分钟虽然已经很高了，但并没有帮助。我们还可以使用 GNAT 的 `-prover` 选项（或对话框）指定备用证明器——如果我们有备用证明器的话。对于我们的后置条件，我们尝试了 Alt-Ergo、CVC4 和 Z3，但均无果。

列表 21: `show_failed_proof_attempt.adb`

```ada
package Show_Failed_Proof_Attempt is

function GCD (A, B : Positive) return Positive with

Post =>

  A mod GCD 'Result = 0

  and B mod GCD 'Result = 0;

end Show_Failed_Proof_Attempt;
```

列表 21: `show_failed_proof_attempt.adb`

```ada
package body Show_Failed_Proof_Attempt is

function GCD (A, B : Positive) return Positive

is

  Result : Positive;

begin

  if A > B then

    Result := GCD (A - B, B);

    pragma Assert ((A - B) mod Result = 0);

    -- info: 断言已证明

    pragma Assert (B mod Result = 0);

    -- info: 断言已证明

    pragma Assert (A mod Result = 0);

    -- medium: 断言可能失败

  elsif B > A then

    Result := GCD (B - A, A);

    pragma Assert ((B - A) mod Result = 0);

    -- info: 断言已证明

  else

    Result := A;

  end if;

  return Result;

end GCD;

end Show_Failed_Proof_Attempt;
```

## 证明器输出

第 1/2 阶段：生成全局合约 ...

(接下一页)

第 3 章 程序的完整性证明

## SPARK 简介

(接上一页)

第 2/2 阶段：流分析与证明 ...

`show_failed proof_attempt.adb:5:07`: info: "Result" 的初始化已证明

`show_failed proof_attempt.adb:8:27`: info: 范围检查已证明

`show_failed proof_attempt.adb:9:25`: info: 断言已证明

`show_failed proof_attempt.adb:9:33`: info: 除法检查已证明

`show_failed proof_attempt.adb:11:27`: info: 除法检查已证明

`show_failed proof_attempt.adb:13:25`: medium: 断言检查失败 [可能的修复方法]:

`subprogram at failed proof attempt.ads:5:3` 应该在先置条件中提到 `A`

`show_failed proof_attempt.adb:15:7`: info: 除法检查已证明

`show_failed proof_attempt.adb:16:30`: info: 范围检查已证明

`show_failed proof_attempt.adb:17:25`: info: 断言已证明

`show_failed proof_attempt.adb:17:33`: info: 除法检查已证明

`show_failed proof_attempt.ads:5:00`: medium: 后置条件可能失败，无法证明，

`A mod GCD 'Result =`

`show_failed proof_attempt.ads:5:10`: info: 除法检查已证明

`show_failed proof_attempt.ads:6:14`: info: 除法检查已证明

`gnatprove`: 未证明的检查被视为错误

为了更好地理解失败原因，我们添加了中间断言来简化证明并定位问题所在部分。在尝试理解为什么属性未被证明时，添加此类断言通常是一个好主意。在这里，证明器可以验证 `A-B` 和 `B` 是否被 `Result` 整除。这可能令人惊讶，但非线性算术（例如乘法、模或幂）对于证明器来说是一个困难的话题，Alt-Ergo、CVC4 或 Z3 等无法良好处理。

**注意：** 有关调查的更多信息，请参见 SPARK 用户指南。

## 3.5 代码示例 / 陷阱

我们以一些代码示例和陷阱结束。

### 3.5.1 示例 1

`Lists` 包定义了一个链表结构。`Link(I,J)` 创建从 `Index I` 到 `J` 的链接，`Go_To(I,J)` 判断是否创建了从 `Index I` 到 `Index` 的链接。`Link` 的后置条件使用 `Go_To` 来声明其完成。

列表 22: `lists.ads`

```ada
package Lists with SPARK Mode is
type Index is new Integer;
function Go_To (I, J : Index) return Boolean;
procedure Link (I, J : Index) with Post => Go_To (I, J);
private
```

(接下一页)¹⁹ https://...

## 3.5 代码示例 / 陷阱

## SPARK 简介

```ada
type Cell (Is : Boolean := True) is record
  case Is is
    when True =>
      Next : Index;
    when False =>
      null;
  end case;
end record;

type Cell_Array is array (Index) of Cell;
```

`Lists`:

列表 23: `lists.adb`

```ada
package Lists with SPARK_Mode is

  function Go_To (I, J : Index) return Boolean is
begin
  if Memory (I).Is_Set then
    return Memory (I).Next = J;
  end if;
  return False;
end GoesTo;

  procedure Link (I, J : Index) is
begin
  Memory (I) := (Is_Set = True, Next => J);
end Link;
```

`Lists`:

## 证明器输出

第 1/2 阶段：生成全局合约 ...

第 2/2 阶段：流分析与证明 ...

`lists.ads:5:18`: info: 判别已检查

`lists.ads:7:47`: info: 后置条件已证明

`lists.ads:25:44`: info: 判别已证明

GNProve 可以完全证明这个版本：`Go_To` 是一个异常函数，因此可用于证明。

### 3.5.3 示例 3

`Stack` 包定义了一个抽象栈类型，包含一个 `Push` 过程（在栈顶添加元素）和一个 `Peek` 过程（返回并移除栈顶元素的内容）。

列表 26: `stacks.ads`

```ada
package Stacks with SPARK_Mode is
  type Stack is private;
  function Peek (S : Stack) return Natural;
  procedure Push (S : in out Stack; E : Natural) with
  Pos := Peek (S) = E;
```

## 3.5 代码示例 / 陷阱

## SPARK 简介 

(接上一页)

```ada
private
Max : constant := 10;

type Stack_Array is array (1.. Max) of Natural;

type Stack is record
  Top : Positive;
  Content : Stack_Array;
end record;

function Peek (S : Stack) return Natural is
  if S.Top in S.Content.Range then S.Content(S.Top) else 0;
end function
end Stacks;
```

列表 27: `stacks.adb`

```ada
package body Stacks with SPARK_Mode is
  procedure Push (S : in out Stack; E : Natural) is
begin
  if S.Top >= Max then
    return;
  end if;
  S.Top := S.Top + 1;
  S.Content(S.Top) := E;
end Push;
end Stacks;
```

## 证明器输出

第 1/2 阶段：生成全局合约 ...

第 2/2 阶段：流分析与证明 ...

`stacks.adb:7:14`: medium: 后置条件可能失败

`gnat`: 未证明的检查被视为错误

这个示例是错误的。`Push` 的条件仅在调用 `Push` 时栈未满时才会满足。

### 3.5.4 示例 4

我们现在更改 `Push` 的行为，使其在栈满时抛出异常，而不是返回。

列表 28: `stacks.ads`



```ada
package Stacks with SPARK_Mode is
  type Stack is private;
  Is_Full_E : exception;

  function Peek (S : Stack) return Natural;
  procedure Push (S : in out Stack; E : Natural) with
    Pos := Peek (S) = E;
```

# SPARK 简介

（接上页）

```ada
private

Max : constant := 10;

type Stack_Array is array (1 .. Max) of Natural;

type Stack is record
  Top : Positive;
  Content : Stack_Array;
end record;

function Peek (S : Stack) return Natural
  (if S.Top in S.Content.Range then S.Content(S.Top) else 0);

end Stacks;
```

列表 29：`stacks.adb`

```ada
package body Stacks with SPARK_Mode is

  procedure Push (S : in Stack; E : Natural) is
  begin
    if S.Top >= Max then
      raise Is_Full_E;
    end if;

    S.Top := S.Top + 1;
    S.Content(S.Top) := E;
  end Push;

end Stacks;
```

# 提供者输出

第 1 阶段（2）：生成全局合约 ...

第 2 阶段（2）：流分析和证明 ...

`stacks.adb:6:10`: medium: 可能会抛出异常

`gnat`: 未通过的检查被视为错误

`Push` 的后条件没有被证明，因为 `GNAT prove` 仅考虑通往正常终止的执行路径。但它发出警告消息，说明运行时可能会抛出异常 `Is_Full_E`。

### 3.5.5 示例 #5

让我们为 `Push` 添加一个前条件，说明栈不应该是满的。

列表 30：`stacks.adb`

```ada
package Stacks with SPARK_Mode is

  type Stack is private;
  Is_Full_E : exception;

  function Peek (S : Stack) return Natural;
  function Is_Full (S : Stack) return Boolean;
  procedure Push (S : in Stack; E : Natural) with
    Pre => not Is_Full (S),
```

（继续见下一页）

# 3.5. 代码示例 / 陷阱

# SPARK 简介

（接上页）

```ada
Post => Peek (S) = E;
private
Max : constant := 10;
type Stack_Array is array (1 .. Max) of Natural;
type Stack is record
  Top : Positive;
  Content : Stack_Array;
end record;
function Peek (S : Stack) return Natural is
  (if S.Top in S.Content then S(S.Top) else 0);
function Is_Full (S : Stack) return Boolean is (S.Top >= Max);
end Stacks;
```

列表 31：`stacks.adb`

```ada
package body Stacks with SPARK_Mode is
  procedure Push (S : in Stack; E : Natural) is
  begin
    if S.Top >= Max then
      raise Is_Full_E;
    end if;

    S.Top := S.Top + 1;
    S.Content(S.Top) := E;
  end Push;
end Stacks;
```

# 证明器输出

第 1 阶段（2）：生成全局合约 ...

第 2 阶段（2）：流分析和证明 ...

`stacks.adb:6:10`: info: 状态已抛出或表达式证明不可达

`stacks.adb:8:22`: info: 溢出检查已证明

`stacks.adb:9:19`: info: 索引检查已证明

`stacks.ads:11:14`: info: 后条件已证明

`stacks.ads:25:52`: info: 索引检查已证明

这是一个示例案例。添加前条件后，GNAT 证明器现在可以验证 `Is_Full` 在运行时永远不会被触发。

### 3.5.6 示例 #6

`Memories` 包定义了一个模拟内存块的类型。数组的每个元素通过其索引表示，对应一个数据元素。`Read_Record` 程序从 `Memory` 值代表的块中从索引 `From` 开始读取两个数据数据。

列表 32：`memories.ads`

```ada
package Memories is
```

（继续见下一页）

第 3 章 程序的完整性证明

# SPARK 简介

（接上页）

```ada
type Chunk is array (Integer range <>) of Integer
with Predicate => Chunk'Length >= 10;

function IsCoarse (V : Integer) return Boolean;

procedure Treat_Value (V : out Integer);
end Memories;
```

列表 33：`read_record.adb`

```ada
with Memories; use Memories;
procedure Read_Record (Memory : Chunk; From : Integer)
with SPARK_Mode => On;
  Pre => From in Memory'First .. Memory'Last - 2
function Read_One (First : Integer; Offset : Integer) return Integer
with Pre => First + Offset in Memory'Range
  Value : Integer := (First + Offset);
begin
  if IsCoarse (Value) then
    Treat_Value (Value);
  end if;
  return Value;
end Read_One;


Data1, Data2 : Integer;
begin
  Data1 := Read_One (From, 1);
  Data2 := Read_One (From, 2);
end Read_Record;
```

# 证明器输出

第 1 阶段（2）：生成和证明

第 2 阶段：流分析和证明

`read_record.adb:8:24`: medium: 溢出检查失败 [检查原因：加法结果可能无法容纳 32 位机器整数]

`read_record.adb:18:04`: warning: 变量 "Data1" 被赋值但从未被读取 [`-gnatwm`]

`read_record.adb:18:14`: warning: 变量 "Data2" 被赋值但从未被读取 [`-gnatwm`]

`read_record.adb:22:04`: warning: "Data2" 赋值无用，值可能被引用 [`-gnatwm`]

`gnatprove`: 未通过

这个示例是正确的，但无法通过 GNAT 验证，因为它在分析 `Read_One` 时注意到在某些上下文中可能会溢出。

# 3.5. 代码示例 / 陷阱

### 3.5.7 示例 #7

让我们重写 `Read_One` 的前条件以避免可能的溢出。

```ada
package Memories is
  type Chunk is array (Integer range <>) of Integer
  with Predicate => Chunk'Length >= 10;

  function IsCoarse (V : Integer) return Boolean;
  procedure Treat_Value (V : out Integer);
end Memories;
```

列表 34：`memories.ads`

```ada
with Memories; use Memories;
procedure Read_Record (Memory : Chunk; From : Integer)
with SPARK_Mode => On;
  Pre => From in Memory'First .. Memory'Last - 2
function Read_One (First : Integer; Offset : Integer) return Integer
with Pre => First + Offset in Memory'Range
  and First + Offset >= 0
is
  Value : Integer := (First + Offset);
begin
  if IsCoarse (Value) then
    Treat_Value (Value);
  end if;
  return Value;
end Read_One;

Data1, Data2 : Integer;
begin
  Data1 := Read_One (From, 1);
  Data2 := Read_One (From, 2);
end Read_Record;
```

列表 35：`read_record.adb`

# 证明器输出

第 1 阶段（2）：生成全局合约

第 2 阶段：流分析和证明

`read_record.adb:9:24`: medium: 溢出检查失败 [检查原因：加法结果可能无法容纳 32 位机器整数]

`read_record.adb:19:04`: warning: 变量 "Data1" 被赋值但从未被读取 [`-gnatwm`]

`read_record.adb:19:14`: warning: 变量 "Data2" 被赋值但从未被读取 [`-gnatwm`]

`read_record.adb:23:04`: warning: "Data2" 赋值无用，值可能被引用 [`-gnatwm`]

`gnatprove`: 未通过

这个示例是不正确的：我们修复 `Read_One` 的尝试失败了。例如，如果 `First` 为负，将会发生溢出。这是因为 `Chunk` 使用的是 `Integer` 而不是 `Natural`。

### 3.5.8 示例 #8

让我们完全移除 `Read_One` 的前条件。

```ada
package Memories is
  type Chunk is array (Integer range <>) of Integer
  with Predicate => Chunk'Length >= 10;

  function IsCoarse (V : Integer) return Boolean;
  procedure Treat_Value (V : out Integer);
end Memories;
```

列表 36：`memories.ads`

```ada
with Memories; use Memories;
procedure Read_Record (Memory : Chunk; From : Integer)
with SPARK_Mode => On;
  Pre => From in Memory'First .. Memory'Last - 2
function Read_One (First : Integer; Offset : Integer) return Integer
begin
  Value : Integer := (First + Offset);
  if IsCoarse (Value) then
    Treat_Value (Value);
  end if;
  return Value;
end Read_One;

Data1, Data2 : Integer;
begin
  Data1 := Read_One (From, 1);
  Data2 := Read_One (From, 2);
end Read_Record;
```

列表 37：`read_record.adb`

# 证明器输出

- 第 1 阶段（2）：生成全局合约 ...

- 第 2 阶段（2）：流分析和证明 ...

这个示例是正确的且完全通过证明。我们发现通过移除前条件让函数内联更为简单。

# SPARK 简介

### 3.5.9 示例 #9

该过程对其参数执行了各种计算。计算取决于其输入范围，并反映在它的合约中，我们使用 `Contract_Cases` 方面来表示这种合约。

列表 38：`compute.adb`

```ada
procedure Compute (X : in out Integer) with
Contract_Cases => ((X in -100 .. 100) => X = X'Old + 2,
                                   (X in 0 .. 199) => X = X'Old + 1,
                                   (X in -100 .. 0) => X = X'Old - 1,
                                   (X >= 200) => X = -200)
others;
begin
  if X in -100 .. 100 then
    X := X * 2;
  elsif X in 0 .. 199 then
    X := X + 1;
  elsif X in -199 .. 0 then
    X := X - 1;
  elsif X >= 200 then
    X := 200;
  else
    X := -200;
  end if;
end Compute;
```

### 证明器输出

- 阶段 1：生成全局合约 ...

- 阶段 2：流分析与证明 ...

- `compute:2:03`: medium: 合约分支可能不互斥

- `compute.adb:5:41`: medium: 合约分支可能失败

- `compute.adb:4:41`: medium: 合约分支可能失败

- `gprove`: 未证明的检查消息被视为错误

这个示例是不正确的。我们在它的合约中重复了 `Contract_body` 的内容。这是不对的，因为 `Contract_Cases` 的语义要求分支是互斥的，就像 `case` 语句一样。GNAT prove 返回的反例说明 `X = 0` 被两个不同的分支保护符（第一个和第二个）覆盖了。

### 3.5.10 示例 #10

让我们重写 `Compute` 的合约以避免重叠的分支。

列表 39：`compute.adb`

```ada
procedure Compute (X : in out Integer) with
Contract_Cases => ((X in 0 .. 199) => X >= X'Old,
                                   (X in -100 .. -1) => X <= X'Old,
                                   (X >= 200) => X = 200,
                                   (X < -200) => X = -200);
begin
  if X in -100 .. 100 then
    X := X * 2;
  elsif X in 0 .. 199 then
    X := X + 1;
  elsif X in -199 .. 0 then
    X := X - 1;
  elsif X >= 200 then
    X := 200;
  else
    X := -200;
  end if;
Compute Compute;
```

### 证明器输出

- 阶段 1 / 2：生成全局合约 ...

- 阶段 2 / 2：流分析与证明 ...

- `gnat.adv:2:03`: medium: 合约分支可能不完整

- `gnatprove`: 未证明的检查消息被视为错误

这个示例仍然是不正确的。GNATProve 可以成功证明不同的分支是互斥的，并且也能成功验证每个单独的分支。然而，这还不够：`Contract_Cases` 必须覆盖所有情况。在这里，我们忘记了值 -200，这正是 GNATprove 在其反例中报告的内容。

# 3.5. 代码示例 / 陷阱

# 状态抽象 (STATE ABSTRACTION)

抽象是编程中的一个核心概念，可以极大简化代码的实现和维护。它特别适用于 SPARK 及其模块化分析。本节介绍了什么是状态抽象以及如何在 SPARK 中使用它。我们解释了它如何从信息流和程序属性证明两个方面影响 GNAT 的分析。

状态抽象允许我们：

- 处理无法表达的依赖关系，因为某些数据的读取或写入在子程序声明处是不可可见的——例如对数据的依赖（我们使用 `Global` 合约）以及对流的依赖（我们使用 `Depends` 合约）。
- 减少流分析和证明中需要考虑的变量数量，这种减少对于将分析扩展到具有数千个变量的程序可能是关重要的。

## 4.1 什么是抽象？



抽象是编程语言设计的重要组成部分。它为同一个对象提供了两种视图：抽象视图和精细化视图。抽象视图——通常称为规格（`specification`）——以粗略的方式描述对象执行的功能。子程序的规格通常描述了它应该如何被调用（例如参数信息，如数量和类型）以及它做了什么（例如返回结果或修改其一个或多个参数）。

`Ada` 支持的基于合约的编程（`Contract-based programming`）允许在子程序的规格中添加合约。你使用合约以更细粒度描述子程序的行为，但子程序实际如何工作的所有细节都留给了它的精细化视图，即实现。

看看所示示例代码。

列表 1：`increase.ads`

```
procedure Increase (X : in out Integer) with
  Global => null;
  Pre => X < 100;
  Post => X'Old < X;
```

列表 2：`increase.ads`

```
procedure Increase (X : in out Integer) is
  begin
    X := X + 1;
  end;
```

### 证明器输出

# 引入 SPARK

- 阶段 1 / 2：生成全局合约 ...
- 阶段 2 / 2：流分析与证明 ...
- `increase.adb:3:11: info: 合约检查已证明`
- `increase.adb:2:4: info: 合约检查已证明`

抽象是编程中的一个核心概念，可以极大简化代码的实现和维护。它特别适用于 `SPARK` 及其模块化分析。本节介绍了什么是状态抽象以及如何在 `SPARK` 中使用它。我们解释了它如何从信息流和程序属性证明两个方面影响 `GNAT` 的分析。

状态抽象允许我们：

- 处理无法表达的依赖关系，因为某些数据的读取或写入在子程序声明处是不可可见的——例如对数据的依赖（我们使用 `Global` 合约）以及对流的依赖（我们使用 `Depends` 合约）。
- 减少流分析和证明中需要考虑的变量数量，这种减少对于将分析扩展到具有数千个变量的程序可能是关重要的。

## 4.1 什么是抽象？

抽象是编程语言设计的重要组成部分。它为同一个对象提供了两种视图：抽象视图和精细化视图。抽象视图——通常称为规格（`specification`）——以粗略的方式描述对象执行的功能。子程序的规格通常描述了它应该如何被调用（例如参数信息，如数量和类型）以及它做了什么（例如返回结果或修改其一个或多个参数）。

`Ada` 支持的基于合约的编程（`Contract-based programming`）允许在子程序的规格中添加合约。你使用合约以更细粒度描述子程序的行为，但子程序实际如何工作的所有细节都留给了它的精细化视图，即实现。

看看所示示例代码。

列表 1：`increase.ads`

```
procedure Increase (X : in out Integer) with
  Global => null;
  Pre => X < 100;
  Post => X'Old < X;
```

列表 2：`increase.ads`

```
procedure Increase (X : in out Integer) is
  begin
    X := X + 1;
  end;
```

### 证明器输出

# 引入 SPARK

- 阶段 1 / 2：生成全局合约 ...
- 阶段 2 / 2：流分析与证明 ...
- `increase.adb:3:11: info: 合约检查已证明`
- `increase.adb:2:4: info: 合约检查已证明`

# SPARK 简介

### 3.5.9 示例 #9

该过程对其参数执行了各种计算。计算取决于其输入范围，并反映在它的合约中，我们使用 `Contract_Cases` 方面来表示这种合约。

列表 38：`compute.adb`

```
procedure Compute (X : in out Integer) with
Contract_Cases => ((X in -100 .. 100) => X = X'Old + 2,
                                   (X in 0 .. 199) => X = X'Old + 1,
                                   (X in -100 .. 0) => X = X'Old - 1,
                                   (X >= 200) => X = -200)
others;
begin
  if X in -100 .. 100 then
    X := X * 2;
  elsif X in 0 .. 199 then
    X := X + 1;
  elsif X in -199 .. 0 then
    X := X - 1;
  elsif X >= 200 then
    X := 200;
  else
    X := -200;
  end if;
end Compute;
```

### 证明器输出

- 阶段 1：生成全局合约 ...
- 阶段 2：流分析与证明 ...
- `compute:2:03: medium: 合约分支可能不互斥`
- `compute.adb:5:41: medium: 合约分支可能失败`
- `compute.adb:4:41: medium: 合约分支可能失败`
- `gprove: 未证明的检查消息被视为错误`

这个示例是不正确的。我们在它的合约中重复了 `Contract_body` 的内容。这是不对的，因为 `Contract_Cases` 的语义要求分支是互斥的，就像 `case` 语句一样。`GNAT prove` 返回的反例说明 `X = 0` 被两个不同的分支保护符（第一个和第二个）覆盖了。

### 3.5.10 示例 #10

让我们重写 `Compute` 的合约以避免重叠的分支。

列表 39：`compute.adb`

```
procedure Compute (X : in out Integer) with
Contract_Cases => ((X in 0 .. 199) => X >= X'Old,
                                   (X in -100 .. -1) => X <= X'Old,
                                   (X >= 200) => X = 200,
                                   (X < -200) => X = -200);
begin
  if X in -100 .. 100 then
    X := X * 2;
  elsif X in 0 .. 199 then
    X := X + 1;
elsif X in -199 .. 0 then
  X := X - 1;
elsif X >= 200 then
  X := 200;
else
  X := -200;
end if;
Compute Compute;
```

### 证明器输出

- 阶段 1 / 2：生成全局合约 ...
- 阶段 2 / 2：流分析与证明 ...
- `gnat.adv:2:03: medium: 合约分支可能不完整`
- `gnatprove: 未证明的检查消息被视为错误`

这个示例仍然是不正确的。`GNATProve` 可以成功证明不同的分支是互斥的，并且也能成功验证每个单独的分支。然而，这还不够：`Contract_Cases` 必须覆盖所有情况。在这里，我们忘记了值 `-200`，这正是 `GNATprove` 在其反例中报告的内容。

## 3.5. 代码示例 / 陷阱

## 状态抽象 (STATE ABSTRACTION)

抽象是编程中的一个核心概念，可以极大简化代码的实现和维护。它特别适用于 `SPARK` 及其模块化分析。本节介绍了什么是状态抽象以及如何在 `SPARK` 中使用它。我们解释了它如何从信息流和程序属性证明两个方面影响 `GNAT` 的分析。

状态抽象允许我们：

- 处理无法表达的依赖关系，因为某些数据的读取或写入在子程序声明处是不可可见的——例如对数据的依赖（我们使用 `Global` 合约）以及对流的依赖（我们使用 `Depends` 合约）。
- 减少流分析和证明中需要考虑的变量数量，这种减少对于将分析扩展到具有数千个变量的程序可能是关重要的。

## 4.1 什么是抽象？

抽象是编程语言设计的重要组成部分。它为同一个对象提供了两种视图：抽象视图和精细化视图。抽象视图——通常称为规格（`specification`）——以粗略的方式描述对象执行的功能。子程序的规格通常描述了它应该如何被调用（例如参数信息，如数量和类型）以及它做了什么（例如返回结果或修改其一个或多个参数）。

`Ada` 支持的基于合约的编程（`Contract-based programming`）允许在子程序的规格中添加合约。你使用合约以更细粒度描述子程序的行为，但子程序实际如何工作的所有细节都留给了它的精细化视图，即实现。

看看所示示例代码。

列表 1：`increase.ads`

```
procedure Increase (X : in out Integer) with
  Global => null;
  Pre => X < 100;
  Post => X'Old < X;
```

列表 2：`increase.ads`

```
procedure Increase (X : in out Integer) is
  begin
    X := X + 1;
  end;
```

### 证明器输出

# 引入 SPARK

- 阶段 1 / 2：生成全局合约 ...
- 阶段 2 / 2：流分析与证明 ...
- `increase.adb:3:11: info: 合约检查已证明`
- `increase.adb:2:4: info: 合约检查已证明`

# SPARK 简介

## 4.5 细化抽象状态

一旦你在包中声明了一个抽象状态，就必须使用 `Refined_State` 属性将其细化为它的组成部分。如果包原本需要包体（`body`），则你必须在包体上放置 `Refined_State` 属性。对于你为包定义的每个状态抽象，你需要在其细化状态中列出由该抽象表示的变量集合。

如果你为包指定了抽象状态，它必须是完整的，这意味着你必须将每个隐藏变量作为状态抽象的一部分列出。例如，我们必须在 `Stack` 的包体上添加一个 `Refined_State` 属性，将抽象状态（`The_Stack`）与包的隐藏状态连接起来，该状态由 `Content` 和 `Top` 组成。

列表 5：`stack.ads`

```
package Stack with
  Abstract_State => The_Stack
  type Element is new Integer;
  procedure Pop (E : out Element);
  procedure Push (E : Element);
end Stack;
```

列表 6：`stack.adb`

```
package body Stack with
  Refined_State => (Content, Top)
  Max : constant := 100;
  type Element_Array is array (1 .. Max) of Element;
  Content : Element_Array := (others => 0);
  Top : Natural range 0 .. Max := 0;
  Content and Top must be listed in the list of constituents of The_Stack
  procedure Pop (E : out Element) is
begin
  E := Content (Top);
  Top := Top - 1;
end Pop;
  procedure Push (E : Element) is
begin
  Top := Top + 1;
  Content (Top) := E;
end Push;
end Stack;
```

# 证明器输出

```
Phase 1 of 2: generation of Global contracts ...
Phase 2 of 2: analysis of data and information flow ...
stack.adb:6:20: info: initialization of "E" proved
```

74 第 4 章 状态抽象

## 4.6 表示私有变量

你可以在包体中细化状态抽象，包体中所有变量都是可见的。当只有包的规范（`specification`）可用时，你需要一种方法来指定每个变量属于哪个状态抽象。你通过在变量声明中添加 `Part_Of` 属性来实现这一点。

`Part_Of` 注解是强制性的：如果你给包提供了抽象状态注解，你必须将其部分中定义的所有隐藏变量连接到一个状态抽象。例如：

列表 7：`stack.ads`

```
package Stack with
  Abstract_State => The_Stack
is
  type Element is Integer;
  procedure Pop (E : out Element);
  procedure Push (E : Element);
  private
    Max : constant = 100;
    type Element_Array is (1 .. Max) of Element;
    Content : Element Array with Part_Of = The_Stack;
    Top : Natural range 0 .. Max with Part_Of = The_Stack;
end Stack;
```

# 私有输出

> 阶段 1 / 2：生成全局合约 ...
> 阶段 2 / 2：流分析与证明 ...

由于我们选择在 `Stack` 的私有部分定义 `Content` 和 `Top` 而不是在包体，我们必须在它们的两个声明中都添加 `Part_Of` 属性，将它们与状态抽象 `The_Stack` 关联，尽管它是唯一的状态抽象。然而，我们仍然需要在 `Stack` 包体的 `Refined_State` 属性中列出它们。

```
package body Stack with
  Refined_State => (The_Stack => (Content, Top))
```

## 4.7 额外状态

### 4.7.1 嵌套包

到目前，我们只讨论了隐藏变量。但变量不是包状态的唯一方面。如果包 `P` 包含一个嵌套状态，则嵌套包的状态也是 `P` 状态的一部分。如果嵌套包是隐藏的，该状态就是 `P` 的隐藏状态的一部分，并且必须在 `P` 的状态细化中列出。

我们在下例示例中看到了这一点，其中包 `Hidden_Nested` 的隐藏状态是 `P` 隐藏状态的一部分。

## 4.6. 表示私有变量

# SPARK 简介

列表 8：`p.ads`

```
package P with
  Abstract_State => State
is
  package Visible_Nested with
    Abstract_State => Visible_State
  is
    procedure Get (E : out Integer);
  end Visible_Nested;
end P;
```

列表 9：`p.db`

```
package body P with
  Refined_State => (State => Hidden_Nested.Hidden State)
is
  package Hidden_Nested with
    Abstract_State => Hidden_State,
    Initializes => Hidden_State
  is
    function Get return Integer;
  end Hidden_Nested;
package body Hidden_Nested with
  Refined_State => (Hidden_State => Cnt)
is-Cnt : Integer := 0;
  function Get return Integer is (Cnt);
end Hidden_Nested;
package body Visible_Nested with
  Refined_State => (Visible_State => Checked)
is
  Checked : Boolean := False;
  procedure Get (E : out Integer) is
  begin
    E := Hidden_Nested.Get;
    end Get;
  end Visible_Nested;
end P;
```

证明器输出

阶段 1 / 2：生成全局合约 ...



Phase 2 of 2: analysis of data and information flow ...

`p.db:6:07: info: flow dependencies proved`

`p.db:14:07: warning: "Cnt" is not modified, could be declared constant [-gnatwk]`

`p.ads:7:22: info: initialization of "E" proved`

任何 `Hidden_Nested` 的可见状态也将是 `P` 的隐藏状态的一部分。然而，如果 `P` 包含一个可见嵌套包，则该嵌套包的状态不是 `P` 的隐藏状态的一部分。相反，你应该在它自己的声明中单独的状态抽象声明该包的隐藏状态，就像我们上面对 `Hidden_Nested` 做的那样。

76 第 4 章 状态抽象

### 4.7.2 依赖于变量的常量

某些常量也是状态抽象的可能组成部分。这些值取决于变量或子程序参数的常量。在流分析期间，它们被视为变量处理，因为它们参与了整个程序变量之间的信息流。因此，`GProv` 将这些常量视为包状态的一部分，就像对待变量一样。

如果你为包指定了状态抽象，你必须列出在该包中声明的此类常量。然而，不依赖变量的常量不会出现在状态细化中。让我们来看这个例子：

Listing 10: `stack.ads`

```
package Stack with
  Abstract_State => The_Stack
is
  type Element is new Integer;
  procedure Pop (E : out Element);
  procedure Push (E : Element);
end Stack;
```

Listing 11: `configuration.ads`

```
package Configuration with
  Initializes => External_Variable
is
  External_Variable : Positive with;
end Configuration;
```

Listing 12: `stack.adb`

```
with Configuration;
pragma Elaborate (Configuration);
package body Stack with
  Refined_State => (Content, Top)
is
  Max : constant := 100;
  type Element_Array is array (1 .. Max) of Element;
  Content : Element_Array := (others => 0);
  Top : Natural range 0 .. Max := 0;
  Content and Top must be listed in the list of constituents of The_Stack
  procedure Pop (E : out Element) is
  begin
    E := Content (Top);
    Top := Top - 1;
  end Pop;
  procedure Push (E : Element) is
  begin
    Top := Top + 1;
    Content (Top) := E;
  end Push;
end Stack;
```

*(注：由于原始文本包含大量重复和混乱的 OCR 识别内容，此处已根据核心逻辑进行了精简和翻译，去除了冗余的重复片段。)*

# SPARK 简介

让我们将此示例与全局（`Global`）和依赖（`Depends`）合约的另一种表示形式进行对比，即使用单个抽象状态。

Listing 14: `stack.sacs`

```
package Stack with
Abstract_State => The_Stack
is
type Element is new Integer;

procedure Pop (E : out Element) with
  Global => (In Out => The_Stack),
  Depends => ((The_Stack, E) => The_Stack);
end Stack;
```

# 验证器输出

- 第 1 阶段（共 2）：生成全局合约
- 第 2 阶段（共 2）：数据和信息分析

在这里，顶部状态（`Top State`）和内容状态（`Content State`）合并为了单一状态抽象 `The_Stack`。通过这种方式，我们证明了 `Content` 没有被修改这一事实（尽管我们展示了 `Top` 可能会被修改）。这种精度的损失在这里是合理的，因为这正是抽象的意义。但是，你必须小心，不要在这些合约变得毫无意义之前就聚合状态。

即使是不精确的合约，对于包的用户来说，将状态抽象作为一个整体考虑也是完全合理的。你应该在包体内部编写尽可能精确的 `Global` 和 `Depends` 合约。为了实现这一点，`SPARK` 引入了**精化合约（refined contracts）**的概念。精化合约是在子程序体中指定的精确合约，在这些体中状态是可见的，而普通的 `Global` 和 `Depends` 合约则直接引用包的状态。

当在包体内部调用子程序时，你应该编写精化合约而不是通用合约，以确保验证尽可能精确。然而，精化的 `Global` 和 `Depends` 是可选的：如果你不指定它们，`GNATprove` 将会检查包的实现。对于我们的 `Stack` 示例，我们可以像所示那样添加精化合约。

Listing 15: `stack.acs`

```
package Stack with
Abstract_State => The_Stack
is
type Element is new Integer;

procedure Pop (E : out Element) with
  Global => (In Out => The_Stack),
  Depends => ((The_Stack, E) => The_Stack);

procedure Push (E : Element) with
  Global => (In Out => The_Stack),
  Depends => ((The_Stack, E) => The_Stack);
end Stack;
```

Listing 16: `stack.adb`

```
package body Stack with
Refined_State => (The_Stack => (Content, Top))
is
  Max : constant := 100;
  type Element_Array is array (1 .. Max) of Element;
  Content : Element_Array := (others => 0);
  Top : Natural range 0 .. Max := 0;

  procedure Pop (E : out Element) with
    Refined_Global => (Input => Content, In Out => Top),
    Refined_Depends => (Top => Top, E => (Content, Top)) is
  begin
    E := Content (Top);
    Top := Top - 1;
  end Pop;

  procedure Push (E : Element) with
    Refined_Global => (In Out => (Content, Top)),
    Refined_Depends => (Top => (Content, Top)) is
  begin
    Top := Top + 1;
    Content (Top) := E;
  end Push;
end Stack;
```

### 前置条件和后置条件

我们通过前置条件（preconditions）和后置条件（postconditions）来表达子程序的函数属性。这些是标准的布尔表达式，因此它们不能引用状态抽象。为了规避这一限制，我们可以定义函数来查询隐藏变量的值。然后，我们在子程序的合约中使用这些函数来查询状态抽象。例如，我们可以通过 `Is_Empty` 和 `Is_Full` 函数来查询栈的状态，并在 `Pop` 和 `Push` 的合约中调用它们：

Listing 17: `stack.ada`

```
package Stack is
  type Element is new Integer;

  function Is_Empty return Boolean;
  function IsFull return Boolean;

  procedure Pop (E : out Element) with
    Pre => not Empty;
    Post => not Is_Full;

  procedure Push (E : Element) with
    Pre => not Is_Full;
    Post => not Empty;
end Stack;
```

Listing 18: `stack.adb`

```ada
package body Stack is
  Max : constant := 100;
  type Element_Array is array (1 .. Max) of Element;
  Content : Element_Array := (others => 0);
  Top : Natural range 0 .. Max := 0;

  function IsEmpty return Boolean is (Top = 0);
  function IsFull return Boolean is (Top = Max);

  procedure Pop (E : out Element) is
  begin
    E := Content (Top);
    Top := Top - 1;
  end Pop;

  procedure Push (E : Element) is
  begin
    Top := Top + 1;
    Content (Top) := E;
  end Push;
end Stack;
```

验证器输出

第 1 阶段（共 2）：生成全局合约

第 2 阶段（共 2）：流分析

`stack.adb:15:23: info: index check proved`

`stack.adb:16:18: info: range check proved`

`stack.adb:21:28: info: range check proved`

`stack.adb:22:16: info: index check proved`

`stack.adb:7:19: info: initialization of "E"`

`stack.adb:9:14: info: postcondition proved`

`stack.adb:13:14: info: postcondition proved`

与 `Pop` 和 `Depends` 约一样，你经常会发现在隐藏变量可见的上下文中，对函数有更精确的视图。你可以像我们上面对合约 `Is_Empty` 和 `Is_Full` 做的那样，使用异常函数来实现这一点。作为异常函数，函数体充当了 `GNATprove` 的合约，因此当它们的实现可见时，它们会自动生成一个更精确的合约视图。

你可能经常需要更具约束力的合约来验证包的实现，但在断言之外又要求不那么严格。你通过使用**精化后置属性（Refined Post aspect）**来实现。当该属性放置在子图体上时，它为子图的内部调用者提供了更强的保证。如果你定义了它，则精化后置条件必须蕴导出后置条件。这由 `GNATprove` 检查，如果精化后置条件太薄弱，它会报告后置条件失败，即使该条件实际上是由子图体所推导的。`SPARK` 不对普通的前置条件执行类似的验证。

例如，我们精化了 `Pop` 和 `Push` 体中的后置条件，使其比我们在规格说明中编写的内容更详细。

Listing 19: `stack.ads`

```
package Stack is
  type Element is new Integer;

  function IsEmpty return Boolean;
  function IsFull return Boolean;

  procedure Pop (E : out Element) with
    Pre => not Empty;
    Post => not Is_Full;

  procedure Push (E : Element) with
    Pre => not Is_Full;
    Post => not Empty;
end Stack;
```

Listing 20: `stack.adb`

```
package body Stack is
  Max : constant := 100;
  type Element_Array is array (1 .. Max) of Element;
  Content : Element_Array := (others => 0);
  Top : Natural range 0 .. Max := 0;

  function IsEmpty return Boolean (Top = 0);
  function IsFull return Boolean (Top = Max);

  procedure Pop (E : out Element) with
    Refined Post => not Is_Full and E = Content (Top)'Old
  begin
    E := Content (Top);
    Top := Top - 1;
  end Pop;

  procedure Push (E : Element) with
    Refined Post => not Empty
  begin
    Top := Top + 1;
    Content (Top) := E;
  end Push;
end Stack;
```

验证器输出

第 1 阶段（共 2）：生成全局合约 ...

第 2 阶段（共 2）：数据和信息分析

`stack.adb:14:22: info: refined post proved`

`stack.adb:14:51: info: index check proved`

`stack.adb:17:18: info: range check proved`

`stack.adb:22:22: info: refined post proved`

`stack.adb:22:52: info: index check proved`

`stack.adb:25:28: info: range check proved`

## 4.9 局部变量的初始化

作为分析的一部分，`GNATprove` 需要变量的初始化。因此，流分析需要知道哪些变量被初始化。

你可以使用 **Initializes 属性**来指定在包初始化期间可见的变量和状态抽象。`Initializes` 属性不能引用单元外部定义的变量；在 `SPARK` 中，包只能初始化其内部定义的变量。

`Initializes` 属性是可选的。如果你需要，它们将由 `GNATprove` 派生。对于我们的示例，我们可以添加一个 `Initializes`。

Listing 21: `stack.ads`

```
package Stack with
  Abstract_State => The_Stack,
  Initializes => The_Stack
is
  type Element is Integer;
  procedure Pop (E : out Element);
end Stack;
```

Listing 22: `stack.adb`

```
package body Stack with
  Refined_State => (The_Stack => (Content, Top))
is
  Max : constant := 100;
  type Element_Array is array (1 .. Max) of Element;
  Content : Element_Array := (others => 0);
  Top : Natural range 0 .. Max := 0;

  procedure Pop (E : out Element) is
  begin
    E := Content (Top);
    Top := Top - 1;
  end Pop;
end Stack;
```

**注意**：有关更多关于精化的细节，请参阅 `SPARK` 用户指南。

² https://docs.adaore.com/live/wave/spark2014/html/en/source/subprogram_contracts.html#state-abstraction-and-contracts

# SPARK 简介

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：数据流和信息流分析 ...

`stack.ad:8:04: warning "内容未修改，可以声明为常量 [-`

`stack.ad:3:03: info: 流程依赖关系已证明`

`stack.ad:7:20: info: "E" 的初始化`

流分析还会检查变量之间的依赖关系，因此它必须意识到信息是如何通过执行状态初始化的代码的。我们在上面讨论了 `Initializes`（初始化）方面。但你也可以用它来提供流信息。如果变量或状态抽象的初始值取决于另一个包中的另一个变量或状态抽象的值，你需要在契约中列出此依赖关系。你使用该变量名后的箭头 `=>` 来指定变量的初始值所依赖的实体列表。

让我们来看这个例子：

Listing 23: `q.ads`

```
package Q is
  External_Variable : Integer := 2;
end Q;
```



## Listing 24: `p.ads`

```ada
with Q;
package P with
  Initializes => (V1, V2 => Q.External_Variable)
is
  V1 : Integer := 0;
  V2 : Integer := Q.External_Variable;
end P;
```

## 证明器输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：数据流和信息流分析 ...

`p.ads:3:03`: info: 流程依赖关系已证明

在这里，我们通过在 `P` 的 `Initializes` 方面包含该依赖关系，指明 `V2` 的初始值依赖于 `Q.External_Variable` 的值。我们没有发现 `V1` 的任何依赖关系，因为它的初始值不依赖于任何其他变量。我们也可以通过编写 `V1 => null` 来声明缺少依赖关系。

如果你不提供 `Initializes` 方面，GNAT 会证明初始值的依赖关系。然而，如果你为一个包提供了 `Initializes` 方面，它必须是完整的：你必须列出包的每个初始化的状态，以及它所有的外部依赖项。

> 注意：有关 `Initializes` 的详情，请参阅《SPARK 用户指南》第 22 页。

22 https://docs.adore.com/live/wave/spark2014/html/spark2014_ug/en/source/package_contracts.html#package-initialization

84 第 4 章 状态抽象

## 4.10 代码示例 / 陷阱

本节包含了一些代码示例以说明潜在的陷阱。

### 4.10.1 示例 #1

`Communication` 包定义了一个隐藏的本地包 `Ring_Buffer`，其容量在精化（elaboration）期间从外部配置初始化。

> Listing 25: `configuration.ads`

```ada
package Configuration is
  External_Variable : Natural := 1;
end Configuration;
```

> Listing 26: `communication.ads`

```ada
with Configuration;
package Communication with
  Abstract_State => State,
  Initializes => (State => Configuration.External_Variable)
is
  function Get_Capacity return Natural;
private
  package Ring_Buffer with
    Initializes => (Capacity => Configuration.External_Variable)
  is
    Capacity : constant Natural := Configuration.External_Variable;
  end Ring_Buffer;
end Communication;
```

> Listing 27: `communication.adb`

```ada
package body Communication with
  Refined_State => (State => Ring_Buffer.Capacity)
is
  function Get_Capacity return Natural is
  begin
    return Ring_Buffer.Capacity;
  end Get_Capacity;
end Communication;
```

## 证明器输出

第 1/2 阶段：生成全局契约 ...

`communication.ads:2:41`: error: 不能在精化中使用 `"Capacity"`，该组成部分是隐藏的，而不是包 `"Communication"` 的隐藏状态

`gnatprove`: 在生成全局契约期间发生错误

这个例子是不正确的。`Capacity` 声明在 `Communication` 的私有部分。因此，我们应该在它的声明中使用 `Part_Of` 方面链接到 `State`。

### 4.10.2 示例 #2

让我们将状态的 `Part Of` 添加到隐藏本地包 `Ring_Buffer` 中，但这次我们将变量 `Capacity` 隐藏在 `Ring_Buffer` 的私有部分内部。

Listing 28: `configuration.ads`

```ada
package Configuration is
  External_Variable : Natural := 1;
end Configuration;
```

Listing 29: `communication.ads`

```ada
with Configuration;
package Communication with
  Abstract_State => State
is
private
  package Ring_Buffer with
    Abstract_State => (B State with Part Of = State);
    Initializes
  is
    function Get_Capacity return Natural;
  private
    Capacity : constant Natural := External_Variable
      with Part Of = B State;
  end Ring_Buffer;
end Communication;
```

Listing 30: `communication.adb`

```ada
package body Communication with
  Refined_State => (State => Ring_Buffer.B_State)
is
  package body Ring_Buffer with
    Refined_State => (State => Capacity)
  is
    function Get_Capacity return Natural;
  end Ring_Buffer;
end Communication;
```

## 证明器输出

> 第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：数据流和信息流分析

`communication.ads:10:06`: info: 流程依赖关系已证明

这个程序是正确的，GNAT 能够验证它。

### 4.10.3 示例 #3

`Communication` 包定义了两个计数器 `Black_Counter` 和 `Red_Counter`。它为每个计数器提供了初始化程序，并在主程序调用。

Listing 31: `counting.ads`

```ada
package Counting with
  Abstract_State => State
is
  procedure Reset_Black;
  procedure Reset_Red;
end Counting;
```

Listing 32: `counting.adb`

```ada
package body Counting with
  Refined_State => (Black_Counter, Red_Counter)
is
  Black_Counter, Red_Counter : Natural;

  procedure Reset_Black is
  begin
    Black_Counter := 0;
  end Reset_Black;

  procedure Reset_Red is
  begin
    Red_Counter := 0;
  end Reset_Red;
end Counting;
```

Listing 33: `main.adb`

```ada
with Counting; use Counting;
procedure Main is
begin
  Reset_Black;
  Reset_Red;
end Main;
```

## 证明器输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：数据流和信息流分析 ...

### 4.10.4 示例 #4

让我们从 `Counting` 包中移除抽象状态。

> Listing 34: `counting.ads`

```ada
package Counting is
  procedure Reset_Black_Count;
  procedure Reset_Red_Count;
end Counting;
```

> Listing 35: `counting.adb`

```ada
package body Counting is
  Black_Counter, Red_Counter : Natural;

  procedure Reset_Black_Count is
  begin
    Black_Counter := 0;
  end Reset_Black_Count;

  procedure Reset_Red_Count is
  begin
    Red_Counter := 0;
  end Reset_Red_Count;
end Counting;
```

> Listing 36: `main.adb`

```ada
with Counting; use Counting;
procedure Main is
begin
  Reset_Black_Count;
  Reset_Red_Count;
end Main;
```

## 证明器输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：数据流和信息流分析 ...

`counting.adb:2:04`: warning 变量 `"Black_Counter"` 被赋值但未被读取 [`-_gnatwm`]

`counting.adb:2:19`: warning 变量 `"Red_Counter"` 被赋值但未被读取 [`-_gnatwm`]

这个例子是正确的。因为我们没有提供抽象状态，GNAT 以变量而非状态进行证明，并无地证明了数据初始化。

### 4.10.5 示例 #5

让我们为 `Counting` 包恢复抽象状态，但这次提供一个 `Reset_All` 过程，它调用初始化程序 `Reset_Black_Counter` 和 `Reset_Red_Counter`。

# SPARK 简介

（接上页内容）

```ada
procedure Reset_Black_Count with Global => (In Out => State);
procedure Reset_Red_Count with Global => (In Out => State);
procedure Reset_All with Global => (Output => State);
end Counting;
```

Listing 38: `counting.adb`

```ada
package body Counting with
  Refined_State => (State => (Black_Counter, Red_Counter))
Black_Counter, Red_Counter : Natural;

procedure Reset_Black_Count is
begin
  Black_Counter := 0;
end Reset_Black_Count;

procedure Reset_Red_Count is
begin
  Red_Counter := 0;
end Reset_Red_Count;

procedure Reset_All is
begin
  Reset_Black_Count;
  Reset_Red_Count;
end Reset_All;
end Counting;
```

## 示例输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：分析数据和信息流

`counting.ads:4:37`: info: 数据依赖关系已证明

`counting.ads:5:37`: info: 数据依赖关系已证明

`counting.ads:6:14`: info: `"State"` 的组成部分 `"Black Counter"` 初始化证明

proved

`counting.ads:6:14`: info: `"State"` 的组成部分 `"Red_Counter"` 初始化证明

proved

`counting.ads:6:37`: info: 数据依赖关系已证明

这个示例非常清晰。流分析为内部调用计算全局契约的精化版本，并利用这些版本验证 `All` 正确地初始化了 `State`。`Refined_Global` 和 `Global` 注解不是强制性的，可以通过 `GNATprove` 进行计算。

### 4.10.6 示例 #6

让我们考虑抽象栈的另一个版本。

Listing 39: `stack.ads`

```ada
package Stack with
  Abstract_State => The_Stack

pragma Unevaluated_Use_Of_Old (Allow);

type Element is new Integer;
type Element_Array is array (Positive range <>) of Element;
```

（接下页）

# 4.10. 代码示例 / 陷阱

# SPARK 简介

（接上页内容）

```ada
Max : constant Length_Type := 100;
subtype Length_Type is range 0 .. Max;
procedure Push (E : Element) with
Post =>
  not Is_Empty
  (if Is_Full then The_Stack = The_Stack old else Peek = E);

function Peek return Element with Pre => not Is_Empty;
function Full return Boolean;
function Is_Empty return Boolean;
end Stack;
```

Listing 40: `stack.adb`

```ada
package body Stack with
  Refined_State => (Top, Content)
Top : Length_Type := 0;
Content : Element_Array (1 .. Max) := (others => 0);

procedure Push (E : Element) is
begin
  Top := Top + 1;
  Content (Top) := E;
end Push;

function Peek return Element is (Content(Top));
function Full return Boolean is (Top >= Max);
function Is_Empty return Boolean is (Top = 0);
end Stack;
```

## 构建输出

`stack.ads:15:39`: error: 对于 package 或 procedure 名称没有适用的运算符 `=`

`gprbuild`: *** 编译失败

## 证明器输出

第 1/2 阶段：生成全局契约 ...

`stack.ads:15:39`: error: 对于 package 或 procedure 名称没有适用的运算符 `=`

`gnatprove`: 在生成全局契约期间出错

这个示例是不正确的。`Push` 的后置条件中存在一个编译错误：`The_Stack` 是一个状态抽象，而不是变量，因此不能在表达式中使用。

### 4.10.7 示例 #7

在这个抽象栈的版本中，函数 `Get_Stack` 返回栈的副本，我们在 `Push` 的后置条件中调用了它，以指定如果栈已满，则不应修改栈。我们还断言向栈中推入了一个元素：要么栈保持不变（如果它已经满了），要么其顶端元素等于刚刚推入的元素。

90 第 4 章 状态抽象

# SPARK 简介

# Listing 41: `stack.ads`

```ada
package Stack with
  Abstract_State => The_Stack
is
  pragma Unevaluated_Use_Of_Old (Allow);

  type Stack_Model is private;
  type Element is integer;
  type Element_Array is array (range <>) of Element;
  Max : constant Natural := 100;
  subtype Length_Type is Natural 0 .. Max;

  function Peek return Element with Pre => not Is_Empty;
  function Is_Full return Boolean;
  function Is_Empty return Boolean;
  function Get_Stack return Stack_Model;

  procedure Push (E : Element) with
    Post => not Is_Empty
      and (if Full then Get_Stack = Stack_Old else Peek = E);

private
  type Stack_Model is record
    Top : Length_Type := 0;
    Content : Element_Array (1 .. Max) := (others => 0);
  end record;
end Stack;
```

# Listing 42: `stack.adb`



```ada
package body Stack with
  Refined_State => (The_Stack = (Top, Content))
is
  Top : Length_Type := 0;
  Content : Element_Array (1 .. Max) := (others => 0);

  procedure Push (E : Element) is
  begin
    if Top >= Max then
      return;
    end if;
    Top := Top + 1;
    Content (Top) := E;
  end Push;

  function Peek return Element is (Content (Top));
  function Full return Boolean is (Top >= Max);
  function Is_Empty return Boolean is (Top = 0);

  function Get_Stack return Stack_Model is (Top, Content);
end Stack;
```

## Listing 43: `use_stack`

```ada
with Stack;
procedure Use_Stack (E : Element) with
  Post => not Is_Empty and
    (if Full then Get_Stack = Stack_Old else Peek = E);
```

（接下页）

# 4.10. 代码示例 / 陷阱

# SPARK 简介

（接上页内容）

```ada
F : Element := Peek;
begin
  Push (E);
  pragma Assert (Peek = E or Peek = F);
```

## 证明器输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：分析数据和信息流

`use_stack.ads:6:04`：warning: `"F"` 未被修改，可以声明为常量

这个示例非常清晰。流分析为内部调用计算全局契约的精化版本，并利用这些版本验证 All 正确地初始化了 State。`Refined_Global` 和 `Global` 注解不是强制性的，可以通过 `GNATprove` 进行计算。

### 4.10.8 示例 #8

让我们考虑抽象栈的另一个版本。

#### Listing 44: `stack.ads`

```ada
package Stack with
  Abstract_State => The_Stack

pragma Unevaluated_Use_Of_Old (Allow);

type Element is new Integer;
type Element_Array is array (Positive range <>) of Element;
Max : constant Natural := 100;
subtype Length_Type is Natural 0 .. Max;
function Peek return Element with Pre => not Is_Empty;
function Is_Full return Boolean;
function Is_Empty return Boolean;
function Get_Stack return Stack_Model;

procedure Push (E : Element) with
  Post => not Is_Empty and
    (if Full then Get_Stack = Stack_Old else Peek = E);

private

type Stack_Model is record
  Top : Length_Type := 0;
  Content : Element_Array (1 .. Max) := (others => 0);
end record;

end Stack;
```

#### Listing 45: `stack.adb`

```ada
package body Stack with
  Refined_State => (The_Stack = (Top, Content))
is
  Top : Length_Type := 0;
  Content : Element_Array (1 .. Max) := (others => 0);

  procedure Push (E : Element) is
  begin
    if Top >= Max then
      return;
    end if;
    Top := Top + 1;
    Content (Top) := E;
  end Push;

  function Peek return Element is (Content (Top));
  function Full return Boolean is (Top >= Max);
  function Is_Empty return Boolean is (Top = 0);

  function Get_Stack return Stack_Model is (Top, Content);
end Stack;
```

#### Listing 46: `use_stack.adb`

```ada
with Stack; use Stack;

procedure Use_Stack (E : Element) with
  Post => not Is_Empty and
    (if Full then Get_Stack = Stack_Old else Peek = E)
is
  F : Element := Peek;
begin
  Push (E);
  pragma Assert (Peek = E or Peek = F);
end Use_Stack;
```

### 4.10.9 示例 #9

包 `Data` 定义了三个变量 `Data_1`、`Data_2` 和 `Data_3`，它们在 `Data` 包体的具体化（elaboration）阶段通过一个读取文件系统的外部接口进行初始化。

#### Listing 47: `external_interface.ads`

```ada
package External_Interface with
  Abstract_State => File_System;
  Initializes => File_System;

  type Data_Type_1 is Integer;
  type Data_Type_2 is Integer;
  type Data_Type_3 is Integer;

  type Data_Record is record
    Field 1 : Data_Type_1;
    Field 2 : Data_Type_2;
    Field 3 : Data_Type_3;
  end record;
```

#### Listing 48: `data.ads`

```ada
with External_Interface; use External_Interface;

package Data with
  Initializes => (Data_1, Data_2, Data_3)
is
  pragma Elaborate_Body;

  Data_1 : Data_Type_1;
  Data_2 : Data_Type_2;
  Data_3 : Data_Type_3;
end Data;
```

#### Listing 49: `data.adb`

```ada
with External_Interface;
pragma Elaborate_All (External_Interface);

package body Data is
begin
  declare
    Data_Read : Data_Record;
  begin
    Read Data ("file name", Data_Read);
    Data_1 := Data_Read.Field_1;
    Data_2 := Data_Read.Field_2;
    Data_3 := Data_Read.Field_3;
  end;
end Data;
```

## 证明器输出

第 1/2 阶段：生成全局常量 ...

第 2/2 阶段：分析数据和信息流 ...

`data.adb:9:07`；high: `"External_Interface.File_System"` 必须列为 `"Data" Initializes` 的输入（SPARK RM 7.1.5(11)）

`atprove`：未证明的检查被视为错误

此示例是错误的。`Data_1`、`Data_2` 和 `Data_3` 的初始值与 `File_System` 之间的依赖必须列在 `Data` 的 `Initializes` 集中。

### 4.10.10 示例 #10

让我们回顾包 `Data` 的 `Initializes` 契约。

#### Listing 50: `external_interface.ads`

```ada
1 package External_Interface with
2   Abstract_State => File_System;
3   Initializes => File_System;
4 is
5   type Data_Type_1 is new Integer;
6   type Data_Type_2 is new Integer;
7   type Data_Type_3 is new Integer;
8
9   type Data_Record is record
10    Field 1 : Data_Type_1;
11    Field 2 : Data_Type_2;
12    Field 3 : Data_Type_3;
13  end record;
14
15  procedure Read Data (FileName : String; Data : out Data_Record)
16  with Global => File_System;
17 end External_Interface;
```

#### Listing 51: `data_interface.ads`

```ada
1 with External_Interface;
2 package Data is
3   pragma Elaborate_Body;
4
5   Data_1 : Data_Type_1;
6   Data_2 : Data_Type_2;
7   Data_3 : Data_Type_3;
8
9 end Data;
```

#### Listing 52: `data.adb`

```ada
1 with External_Interface;
2 pragma Elaborate_All (External_Interface);
3 package body Data is
4 begin
5 declare
6   Data_Read : Data_Record;
7 begin
8   Read Data ("file name", Data_Read);
9   Data_1 := Data_Read.Field_1;
10  Data_2 := Data_Read.Field_2;
11  Data_3 := Data_Read.Field_3;
```

# 4.10. 代码示例 / 陷阱

```ada
end;
end Data;
```

## 证明器输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：分析数据和信息流 ...

`data.adv:7:07`：info: `"Data_Read"` 的初始化已证明

`external_interface.ads:3:03`：info: 流程依赖已证明

此示例是正确的。由于 `Data` 没有 `Initializes` 属性，`GNATprove` 也会计算在其具体化期间初始化的变量集。

# 第五章 函数正确性证明

本节专门介绍程序的正确性。它介绍了您在验证程序时可能需要的高级证明特性。

## 5.1. 跨越程序完整性

当我们谈论子程序的正确性时，指的是它符合其规范的程度。功能正确性专门指涉及输入和输出的属性，而不是其他属性（如运行时间或内存消耗等）。对于功能正确性，我们通常会指定比系统要求的更强的属性，特别是在非认证背景的语境下，这些属性也可能来自非正式的注释。

例如，如果我们想确保不会引发运行时错误，可以使用契约来证明下所示 `Find` 函数的结果。

#### Listing 1: `show_find.ads`

```ada
package Show_Find is
  type NatArray is array (Positive range <=) of Natural;

  function Find (A : NatArray; E : Natural) return Natural with
    Post => (if all I in A'Range => A (I) /= E
      then Result = 0
      else Result in A'Range and then A (Result) = E);
end Show_Find;
```

#### Listing 2: `show_find.adb`

```ada
package body Show_Find is

  function Find (A : NatArray; E : Natural) return Natural is
  begin
    for I in A'Range loop
      if A (I) = E then
        return I;
      end if;
    end loop;
    return 0;
  end Find;

end Show_Find;
```

# SPARK 简介

（接上页）

```ada
end Find;
```

## 证明器输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：流程分析和证明

`show_find.ads:9:14`：info: 范围已证明

`show_find.ads:6:20`：info: 后条件已证明

这次，`GNATprove` 无法证明此后条件：未证明的检查被视为错误

此示例是错误的。`Data_1`、`Data_2` 和 `Data_3` 的初始值与 `File_System` 之间的依赖必须列在 `Data` 的 `Initializes` 集中。

以契约形式编写规范有许多优势。你可以在测试期间使用它们，这可以提高代码的可维护性。最后，如果代码是 SPARK 代码，你可以使用 `GNATprove` 正式证明这些契约。正式证明的优势在于它验证了所有可能的执行路径，而这通过运行测试用例并不总是可能的。例如，在测试期间，下述 `Find` 子过程的后条件会对调用 `Find` 时的输入集进行动态检查，但仅限于该组输入。

在开发更早的阶段就能发现程序中的差异。如果契约足够精确，你可以将其作为断言依据（oracle）来判断测试的通过或失败。在这种情况下，`GNATprove` 也可以验证子程序的输出。

# SPARK 简介

（接上一页）

`show.find.ads:9:14`：medium: 后置条件可能失败，无法证明 A 中的 `Find'Result`

- 范围（range）

`gnatprove`：未经证明的消息被视为错误

## 运行时输出

在数组索引 # 3 找到 3

然而，如果 `Find` 最终通过了验证，那么该验证将对所有可能的输入检查其后置条件。在开发过程中，你可以尝试更早地进行此类验证，因为它是基于子程序模块化执行的。例如，在上面的代码中，你可以在编写子程序 `Find` 的体之前，正式地验证 `Use_Find`。

## 5.2. 高级合约

用于功能正确性的合约通常比用于程序完整性的合约更复杂，因此它们更经常要求你使用 Ada 2012 标准引入的新型表达式形式。特别是限定表达式（qualified expressions），它们允许你指定对于范围内的所有元素或至少一个元素必须满足的属性，在指定数组属性时非常有用。

随着合约变得越来越复杂，你可能会发现引入新的抽象可以提高合约的可证明性。表达式函数（expression functions）是实现此目的的良好手段，因为你可以在包规范中保留它们的函数体。

最后，某些属性（特别是那些描述为数据不变性而非子数组属性的属性）作为子合约表示时可能很繁琐。类型谓词（type predicates）通常更适合此目的。这里有一个：

#### Listing 8: `show_sort.ads`

```ada
package Show_Sort is
  type Nat_Array is array (Positive range <>) of Natural;

  function Sorted (A : Nat_Array) return Boolean is
    (for I < 'Last A then A (I) <= A (I + 1));
    如果 A 是升序排列的，则返回 True。

  subtype Sorted Nat_Array is Nat_Array with
    Dynamic_Predicate => Is_Sorted (Sorted_Nat_Array);

  类型为 Sorted_Nat_Array 的元素都是排序的。
end Show_Sort;
```

## 证明器输出

Phase 1 of 2: 生成全局合约 ...

Phase 2 of 2: 数据流分析和证明 ...

`show.sort.ads:7:32`：info: 索引检查已证明

`show.sort.ads:7:43`：info: 溢出检查已证明

`show.sort.ads:7:43`：info: 索引检查已证明

`show.sort.ads:14:37`：info: 范围检查已证明

`show.sort.ads:14:37`：info: 谓词检查已证明

# SPARK 简介



我们可以使用子类型 `Sorted_Array`我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。作为变量类型，该变量在整个程序执行过程中保持排序状态。指定数组是排序的需要一个涉及量化器的复杂表达式，因此我们将属性抽象为一种表达式以提高可读性。`Is_Sorted` 的函数体保留在程序的规范中，允许代码的使用者对其含义保持精确的理解（当你必须使用 `Nat_Array` 作为操作数 `Is_Sorted` 的类型时。如果你使用 `Sorted_Array`，当启用排序检查并调用该函数来检查所有 `Sorted_Array` 类型的操作数时，运行时将会导致无限递归）。

## 2.2.1 幽灵代码（Ghost Code）

随着你需要指定的属性变得越来越复杂，你可能会拥有仅因为在规范（合约）中使用才需要的实体。你可能发现，重要的是这些实体不会影响程序的行为，或者它们从生产代码中被完全移除。在概念上，`ghost_code` 通常在 SPARK 中通过 `Ghost` 方面来使用。

你可以使用幽灵代码来标注任何实体，包括变量、子程序和包。如果你将一个实体标记为 `Ghost`，GNATPro 确保它不会影响程序的行为。当程序带有断言进行编译时，幽灵代码会像普通代码一样执行，以便它可以执行使用它的合约。你还可以插入编译器来为幽灵实体生成代码。

考虑过程 `Something`，它对其输入 `X` 调用一个函数，并想要检查 `X` 的初始值和修改值是否以这种复杂的方式相关。

**Listing 9：`show_ghost.ads`**

```ada
package Show_Ghost is
   type T is record
      A, B, C, D, E : Boolean;
   end record;

   function Formula (X : T) return Boolean is
      ((X.A and X.B) or (X.D or X.E));

   function IsCorrect (X, Y : T) return Boolean is
      (Formula (X) = Formula (Y));

   procedure Do_Something (X : in out T);
end Show_Ghost;
```

**Listing 10：`show_ghost.adb`**

```ada
package body Show_Ghost is
   procedure Do_Something (X : in out T) is
      X_Init : constant T := X with Ghost;
   begin
      Do_Complex_Stuff (X);
      pragma Assert (IsCorrect (X_Init, X));
      -- 在断言内部使用 X_Init 是允许的。
   end Do_Something;
end Show_Ghost;
```

## 证明器输出

Phase 1 of 2: 生成全局合约 ...

Phase 2 of 2: 数据流分析和证明 ...

`show_ghost.adb:12:22: info`：断言已证明

`Something` 存储了 `X` 的值。在比较这个编译器时，编译器会将 `X_Init` 的使用标记为非法，但在幽灵代码和普通代码之间更复杂的干扰情况在运行 GNATProve 时会被检测到。

**Listing 11：`show_ghost.ads`**

```ada
package Show_Ghost is
   type T is record
      A, B, C, D, E : Boolean;
   end record;

   function Formula (X : T) return Boolean is
      ((X.A and X.B) or (X.D or X.E));

   function IsCorrect (X, Y : T) return Boolean is
      (Formula (X) = Formula (Y));

   procedure Do_Something (X : in out T);
end Show_Ghost;
```

**Listing 12：`show_ghost.adb`**

```ada
package body Show_Ghost is
   procedure Do_Something (X : in out T) is
      X_Init : constant T := X with Ghost;
   begin
      Do_Complex_Stuff (X);
      pragma Assert (IsCorrect (X_Init, X));
      -- 在断言内部使用 X_Init 是允许的。
   end Do_Something;
end Show_Ghost;
```

**Listing 13：`use_ghost.adb`**

```ada
with Show_Ghost;
use Show_Ghost;

procedure Use_Ghost is
   X : T := (True, True, False, True);
begin
   Do_Something (X);
end Use_Ghost;
```

## 5.2 功能正确性的证明

## 构建输出

`show_ghost.adb:14:12: error`

`build: *** 编译失败`

## 证明器输出

Phase 1 of 2: 生成全局合约 ...

`show_ghost.adb:14:12: error`：ghost 实体不能出现在此处

`gnatprove`：生成全局合约时出错

### 5.2.2 幽灵函数

在编写功能正确性合约时，仅用于规范的函数是常见现象。例如，用于简化或提取合约中常见模式的表达式函数通常可以标记为 ghost。

但幽灵函数的作用不仅仅是提高可读性。在真实世界的程序中，通常功能规范所需的某些信息由于抽象的原因在包规范中是无法访问的。

将这些信息提供给包的用户通常是不可能的，因为这破坏了抽象。幽灵函数在这方面非常方便，因为它们提供了一种访问这些信息的方法，而不会让普通代码可见。

让我们看这个例子。

**Listing 14：`stacks.ads`**

```ada
package Stacks is
   pragma Unevaluated_Use_Of_Old (Allow);

   type Stack is private;
   type Element is new Natural;
   type Element_Array is array (Positive range <>) of Element;
   Max : constant Natural := 100;

   function Get_Model (S : Stack) return Element_Array with Ghost;
   -- 返回栈模型的数组。

   procedure Push (S : in Stack; E : Element) with
      Pre  => Get_Model (S)'Length < Max,
      Post => Get_Model (S) = Get_Model (S)'Old & E;

private
   subtype Length_Type is Natural range 0 .. Max;

   type Stack is record
      Top     : Length_Type := 0;
      Content : Element_Array (1 .. Max) := (others => 0);
   end record;
end Stacks;
```

**Listing 15：`stacks.ads`**

```ada
package Stacks is
   pragma Unevaluated_Use_Of_Old (Allow);

   type Stack is private;
   type Element is new Natural;
   type Element_Array is array (Positive range <>) of Element;
   Max : constant Integer := 100;

   function Get_Model (S : Stack) return Element_Array with Ghost;
   -- 返回一个作为栈模型的数组。

   procedure Push (S : in Stack; E : Element) with
      Pre  => Get_Model (S)'Length < Max,
      Post => Get_Model (S) = Get_Model (S)'Old & E;

   function Peek (S : Stack; I : Positive) return Element is
     (Get_Model (S)); -- 错误

private
   subtype Length_Type is Natural range 0 .. Max;

   type Stack is record
      Top     : Length_Type := 0;
      Content : Element_Array (1 .. Max) := (others => 0);
   end record;
end Stacks;
```

我们看到，将函数标记为 `Ghost` 实现了这一目标：它确保了子程序 `Get_Model` 永远不会在生产代码中使用。

104 第 5 章 功能性正确性证明

## 5.2.3 全局幽灵变量

虽然发生频率较低，但你可能会遇到某些规范，要求你在幽灵变量（ghost variables）中存储普通代码中不需要的额外信息。你应当将这些全局变量标记为 `ghost`，允许编译器在启用断言时将它们移除。你可以在构建规范的契约中的任何地方使用这些变量。一种常见的场景是为修改复杂或私有全局数据结构的子程序编写规范：你可以使用这些变量为结构提供模型，当程序执行数据结构操作时，由幽灵代码对结构进行更新。

你还可以使用幽灵变量来存储关于指定的子程序之前运行情况的信息。在这个示例中，我们有两个过程；一个访问状态 A，另一个访问状态 B。使用幽灵变量 `Last_Accessed_Is_A` 来指定在中间没有访问 A 的情况下，不能连续访问 B。

**列表 16：`call_sequence.ads`**

```ada
package Call_Sequence is
   type T is new Integer;

   Last_Accessed_Is_A : Boolean := False with Ghost;

   procedure Access_A with
      Post => Last_Accessed_Is_A;

   procedure Access_B with
      Pre => not Last_Accessed_Is_A;
   -- B 只能在 A 之后被访问
end Call_Sequence;
```

**列表 17：`call_sequence.adb`**

```ada
package body Call_Sequence is
   procedure Access_A is
   begin
      Last_Accessed_Is_A := True;
   end Access_A;

   procedure Access_B is
   begin
      Last_Accessed_Is_A := False;
   end Access_B;
end Call_Sequence;
```

**列表 18：`main.adb`**

```ada
with Call_Sequence;
use Call_Sequence;

procedure Main is
begin
   Access_A;
   Access_B;
   Access_B; -- 错误
end Main;
```

## 5.2. 进阶契约

## 证明器输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：流分析与证明 ...

`main.adb:7:04: medium`：前置条件可能失败，无法证明 `Last_Accessed_Is_A`

`gnatprove`：将未证明的检查信息视为错误

## 运行时输出

```text
raised Ada.ASSERTIONS.ASSERTION_ERROR : 来自 call_sequence 的前置条件失败
ads:11
```

让我们来看另一个示例。子程序预期行为的规范有时最好表示为它必须执行的动作序列。你可以使用幽灵变量来存储变量的中间值，以便更方便地编写此类规范。

例如，我们分两个步骤指定程序 `Do_Things`，使用幽灵变量 `V_Inter` 来存储这些步骤之间变量 `V` 的中间值。我们也可以使用对 `V_Inter` 现有的量化来表达，但迭代所有迭代是不现实的，而且这在 SPARK 中无法验证，因为量化被限制在 `for` 循环模式。

最后，提供变量的值可能有助于证明器验证契约。

**列表 19：`action_sequence.ads`**

```ada
package Action_Sequence is
   type T is new Integer;

   V_Inter : T with Ghost;

   function First_Thing_Done (X, Y : T) return Boolean with Ghost;
   function Second_Thing_Done (X, Y : T) return Boolean with Ghost;

   procedure Do_Things (V : out T) with
      Post => First_Thing_Done (V);
end Action_Sequence;
```

## 证明器输出

第 1/2 阶段：生成全局契约 ...

第 2/2 阶段：流分析与证明 ...

注意：关于 ghost 代码的更多细节，请参阅 SPARK 用户指南。

106 第 5 章 功能性正确性证明

# SPARK 简介

## 5.3 证明指南

由于感兴趣的属性比证明涉及的属性更复杂，我们预计 `GNATprove` 最初无法验证它们，尽管它们是有效的。你会发现我们在 54 页讨论的调试失败尝试大有帮助。为了这个目的，你可以通过添加断言将复杂的证明分解为更易理解的步骤。

```ada
pragma Assert (Assertion_Checked_By_Tool);
-- info: 断言已证明
```

```ada
pragma Assert (Assertion_Validated_By_Means);
-- medium: 断言可能失败
```

```ada
pragma Assume (Assumption_Validated_By_Means);
-- 工具不尝试检查此表达式。
-- 它被记录为一个假设。
```

一个中间步骤对于证明理论等效的版本可能非常有用，但你通过拆分不同情况或内联定义简化了问题。

某些中间断言可能无法被 `GNATprove` 证明，因为缺少信息或信息量令人混乱。你可以通过其他手段验证这些断言，例如测试（因为它们是可执行的）或审查。你也可以选择指示 `GNATprove` 证明它们，或者将其转换为断言（如示例所示），或者使用 `pragma Assert`。在两种情况下，编译器会在启用断言时生成检查这些断言的代码。

### 5.3.1 本地幽灵变量

你可以像上面增强规范契约那样，使用幽灵代码来增强你可以表达的中间断言。特别是，你通常会有局部变量或常量，其唯一目的是存储你想在断言中引用的变量或表达式的值。对于引用参数和表达式特别有用。

在下面的示例中，我们想要帮助验证 `P` 的后置条件。我们通过引入本地幽灵变量 `X_Int` 来表示该值，并在两个分支中编写断言，重复后置条件，但使用了 `X_Int`。

> 列表 20：`show_local_ghost.adsc`

```ada
package Show_Local_Ghost is

   type T is Natural;

   function F (X, Y : T) return Boolean is (X > Y) with Ghost;
   function Condition (X : T) return Boolean is (X mod 2 = 0);

   procedure P (X : in T) with
      Pre  => X < 1_000_000,
      Post => F (X, X'Old);

end Show_Local_Ghost;
```

**Listing 21：`show_local_ghost.adb`**



```ada
package body Show_Local_Ghost is
  procedure P (X : in T) is
    X Init : constant T := X with Ghost
  begin
    if Condition (X) then
      X := X + 1;
      pragma Assert (F (X, Init));
    else
      X := X * 2;
    end if;
  end P;
Show_Local_Ghost;
```

# 证明器输出

```text
Phase 1 of 2: generation analysis and proof ...
Phase 2 of 2: flow analysis and proof ...
show_local_ghost.adb:7:17: info: overflow check proved
show_local_ghost.adb:8:25: info: overflow check proved
show_local_ghost.adb:10:17: info: assertion proved
show_local_ghost.adb:11:25: info: assertion proved
show_local_ghost.ads:7:52: info: division check proved
show_local_ghost.adb:10:23: info: precondition proved
```

你也可以使用局部变量来处理更复杂的属性，例如作为子组复杂属性见证的数据结构。在我们的示例中，我们想要证明 `Sort` 过程没有创建新元素，也就是说，`Sort` 之后 A 中存在的所有元素都是原始排序的排列。这个属性不足以确保调用 `Sort` 产生的 A 值是调用前值的排列（或这些值是排过序的）。对于一个属性来说，验证它已经很复杂了，因为它涉及了量词嵌套。为了获得 GNATP，你可能会发现为每个索引 `I` 搜索一个满足条件的索引 `J`：

```ada
procedure Sort (A : in nat Array) with
  Post => (for all I in A'Range => A (I) = A'Old (J))
is
  Permutation : Index Array := (1 => 1, 2 => 2, ...) with Ghost;
begin
  ...
end Sort;
```

108 第 5 章 功能正确性证明

## 5.3.2 幽灵过程（Ghost Procedures）

幽灵过程影响普通变量的值，因此它们主要用于对幽灵变量进行操作，或者将一组中间断言组合在一起。

在幽灵过程内部抽象断言和幽灵变量的处理有几个优势。首先，你可以在幽灵过程内部的代码中使用你选择的任何方式使用这些变量。在幽灵过程之外就不一样，那里只允许的幽灵语句是幽灵变量和对幽灵过程的调用。

例如，`Increase_A` 中包含的 for 循环不能单独出现在普通代码中。

**List 22: show_ghost_Proc.ads**

```ada
package Show_Ghost_Proc is
  type Nat_Array is array (Integer range) of Natural;
  A : Nat_Array (1 .. 100) with Ghost;
  procedure Increase_A with
    Ghost;
    Pre := (for all I in A'Range => A (I) < Natural'Last);
  end Show_Ghost_Proc;
```

**List 23: show_ghost_proc.adb**

```ada
package Show_Ghost_Proc is
  procedure Increase_A is
  begin
    for I in A'Range loop
      A (I) := A (I) + 1;
    end loop;
  end Increase_A;
end Show_Ghost_Proc;
```

# 证明输出

```text
Phase 1 of 2: generation of contracts

Phase 2 of 2: flow analysis and proof ...

show_ghost_proc.adb:6:25: info: overflow checked
```

使用抽象来隐藏不是子程序功能行为部分的复杂代码以提高可读性，可以帮助 GNAT 通过抽象化本会使其工作变得复杂的断言来完成证明。在下文所示的示例中，使用 `X` 作为操作数调用 `Prove_P` 仅将 `P (X)` 添加到后置上下文中，而不是为了验证它所需的更大的断言集。此外，`P` 的后置条件只需要执行一次，而无需在其上下文中包含不必要的信息。此外，除非它们在较小的上下文中，否则 GNAT 无法完全验证 `Prove_P`。

```ada
procedure Prove_P (X : T) with
  Ghost,
  Global => null,
  Post => P (X);
```

## 5.3.3 处理循环

当程序涉及循环时，你总是需要提供额外的注解以允许 GNATprove 完成证明，因为 GNATprove 使用的验证技术不处理子程序控制流中的环路。相反，循环通过将它们划分为若干个无环部分来“扁平化”。例如，让我们来看一个带有退出条件的简单循环。

```ada
Stmt1;
loop
  Stmt2;
  exit when Cond;
  Stmt3;
end loop;
Stmt4;
```

如下所示，控制流被分为三部分。第一部分（黄色）在子程序中较早开始并进入循环语句。循环本身被分为两部分。红色代表循环体的完整执行：即退出条件不满足的执行。蓝色代表循环的最后一次执行，包含了后续的子程序。对于该路径，假设退出条件成立。红色部分和蓝色部分在黄色部分之后执行。

GNATprove 独立地分析这些部分，因为它不跟踪变量在循环中是如何更新的。在进入循环的另一个迭代时，它会忘记这些变量。换句话说，处理循环的方式使得 GNATprove 无法验证涉及循环的属性：它无法从循环中推出关于常量或未修改变量的新信息。例如，考虑 `Find` 函数，它返回 A 并在 A 中搜索元素 E。

**Listing 24: show_find.ads**

```ada
package Show_Find is
  type Nat_Array is array (Positive range) of Natural;
  function Find (A : Nat_Array; E : Natural) return Natural;
end Show_Find;
```

**Listing 25: show_find.adb**

```ada
package Show_Find is
  function Find (A : Nat_Array; E : Natural) return Natural is
  begin
    for I in A'Range loop
      pragma (all J in A'First .. I - 1 => A (J) /= E);
      assertion is not proved
      if (I) = E then
        return I;
      end if;
      pragma Assert (A (I) /= E);
      assertion is proved
    end loop;
    return 0;
  end Find;
end Show_Find;
```

# 证明器输出

```text
Phase 1 of 2: generation of Global contracts

Phase 2 of 2: flow analysis and proof ...

show_find.adb:6:51: info: overflow checked proved

show.find.adb:6:58: medium: assertion might fail, cannot prove A (J) /= E

[possible fix: subprogram at show.find.adb:5 should mention A and E in a precondition]

show.find.adb:6:61: info: index checked proved

show.find.adb:9:20: info: range checked proved

show.find.adb:11:25: info: assertion proved

gnatprove: prove check messages considered as errors
```

在每次迭代结束时，GNATprove 知道存储在 `I` 中的值不等于 `E`（否则循环就不会结束）。这证明了第二个断言。但它无法在多次循环迭代中聚合这些信息以推导出对所有索引都成立，因此无法证明第一个断言。

## 5.3.4 循环不变式（Loop Invariants）

为了克服这些局限性，你可以通过循环不变式的形式向 GNATprove 提供额外信息。在 SPARK 中，循环不变式是在循环的每次迭代中都成立的布尔表达式。和其他断言一样，你可以在通过带有断言编译程序时在运行时检查它。

循环不变式与其他断言的主要区别在于它被用于证明。GNATprove 分两个步骤执行循环不变式的证明：首先，它检查其在循环的第一次迭代中是否成立，然后检查在假设上一次迭代中成立的情况下，在任意迭代中是否成立。这被称为归纳法。

24 https://en.wikipedia.org/wiki/Mathematical_induction

# SPARK 简介

（接上页）

```ada
function Find (A : Nat_Array; E : Natural) return Natural;
end Show_Find;
```

**Listing 27: show_find.adb**

```ada
package body Show_Find is
  function Find (A : Nat_Array; E : Natural) return Natural is
  begin
    for I in A'Range loop
      pragma Invariant (A ('First) /= E);
      loop invariant not proved in first iteration
      but preservation of loop invariant proved
      if A (I) = E then
        return I;
      end if;
    end loop;
    return I;
  end;
end Show_Find;
```

# 证明器输出

```text
第 1/2 阶段：生成全局合约 ...

第 2/2 阶段：流分析与证明 ...

show.find.adb:63: info: loop invariant preservation proved

show.find.adb:63: medium: loop invariant might fail in first iteration [possible,

fix: program at show find should mention A and E in a precondition]

show.find.adb:67: info: index check proved

show.find.adb:10:20: info: range check proved

gnatprove: unproved check messages considered errors
```

为了验证此不变性，GNATProve 生成了两个检查。第一个检查确保断言在循环的第一次迭代中成立。这并没有通过 GNATProve 验证。而且，确实没有理由在这次迭代中检查 A 的第一个元素是否不等于 E。然而，第二个检查被证明了；很容易推断出，如果在给定的迭代中 A 的元素不是 E，那么在当前迭代中它也不可能是 E。但是，我们将不变性移动到循环的末尾，它就能被 GNATProve 成功验证。

GNATProve 不仅允许你使用不变性来验证循环的复杂属性，还利用它们来验证其他属性，例如循环体以及循环后续语句中不存在运行时错误。更准确地说，验证运行时检查或其他断言可以确保该检查或断言之前的循环不变性是真成立的。

让我们来看一个 `Find` 的示例，在该示例中，我们使用循环不变性而非断言来表示所看到的数组元素都不等于 E。

**Listing 28: show_find.adb**

```ada
package Show_Find is
  type Nat_Array is array (Positive range <>) of Natural;
  function Find (A : Nat_Array; E : Natural) return Natural;
end Show_Find;
```

第 5 章.功能正确性证明

# Listing 29: show_find.adb

```ada
package body Show_Find is
  function Find (A : Nat_Array; E : Natural) return Natural is
  begin
    for I in A'Range loop
      pragma Loop Invariant
        (for all J in A'First .. I - 1 => A (J) /= E);
      if A (I) = E then
        return I;
      end;
    end loop;
    pragma Assert (for all I in A'Range => A (I) /= E);
    return 0;
  end Find;
end Show_Find;
```

第 1/2 阶段：生成全局合约 ...

第 2/2 阶段：流分析与证明 ...

```text
show_find.adb:73: info: loop invariant initialization proved

show.find.adb:73: info: loop invariant preservation proved

show.find.adb:39: info: overflow check proved

show.find.adb:49: info: index check proved

show.find.adb:90: info: range check proved

show.find.adb:12:25: info: insertion proved

show.find.adb:12:49: info: index check proved
```

这被 GNAT 完全验证了！这证明了循环不变性在循环的每次迭代中都成立（区分第一次迭代和后续迭代）。它还证明了在循环退出后 A 的元素都不等于 E，这是通过断言不变性在最后一次迭代中实现的。

> 注意：关于不变性的更多细节，请参阅 SPAR 用户手册。

寻找良好的循环不变性可能是一项挑战。为了使这变得更容易，让我们回顾一下良好的循环不变性的四个良好属性：

| 属性 | 描述 |
|---|---|
| INIT | 它应该在循环的第一次迭代中被证明。 |
| INSIDE | 它允许循环内部不存在运行时错误和局部断言。 |
| AFTER | 它允许循环结束后不存在运行时错误、局部断言和子程序后条件。 |
| PRESERVE | 它应该在循环的第一次迭代之后被证明。 |

让我们来看每一个属性。第一个循环不变性应该在循环的第一次迭代中被证明（INIT）。如果你的不变性未能实现这一目标，你可以调试不变性的初始化。

# 5.3 证明指南

# SPARK 简介

其次，循环不变性应该足够精确，以概述循环体（INSIDE）和循环后续语句（AFTER）不存在运行时错误。为了做到这一点，你应该在不变性中包含整个循环过程中修改的变量。

最后，循环不变性应该足够精确，以便在第一次迭代之后被证明（PRESERVE）。这通常是最棘手的部分。为了理解为什么 GNATprove 无法证明不变性的保持，你可能会发现这些内容很有帮助。

## SPARK 简介（接上上一页）

```text
show_map.adb:8:18: info: overflow check proved
show_map.adb:8:18: info: index check proved
show_map.adb:11:13: info: loop invariant proved
show_map.adb:12:36: medium: loop invariant might not be preserved by an arbitrary,
iteration, cannot prove L 13 is (A 'Loop_Entry (J))
show_map.adb:12:41: info: overflow check proved
show_map.adb:12:41: info: index check proved
show_map.adb:12:65: info: index check proved
show_map.adb:16:22: info: assertion proved
show_map.adb:17:50: info: overflow check proved
show_map.adb:17:50: info: index check proved
show_map.adb:17:65: info: index check proved
show_map.ads:6:35: info: overflow check proved
gnatprove: unproved check messages considered as errors
```



你需要取消注释包含帧条件（frame condition）的第二个循环不变式，以证明循环后的断言。

**注意：**关于如何编写循环不变式的更多信息，请参阅《SPARK 用户指南》第 26 页。

## 5.4 代码示例 / 陷阱

本节包含代码示例和陷阱。

### 5.4.1 示例 #1

我们在数组 `Content` 内部实现了一个环形缓冲区，其中长度为 `Length` 的环形缓冲区的内容从索引 `First` 开始，并可能绕过缓冲区末尾。我们使用 ghost 函数 `Get_Model` 返回环形缓冲区的内容，用于合约。

> 列表 34：`ring_buffer.ads`

```ada
package Ring_Buffer is
  Max_Size : constant := 100;
  type Nat_Array is array (Positive range <>) of Natural;

  function Get_Model return Nat_Array with Ghost;

  procedure Push (E : Natural) with
    Pre  = Get_Model'Length < Max_Size;
    Post = Get_Model'Length = Get_Model'Old'Length + 1;
end Ring_Buffer;
```

> 列表 35：`ring_buffer.adb`

```ada
package body Ring_Buffer is
  subtype Length_Range is Natural range 0 .. Max_Size;
```

26 https://docs.adore.com/live/wave/spark2014/html/spark2014_ug/en/source/how_to_write_loop_invariants/html

116 第 5 章 性正确性证明

## SPARK 简介（接上上一页）

```ada
subtype Index_Range is Natural range 1 .. Max_Size;
Content : Nat_Array (1 .. Max_Size) := (others => 0);
First : Index_Range := 1;
Length : Index_Range := 0;

function Get_Model return Nat_Array with
  Refined Post => Get_Model'Result'Length = Length
is
  Size : constant Length_Range := Length;
  Result : Nat_Array (1 .. Size) := (others => 0);
begin
  if First + Length <= Max_Size then
    Content := Content (First + Length - 1);
  else
    declare
      Len : constant Length_Range := Max_Size - First + 1;
    begin
      Result (1 .. Len) := Content (First .. Max_Size);
      Result (Len + 1 .. Length) := Content (1 .. Length - Len);
    end;
  end if;
  return Result;
end procedure Push_Last (E : Natural) is
begin
  if First + Length <= Max_Size then
    Content (First + Length) := E;
  else
    Content (Length - Max_Size + First) := E;
  end if;
  Length := Length + 1;
end procedure Push_Last;
```

## 环形缓冲区

第 1/2：生成全局合约……

第 2/2：流分析和证明……

`ring_buffer:7:084: warning: "First" is not modified, could be declared constant, ...`

```text
ring_buffer.adb:11:22: info: refined post proved
ring_buffer.adb:11:38: info: range check proved
ring_buffer.adb:14:07: info: range check proved
ring_buffer.adb:14:41: info: length check proved
ring_buffer.adb:17:17: info: length check proved
ring_buffer.adb:17:20: info: range check proved
ring_buffer.adb:20:61: info: range check proved
ring_buffer.adb:22:13: info: range check proved
ring_buffer.adb:22:31: info: length check proved
ring_buffer.adb:22:34: info: range check proved
ring_buffer.adb:23:13: info: length check proved
ring_buffer.adb:23:40: info: length check proved
ring_buffer.adb:23:43: info: range check proved
ring_buffer.adb:23:45: info: range check proved
ring_buffer.adb:32:25: info: index check proved
ring_buffer.adb:34:37: info: index check proved
```

（接下一页）

## 5.4 代码示例 / 陷阱

17

## SPARK 简介（接上上一页）

`ring_buffer.adb:36:24: info: range check proved`

`ring_buffer.ads:1:24: info: postcondition proved`

这是正确的：`Get_Model` 仅用于合约。调用 `Get_Model` 会产生内容的副本，这并不高效，但由于 `Get_Model` 仅用于验证，我们通过使用 ghost 函数来强制这一点。我们将产生忽略断言的最终生产代码。

### 5.4.2 示例 #2

与其使用 ghost 函数 `Get_Model` 获取环形缓冲区的内容，我们现在使用全局变量 `Model`。

> 列表 36：`ring_buffer.ads`

```ada
package Ring_Buffer is
  Max_Size : constant := 100;
  subtype Length_Range is Natural range 0 .. Max_Size;
  subtype Index_Range is Natural range 1 .. Max_Size;

  type Nat_Array is (Positive range <>) of Natural;

  type Model_Type is (Length : Length_Range := 0) is
    Content : Nat_Array (1 .. Length);
  end record;

  Model : Model_Type with Ghost;

  function Valid Model return Boolean;

  procedure Push_Last (E : Natural) with
    Pre  => Valid Model;
    Post => Model.Length < Max_Size;
    Post => Model.Length = Model.Length'Old + 1;
end Ring_Buffer;
```

> 列表 37：`ring_buffer.adb`

```ada
package body Ring_Buffer is
  Content : Nat_Array (1 .. Max_Size) := (others => 0);
  First : Index_Range := 1;
  Length : Length_Range := 0;

  function Valid Model return Boolean is
    (Model.Content = Length);

  procedure Push_Last (E : Natural) is
  begin
    if First + Length <= Max_Size then
      Content (First + Length) := E;
    else
      Content (Length - Max_Size + First) := E;
    end if;
```

（接下一页）

118

第 5 章 性正确性证明

## SPARK 简介（接上上一页）

```ada
Length := Length + 1;
end Push_Last;
end Ring_Buffer;
```

## 构建输出

`ring_buffer.adb:8:08: error: ghost entity cannot appear in context`

## 证明输出

第 1/2：生成全局合约

`ring_buffer.adb:8:08: error: ghost entity cannot appear in context`

这个示例是正确的。只要 ghost 变量 `Model` 只用于 ghost 语句，就可以在 ghost 函数 `Valid` 和非 ghost 过程 `Push_Last` 中引用。

### 5.4.3 示例 #3

我们现在修改 `Push_Last`，在运算符和 ghost 代码之间共享新长度的计算。

> 列表 38：`ring_buffer.ads`

```ada
package Ring_Buffer is
  Max_Size : constant := 100;
  subtype Length_Range is Natural range 0 .. Max_Size;
  subtype Index_Range is Natural range 1 .. Max_Size;

  type Nat_Array is (Positive range <>) of Natural;

  type Model_Type is (Length : Length_Range := 0) is
    Content : Nat_Array (1 .. Length);
  end record;

  Model : Model_Type with Ghost;

  function Valid Model return Boolean;

  procedure Push_Last (E : Natural) with
    Pre  => Valid Model;
    Post => Model.Length < Max_Size;
    Post => Model.Length = Model.Length'Old + 1;
end Ring_Buffer;
```

> 列表 39：`ring_buffer.adb`

```ada
package body Ring_Buffer is
  Content : Nat_Array (1 .. Max_Size) := (others => 0);
  First : Index_Range := 1;
  Length : Length_Range := 0;
```

（接下一页）

119

## SPARK 简介（接上上一页）

```ada
function Valid Model return Boolean is
  (Model.Content = Length);

procedure Push_Last (E : Natural) is
begin
  if First + Length <= Max_Size then
    Content (First + Length) := E;
  else
    Content (Length - Max_Size + First) := E;
  end if;

  Length := Length + 1;
  Model := (Length => Length + 1,
            Content => Model.Content + E);
end Push_Last;

end Ring_Buffer;
```

## 分析器输出

第 1/2：生成全局合约

第 2/2：流分析和证明……

`gnatw`

`ring_buffer.ads:3:04: warning "Content" is assigned but never read`

`gnatw`

`ring_buffer.ads:4:04: warning "First" is not modified, could be declared constant ...`

`gnatw`

`ring_buffer.ads:8:21: info: range check proved`

`ring_buffer.ads:13:25: info: index check proved`

`ring_buffer.ads:15:37: info: index check proved`

`ring_buffer.ads:17:24: info: range check proved`

`ring_buffer.ads:18:13: info: dclariant checked proved`

`ring_buffer.ads:18:41: info: range check proved`

`ring_buffer.ads:19:42: info: range check proved`

`ring_buffer.ads:19:42: info: length check proved`

`ring_buffer.ads:20:07: info: range check proved`

`ring_buffer.ads:21:14: info: postcondition proved`

### 5.4.4 示例 #4

我们现在修改 `Push_Last`，在运算符和 ghost 代码之间共享新长度的计算。

> 列表 40：`ring_buffer.ads`

```ada
package Ring_Buffer is
  Max_Size : constant := 100;
  subtype Length_Range is Natural range 0 .. Max_Size;
  subtype Index_Range is Natural range 1 .. Max_Size;
  type Nat_Array is array (Positive range <=) of Natural;

  type Model_Type is array (Length : Length_Range := 0) is
    Content : Nat_Array (1 .. Length);
  end
  with Ghost;
```

## SPARK 简介

```ada
Model : Model_Type with Ghost;

function Valid Model return Boolean with Ghost;

procedure PushLast (E : Natural) with
  Pre => Valid Model
    and then Model.Length < Max_Size;
  Post => Model.Length = Model.Length'Old + 1;
```

（接上页）

```ada
end Ring_Buffer;
```

> 列表 41：`ring_buffer.adb`

```ada
package body Ring_Buffer is
  Content : Nat_Array (1 .. Max_Size) := (others => 0);
  First : Index_Range := 1;
  Length : Length_Range := 0;

  function Valid Model return Boolean is
    (Model.Content_Length = Length);

  procedure PushLast (E : Natural) is
    New_Length : constant Length_Range := Model.Length + 1;
  begin
    if First + Length <= Max_Size then
      Content (First + Length) := E;
    else
      Length := New_Length;
      Model := (Length => New_Length,
                Content => Model.Content & E);
    end if;
  end Push_Last;

end Ring_Buffer;
```

## 构建输出

```text
ring_buffer.adb:11:45: error: ghost entity cannot appear in this context
gprbuild: *** compilation phase failed
```

## 证明器输出

`Phase 1 of 2: generation of Global contracts...`



`ring_buffer.adb:11:45: error: ghost entity cannot appear in context`

`gnatprove: error during generation of Global contracts`

这个例子是不正确的。我们没有将`New`设为 Ghost，因此无法从`Model`的值计算出来。如果我们把`New`设置为 ghost，编译器会在赋值给`New_Length`时报告问题。正确的解决方案是从非 ghost 变量`Length`的值计算`New_Length`。

# 5.4. 代码示例 / 陷阱

## SPARK 简介

### 5.4.5 示例 #5

我们将更新`Model`的移动到一个 ghost 过程`Update_Model`中，但仍然使用局部变量`New_Length`来计算长度。

Listing 42: ring_buffer is

```ada
package Ring_Buffer is
  Max_Size : constant := 100;
  subtype Length_Range is Natural 0 .. Max_Size;
  subtype Index_Range is Natural 1 .. Max_Size;
  type Nat_Array is array (Positive range) of Natural;
  type Model_Type is (Length : Length_Range := 0) is record
    Content : Nat Array (1 .. Length);
  end record with Ghost;
  Model : Model_Type with Ghost;
  function Valid_Model return Boolean with Ghost;
  procedure PushLast(E : Natural) with
    Pre => Valid_Model
    and then Model.Length < Max_Size;
    Post => Model.Length = Model.Length'Old + 1;
end Ring_Buffer;
```

Listing 43: ring_buffer.adb

```ada
package body Ring_Buffer is
  Content : Nat Array (1 .. Max_Size) := (others => 0);
  First : Index_Range := 1;
  Length : Length_Range := 0;

  function Valid_Model return Boolean is
    (Model.Content_Length = Length);

  procedure PushLast(E : Natural) is
    procedure Update_Model with Ghost is
      New_Length : constant Length_Range := Model.Length + 1;
    begin
      Model := (Length => New_Length,
                Content => Model.Content & E);
    end Update_Model;
  begin
    if First + Length <= Max_Size then
      Content (First + Length) := E;
    else
      Content (Length - Max_Size + First) := E;
    end if;
    Length := Length + 1;
    Update_Model;
  end Push_Last;
end Ring_Buffer;
```

## 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: flow analysis and proof ...

ring_buffer.adb:3:04: warning: variable "Content" is assigned but never read [-gnatw]

ring_buffer.adb:4:04: warning: variable "First" is not modified, could be declared constant [-gnatw]

ring_buffer.adb:8:21: info: range check proved

ring_buffer.adb:13:61: info: range check proved, inlined in ring_buffer.adb:26

ring_buffer.adb:15:16: info: range check proved, inlined in ring_buffer.adb:26

ring_buffer.adb:16:45: info: range check proved, inlined in ring_buffer.adb:26

ring_buffer.adb:21:25: info: index check proved

ring_buffer.adb:23:37: info: index check proved

ring_buffer.adb:25:24: info: range check proved

ring_buffer.adb:10:07: info: range check proved

ring_buffer.adb:21:14: info: postcondition proved
```

这里一切正常。`Model`只在`Update`内部访问，而`Update`本身是一个 ghost 过程，所以声明局部变量`New`是可以。如果没有 Ghost 属性：期望 ghost 过程体是 ghost。此外，我们不需要为`Update_Model`添加任何契约：它被 GNATprove 内联了。

### 5.4.6 示例 #6

`Max`函数接收两个长度相同的数组（但不一定边界相同），并返回一个每个元素均为两个参数最大值的数组。

Listing 44: array_util.ads

```ada
package Array_Util is
  type Nat_Array is array (Positive range) of Natural;

  function Max (A, B: Nat_Array) return Nat_Array with
    Pre => A'Length = B'Length;

end Array_Util;
```

Listing 45: array_util.adb

```ada
package body Array_Util is
  function Max (A, B: Nat_Array) return Nat_Array with
    R: Nat_Array (A'Range);
    J: Integer := B'First;
  begin
    for I in A'Range loop
      if A (I) = B (J) then
        R (I) := A (I);
      else
        R (I) := B (J);
      end if;
      J := J + 1;
    end loop;
  end Max;
end Array_Util;
```

## 5.4. 代码示例 & 陷阱

## SPARK 简介

（接上页）

```ada
  end loop;
  return R;
end Max;
```

## 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: flow analysis and proof ...

ring_buffer.adb:3:04: warning: variable "Content" is assigned but never read [-gnatw]

ring_buffer.adb:4:04: warning: variable "First" is not modified, could be declared constant [-gnatw]

ring_buffer.adb:8:21: info: range check proved

ring_buffer.adb:13:61: info: range check proved, inlined in ring_buffer.adb:26

ring_buffer.adb:15:16: info: range check proved, inlined in ring_buffer.adb:26

ring_buffer.adb:16:45: info: range check proved, inlined in ring_buffer.adb:26

ring_buffer.adb:21:25: info: index check proved

ring_buffer.adb:23:37: info: index check proved

ring_buffer.adb:25:24: info: range check proved

ring_buffer.adb:10:07: info: range check proved

ring_buffer.adb:21:14: info: postcondition proved
```

这里一切正常。`Model`只在`Update`内部访问，`Update`本身是一个 ghost 过程，所以声明局部变量`New`是可以。如果没有 Ghost 属性：期望 ghost 过程体是 ghost。此外，我们不需要为`Update_Model`添加任何契约：它被 GNATprove 内联了。

### 5.4.7 示例 #7

添加一个循环不变式，说明`J`在`B`的范围内。

Listing 46: array_util.ads

```ada
package Array_Util is
  type Nat_Array is array (Positive range) of Natural;
  function Max (A, B: Nat_Array) return Nat_Array with
    Pre => A'Length = B'Length;

end Array_Util;
```

Listing 47: array_util.adb

```ada
package body Array_Util is
  function Max (A, B: Nat_Array) return Nat_Array with
    R: Nat_Array (A'Range);
    J: Integer := B'First;
  begin
    for I in A'Range loop
      if A (I) = B (J) then
        R (I) := A (I);
      else
        R (I) := B (J);
      end if;
      if J < Integer'Last then
        J := J + 1;
      end if;
    end loop;
    return R;
  end Max;
end Array_Util;
```

### 5.4.8 示例 #8

我们考虑一个`Max_Array`版本，它断言两者边界相同。我们要证明`Max_Array`返回一个每个索引上两个参数最大值的数组。

Listing 48: array_util.ads

```ada
package Array_Util is
  type Nat_Array is array (Positive range) of Natural;
  function Max (A, B: Nat_Array) return Nat_Array with
    Pre => A'First = B'First and A'Last = B'Last,
    Post => (all K in A'Range => Max_Array'Result (K) = Natural'Max (A (K), B (K)));
end Array_Util;
```

Listing 49: array_util.db

```ada
package body Array_Util is
  function Max (A, B: Nat_Array) return Nat_Array is
    R : Nat_Array (A'Range) := (others => 0);
  begin
    pragma Loop_Invariant (for all K in A'First .. I =>
      R (K) = Natural'Max (A (K), B (K)));
    for I in A'Range loop
      if A (I) > B (I) then
        R (I) := A (I);
      else
        R (I) := B (I);
      end if;
    end loop;
    return R;
  end Max;
end Array_Util;
```

# SPARK 简介

（接上页）

```ada
end Array_Util;
```

Listing 50: main.adb

```ada
with Array_Util;
  use Array_Util;
procedure Main is
  A : Nat Array := (1, 1, 2);
  B : Nat Array := (2, 1, 0);
  R : Nat Array (1 .. 3);
begin
  R := Max Array (A, B);
end Main;
```

# 编译输出

```text
main.adb:4:04: warning: "A" is not modified, could be declared constant [-gnatwk]
main.adb:5:04: warning: "B" is not modified, could be declared constant [-gnatwk]
main.adb:6:04: warning: variable "R" is assigned but never read [-gnatwm]
main.adb:8:04: warning: possibly useless assignment to "R", value might not be referenced [-gnatwm]
```

# 证明器输出

```text
Phase 1 of 2: generation of Global contracts ...
Phase 2 of 2: flow analysis and proof ...
main.adb:4:04: warning: "A" is not modified, could be declared constant [-gnatwk]
main.adb:5:04: warning: "B" is not modified, could be declared constant [-gnatwk]
main.adb:6:04: warning: variable "R" is assigned but never read [-gnatwm]
main.adb:8:04: warning: possibly useless assignment to "R", value might not be referenced [-gnatwm]
main.adb:8:09: medium: length check fail [reason for check: array must be of appropriate length]
array.util:adb:35: medium: loop invariant might not be preserved by arbitrary iteration, cannot prove R (K) = Natural'max
array.util:8:35: medium: loop invariant might fail in first iteration, cannot prove R (K) = Natural'max
gnatprove: unproved check messages considered as errors
```

# 运行时输出

```text
raised ADA.ASSERTIONS.ASSERTION_ERROR : Loop Invariant failed at array_util.adb:7
```

在这里，Gnatprove 无法证明循环不变性，即使在第一次迭代中如此（该属性见第111页的循环不变性节）。实际上，正如你执行带有断言的函数`Max_Array`时所示：在每次循环迭代中，`R`包含`A`和`B`的最大值仅到`I-1`为止，因为`I`索引尚未确定。

# 第 5 章 功能性正确性证明

### 5.4.9 示例 #9

我们现在考虑`Max_Array`的过程化版本，它更新第一个参数而不是返回新参数。我们想要证明`Max_Array`将其两个参数的最大值设置到其第一个参数的每个索引上。

Listing 51: array_util.adb



```ada
package Array_Util is
  type Nat_Array is array (Positive range <>) of Natural;
  procedure Max_Array (A : in out Nat_Array; B : Nat_Array) with
    Pre => A'First = B'First and A'Last = B'Last,
    Post => (all K in A'Range =>
      A (K) = Natural'Max (A'Old (K), B (K)));
end Array_Util;
```

Listing 52: `array_util.adb`

```ada
package body Array_Util is
  procedure Max_Array (A : in out Nat_Array; B : Nat_Array) is
begin
    for I in A'Range do
      procedure Loop_Invariant
        (all K in A'First .. I - 1 =>
          A (K) = Natural'Max (A'Entry (K), B (K)));
      procedure Loop_Invariant
        (all K in I .. A'Last => A (K) = A'Loop_Entry (K));
      if A (I) < B (I) then
        A (I) := B (I);
      end if;
    end loop;
  end Max_Array;
end Array_Util;
```

# 输出原理

Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: flow analysis and proof ...

`array_util.adb:7:13: info: loop invariant proved`

`array_util.adb:7:13: info: loop initialization proved`

`array_util.adb:7:39: info: overflow check proved`

`array_util.adb:8:10: info: index check proved`

`array_util.adb:8:50: info: index check proved`

`array_util.adb:8:57: info: index check proved`

`array_util.adb:10:13: info: loop invariant initialization proved`

`array_util.adb:10:44: info: loop invariant proved`

`array_util.adb:10:63: info: index check proved`

`array_util.adb:11:25: info: index check proved`

`array_util.adb:12:32: info: index check proved`

`array_util.adb:14:20: info: postcondition proved`

`array_util.adb:8:20: info: index check proved`

`array_util.adb:8:45: info: index check proved`

`array_util.adb:8:52: info: index check proved`

一切都证明了。第一个循环不变性说明了循环之前的 own包含了 `Max_Array` 的参数的最大值（引用 `A` 的输入值）。第二个循环不变性说明了循环索引及之后的值与进入循环时相同。这是循环的帧条件。

### 5.4.10 示例 #10

从上一个示例中移除帧条件。

Listing 53: `array_util.ads`

```ada
package Array_Util is

  type Nat_Array is array (Positive range <>) of Natural;

  procedure Max_Array (A : in out Nat_Array; B : Nat_Array) with
    Pre => A'First = B'First and A'Last = B'Last,
    Post => (for K in A'Range =>
      A (K) = Natural'Max (A'Old (K), B (K)));

end Array_Util;
```

Listing 54: `array_util.adb`

```ada
package body Array_Util is

  procedure Max_Array (A : in out Nat_Array; B : Nat_Array) is
  begin
    for I in A'Range loop
      pragma Loop_Invariant
        (for K in A'First .. I - 1 =>
          A (K) = Natural'Max (A'Loop_Entry (K), B (K)));
      if A (I) <= B (I) then
        A (I) := B (I);
      end if;
    end loop;
  end Max_Array;

end Array_Util;
```

# 证明输出

Phase 1 of 2: generation of Global contracts ...

Phase 2 of 2: analysis and proof ...

`array_util.adb:7:13: info: loop invariant initialization proved`

`array_util.adb:7:13: info: loop invariant preservation proved`

`array_util.adb:7:39: info: overflow check proved`

`array_util.adb:8:18: info: index check proved`

`array_util.adb:5:90: info: index check proved`

`array_util.adb:8:57: info: index check proved`

`array_util.adb:9:25: info: index check proved`

`array_util.adb:10:25: info: index check proved`

`array_util.adb:7:14: info: postcondition proved`

`array_util.adb:5:28: info: index check proved`

`array_util.adb:8:45: info: index check proved`

`array_util.adb:8:52: info: index check proved`
