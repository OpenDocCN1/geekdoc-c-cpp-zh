
## 复合语句（语句块）

`if` 和 `if...else` 结构一次只控制一条语句。然而，假设当 `if` 或 `if...else` 语句中的表达式求值为 `true` 时，你希望执行多条语句。为了允许更复杂的语句，C++ 提供了一种称为**复合语句**或**语句块**的结构。复合语句采用以下形式：

```text
{
    statement_1
    statement_2
        .
        .
        .
    statement_n
}
```

也就是说，复合语句由一系列用花括号 `{` 和 `}` 括起来的语句组成。在 `if` 或 `if...else` 结构中，复合语句的作用就像单条语句一样。因此，与其像下面代码那样使用简单的双向选择：

```cpp
if (age >= 18)
    cout << "Eligible to vote." << endl;
else
    cout << "Not eligible to vote." << endl;
```

你可以包含复合语句，类似下面的代码：

```cpp
if (age >= 18)
{
    cout << "Eligible to vote." << endl;
    cout << "No longer a minor." << endl;
}
else
{
    cout << "Not eligible to vote." << endl;
    cout << "Still a minor." << endl;
}
```

复合语句非常有用，本章中大多数结构化语句都会用到它。

## 多重选择：嵌套 `if`

在前面的章节中，你学习了如何在程序中实现单向和双向选择。有些问题需要实现两个以上的备选方案。例如，假设如果支票账户余额超过 $50,000，利率为 7%；如果余额在 $25,000 到 $49,999.99 之间，利率为 5%；如果余额在 $1,000 到 $24,999.99 之间，利率为 3%；否则，利率为 0%。这个特定问题有四个备选方案——也就是多条选择路径。如果操作语句本身是 `if` 或 `if...else` 语句，你可以使用 `if...else` 结构在程序中包含多条选择路径。当一个控制语句位于另一个控制语句内部时，就称其为**嵌套**。

例 4-15 说明了如何使用嵌套 `if...else` 结构来实现多重选择。

### 例 4-15

假设 `balance` 和 `interestRate` 是 `double` 类型的变量。以下语句根据 `balance` 的值确定 `interestRate`。

```
if (balance > 50000.00)                 //Line 1
    interestRate = 0.07;                //Line 2
else                                    //Line 3
    if (balance >= 25000.00)            //Line 4
        interestRate = 0.05;            //Line 5
    else                                //Line 6
        if (balance >= 1000.00)         //Line 7
            interestRate = 0.03;        //Line 8
        else                            //Line 9
            interestRate = 0.00;        //Line 10
```

嵌套的 `if...else` 结构要求回答一个重要问题：如何知道哪个 `else` 与哪个 `if` 配对？回想一下，在 C++ 中，不存在独立的 `else` 语句。每个 `else` 都必须与一个 `if` 配对。将 `else` 与 `if` 配对的规则如下：

**将 `else` 与 `if` 配对：** 在嵌套 `if` 语句中，C++ 会将 `else` 与最近一个尚未完成的 `if` 关联起来——也就是说，与最近一个尚未与 `else` 配对的 `if` 关联。

使用这条规则，在例 4-15 中，第 3 行的 `else` 与第 1 行的 `if` 配对。第 6 行的 `else` 与第 4 行的 `if` 配对，第 9 行的 `else` 与第 7 行的 `if` 配对。

为避免过度缩进，例 4-15 中的代码可以改写如下：

```
if (balance > 50000.00)             //Line 1
    interestRate = 0.07;            //Line 2
else if (balance >= 25000.00)       //Line 3
    interestRate = 0.05;            //Line 4
else if (balance >= 1000.00)        //Line 5
    interestRate = 0.03;            //Line 6
else                                //Line 7
    interestRate = 0.00;            //Line 8
```

以下示例将帮助你了解使用嵌套 `if` 结构实现多重选择的各种方式。

在这段代码中，第 4 行的 `else` 与第 2 行的 `if` 配对。注意，对于第 4 行的 `else`，最近一个尚未完成的 `if` 位于第 2 行。在这段代码中，第 1 行的 `if` 没有 `else`，是一个单向选择。再一次说明，缩进并不决定配对关系，但它传达配对关系。

### 例 4-19

假设所有变量都已正确声明，并考虑以下语句：

```cpp
if (gender == 'M')                 //Line 1
    if (age < 21)                  //Line 2
        policyRate = 0.05;         //Line 3
    else                           //Line 4
        policyRate = 0.035;        //Line 5
else if (gender == 'F')            //Line 6
    if (age < 21)                  //Line 7
        policyRate = 0.04;         //Line 8
    else                           //Line 9
        policyRate = 0.03;         //Line 10
```

在这段代码中，第 4 行的 `else` 与第 2 行的 `if` 配对。注意，对于第 4 行的 `else`，最近一个尚未完成的 `if` 是第 2 行的 `if`。第 6 行的 `else` 与第 1 行的 `if` 配对。第 9 行的 `else` 与第 7 行的 `if` 配对。再一次说明，缩进并不决定配对关系，但它传达配对关系。

## 将 `if...else` 语句与一系列 `if` 语句进行比较

考虑以下 C++ 程序段，它们都完成相同的任务。

```cpp
a.  if (month == 1)                         //Line 1
        cout << "January" << endl;          //Line 2
    else if (month == 2)                    //Line 3
        cout << "February" << endl;         //Line 4
    else if (month == 3)                    //Line 5
        cout << "March" << endl;            //Line 6
    else if (month == 4)                    //Line 7
        cout << "April" << endl;            //Line 8
    else if (month == 5)                    //Line 9
        cout << "May" << endl;              //Line 10
    else if (month == 6)                    //Line 11
        cout << "June" << endl;             //Line 12

b.  if (month == 1)
        cout << "January" << endl;
    if (month == 2)
        cout << "February" << endl;
    if (month == 3)
        cout << "March" << endl;
    if (month == 4)
        cout << "April" << endl;
    if (month == 5)
        cout << "May" << endl;
    if (month == 6)
        cout << "June" << endl;
```

程序段 (a) 写成一系列 `if...else` 语句；程序段 (b) 写成一系列 `if` 语句。两个程序段完成相同的事情。如果 month 为 3，那么两个程序段都输出 March。如果 month 为 1，那么在程序段 (a) 中，第 1 行 `if` 语句中的表达式求值为 `true`。随后执行与该 `if` 关联的语句（第 2 行）；该结构的其余部分，也就是这个 `if` 语句的 `else`，被跳过；其余的 `if` 语句不会被求值。在程序段 (b) 中，由于没有 `else` 语句，计算机必须对每个 `if` 语句中的表达式求值。因此，程序段 (b) 的执行速度比程序段 (a) 慢。

## 短路求值

C++ 中的逻辑表达式使用一种非常高效的算法进行求值。下面的语句说明了该算法：

```cpp
(x > y) || (x == 5)      //Line 1
(a == b) && (x >= 7)     //Line 2
```

在第 1 行的语句中，运算符 `||` 的两个操作数是表达式 `(x > y)` 和 `(x == 5)`。如果操作数 `(x > y)` 为 `true`，或者操作数 `(x == 5)` 为 `true`，则该表达式求值为 `true`。使用短路求值时，计算机会从左到右对逻辑表达式求值。一旦整个逻辑表达式的值已知，求值就会停止。例如，在语句 1 中，如果操作数 `(x > y)` 求值为 `true`，那么整个表达式求值为 `true`，因为 `true || true` 为真，且 `true || false` 为真。因此，操作数 `(x == 5)` 的值与最终结果无关。

类似地，在第 2 行的语句中，运算符 `&&` 的两个操作数是 `(a == b)` 和 `(x >= 7)`。如果操作数 `(a == b)` 求值为 `false`，那么整个表达式求值为 `false`，因为 `false && true` 为假，且 `false && false` 为假。

**短路求值**（针对逻辑表达式）：计算机从左到右对逻辑表达式求值，并一旦表达式的值已知就停止的过程。

### 例 4-20

考虑以下表达式：

```cpp
(age >= 21) || ( x == 5)       //Line 1
(grade == 'A') && (x >= 7)     //Line 2
```

