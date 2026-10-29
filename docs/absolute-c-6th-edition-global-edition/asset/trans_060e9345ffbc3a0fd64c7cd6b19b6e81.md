

由于关系运算符 > 和 == 是在 && 运算符之前执行的，你可以在之前的表达式中省略括号，其含义也相同，但包含一些括号会使表达式更易读。

当表达式中省略了括号时，编译器会根据称为优先级规则的规则对项目进行分组。C++ 大多数的优先级规则在第 2.3 显示中给出。该表包含了一些直到本书后面才讨论的运算符，但为了完整性和那些可能已经了解它们的人而包含在内。

## Display 2.3 Precedence of Operators (part 1 of 2)

| Operator | Description |
|---|---|
| :: | Scope resolution operator |
| . | Dot operator |
| -> | Member selection |
| [] | Array indexing |
| ( ) | Function call |
| ++ | Postfix increment operator (placed after the variable) |
| -- | Postfix decrement operator (placed after the variable) |
| ++ | Prefix increment operator (placed before the variable) |
| -- | Prefix decrement operator (placed before the variable) |
| ! | Not |
| - | Unary minus |
| + | Unary plus |
| * | Dereference |
| & | Address of |
| new | Create (allocate memory) |
| delete | Destroy (deallocate) |
| delete [] | Destroy array (deallocate) |
| sizeof | Size of object |
| ( ) | Type cast |
| * | Multiply |
| / | Divide |
| % | Remainder (modulo) |
| + | Addition |
| - | Subtraction |
| << | Insertion operator (console output) |
| >> | Extraction operator (console input) |

Highest precedence (done first)

Lower precedence (done later)

precedence rules

## Display 2.3 Precedence of Operators (part 2 of 2)

*All operators in part 2 are of lower precedence than those in part 1.*

| Operator | Description |
|---|---|
| `<` | Less than |
| `>` | Greater than |
| `<=` | Less than or equal to |
| `>=` | Greater than or equal to |
| `==` | Equal |
| `!=` | Not equal |
| `&&` | And |
| `||` | Or |
| `=` | Assignment |
| `+=` | Add and assign |
| `-=` | Subtract and assign |
| `*=` | Multiply and assign |
| `/=` | Divide and assign |
| `%=` | Modulo and assign |
| `? :` | Conditional operator |
| `throw` | Throw an exception |
| `,` | Comma operator |

lowest precedence
(done last)

如果一个操作在另一个操作之前执行，则先执行的那个操作被称为具有**更高的优先级**。Display 2.3 中同一框中的所有运算符具有相同的优先级。较高框中的运算符比较低框中的运算符具有更高的优先级。

当运算符具有相同的优先级并且顺序未由括号确定时，则一元操作从右到左执行。赋值操作也从右到左执行。例如，`x = y = z` 表示 `x = (y = z)`。其他具有相同优先级的二元

higher precedence

操作从左到右执行。例如，x + y + z 表示 (x + y) + z。

请注意，优先级规则包括算术运算符如 + 和 * 以及布尔运算符如 && 和 ||。这是因为许多表达式结合了算术和布尔操作，如以下简单示例：

```
(x + 1) > 2 || (x + 1) < -3
```

如果你检查 Display 2.3 中给出的优先级规则，你会看到这个表达式等价于

```
((x + 1) > 2) || ((x + 1) < -3)
```

因为 > 和 < 的优先级高于 ||。事实上，你可以省略前一个表达式中的所有括号，其含义也相同，尽管可读性会变差。虽然我们不提倡省略所有括号，但了解使用优先级规则如何解释此类表达式可能会有所帮助。以下是没有任何括号的表达式：

```
x + 1 > 2 || x + 1 < -3
```

优先级规则说首先应用一元 -，然后应用 +，然后应用 > 和 <，最后应用 ||，这正是完全加括号的版本所指示的。

之前对布尔表达式如何求值的描述基本上是正确的，但在 C++ 中，计算机在求值布尔表达式时偶尔会采用捷径。请注意，在许多情况下，你只需要求值布尔表达式中两个子表达式中的第一个。例如，考虑以下内容：

```
(x >= 0) && (y > 1)
```

如果 x 为负，则 (x >= 0) 为假。正如你在 Display 2.2 中的表中看到的那样，当 && 表达式中的一个子表达式为假时，整个表达式为假，无论另一个表达式是真还是假。因此，如果我们知道第一个表达式为假，就没有必要求值第二个表达式。|| 表达式也会发生类似的情况。如果由 || 运算符连接的两个表达式中的第一个为真，则你知道整个表达式为真，无论第二个表达式是真还是假。C++ 语言利用这一事实，有时可以免去求值由 && 或 || 连接的逻辑表达式中的第二个子表达式的麻烦。C++ 首先求值由 && 或 || 连接的两个表达式中的左侧表达式。如果这提供了足够的信息来确定表达式的最终值（与第二个表达式的值无关），则 C++ 不会费心求值第二个表达式。这种求值方法称为短路求值。

C++ 以外的一些语言使用完全求值。在完全求值中，当两个表达式由 && 或 || 连接时，两个子表达式总是被求值，然后使用真值表来获得最终表达式的值。

## PITFALL: Integer Values Can Be Used as Boolean Values

C++ 有时会将整数当作布尔值使用，并将布尔值当作整数使用。特别是，C++ 将整数 1 转换为 true 并将整数 0 转换为 false，反之亦然。情况甚至比简单地使用 1 表示 true 和 0 表示 false 更复杂。编译器会将任何非零数字视为 true 值，并将 0 视为 false 值。只要你在编写布尔表达式时不犯错误，这种转换就不会引起问题。然而，当你在调试时，了解编译器很乐意使用布尔运算符 &&、|| 和 ! 组合整数可能会有所帮助。

例如，假设你想要一个布尔表达式，只要时间尚未用完（在某些游戏或过程中）就为真。你可能会使用以下内容：

```
!time > limit
```

如果你大声读出来，这听起来是正确的：“不是时间大于限制。” 然而，布尔表达式是错误的，而且不幸的是，编译器不会给你错误信息。编译器将应用 Display 2.3 中的优先级规则并将你的布尔表达式解释为以下内容：

```
(!time) > limit
```

这看起来像胡说八道，直觉上也是胡说八道。如果 time 的值为例如 36，那么 (!time) 可能有什么意义呢？毕竟，那相当于“不是 36”。但在 C++ 中，任何非零整数都会转换为 true，而 0 会转换为 false。因此，36 被解释为“不是 true”，因此求值结果为 false，然后再次转换回 0，因为我们正在与 int 进行比较。

我们想要的这个布尔表达式的值和 C++ 给出的值是不一样的。如果 time 的值为 36 且 limit 的值为 60，你希望之前显示的布尔表达式求值为 true（因为 time > limit 不为真）。不幸的是，布尔表达式的求值如下：(!time) 求值为 false，转换为 0，因此整个布尔表达式等价于

```
0 > limit
```

这又等价于 0 > 60，因为 60 是 limit 的值，而它求值为 false。因此，上述逻辑表达式求值为 false，而你希望它求值为 true。

## PITFALL: (continued)

纠正此问题的另一种方法是完全避免使用 ! 运算符。例如，以下内容也是正确的且更易读：

```
if (time <= limit)
```

你几乎总可以避免使用 ! 运算符，有些程序员主张尽可能避免它。

短路求值和完全求值给出相同的答案，那么为什么你应该关心 C++ 使用短路求值呢？大多数时候你不必关心。只要由 && 或 || 连接的两个子表达式都有值，这两种方法就会产生相同的结果。然而，如果第二个子表达式未定义，你可能会很高兴知道 C++ 使用短路求值。让我们看一个说明这一点的例子。考虑以下语句：

```
if ( (kids != 0) && ((pieces/kids) >= 2) )
    cout << "Each child may have two pieces!";
```

如果 kids 的值不为零，此语句没有细微差别。然而，假设 kids 的值为零：考虑短路求值如何处理这种情况。表达式 (kids!=0) 求值为 false，因此没有必要求值第二个表达式。使用短路求值，C++ 说整个表达式为假，而不费心求值第二个表达式。这可以防止运行时错误，因为求值第二个表达式将涉及除以零。

## Self-Test Exercises

1. Determine the value, true or false, of each of the following Boolean expressions, assuming that the value of the variable count is 0 and the value of the variable limit is 10. Give your answer as one of the values true or false.

- a. (count == 0) && (limit < 20)
- b. count == 0 && limit < 20
- c. (limit > 20) || (count < 5)
- d. !(count == 12)
- e. (count == 1) && (x < y)
- f. (count < 10) || (x < y)
- g. !((count < 10) || (x < y)) && (count >= 0)
- h. ((limit / count) > 7) || (limit < 20)
- i. (limit / 20) || ((limit / count) > 7)
- j. ((limit / count) > 7) && (limit < 0)
- k. (limit < 0) && ((limit / count) > 7)
- l. (5 && 7) + (!(6))

