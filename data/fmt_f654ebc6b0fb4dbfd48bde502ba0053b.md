
# 6.10 break 和 continue 语句

除了选择和迭代语句外，C# 还提供了 `break` 和 `continue` 来控制控制流。前一节展示了如何使用 `break` 来终止 `switch` 语句的执行。本节将讨论如何使用 `break` 来终止迭代语句。

## 6.10.1 break 语句

当 `break` 语句在 `while`、`for`、`do...while`、`switch` 或 `foreach` 中执行时，会导致立即退出循环或 `switch`。执行将从注释语句后的第一个语句继续。图 6.13 展示了 `break` 语句退出 `for` 循环。当它嵌套在 `for` 的第 13 行（第 11-19 行）内部并确定 `count` 为 5 时，第 15 行的 `break` 语句执行。这终止了该语句，程序继续到第 21 行（该语句之后），该行会显示循环结束时控制变量的值。由于 `break` 的存在，循环体仅完全执行了四次而不是 10 次。

```cs
// Fig. 6.13: BreakTest.cs
// break 语句退出 for 语句。
using System;
class BreakTest
{
    static void Main() {
        int count; // 循环结束后使用的控制变量
        for (count = 1; count <= 10; ++count) // 循环 10 次
        {
            if (count == 5) // 如果 count 是 5，
                break; // 终止循环
        }
        Console.Write($"{count}");
    }
}
// 输出:
// Broke out of loop at count = 5
```

在 `count = 5` 时跳出循环

**图 6.13** | `break` 语句退出 `for` 语句。

## 6.10.2 continue 语句

当 `continue` 语句在 `while`、`for`、`do...while` 或 `for each` 中执行时，会跳过循环体中的剩余语句并进入循环的下次迭代。在 `while` 和 `do...while` 语句中，程序会在 `continue` 语句后立即评估循环延续。图 14 在 `for` 中使用 `continue` 语句跳过第 16 行（第 11 行）确定 `count` 值为 5 的语句。当 `continue` 语句执行时，程序控制继续语句（第 9 行）中控制变量的增加。

### 软件工程观察

有些程序员认为 `break` 和 `continue` 语句违反了结构化编程。由于结构化技术可以实现相同的效果，程序员倾向于不使用 `break` 或 `continue`。实现高质量软件工程与实现高性能软件之间存在张力。其中一个目标的实现是以另一个为代价的。对于所有最密集的情况，请应用以下规则：首先，让你的代码简单且正确；只有在必要时才使其快速。

![](img/57baed2319be0bb1b5f98674846f2711_255_0.png)

```cs
// Fig. 6.14: ContinueTest.cs
// continue 语句跳过 for 语句的一次迭代
using System;
class ContinueTest {
    static void Main() {
        for (int count = 1; count <= 10; ++count) // 循环 10 次
            if (count == 5) { // 如果 count 是 5
                continue; // 跳过循环中剩余的代码
            }
            Console.Write($"{count}");
    }
}
// 输出:
// 1234678910
// 使用 continue 跳过显示 5
```

图 6.14 | `continue` 语句跳过 `for` 语句的一次迭代。

## 6.11 逻辑运算符

`if...else`、`while`、`do...while` 和 `for` 语句需要一个条件来决定程序的控制流。到目前为止，我们只学习了简单条件，例如 `count < 10`、`sentinelValue` 和 `total > 100`。简单条件用关系运算符 `>`、`<=` 和 `=` 来表达式，相等运算符为 `!=`。每个表达式只测试一个条件。为了在决策过程中测试多个条件，我们在单独的语句中执行，或者嵌套在 `if...else...` 语句中，这需要更复杂的条件来决定程序的控制流。

C# 提供了逻辑运算符，允许通过组合条件形成更复杂的条件。逻辑运算符有 `&&`（布尔与）、`||`（逻辑与）、`|`（布尔或）、`^`（异或或）和 `!`（逻辑取非）。

### 6.11.1 逻辑与 (&&) 运算符

假设我们希望在程序的某个点，在选择特定的执行路径之前，确保两个条件都为真。在这种情况下，我们可以使用 `&&`（逻辑与）运算符，如下：

```cs
if (gender == 'F' && age >= 65) {
    ++seniorFemales;
}
```

该语句包含两个简单条件。条件 `gender == 'F'` 决定一个人是否为女性。条件 `age >= 65` 可能会被评估以判断一个人是否为老年人。如果语句考虑组合条件 `gender == 'F' && age >= 65`，则当且仅当两个条件都为真时它才为真。如果组合条件为真，语句体会将 `seniorFemales` 增加 1。如果其中一个或两个简单条件为假，程序将跳过增加操作。有些程序员发现，当添加冗余括号时，前面的条件更具可读性，例如

```cs
(gender == 'F') && (age >= 65)
```

表 6.15 中的表格总结了 `&&` 运算符。表格显示了 `expression1` 和 `expression2` 的真假值的四种可能组合。这些被称为真值表。C 将所有包含关系运算符、相等运算符或逻辑运算符的表达式求值为 `bool` 值——即真或假。

| expression1 | expression2 | expression1&&expression2 |
|---|---|---|
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

**图 6.15** `&&`（逻辑与）运算符的真值表。

## 6.11.2 逻辑或 (||) 运算符

现在我们希望在选择特定的执行路径之前，确保两个条件中的一个或两者都为真。在这种情况下，我们使用 `||`（逻辑或）运算符，如下所示：

```cs
if (semesterAverage >= 90) || (finalExam >= 90) {
    Console.WriteLine("Grade A");
}
```

该语句包含两个简单条件。条件 `semesterAverage >= 90` 被评估以判断学生是否因为学期表现良好获得 A。条件 `finalExam >= 90` 被评估以判断学生是否获得 A。如果语句考虑组合条件 `(semesterAverage >= 90) || (finalExam >= 90)`，则当其中一个或两个条件为真时，它授予 A。只有当两个简单条件都为假时，才不显示“Grade A”消息。图 6.16 是逻辑或 (`||`) 的真值表。`&&` 运算符的优先级高于 `||` 运算符。

| expression1 | expression2 | expression1||expression2 |
|---|---|---|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

**图 6.16** `||`（逻辑或）运算符真值表。

### 6.11.3 复杂的短路求值

包含 `&&` `||` 运算符的表达式部分只评估到确定条件为真或假为止。因此，表达式 `gender == 'F' && (age >= 65)` 在 `gender` 不等于 `'F'` 时立即停止（即整个表达式为假），仅在 `gender` 等于 `'F'` 时才继续（如果 `age >= 65`，整个表达式可能为真）。这种逻辑与或表达式的特性被称为短路求值。

> 常见编程错误 6.6

在使用运算符 `&&` 的表达式中，一个条件（被称为依赖条件）可能需要另一个条件为真该条件才有意义。依赖条件应该放在另一个之后，否则可能会发生错误。例如，在表达式 `(i = 0) && (10 / i == 2)` 中，第二个条件必须出现在第一个条件之后，否则可能会发生除以零的错误。

`(birthday == true) | ((++age >= 65)`

保证条件 `++age >= 65` 会被求值。变量 `age` 在前面的表达式中增加，无论整个表达式的结果是真还是假。

## 错误预防提示 6.6

为了代码清晰起见，请避免在条件中使用带有副作用的表达式。这些副作用看起来可能很聪明，但会增加理解代码的难度，并可能导致微妙的逻辑错误。

## 6.1.1.5 布尔逻辑异或运算符 (^)

包含逻辑异或 (`^`) 运算符（也称为逻辑异异 运算符）的复杂条件，当且仅当其中一个操作数为真而另一个为假时才为真。如果两个操作数均为真或均为假，则整个条件为假。图 6.17 是布尔逻辑异或运算符的真值表。该运算符也保证求值它的两个操作数。

| expression1 | expression2 | expression1 ^ expression2 |
| --- | --- | --- |
| false | false | false |
| false | true | true |
| true | false | false |
| true | true | false |

**图 6.17** `^`（布尔逻辑异或）运算符真值表。

## 6.11.6 逻辑取反 (!) 运算符

`!`（逻辑取反或非）运算符允许你“反转”条件的含义。与逻辑 `&&`、`|` 和 `^`（这些组合两个条件的二元运算符）不同，逻辑取反运算符是一个一元运算符，它只有一个条件作为操作数。逻辑取反运算符放在条件之前，如果原始条件（不带逻辑取反运算符）为假，则选择特定的执行路径。代码段如下：

```cs
if (!grade == sentinelValue) {
    Console.WriteLine("The next grade is {grade}");
}
```

只有当 `grade` 不等于 `sentinelValue` 时，才会执行 `WriteLine`。条件 `grade == sentinelValue` 周围的括号是必要的，因为逻辑取反运算符的优先级高于相等运算符。

在大多数情况下，你可以通过使用适当的关系运算符或相等运算符来表达条件，避免使用取反。例如，前面的语句也可以写成：

```cs
if (grade != sentinelValue)
    Console.WriteLine($"The next grade is {grade}");
```

这种灵活性可以帮助你用更方便的方式表达条件。图 6.18 是逻辑取反运算符的真值表。

| expression | !expression |
| false | true |
| true | false |

图 6.18 | `!`（逻辑取反）运算符真值表。

## 6.11.7 逻辑运算符示例

图 6.19 通过生成真值表演示了逻辑运算符和布尔运算符。输出包含了被求值的表达式以及该表达式的布尔 结果。第 10–14 行生成 `&&`（条件与）的真值表。第 17–21 行生成 `||`（条件或）的真值表。第 24–28 行生成 `&`（布尔与）的真值表。第 31–35 行生成 `|`（布尔包含或）的真值表。第 38–42 行生成 `^`（布尔异或）的真值表。第 45–47 行生成 `!`（逻辑取反）的真值表。

```cs
// LogicalOperators.cs
// 逻辑运算符。
using System;
class LogicalOperators {
    static void Main() {
        // 为 && (条件与 (&&)) 创建真值表
        Console.WriteLine($"false && false: {false && false}");
        Console.WriteLine($"false && true: {false && true}");
        Console.WriteLine($"true && false: {true && false}");
        Console.WriteLine($"true && true: {true && true}\n");

        // 为 || (条件或 (||)) 创建真值表
        Console.WriteLine("Conditional OR (||)");
        Console.WriteLine($"false || false: {false || false}");
        Console.WriteLine($"false || true: {false || true}");
        Console.WriteLine($"true || false: {true || false}");
        Console.WriteLine($"true || true: {true || true}\n");
    }
}
```

图 6.19 | 逻辑运算符。（第 3 部分。）

```cs
// 为 & (布尔逻辑与) 运算符创建真值表
Console.WriteLine("Boolean logical AND (&)\n");
Console.WriteLine($"false & false: {false & false}\n");
Console.WriteLine($"false & true: {false & true}\n");
Console.WriteLine($"true & false: {true & false}\n");
Console.WriteLine($"true & true: {true & true}\n");
// 为 | (布尔逻辑包含或) 运算符创建真值表
Console.WriteLine("Boolean logical inclusive OR (|)\n");
Console.WriteLine($"false | false: {false | false}\n");
Console.WriteLine($"false | true: {false | true}\n");
Console.WriteLine($"true | false: {true | false}\n");
Console.WriteLine($"true | true: {true | true}\n");
// 为 ^ (布尔逻辑异或) 运算符创建真值表
Console.WriteLine("Boolean logical exclusive OR (^)\n");
Console.WriteLine($"false ^ false: {false ^ false}\n");
Console.WriteLine($"false ^ true: {false ^ true}\n");
Console.WriteLine($"true ^ false: {true ^ false}\n");
Console.WriteLine($"true ^ true: {true ^ true}\n");
// 为 ! (逻辑取反) 运算符创建真值表
Console.WriteLine("Logical negation (!)\n");
Console.WriteLine($"!false: {!false}\n");
Console.WriteLine($"!true: {!true}\n");
```

Conditional AND (&&)

false && false: False

false && true: False

true && false: False

true && true: True

Conditional OR (||)

false || false: False

false || true: True

true || false: True

true || true: True

Boolean logical AND (&)

false & false: False

false & true: False

true & false: False

true & true: True

Boolean logical inclusive OR (|)

false | false: False

false | true: True

true | false: True

true | true: True

Boolean logical exclusive OR (^)

false ^ false: False

图 6.19 逻辑运算符。（部分 2/3。）

## 6.12 结构化编程总结

```cs
false ^ true: True
true ^ false: True
true ^ true: False

逻辑取反 (!)
!false: True
true: False
```

**图 6.19** 逻辑运算符。（部分 3/3。）

**目前介绍的运算符优先级和结合性**

图 6.20 显示了目前介绍的 C# 运算符的优先级和结合性。运算符按优先级从高到低排列。

| Operators | 结合性 | 类型 |
| --- | --- | --- |
| new ++(postfix) --(postfix) | 从左到右 | 最高优先级 |
| ++ -- ! (type) | 从右到左 | 一元前缀 |
| * / % | 从左到右 | 乘法 |
| + | 从左到右 | 加法 |
| < <= >= | 从左到右 | 关系 |
