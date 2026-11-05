
```
switch (i) {
case 0:
    while (true) F();
case 1:
    throw new ArgumentException();
case 2:
    return;
}
```

switch 语句的控制类型可以是 string 类型。例如：

```
void DoCommand(string command) {
    switch (command.ToLower()) {
    case "run":
        DoRun();
        break;
    case "save":
        DoSave();
        break;
    case "quit":
        DoQuit();
        break;
    default:
        InvalidCommand(command);
        break;
    }
}
```

与字符串相等运算符（§7.10.7）类似，switch 语句区分大小写，并且仅当 switch 表达式字符串与某个 case 标签常量完全匹配时，才会执行给定的 switch 节。

当 switch 语句的控制类型为 string 时，允许将 null 值作为 case 标签常量。

switch 块的语句列表可以包含声明语句（§8.5）。在 switch 块中声明的局部变量或常量的作用域是该 switch 块。

在 switch 块内，在表达式上下文中使用的名称的含义必须始终相同（§7.6.2.1）。

如果 switch 语句可到达，并且下列条件中至少有一项为真，则给定 switch 节的语句列表可到达：

- switch 表达式是非常量值。
- switch 表达式是与该 switch 节中的某个 case 标签匹配的常量值。
- switch 表达式是不匹配任何 case 标签的常量值，并且该 switch 节包含 default 标签。
- 该 switch 节的某个 switch 标签被可到达的 goto case 或 goto default 语句引用。

如果下列条件中至少有一项为真，则 switch 语句的结束点可到达：

- switch 语句包含一个可到达的 break 语句，该语句退出 switch 语句。
- switch 语句可到达，switch 表达式是非常量值，并且不存在 default 标签。
- switch 语句可到达，switch 表达式是不匹配任何 case 标签的常量值，并且不存在 default 标签。

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

- 计算布尔表达式（§7.20）。
- 如果布尔表达式的结果为 true，则控制转移到嵌入语句。当控制到达嵌入语句的结束点（可能来自执行 continue 语句）时，控制转移到 while 语句的开头。
- 如果布尔表达式的结果为 false，则控制转移到 while 语句的结束点。

在 while 语句的嵌入语句中，可以使用 break 语句（§8.9.1）将控制转移到 while 语句的结束点（从而结束嵌入语句的迭代），也可以使用 continue 语句（§8.9.2）将控制转移到嵌入语句的结束点（从而执行 while 语句的下一次迭代）。

如果 while 语句可到达，并且布尔表达式不具有常量值 false，则 while 语句的嵌入语句可到达。

如果下列条件中至少有一项为真，则 while 语句的结束点可到达：

- while 语句包含一个可到达的 break 语句，该语句退出 while 语句。
- while 语句可到达，并且布尔表达式不具有常量值 true。

### 8.8.2 do 语句

do 语句有条件地执行嵌入语句一次或多次。

```
do-statement:
do embedded-statement while ( boolean-expression ) ;
```

do 语句按如下方式执行：

- 控制转移到嵌入语句。
- 当控制到达嵌入语句的结束点（可能来自执行 continue 语句）时，计算布尔表达式（§7.20）。如果布尔表达式的结果为 true，则控制转移到 do 语句的开头。否则，控制转移到 do 语句的结束点。

在 do 语句的嵌入语句中，可以使用 break 语句（§8.9.1）将控制转移到 do 语句的结束点（从而结束嵌入语句的迭代），也可以使用 continue 语句（§8.9.2）将控制转移到嵌入语句的结束点。

如果 do 语句可到达，则 do 语句的嵌入语句可到达。

如果下列条件中至少有一项为真，则 do 语句的结束点可到达：

- do 语句包含一个可到达的 break 语句，该语句退出 do 语句。
- 嵌入语句的结束点可到达，并且布尔表达式不具有常量值 true。

### 8.8.3 for 语句

for 语句计算一系列初始化表达式，然后，在条件为 true 时，重复执行嵌入语句并计算一系列迭代表达式。

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

for 初始值设定项（如果存在）由局部变量声明（§8.5.1）或以逗号分隔的语句表达式列表（§8.6）组成。由 for 初始值设定项声明的局部变量的作用域从该变量的局部变量声明符开始，一直延伸到嵌入语句的结尾。该作用域包括 for 条件和 for 迭代器。

for 条件（如果存在）必须是布尔表达式（§7.20）。

for 迭代器（如果存在）由以逗号分隔的语句表达式列表（§8.6）组成。

for 语句按如下方式执行：

- 如果存在 for 初始值设定项，则按书写顺序执行变量初始值设定项或语句表达式。此步骤仅执行一次。
- 如果存在 for 条件，则计算该条件。
- 如果不存在 for 条件，或者计算结果为 true，则控制转移到嵌入语句。当控制到达嵌入语句的结束点（可能来自执行 continue 语句）时，按顺序计算 for 迭代器的表达式（如果有），然后执行下一次迭代，并从上述步骤中对 for 条件的计算开始。
- 如果存在 for 条件且计算结果为 false，则控制转移到 for 语句的结束点。

在 for 语句的嵌入语句中，可以使用 break 语句（§8.9.1）将控制转移到 for 语句的结束点（从而结束嵌入语句的迭代），也可以使用 continue 语句（§8.9.2）将控制转移到嵌入语句的结束点（从而执行 for 迭代器，并从 for 条件开始执行 for 语句的下一次迭代）。

如果下列条件之一为真，则 for 语句的嵌入语句可到达：

- for 语句可到达，并且不存在 for 条件。
- for 语句可到达，并且存在 for 条件，且该条件不具有常量值 false。

如果下列条件中至少有一项为真，则 for 语句的结束点可到达：

- for 语句包含一个可到达的 break 语句，该语句退出 for 语句。
- for 语句可到达，并且存在 for 条件，且该条件不具有常量值 true。

### 8.8.4 foreach 语句

foreach 语句枚举集合的元素，并为集合的每个元素执行嵌入语句。

```
foreach-statement:
    foreach ( local-variable-type identifier in expression ) embedded-statement
```

foreach 语句的类型和标识符声明该语句的迭代变量。如果给定 var 标识符作为局部变量类型，并且作用域中不存在名为 var 的类型，则称该迭代变量为隐式类型迭代变量，其类型按如下指定取为 foreach 语句的元素类型。该迭代变量对应于一个只读局部变量，其作用域覆盖嵌入语句。在执行 foreach 语句期间，迭代变量表示当前正在执行迭代的集合元素。如果嵌入语句试图修改迭代变量（通过赋值或 ++ 和 -- 运算符）或将迭代变量作为 ref 或 out 参数传递，则会发生编译时错误。

foreach 语句的编译时处理首先确定表达式的集合类型、枚举器类型和元素类型。该确定过程如下：

- 如果表达式的类型 X 是数组类型，则存在从 X 到 System.Collections.IEnumerable 接口的隐式引用转换（因为 System.Array 实现此接口）。集合类型为 System.Collections.IEnumerable 接口，枚举器类型为 System.Collections.IEnumerator 接口，元素类型为数组类型 X 的元素类型。
- 如果表达式的类型 X 是 dynamic，则存在从表达式到 System.Collections.IEnumerable 接口的隐式转换（§6.1.8）。集合类型为 System.Collections.IEnumerable 接口，枚举器类型为 System.Collections.IEnumerator 接口。如果给定 var 标识符作为局部变量类型，则元素类型为 dynamic；否则为 object。
- 否则，确定类型 X 是否具有适当的 GetEnumerator 方法：
  - 在类型 X 上使用标识符 GetEnumerator 且不带类型实参执行成员查找。如果成员查找未产生匹配、产生二义性，或产生的匹配不是方法组，则按下文所述检查可枚举接口。建议在成员查找产生的结果除方法组或无匹配之外的任何内容时发出警告。
  - 使用得到的方法组和空实参列表执行重载决策。如果重载决策未产生适用方法、产生二义性，或产生单个最佳方法但该方法为静态方法或不是公共方法，则按下文所述检查可枚举接口。建议在重载决策产生的结果除明确的公共实例方法或无适用方法之外的任何内容时发出警告。
  - 如果 GetEnumerator 方法的返回类型 E 不是类、结构或接口类型，则产生错误，并且不执行后续步骤。
  - 在 E 上使用标识符 Current 且不带类型实参执行成员查找。如果成员查找未产生匹配、结果为错误，或结果除允许读取的公共实例属性之外的任何内容，则产生错误，并且不执行后续步骤。
