
## 8.8 迭代语句

迭代语句重复执行嵌入语句。

```
iteration-statement:
  while-statement
  do-statement
  for-statement
  foreach-statement
```

### 8.8.1 while 语句

while 语句有条件地执行嵌入语句零次或多次。

```
while-statement:
  while ( boolean-expression ) embedded-statement
```

while 语句按如下方式执行：

- 对布尔表达式（§7.20）进行求值。
- 如果布尔表达式的结果为 true，则控制转移到嵌入语句。当控制到达嵌入语句的结束点（可能是在执行 continue 语句之后）时，控制转移到 while 语句的开头。
- 如果布尔表达式的结果为 false，则控制转移到 while 语句的结束点。

在 while 语句的嵌入语句内，可以使用 break 语句（§8.9.1）将控制转移到 while 语句的结束点（从而结束嵌入语句的迭代），也可以使用 continue 语句（§8.9.2）将控制转移到嵌入语句的结束点（从而执行 while 语句的另一次迭代）。

如果 while 语句可到达，且布尔表达式不具有常量值 false，则 while 语句的嵌入语句可到达。

如果以下至少一项为真，则 while 语句的结束点可到达：

- while 语句包含一个可到达的 break 语句，该语句退出 while 语句。

> **弗拉基米尔·列舍特尼科夫** 当 break 语句位于包含 finally 块的 try 语句的 try 块或 catch 块内，且 break 语句的目标位于该 try 语句之外，并且 finally 块的结束点不可到达时，此规则不适用。

- while 语句可到达，且布尔表达式不具有常量值 true。

### 8.8.2 do 语句

do 语句有条件地执行嵌入语句一次或多次。

```
do-statement:
    do embedded-statement while ( boolean-expression ) ;
```

do 语句按如下方式执行：

- 控制转移到嵌入语句。
- 当控制到达嵌入语句的结束点（可能是在执行 continue 语句之后）时，对布尔表达式（§7.20）进行求值。如果布尔表达式的结果为 true，则控制转移到 do 语句的开头。否则，控制转移到 do 语句的结束点。

在 do 语句的嵌入语句内，可以使用 break 语句（§8.9.1）将控制转移到 do 语句的结束点（从而结束嵌入语句的迭代），也可以使用 continue 语句（§8.9.2）将控制转移到嵌入语句的结束点。

如果 do 语句可到达，则 do 语句的嵌入语句可到达。

如果以下至少一项为真，则 do 语句的结束点可到达：

- do 语句包含一个可到达的 break 语句，该语句退出 do 语句。

> **弗拉基米尔·列舍特尼科夫** 当 break 语句位于包含 finally 块的 try 语句的 try 块或 catch 块内，且 break 语句的目标位于该 try 语句之外，并且 finally 块的结束点不可到达时，此规则不适用。

- 嵌入语句的结束点可到达，且布尔表达式不具有常量值 true。

### 8.8.3 for 语句

for 语句会求值一系列初始化表达式，然后当条件为 true 时，重复执行嵌入语句并求值一系列迭代表达式。

```
for-statement:
  for ( for-initializer_opt ; for-condition_opt ; for-iterator_opt ) embedded-statement

for-initializer:
  local-variable-declaration
  statement-expression-list

for-condition:
  boolean-expression

for-iterator:
  statement-expression-list

statement-expression-list:
  statement-expression
  statement-expression-list , statement-expression
```

for 初始值设定项（如果存在）由一个局部变量声明（§8.5.1）或以逗号分隔的语句表达式列表（§8.6）组成。由 for 初始值设定项声明的局部变量的作用域从该变量的局部变量声明符开始，一直延伸到嵌入语句的结束点。该作用域包括 for 条件和 for 迭代器。

for 条件（如果存在）必须是布尔表达式（§7.20）。

for 迭代器（如果存在）由以逗号分隔的语句表达式列表（§8.6）组成。

for 语句按如下方式执行：

- 如果存在 for 初始值设定项，则按书写顺序执行变量初始值设定项或语句表达式。此步骤只执行一次。
- 如果存在 for 条件，则对其进行求值。
- 如果不存在 for 条件，或者求值结果为 true，则控制转移到嵌入语句。当控制到达嵌入语句的结束点（可能是在执行 continue 语句之后）时，按顺序对 for 迭代器的表达式（如果有）进行求值，然后执行另一次迭代，并从上述步骤中对 for 条件求值开始。
- 如果存在 for 条件且求值结果为 false，则控制转移到 for 语句的结束点。

在 for 语句的嵌入语句内，可以使用 break 语句（§8.9.1）将控制转移到 for 语句的结束点（从而结束嵌入语句的迭代），也可以使用 continue 语句（§8.9.2）将控制转移到嵌入语句的结束点（从而执行 for 迭代器，并从 for 条件开始执行 for 语句的另一次迭代）。

如果以下一项为真，则 for 语句的嵌入语句可到达：

- for 语句可到达，且不存在 for 条件。
- for 语句可到达，且存在 for 条件，并且该条件不具有常量值 false。

如果以下至少一项为真，则 for 语句的结束点可到达：

- for 语句包含一个可到达的 break 语句，该语句退出 for 语句。

> **弗拉基米尔·列舍特尼科夫** 当 break 语句位于包含 finally 块的 try 语句的 try 块或 catch 块内，且 break 语句的目标位于该 try 语句之外，并且 finally 块的结束点不可到达时，此规则不适用。

- for 语句可到达，且存在 for 条件，并且该条件不具有常量值 true。

### 8.8.4 foreach 语句

foreach 语句枚举集合的元素，并为集合中的每个元素执行嵌入语句。

```
foreach-statement:
    foreach ( local-variable-type identifier in expression ) embedded-statement
```

foreach 语句的类型和标识符声明该语句的迭代变量。如果给定 var 标识符作为局部变量类型，且作用域中不存在名为 var 的类型，则称该迭代变量为隐式类型化迭代变量，并且其类型按下面指定被视为 foreach 语句的元素类型。该迭代变量对应于一个只读局部变量，其作用域覆盖嵌入语句。在执行 foreach 语句期间，迭代变量表示当前正在对其进行迭代的集合元素。如果嵌入语句试图修改迭代变量（通过赋值或 ++ 和 -- 运算符），或者将迭代变量作为 ref 或 out 参数传递，则发生编译时错误。

> **克里斯·塞尔斯** 为了可读性，应优先使用 foreach 语句而不是 for 语句。

> **乔恩·斯基特** 只有一个迭代变量（它是只读的，却会在每次迭代时神奇地改变其值）这一事实，导致了捕获变量最常见的问题之一。下面的代码看起来会打印 "a"、"b"、"c"、"d"，但实际上会打印四次 "d"。

```
List<Action> actions = new List<Action>();
foreach (string value in new[] { "a", "b", "c", "d" })
{
    actions.Add(() => Console.WriteLine(value));
}
foreach (Action action in actions)
{
    action();
}
```

> 通常的解决方案是在 foreach 语句体内引入一个额外变量，用于保存迭代变量当前值的副本。这样，每个委托将捕获不同的变量。在这种情况下，第一个循环将变为

```
foreach (string value in new[] { "a", "b", "c", "d" })
{
    String copy = value;
    actions.Add(() => Console.WriteLine(copy));
}
```

> **彼得·塞斯托夫特** foreach 语句本可以用不同方式定义，以避免乔恩·斯基特的评论中讨论的变量捕获问题：只需在本节后面展示的 try-while-finally 展开中，将声明 v 移到 while 循环内部。确实，在最初的 C# 语言规范中，该声明出现在 while 循环内部，但在 C# 2.0 标准化期间，人们发现将 v 声明在循环外部更接近事实，至少在微软的实现中如此，因此标准也相应更改。

foreach 语句的编译时处理首先确定表达式的集合类型、枚举器类型和元素类型。此确定过程如下：

