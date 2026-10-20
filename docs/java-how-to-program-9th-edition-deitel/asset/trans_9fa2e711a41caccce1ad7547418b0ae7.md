
或者在嵌套的 if 或 if...else 语句中。有时控制语句需要更复杂的条件来确定程序的控制流。

Java 的逻辑运算符使您能够通过组合简单条件来形成更复杂的条件。逻辑运算符包括 &&（条件与）、||（条件或）、&（布尔逻辑与）、|（布尔逻辑或）、^（布尔逻辑异或）和 !（逻辑非）。[注意：&、| 和 ^ 运算符在应用于整型操作数时也是位运算符。我们在附录 N 中讨论位运算符。]

## 条件与（&&）运算符

假设我们希望确保在程序中某个时刻两个条件都为真，然后才选择某条执行路径。在这种情况下，我们可以使用 &&（条件与）运算符，如下所示：

```
if ( gender == FEMALE && age >= 65 )
    ++seniorFemales;
```

这个 if 语句包含两个简单条件。条件 `gender == FEMALE` 将变量 gender 与常量 FEMALE 进行比较，以确定一个人是否为女性。条件 `age >= 65` 可能被求值以确定一个人是否为老年人。if 语句考虑组合条件

```
gender == FEMALE && age >= 65
```

当且仅当两个简单条件都为真时，该组合条件才为真。在这种情况下，if 语句体将 seniorFemales 递增 1。如果其中一个或两个简单条件为假，程序将跳过该递增操作。有些程序员发现，添加冗余括号后，上述组合条件更具可读性，如下所示：

```
( gender == FEMALE ) && ( age >= 65 )
```

图 5.14 中的表格总结了 && 运算符。该表显示了 expression1 和 expression2 的 false 和 true 值的所有四种可能组合。这样的表称为真值表。Java 对包含关系运算符、相等运算符或逻辑运算符的所有表达式求值为 false 或 true。

| 表达式1 | 表达式2 | 表达式1 && 表达式2 |
|---|---|---|
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

图 5.14 | &&（条件与）运算符真值表。

## 条件或（||）运算符

现在假设我们希望确保在执行某条路径之前，两个条件中的一个或两个为真。在这种情况下，我们使用 ||（条件或）运算符，如下面的程序片段所示：

```
if ( ( semesterAverage >= 90 ) || ( finalExam >= 90 ) )
    System.out.println( "Student grade is A" );
```

该语句也包含两个简单条件。条件 `semesterAverage >= 90` 的求值用于确定学生是否因为整个学期的扎实表现而在课程中获得 A。条件 `finalExam >= 90` 的求值用于确定学生是否因为期末考试中的出色表现而在课程中获得 A。然后 if 语句考虑组合条件

```
( semesterAverage >= 90 ) || ( finalExam >= 90 )
```

如果两个简单条件中的一个或两个为真，则授予学生 A。只有两个简单条件都为假时，才不打印消息 "Student grade is A"。图 5.15 是条件或（||）运算符的真值表。运算符 && 的优先级高于运算符 ||。这两个运算符都从左到右结合。

| 表达式1 | 表达式2 | 表达式1 || 表达式2 |
|---|---|---|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

图 5.15 | ||（条件或）运算符真值表。

## 复杂条件的短路求值

包含 && 或 || 运算符的表达式的各部分仅被求值到已知条件为真或为假为止。因此，表达式

```
( gender == FEMALE ) && ( age >= 65 )
```

如果 gender 不等于 FEMALE（即整个表达式为假），则立即停止；如果 gender 等于 FEMALE（即如果条件 age >= 65 为真，整个表达式仍可能为真），则继续求值。条件与和条件或表达式的这种特性称为短路求值。

## 常见编程错误 5.7

> 在使用运算符 && 的表达式中，一个条件——我们称之为依赖条件——可能需要另一个条件为真，依赖条件的求值才有意义。在这种情况下，依赖条件应放在另一个条件之后，否则可能会发生错误。例如，在表达式 ( 1 != 0 ) && ( 10 / i == 2 ) 中，第二个条件必须出现在第一个条件之后，否则可能会发生除以零的错误。

## 布尔逻辑与（&）和布尔逻辑或（|）运算符

布尔逻辑与（&）和布尔逻辑或（|）运算符与 && 和 || 运算符相同，只是 & 和 | 运算符总是对两个操作数进行求值（即它们不执行短路求值）。因此，表达式

```
( gender == 1 ) & ( age >= 65 )
```

无论 gender 是否等于 1，都会对 age >= 65 进行求值。如果布尔逻辑与或布尔逻辑或运算符的右操作数具有必需的副作用——修改变量的值——这将非常有用。例如，表达式

```
( birthday == true ) | ( ++age >= 65 )
```

保证条件 `++age >= 65` 会被求值。因此，无论整个表达式为真还是假，变量 age 都会被递增。

## 防错提示 5.6

> 为了清晰起见，避免在条件中使用带副作用的表达式。副作用可能看起来很巧妙，但会使代码更难理解，并可能导致微妙的逻辑错误。

## 布尔逻辑异或（^）

包含布尔逻辑异或（^）运算符的简单条件，当且仅当其一个操作数为真而另一个为假时为真。如果两个都为真或两个都为假，则整个条件为假。图 5.16 是布尔逻辑异或（^）运算符的真值表。该运算符保证对两个操作数都进行求值。

| 表达式1 | 表达式2 | 表达式1 ^ 表达式2 |
|---|---|---|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | false |

图 5.16 | ^（布尔逻辑异或）运算符真值表。

## 逻辑非（!）运算符

!（逻辑非，也称为逻辑否定或逻辑补）运算符会“反转”条件的含义。与逻辑运算符 &&、||、&、| 和 ^ 不同，这些运算符是组合两个条件的二元运算符，而逻辑非运算符是一元运算符，只有一个条件作为操作数。该运算符放在条件之前，以便在原始条件（不带逻辑非运算符）为假时选择某条执行路径，如以下程序片段所示：

```
if ( ! ( grade == sentinelValue ) )
    System.out.printf( "The next grade is %d\n", grade );
```

只有当 grade 不等于 sentinelValue 时，才会执行 printf 调用。条件 `grade == sentinelValue` 周围的括号是必需的，因为逻辑非运算符的优先级高于相等运算符。

在大多数情况下，您可以通过使用适当的关系运算符或相等运算符以不同方式表达条件来避免使用逻辑非。例如，前面的语句也可以写成如下形式：

```
if ( grade != sentinelValue )
    System.out.printf( "The next grade is %d\n", grade );
```

这种灵活性可以帮助您以更方便的方式表达条件。图 5.17 是逻辑非运算符的真值表。

| 表达式 | !表达式 |
|---|---|
| false | true |
| true | false |

图 5.17 | !（逻辑否定，或逻辑非）运算符真值表。

## 逻辑运算符示例

图 5.18 使用逻辑运算符生成本节讨论的真值表。输出显示了被求值的布尔表达式及其结果。我们使用 %b 格式说明符根据布尔表达式的值显示单词“true”或“false”。第 9–13 行生成 && 的真值表。第 16–20 行生成 || 的真值表。第 23–27 行生成 & 的真值表。第 30–35 行生成 | 的真值表。第 38–43 行生成 ^ 的真值表。第 46–47 行生成 ! 的真值表。

```
1  // Fig. 5.18: LogicalOperators.java
2  // Logical operators.
3
4  public class LogicalOperators
5  {
6      public static void main( String[] args )
7      {
8          // create truth table for && (conditional AND) operator
9          System.out.printf( "%s\n%s: %b\n%s: %b\n%s: %b\n%s: %b\n\n",
10             "Conditional AND (&&)", "false && false", ( false && false ),
11             "false && true", ( false && true ),
12             "true && false", ( true && false ),
13             "true && true", ( true && true ) );
14
15          // create truth table for || (conditional OR) operator
16          System.out.printf( "%s\n%s: %b\n%s: %b\n%s: %b\n%s: %b\n\n",
17             "Conditional OR (||)", "false || false", ( false || false ),
18             "false || true", ( false || true ),
19             "true || false", ( true || false ),
20             "true || true", ( true || true ) );
21
22          // create truth table for & (boolean logical AND) operator
23          System.out.printf( "%s\n%s: %b\n%s: %b\n%s: %b\n%s: %b\n\n",
24             "Boolean logical AND (&)", "false & false", ( false & false ),
25             "false & true", ( false & true ),
26             "true & false", ( true & false ),
27             "true & true", ( true & true ) );
28
29          // create truth table for | (boolean logical inclusive OR) operator
30          System.out.printf( "%s\n%s: %b\n%s: %b\n%s: %b\n%s: %b\n\n",
31             "Boolean logical inclusive OR (|)",
```
