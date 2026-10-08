

(birthday == true) | ((++age >= 65)
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

**图 6.17** ^（布尔逻辑异或）运算符真值表。

## 6.11.6 逻辑取反 (!) 运算符

!`（逻辑取反或非）运算符允许你“反转”条件的含义。与逻辑 `&&`、`|` 和 `^`（这些组合两个条件的二元运算符）不同，逻辑取反运算符是一个一元运算符，它只有一个条件作为操作数。逻辑取反运算符放在条件之前，如果原始条件（不带逻辑取反运算符）为假，则选择特定的执行路径。代码段如下：

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

图 6.18 | !（逻辑取反）运算符真值表。

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
| == != | 从左到右 | 相等 |
| & | 从左到右 | 布尔逻辑与 |
| ^ | 从左到右 | 布尔逻辑异或 |
| | 从左到右 | 布尔逻辑包含或 |
| && | 从左到右 | 条件与 |
| || | 从左到右 | 条件或 |
| ?: += /= % | 从右到左 | 条件赋值 |

图 6.20 已介绍运算符的优先级和结合性。

## 6.12 结构化编程总结

正如建筑师通过利用行业的集体智慧进行设计一样，程序员设计应用也应该如此。我们的领域比建筑年轻，我们的集体智慧正在快速成长。我们了解到结构化编程产生的应用比非结构化应用更容易理解、测试、调试、修改，甚至在数学意义上证明正确。

**控制语句是单入口/单出口**
图 6.21 使用 UML 活动图总结了 C# 控制语句。初始和结束状态表示每个控制语句的单一入口点和单一出口点。随意连接活动图中的符号会导致非结构化应用。因此，一组有限的控制语句可以通过两种简单的方式组合来构建结构化应用。

