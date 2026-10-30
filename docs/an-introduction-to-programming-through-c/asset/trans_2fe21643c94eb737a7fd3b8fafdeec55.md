

坐标必须小于或等于，右侧边缘坐标必须大于或等于。并且我们也必须相应地检查 y 坐标。

该程序只允许 100 次点击；我们稍后会看到如何使循环无限运行或在满足某些条件时停止。

## 6.5 switch 语句

在海龟控制程序中，有一个单一变量 command，根据它我们采取不同的动作。类似的情况在许多程序中都会出现。因此 C++ 提供了 switch 语句，以便我们可以简洁地表达我们的代码。switch 语句的一般形式为：

```
switch (expression){
    case constant1:
        group(1) of statements usually ending with break;
    case constant2:
        group(2) of statements usually ending with break;
    ...
    default:
        default-group of statements
}
```

由 `default:` 及其后的一组语句构成的部分是可选的。表达式 `expression` 必须是 int 类型。此外，上面的每个 `constant_i` 都必须是整数常量。

语句的执行方式如下。首先计算表达式。如果该值与某个 i 的 `constant_i` 完全相同，则我们开始执行 group(i) 语句。我们执行 group(i) 语句，然后执行 group(i+1) 语句，依此类推，包括 default-group 语句，除非我们遇到 `break;` 语句。如果我们遇到 `break`，则 switch 的执行完成，即我们不执行 break 之后的语句，而是直接进入 switch 语句之后程序中的语句。如果表达式的值与提到的任何常量值不同，则执行 default-group 语句。

如果某个 group(i) 没有以 break 结束，则执行会“贯穿”到下一个组。贯穿的情况被认为很少见。

使用 switch，我们的海龟控制程序可以写成如下形式。

```
main_program{
    char command;
    turtleSim();

    repeat(100){
        cin >> command;
        switch(command){
            case 'f': forward(100);
                break;
            case 'r': right(90);
                break;
            case 'l': left(90);
                break;
            default: cout << "Not a proper command, " << command << endl;
        }
    }
}
```

正如你所见，新程序更易于阅读。

下面是一个有贯穿的例子。假设我们想打印一年中第 n 个月的天数，将 n 作为输入。这里是程序。

```
main_program{
    int month;
    cin >> month;
    switch(month){
        case 1: // January
        case 3: // March
        case 5: // May
        case 7: // July
        case 8: // August
        case 10: // October
        case 12: // December
            cout << "This month has 31 days.\n";
            break;
        case 2: // February
            cout << "This month has 28 or 29 days.\n";
            break;
        case 4: // April
        case 6: // June
        case 9: // September
        case 11: // November
            cout << "This month has 30 days.\n";
            break;
        default: cout << "Invalid input.\n";
    }
}
```

假设输入为 5。那么执行将从标记为 `case 5:` 的点之后开始。它将贯穿 case 5、7、8、10 到 case 12。在这种情况下，天数将被打印为 31，然后遇到 break。这将完成 switch 的执行。

switch 语句被认为有点容易出错，因为你可能会忘记写 `break;`。所以要小心。

## 6.6 条件表达式

C++ 有一种 *条件表达式* 的概念，具有以下形式。

```
condition ? consequent-expression : alternate-expression
```

其求值过程如下。首先计算条件。如果为真，则计算 consequent-expression，并且该值就是整个表达式的值。alternate-expression 被忽略。另一方面，如果条件求值为假，则 consequent-expression 被忽略，alternate-expression 被计算，其结果值就是整个表达式的值。

这里有一些简单的例子。

```
int marks; cin >> marks;
int actualmarks = (marks > 100) ? 100 : marks;
char grade = (marks >= 35) ? 'p' : 'f';
```

在此，如果读取的 marks 大于 100，则 actualmarks 将被限制为 100，否则 actualmarks 将被设为等于 marks。此外，如果 marks 至少为 35，则 grade 被设为 'p'（通过），否则为 'f'（失败）。

条件表达式可以嵌套，即 consequent 或 alternate 表达式本身也可以是条件表达式。这使我们能够编写一个非常紧凑但难以阅读的税收计算程序。

```
main_program{
    float income; cin >> income;

    cout << (
        income <= 180000 ? 0 :
        income <= 500000 ? (income - 180000) * 0.1 :
        income <= 800000 ? 32000 + (income - 500000) * 0.2 :
        92000 + (income - 800000) * 0.3
    )
    << endl;
}
```

我们只是读取收入，然后将税作为表达式计算并直接打印出来，而不将其存储到变量中。在上面，标记为 `**` 的括号是必要的。这是因为运算符 `<<` 的优先级高于运算符 `<=`，即默认情况下 C++ 尝试先执行 `<<` 再执行 `<=`。

上面的程序非常紧凑，但不推荐。大多数程序员会认为它难以阅读。然而，不带嵌套的条件表达式被认为是有用的构造。

## 6.7 逻辑数据

if 语句的一个重要部分是条件。我们已经看到条件要么为真要么为假，即我们可以将值 true 或值 false 与每个条件关联。我们还看到条件可以以不同的方式组合。 resulting 组合也将为真或为假。我们还看到用相同的条件可以有几种等价的写法（正如我们在第一个程序的第二个 if 语句中所看到的）。从这个意义上说，条件类似于数值表达式，数值表达式有一个值，数值表达式可以组合成更大的数值表达式，我们可以有等价的数值表达式。在这种情况下，为什么不把条件当作另一种类型的数据呢？这被证明是一个非常好的想法，并且由 George Boole 在 1840 年开发了一种用于操作条件的代数，或我们此后将称之为逻辑表达式的代数。C++ 支持逻辑数据的操作和存储，并且为了纪念 Boole，用于存储逻辑数据的数据类型命名为 bool。你已经在第 3 章中看到过这种数据类型，现在我们将用它做更有趣的事情。

首先我们注意到我们可以将逻辑表达式的值赋给 bool 变量。考虑以下代码。

```
float income; cin >> income;
bool lowIncome, midIncome, highIncome;
lowIncome = (income <= 180000);
midIncome = (income > 180000) && (income <= 800000);
highIncome = (income > 800000);
```

假设在执行期间为 income 给出值 200000。那么在执行后续语句之后，变量 lowIncome、midIncome、highIncome 将分别具有值 false、true、false。

正如你所见，上述赋值语句的右手边是条件，并且这些条件所具有的任何值都将被放入相应的左手边变量中。

作为另一个例子，让我们定义一个 bool 变量，如果从 cin 读取的字符恰好是小写字符，则为真。请注意，这将发生在字符的 ASCII 值至少为 'a' 且最多为 'z' 时。因此此代码可以为

```
char in_ch;
bool lowerCase;
cin >> in_ch;
lowerCase = (in_ch >= 'a') && (in_ch <= 'z');
```

我们接下来将考虑一个更复杂的程序，该程序确定给定的数字 num 是否为质数或合数。在此程序中，能够存储逻辑值将很有用。为了理解该程序，我们需要对包含逻辑数据的表达式进行推理。因此我们首先讨论这一点。

### 6.7.1 关于逻辑数据的推理

正如我们之前讨论的，相同的条件可以用多种方式表达。理解哪些表达式是等价的非常重要。

首先，让我们做一些简单的观察。对于任何逻辑值 v，我们有 `v || false` 与 v 具有相同的值。检查此的最简单方法是尝试所有可能性：

