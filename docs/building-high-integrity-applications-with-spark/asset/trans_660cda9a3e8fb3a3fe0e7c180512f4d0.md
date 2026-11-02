
让我们从一个简单的示例开始，该示例说明了 Ada 程序的基本结构。下面的程序提示用户输入两个整数并显示它们的平均值。

```
    1  with Ada.Text_IO;
    2  with Ada.Integer_Text_IO;
    3  with Ada.Float_Text_IO;
    4  procedure Average is
    5     -- Display the average of two integers entered by the user
    6     A : Integer;   -- The first integer
    7     B : Integer;   -- The second integer
    8     M : Float;     -- The average of the two integers
    9  begin
    10    Ada.Text_IO.Put_Line (Item => "Enter two integers.");
    11    Ada.Integer_Text_IO.Get (Item => A);
    12    Ada.Integer_Text_IO.Get (Item => B);
    13    Ada.Text_IO.New_Line;
    14
    15    M := Float (A + B) / 2.0;
    16
    17    Ada.Text_IO.Put (Item => "The Average of your two numbers is ");
    18    Ada.Float_Text_IO.Put (Item => M,
    19                           Fore => 1,
    20                           Aft  => 2,
    21                           Exp  => 0);
    22    Ada.Text_IO.New_Line;
    23 end Average;
```

程序的前三行是 *上下文项*。这三项上下文项共同构成了程序的 *上下文子句*。这三个 *with* 子句指定了我们的程序所需的库单元。在此示例中，我们使用来自三个不同库单元的输入输出操作：一个用于字符串和字符的输入输出（Ada.Text_IO），一个用于整数的输入输出（Ada.Integer_Text_IO），以及一个用于浮点实数的输入输出（Ada.Float_Text_IO）。我们所有示例中的粗体字都是 *保留字*。你可以在 ARM（2012）第 2.9 节中找到全部七十三個保留字的列表。

紧随上下文子句之后的是第 4 行的程序规约。在此示例中，规约仅由名称 Average 组成且没有参数。该名称在标记此程序单元结束的最后一行中重复出现。注释以两个相邻的连字符开始并延伸到行尾。在我们的列表中，注释以斜体格式显示。

紧随程序单元的规约之后的是 *声明部分*（第 5–8 行）。在我们的示例中，我们声明了三个变量。变量 A 和 B 被声明为类型 `Integer`，这是一种语言定义的整数类型，具有实现定义的范围。变量 M 被声明为类型 `Float`，这是一种语言定义的浮点数类型，具有实现定义的精度和范围。这三个变量的初始值未定义。

程序的可执行语句在保留字 `begin` 之后。我们示例中的可执行语句除一个之外都是对各种库包中定义的例程（子程序）的调用。在第一个语句中，我们调用库包 `Ada.Text_IO` 中的例程 `Put_Line`。

除例程 `New_Line` 外，示例中调用的所有例程都需要参数。Ada 提供了 *命名* 和 *位置* 参数关联。你可能非常熟悉位置参数关联，其中形式参数和实际参数通过参数列表中的位置关联。使用命名参数关联时，我们调用中参数的顺序无关紧要。我们的示例使用命名关联来匹配形式参数和实际参数。要使用命名关联，我们给出形式参数的名称，后跟箭头符号 `=>`，再后跟实际参数。在我们对例程 `Put_Line` 的调用中，形式参数是 `Item`，实际参数是我们提示的字符串字面量。当只有一个参数时，命名参数关联提供的信息很少。然而，当有多个参数时，如在对 `Ada.Float_Text_IO.Put` 的调用中，命名参数关联提供的信息使阅读和编写调用都更轻松。此调用中的形式参数 `Fore`、`Aft` 和 `Exp` 提供了如何格式化实数的信息。有关实数格式化的详细信息在 ARM（2012）第 A.10.9 节中给出。

我们示例中唯一不是例程调用的语句是第 15 行的赋值语句，它计算用户输入的两个整数的平均值。该赋值语句中的算术表达式包含三个操作。首先，将两个整数相加。然后将整数和显式转换为浮点数。最后，将浮点和除以 2。显式转换（强制转换）到类型 `Float` 是必要的，因为 Ada 不进行隐式类型转换。显式类型转换的语法类似于使用类型作为函数名称的函数调用。

你可能会觉得程序 `Average` 需要的输入比你愿意做的更多。为每个库例程的名称加上其包名前缀（例如 `Ada.Integer_Text_IO`）可能看起来令人望而生畏。当然，大多数集成开发环境（如 GNAT 编程工作室 GPS）都提供智能代码补全，使这项任务更容易。Ada 提供了另一种替代方案，即 *use 子句*，它允许我们在不使用单元名称作为前缀的情况下使用来自程序单元的资源。

不同程序单元可能定义了同名的资源。例如，Ada.Text_IO 和 Ada.Integer_Text_IO 都包含一个名为 Put 的子程序。编译器使用子程序调用的签名来确定调用哪个 Put。如果编译器无法解析名称，你将看到错误消息。下面是一个更短的 Average 程序版本，说明了 use 子句的使用。我们还使用了位置参数关联来缩短参数列表。

```
with Ada.Text_IO;        use Ada.Text_IO;
with Ada.Integer_Text_IO; use Ada.Integer_Text_IO;
with Ada.Float_Text_IO;   use Ada.Float_Text_IO;
procedure Average is  -- Shorter version with "use clauses"
   -- Display the average of two integers entered by the user
   A : Integer;   -- The first integer
   B : Integer;   -- The second integer
   M : Float;     -- The average of the two integers
begin
   Put_Line ("Enter two integers.");
   Get (A);
   Get (B);
   New_Line;

   M := Float (A + B) / 2.0;

   Put ("The Average of your two numbers is ");
   Put (M, 1, 2, 0);
   New_Line;
end Average;
```

在本书的其余部分，我们将在使代码对读者更清晰时使用前缀和命名参数关联。在离开这个简单程序之前，最后说明一点。Ada 不区分大小写。因此，三个标识符 — Total、total 和 tOtAl — 是等价的。对同一标识符使用不同的大小写被认为是不良做法。GNAT 编译器常用的一个开关要求对使用不同大小写的情况发出警告。

## 2.1 Control Structures

Ada 提供了两种基于某些条件做出决定的语句：if 语句和 case 语句。ARM（2012）第 5.3 节提供了 if 语句的详细信息，第 5.4 节提供了 case 语句的详细信息。Ada 提供了具有几种不同迭代方案的 loop 语句。这些方案在 ARM 第 5.5 节中有详细描述。在本节中，我们将提供每种控制结构的示例。

### 2.1.1 If Statements

以下是 if 语句各种形式的示例。

```
if A < 0 then
  A := -A;
  D := 1;
end if;

if A in 1 .. 12 then
  B := 17;
end if;

if A > B then
  E := 1;
  F := A;
else
  E := 2;
  F := B;
end if;
```

```
if A = B then
  F := 3;
elsif A > B then
  F := 4;
else
  F := 5;
end if;

if A >= B and A >= C then
  G := 6;
elsif B > A and B > C then
  G := 7;
elsif C > A and C > B then
  G := 8;
end if;
```

Ada 提供了以下在 if 语句的布尔表达式中常用的相等、关系、逻辑和成员运算符。

| Operator | Meaning |
|---|---|
| **Equality Operators** | |
| = | 相等 |
| /= | 不相等 |
| **Relational Operators** | |
| < | 小于 |
| <= | 小于或等于 |
| > | 大于 |
| >= | 大于或等于 |

| Operator | Meaning |
|---|---|
| **Logical Operators** | |
| not | 逻辑否定 |
| and | 逻辑合取 |
| or | 逻辑析取 |
| xor | 异或 |
| and then | 短路与 |
| or else | 短路或 |
| **Membership Operators** | |
| in | 成员 |
| not in | 非成员 |

包含 and 和 or 运算符的布尔表达式必须包含括号以指示期望的求值顺序。ARM（2012）第 4.5 节给出了 Ada 所有运算符的完整列表和描述以及六个优先级级别。
