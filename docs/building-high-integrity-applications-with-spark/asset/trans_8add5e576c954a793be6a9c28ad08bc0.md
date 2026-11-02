
现在考虑一个简单函数，它用于对这样一个数组的元素求和。在本例中，我们只考虑流问题，因此目前可以暂时不考虑计算过程中溢出的问题。

```
function Add_Elements (A : Integer_Array) return Integer is
  Sum : Integer := 0;  -- Ineffective initialization
begin
  Sum := 0;
  for Index in A'Range loop
    Sum := Sum + A (Index);
  end loop;
  return Sum;
end Add_Elements;
```

该函数包含对 Sum 的冗余初始化：首先在变量声明时初始化，随后又在函数体开头再次初始化。流分析会将该初始化标记为流问题，称其“没有效果”，因为所初始化的值在未被使用的情况下就被覆盖了。

这没有问题，但现在考虑使用 Ada 为类型指定默认初始值的机制的情形。你可能会引入一种特殊的整数类型来用作累加器。

```
type Accumulator is new Integer
  with Default_Value => 0;
```

使用 Default_Value 方面意味着，每次声明 Accumulator 类型的对象时，它都会自动被赋值为零。这确保累加器始终被初始化为一个合理的值。现在考虑 Add_Elements 的第二个、略有不同的实现：

```
function Add_Elements2 (A : Integer_Array) return Integer is
  Sum : Accumulator;
begin
  -- Sum is automatically initialized.
  -- Yet assignment below does not cause a flow issue.
  Sum := 1;  -- Start with a bias value.
  for Index in A'Range loop
    Sum := Sum + Accumulator (A (Index));  -- note type conversion
  end loop;
  return Integer (Sum);
end Add_Elements2;
```

在这个版本中，Sum 会自动初始化为其默认值零。通常，对于这样的函数来说，这会带来很好的便利。然而，Add_Elements2 希望将累加和偏移一，因此在函数体中将 Sum 重新初始化为 1。值得注意的是，这不会导致流分析将默认初始化标记为无效。工具理解在某些情况下覆盖默认初始化是合理的，因此不认为这样做是流问题。

由于 Accumulator 是不同于 Integer 的新类型，现在需要在 Add_Elements2 中进行一些类型转换。你可能想知道为什么不将 Accumulator 定义为 Integer 的子类型。唉，Ada 不允许将 Default_Value 方面应用于子类型。

作为另一个例子，考虑以下封装一对整数的记录定义。这里为两个分量都指定了默认值。

```ada
type Pair_With_Default is
   record
      X : Integer := 0;
      Y : Integer := 0;
   end record;
```

现在考虑一个函数 Adjust_Pair，它接受一个 Pair_With_Default，并在 (x, y) 平面上移动它：

```ada
function Adjust_Pair (P : Pair_With_Default) return Pair_With_Default is
   Offset : Pair_With_Default;
begin
   -- Offset is automatically initialized.
   -- Yet assignment below does not cause a flow issue.
   Offset.Y := 1;
   return (P.X + Offset.X, P.Y + Offset.Y);
end Adjust_Pair;
```

与前一个例子一样，Offset 会被默认初始化。然而，对 Offset.Y 的赋值并不是流问题，因为对默认初始化值的重新初始化被认为是合理且正确的。此外，在返回表达式中使用 Offset.X 也不是流问题，因为 Offset 的 X 分量当然具有默认初始化器。

你可能想知道，如果该记录只有部分分量具有默认初始化器，会发生什么：

```ada
type Pair_With_YDefault is
   record
      X : Integer;
      Y : Integer := 0;
   end record;
```

尽管这样的类型声明在完整的 Ada 中是合法的，但在 SPARK 中不允许。要么所有分量都必须具有默认初始化器，要么都不能有。

变量包在精化时实际上也可以被默认初始化。再次考虑 Datebook 示例，这里展示了一个清除日期簿中所有事件的过程。为简洁起见，未展示该包中的其他子程序。

```
with Dates;
package Datebook
   with
      Abstract_State  => State,
      Initializes     => State
is
   procedure Clear
      with
         Global   => (Output => State),
         Depends  => (State => null);
end Datebook;
```

Datebook 包建模了由状态抽象 State 表示的单个对象。Initializes 方面断言该包在精化时初始化该状态。然而，从 Clear 过程的流依赖契约 State => null 可以看出，该过程也会初始化该状态。如果一位紧张的编程人员在使用该包之前调用了 Clear，那么该编程人员就是在重新初始化一个已默认初始化的“变量”。遵循前面描述的原则，流分析不会将此标记为流问题。

一般来说，重新初始化可能会使被重新初始化的实体进入新的起始状态。在前面的 Adjust_Pair 的 Offset 示例中，Y 根据外层子程序的需要被设置为起始值 1。类似地，一个复杂的包可能具有多个以不同方式清除内部状态的“清除”过程。

当然，重新初始化会带来一些开销。当一个值被重新初始化时，进行默认初始化所花费的时间就被浪费了。这是反对在所有地方为所有实体定义默认初始化的一个理由。相反，编程人员可能希望按照自己的意愿、在需要时并以所需方式显式初始化对象。然而，默认初始化对某些类型和某些包是有用的；在那些合理的情况下，SPARK 工具允许重新初始化。

## 4.5 依赖契约的综合

从概念上讲，SPARK 要求每个子程序都具有数据依赖契约和流依赖契约。然而，并非在所有情况下都必须显式包含这些契约；SPARK 工具可以使用本节讨论的规则综合它们。

只要你满足于综合出的契约，就可以编写 SPARK 代码，而不必在每个地方都繁琐地提供数据依赖契约和流依赖契约。这意味着，只需向现有编译单元添加适当的 SPARK_Mode 方面（如我们在第 7.1.1 节所述），并当然移除该单元可能使用的任何非 SPARK 构造，就可以将现有 Ada 代码“转换”为 SPARK。在开始使用 SPARK 工具之前，不必为所有子程序标注依赖契约。以这种方式将 SPARK 应用于现有 Ada 代码称为*回顾性分析*。

前面我们强调过，数据依赖契约和流依赖契约是子程序规范的一部分。与参数列表一样，理想情况下，依赖契约应在实现子程序之前作为设计过程的一部分编写。在设计并实现代码库时应用 SPARK 称为*构造性分析*。

然而，即使在构造性分析的情况下，依赖综合出的契约有时也是合理的。对于嵌套在其他子程序内部的子程序，或仅在特定包上下文中使用的子程序来说，尤其如此。内部子程序的存在是为了服务于外层子程序或包，实际上属于外层实体的实现部分，而不是自身的设计元素。

契约综合的确切规则很详细，但其效果在很大程度上是直观的：

- 1. 如果存在 Global 方面但不存在 Depends 方面，则通过假设每个输出依赖于所有输入来综合流依赖契约。对于像第 105 页的 Search 过程这样的小型子程序，这通常完全正确。无论如何，所得的流依赖是保守的，因为它可能定义比实际存在的更多依赖。这有可能增加调用者中的误报数量，但例如不会允许任何错误，比如意外使用未初始化值²。如果误报被证明是个问题，你始终可以显式添加更精确的流依赖契约。

- 2. 如果存在 Depends 方面但不存在 Global 方面，则通过检查流依赖契约并根据流构造数据依赖来综合数据依赖契约。例如，假设一个子程序声明如下：

```
```
procedure Do_Something(X : in Integer; Y : out Integer)
   with
      Depends => (Y => (X, A, B), B => (X, A), C => X);
```
```

该契约提到了 A、B 和 C，它们在此程序位置必须作为全局变量可见。所指定的流要求 A
