
确定在词法上第一个匹配表达式且其 guard 子句不存在或求值为 true 的模式。结束注记

如果 switch 部分的语句列表的终点可达，则会发生编译时错误。这被称为“no fall through”规则。

示例：示例

```
switch (i)
{
    case 0:
        CaseZero();
        break;
    case 1:
        CaseOne();
        break;
    default:
        CaseOthers();
        break;
}
```

是有效的，因为没有 switch 部分具有可达的终点。与 C 和 C++ 不同，switch 部分的执行不允许“fall through”到下一个 switch 部分，并且示例

```
switch (i)
{
    case 0:
        CaseZero();
    case 1:
        CaseZeroOrOne();
    default:
        CaseAny();
}
```

会导致编译时错误。当 switch 部分的执行需要随后执行另一个 switch 部分时，应使用显式的 goto case 或 goto default 语句：

```
switch (i)
{
    case 0:
        CaseZero();
        goto case 1;
    case 1:
        CaseZeroOrOne();
        goto default;
    default:
        CaseAny();
        break;
}
```

结束示例

在 switch_section 中允许使用多个标签。

示例：示例

```
switch (i)
{
    case 0:
        CaseZero();
        break;
    case 1:
        CaseOne();
        break;
    case 2:
    default:
        CaseTwo();
        break;
}
```

是有效的。该示例不违反 "no fall through" 规则，因为标签 case 2: 和 default: 属于同一个 switch_section。

结束示例

注记：“no fall through”规则可防止在 C 和 C++ 中因意外省略 break 语句而发生的一类常见错误。例如，上述 switch 语句的部分可以反转而不影响语句的行为：

```
switch (i)
{
    default:
        CaseAny();
        break;
    case 1:
        CaseZeroOrOne();
        goto default;
    case 0:
        CaseZero();
        goto case 1;
}
```

结束注记

注记：switch 部分的语句列表通常以 break、goto case 或 goto default 语句结束，但任何使语句列表终点不可达的构造都是允许的。例如，由布尔表达式 true 控制的 while 语句已知永远不会到达其终点。同样，throw 或 return 语句总是转移控制权到别处，永远不会到达其终点。因此，以下示例是有效的：

```
switch (i)
{
    case 0:
        while (true)
        {
            F();
        }
    case 1:
        throw new ArgumentException();
    case 2:
        return;
}
```

结束注记

示例：switch 语句的控制类型可以是 string 类型。例如：

```csharp
void DoCommand(string command)
{
    switch (command.ToLower())
    {
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

*结束示例*

*注记：* 类似于字符串相等运算符（§12.12.8），`switch` 语句是区分大小写的，并且只有当 switch 表达式字符串与某个 case 标签常量完全匹配时，才会执行给定的 switch 部分。 *结束注记* 当 `switch` 语句的控制类型为 `string` 或可空值类型时，值 `null` 允许作为 `case` 标签常量。

*switch块* 的 *语句列表*s 可能包含声明语句（§13.6）。在 switch 块中声明的局部变量或常量的作用域是 switch 块。

switch 标签可达的条件是以下至少一项为真：

- switch 表达式是常量值且满足以下任一条件
  - 该标签是其模式 *会匹配* (§11.2.1) 该值的 *case*，并且标签的 guard 不存在或不是值为 false 的常量表达式；或
  - 它是 *default* 标签，并且没有任何 switch 部分包含其模式会匹配该值且 guard 不存在或为值为 true 的常量表达式的 case 标签。
- switch 表达式不是常量值且满足以下任一条件
  - 该标签是 *case* 且没有 guard 或 guard 的值不是常量 false；或
  - 它是 *default* 标签且
    - switch 语句中没有 guard 或 guard 值为常量 true 的 case 中出现的模式集合，对于 switch 控制类型来说不是 *穷尽的* (§11.4)；或
    - switch 控制类型是可空类型，并且 switch 语句中没有 guard 或 guard 值为常量 true 的 case 中出现的模式集合不包含会匹配值 null 的模式。
- switch 标签被可达的 goto *case* 或 goto *default* 语句引用。

给定 switch 部分的语句列表可达的条件是 `switch` 语句可达并且该 switch 部分包含一个可达的 switch 标签。

switch 语句的终点可达的条件是 switch 语句可达并且以下至少一项为真：

- switch 语句包含一个可达的 break 语句，该语句退出 switch 语句。
- 没有 default 标签存在且满足以下任一条件
  - switch 表达式是非常量值，并且 switch 语句中没有 guard 或 guard 值为常量 true 的 case 中出现的模式集合，对于 switch 控制类型来说不是穷尽的（§11.4）。
  - switch 表达式是可空类型的非常量值，并且 switch 语句中没有 guard 或 guard 值为常量 true 的 case 中出现的模式不会匹配值 null。
  - switch 表达式是常量值，并且没有没有 guard 或 guard 为常量 true 的 case 标签会匹配该值。

示例：以下代码展示了 when 子句的简洁用法：

```
static object CreateShape(string shapeDescription)
{
    switch (shapeDescription)
    {
        case "circle":
            return new Circle(2);
        ...
        case var o when string.IsNullOrWhiteSpace(o):
            return null;
        default:
            return "invalid shape description";
    }
}
```

var case 匹配 null、空字符串或仅包含空白字符的任何字符串。结束示例

## 13.9 迭代语句

### 13.9.1 通用

迭代语句重复执行嵌入的语句。

```
iteration_statement
    : while_statement
    | do_statement
    | for_statement
    | foreach_statement
    ;
```

### 13.9.2 while 语句

while 语句有条件地执行嵌入的语句零次或多次。

A `while` statement is executed as follows:

- *布尔表达式* (§12.24) 被求值。
- 如果布尔表达式产生 `true`，控制权转移到嵌入的语句。当且仅当控制权到达嵌入语句的终点时（可能来自 `continue` 语句的执行），控制权转移到 `while` 语句的开头。
- 如果布尔表达式产生 `false`，控制权转移到 `while` 语句的终点。

在 `while` 语句的嵌入语句内，可以使用 `break` 语句 (§13.10.2) 将控制权转移到 `while` 语句的终点（从而结束嵌入语句的迭代），并且可以使用 `continue` 语句 (§13.10.3) 将控制权转移到嵌入语句的终点（从而执行 `while` 语句的另一次迭代）。

`while` 语句的嵌入语句可达的条件是 `while` 语句可达并且布尔表达式不具有常量值 `false`。

`while` 语句的终点可达的条件是以下至少一项为真：

- `while` 语句包含一个可达的 `break` 语句，该语句退出 `while` 语句。
- `while` 语句可达并且布尔表达式不具有常量值 `true`。

### 13.9.3 do 语句

`do` 语句有条件地执行嵌入的语句一次或多次。

```
do_statement
    : 'do' embedded_statement 'while' '(' boolean_expression ')' ';'
    ;
```

`do` 语句的执行如下：

- 控制权转移到嵌入的语句。
- 当且仅当控制权到达嵌入语句的终点时（可能来自 `continue` 语句的执行），*布尔表达式* (§12.24) 被求值。如果布尔表达式产生 `true`，控制权转移到 `do` 语句的开头。否则，控制权转移到 `do` 语句的终点。

在 `do` 语句的嵌入语句内，可以使用 `break` 语句 (§13.10.2) 将控制权转移到 `do` 语句的终点（从而结束嵌入语句的迭代），并且可以使用 `continue` 语句 (§13.10.3) 将控制权转移到嵌入语句的终点（从而执行 `do` 语句的另一次迭代）。

`do` 语句的嵌入语句可达的条件是 `do` 语句可达。

`do` 语句的终点可达的条件是以下至少一项为真：

- `do` 语句包含一个可达的 `break` 语句，该语句退出 `do` 语句。
- 嵌入语句的终点可达并且布尔表达式不具有常量值 `true`。
