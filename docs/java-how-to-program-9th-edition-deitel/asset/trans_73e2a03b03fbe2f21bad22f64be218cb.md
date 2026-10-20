

如果变量 studentGrade 大于或等于 90，则嵌套的 if...else 语句中的前四个条件都将为 true，但只有第一个 if...else 语句的 if 部分中的语句会执行。该语句执行后，最外层 if...else 语句的 else 部分会被跳过。许多程序员更喜欢将上述嵌套的 if...else 语句编写为：

```
if ( studentGrade >= 90 )
    System.out.println( "A" );
else if ( studentGrade >= 80 )
    System.out.println( "B" );
else if ( studentGrade >= 70 )
    System.out.println( "C" );
else if ( studentGrade >= 60 )
    System.out.println( "D" );
else
    System.out.println( "F" );
```

两种形式除了空格和缩进之外完全相同，编译器会忽略这些空格和缩进。后一种形式避免了代码向右深度缩进。这种缩进常常使源代码行剩余空间很少，迫使行被拆开。

## 悬空 else 问题

Java 编译器总是将 else 与紧邻的前一个 if 关联，除非通过花括号（{ 和 }）的位置指示另作处理。这种行为可能导致所谓的悬空 else 问题。例如，

```
if ( x > 5 )
    if ( y > 5 )
        System.out.println( "x and y are > 5" );
else
    System.out.println( "x is <= 5" );
```

这看起来表示：如果 x 大于 5，嵌套的 if 语句将确定 y 是否也大于 5。如果是，则输出字符串 “x and y are > 5”。否则，看起来如果 x 不大于 5，if...else 的 else 部分将输出字符串 “x is <= 5”。当心！这个嵌套的 if...else 语句并不像看起来那样执行。编译器实际上将该语句解释为：

```
if ( x > 5 )
    if ( y > 5 )
        System.out.println( "x and y are > 5" );
    else
        System.out.println( "x is <= 5" );
```

其中第一个 if 的语句体是一个嵌套的 if...else。外层 if 语句测试 x 是否大于 5。如果是，则继续执行，测试 y 是否也大于 5。如果第二个条件为 true，会显示正确的字符串—— “x and y are > 5”。然而，如果第二个条件为 false，则显示字符串 “x is <= 5”，即使我们知道 x 大于 5。同样糟糕的是，如果外层 if 语句的条件为 false，则内层 if...else 会被跳过，并且不显示任何内容。

```
if ( x > 5 )
{
    if ( y > 5 )
        System.out.println( "x and y are > 5" );
}
else
    System.out.println( "x is <= 5" );
```

这些花括号表示第二个 if 位于第一个 if 的语句体中，并且 else 与第一个 if 关联。习题 4.27–4.28 将进一步研究悬空 else 问题。

## 块

if 语句通常期望其语句体中只有一条语句。若要在 if（或 if...else 语句的 else 部分）的语句体中包含多条语句，请将这些语句括在花括号中。包含在一对花括号中的语句构成一个块。块可以放置在程序中任何可以放置单条语句的位置。

下面的示例在 if...else 语句的 else 部分包含一个块：

```
if ( grade >= 60 )
    System.out.println( "Passed" );
else
{
    System.out.println( "Failed" );
    System.out.println( "You must take this course again." );
}
```

在这种情况下，如果 grade 小于 60，程序将执行 else 语句体中的两条语句并输出：

```
Failed
You must take this course again.
```

请注意 else 子句中包围两条语句的花括号。这些花括号很重要。如果没有花括号，语句：

```
System.out.println( "You must take this course again." );
```

将位于 if...else 语句的 else 部分之外，并且无论 grade 是否小于 60 都会执行。

语法错误（例如，程序中块中缺少一个花括号）由编译器捕获。逻辑错误（例如，程序中块中两个花括号都被遗漏）在运行时才产生影响。致命逻辑错误会导致程序失败并提前终止。非致命逻辑错误允许程序继续执行，但会导致其产生不正确的结果。

正如块可以放置在单条语句可放置的任何位置一样，也可能存在空语句。回忆 2.8 节，空语句是通过在通常放置语句的位置放置分号（;）来表示的。

> **常见编程错误 4.1**
>
> 在 if 或 if...else 语句的条件后放置分号，会在单选择 if 语句中导致逻辑错误，并在双选择 if...else 语句（当 if 部分包含实际的语句体语句时）中导致语法错误。

## 4.7 while 重复语句

重复（或循环）语句允许你指定程序在某个条件保持为 true 时重复执行一个操作。伪代码语句：

```
While there are more items on my shopping list
Purchase next item and cross it off my list
```

描述了购物过程中发生的重复。条件“购物单上还有更多物品”可能为 true 或 false。如果为 true，则执行操作“购买下一件物品并将其从购物单上划掉”。只要条件保持为 true，该操作就会重复执行。While 重复语句中包含的一条或多条语句构成其语句体，该语句体可以是单条语句或一个块。最终，条件会变为 false（当购物单上最后一件物品已被购买并划掉时）。此时，重复终止，重复语句之后的第一条语句执行。

作为 Java 的 while 重复语句的一个示例，考虑一个查找第一个大于 100 的 3 的幂的程序段。假设 int 变量 product 被初始化为 3。执行下面的 while 语句后，product 将包含结果：

```
while ( product <= 100 )
    product = 3 * product;
```

当这个 while 语句开始执行时，变量 product 的值为 3。while 语句的每次迭代都将 product 乘以 3，因此 product 依次取值为 9、27、81 和 243。当变量 product 变为 243 时，while 语句的条件——product <= 100——变为 false。这终止了重复，因此 product 的最终值为 243。此时，程序将继续执行 while 语句之后的下一条语句。

> **常见编程错误 4.2**
>
> 如果在 while 语句的语句体中没有提供最终会使 while 中的条件变为 false 的操作，通常会导致称为无限循环的逻辑错误（循环永不终止）。

图 4.4 中的 UML 活动图说明了上述 while 语句的控制流。同样，图中的符号（除了初始状态、转移箭头、最终状态和三个注释之外）表示一个动作状态和一个决策。此图引入了 UML 的合并符号。UML 将合并符号和决策符号都表示为菱形。合并符号将两条活动流合并为一条。在此图中，合并符号连接来自初始状态和来自动作状态的转移，因此这两条转移都流入决定循环是否应开始（或继续）执行的决策。决策符号和合并符号可以通过“进入”和“离开”的转移箭头数量来区分。决策符号有一个指向菱形的转移箭头，以及两个或更多从菱形指出的转移箭头，以表示从该点出发的可能转移。此外，每条从决策符号指出的转移箭头旁边都有一个守卫条件。合并符号有两个或更多指向菱形的转移箭头，且只有一个从菱形指出的转移箭头，表示多条活动流合并以继续该活动。与合并符号关联的转移箭头都没有守卫条件。

