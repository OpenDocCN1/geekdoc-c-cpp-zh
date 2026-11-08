
## 语法：实际参数列表

实际参数列表的语法是：

```
expression or variable, expression or variable, ...
```

（在此语法中，expression 可以是单个常量值。）因此，要调用有返回值的函数，需使用其名称，并将实际参数（如果有）放在括号中。

函数的形参列表可以为空。然而，如果形参列表为空，仍然需要括号。因此，当形参列表为空时，有返回值函数的函数首部采用以下形式：

```
functionType functionName()
```

如果有返回值函数的形参列表为空，则在函数调用中实际参数也为空。在这种情况下（即形参列表为空），函数调用中仍然需要空括号。因此，对形参列表为空的有返回值函数的调用如下：

```
functionName()
```

在函数调用中，实际参数的数量及其数据类型必须按给定顺序与形式参数匹配。也就是说，实际参数和形式参数一一对应。（本章后面将讨论带默认参数的函数。）

如前所述，有返回值的函数在表达式中调用。该表达式可以是赋值语句或输出语句的一部分，也可以是函数调用中的参数。程序中的函数调用会使被调用函数体执行。

## return 语句

一旦有返回值的函数计算出值，该函数就通过 return 语句返回此值。换句话说，它通过 return 语句将此值传递到函数外部。

### 语法：return 语句

return 语句具有以下语法：

```
return expr;
```

其中 expr 是变量、常量值或表达式。会计算 expr，并返回其值。expr 计算所得值的数据类型必须与函数类型匹配。

在 C++ 中，`return` 是保留字。

当函数中的 return 语句执行时，函数立即终止，控制权返回到调用者。此外，函数调用语句会被 return 语句返回的值替换。当 return 语句在函数 main 中执行时，程序终止。

为了将本讨论中的想法付诸实践，让我们编写一个确定两个数中较大者的函数。由于该函数比较两个数，因此该函数有两个参数，并且这两个参数都是数。假设这些数的数据类型为浮点型（十进制）——例如 double。由于较大的数是 double 类型，因此函数的数据类型也是 double。我们将此函数命名为 larger。完成此函数唯一需要做的就是函数体。因此，按照函数的语法，可以如下编写此函数：

```cpp
double larger(double x, double y)
{
    double max;

    if (x >= y)
        max = x;
    else
        max = y;

    return max;
}
```

注意，函数 larger 使用了一个额外变量 max（称为局部声明，其中 max 是函数 larger 的局部变量）。图 6-2 描述了函数 larger 的各个部分。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_388_0.png)

**图 6-2** 函数 larger 的各个部分

假设 `num`、`num1` 和 `num2` 是 double 变量。还假设 `num1 = 45.75` 且 `num2 = 35.50`。图 6-3 展示了对函数 `larger` 的各种调用。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_389_0.png)

**图 6-3** 函数调用

可以如下编写函数 `larger` 的定义：

```cpp
double larger(double x, double y)
{
    if (x >= y)
        return x;
    else
        return y;
}
```

由于函数中 `return` 语句的执行会终止该函数，因此前面的函数 `larger` 也可以（去掉 `else` 一词）写成：

```cpp
double larger(double x, double y)
{
    if (x >= y)
        return x;

    return y;
}
```

注意，函数 `larger` 的这些形式不要求声明任何局部变量。

- 1. 在函数 `larger` 的定义中，`x` 和 `y` 是形式参数。
- 2. `return` 语句可以出现在函数中的任何位置。回顾一下，一旦 `return` 语句执行，所有后续语句都会被跳过。因此，最好在值计算出来后立即返回该值。

## 示例 6-2

既然函数 larger 已经编写好，以下 C++ 代码说明了如何使用它：

```cpp
double one = 13.00;
double two = 36.53;
double maxNum;
```

考虑以下语句：

```cpp
cout << "The larger of 5 and 6 is " << larger(5, 6)
     << endl;                                      //Line 1

cout << "The larger of " << one << " and " << two
     << " is " << larger(one, two) << endl;       //Line 2

cout << "The larger of " << one << " and 29 is "
     << larger(one, 29) << endl;                   //Line 3

maxNum = larger(38.45, 56.78);                     //Line 4
```

- 第 1 行中的表达式 `larger(5, 6)` 是函数调用，5 和 6 是实际参数。当表达式 `larger(5, 6)` 执行时，5 被复制到 `x`，6 被复制到 `y`。因此，第 1 行中的语句输出 5 和 6 中较大的数。
- 第 2 行中的表达式 `larger(one, two)` 是函数调用。这里，`one` 和 `two` 是实际参数。当表达式 `larger(one, two)` 执行时，`one` 的值被复制到 `x`，`two` 的值被复制到 `y`。因此，第 2 行中的语句输出 one 和 two 中较大的数。
- 第 3 行中的表达式 `larger(one, 29)` 也是函数调用。当表达式 `larger(one, 29)` 执行时，`one` 的值被复制到 `x`，`29` 被复制到 `y`。因此，第 3 行中的语句输出 one 和 29 中较大的数。注意，第一个参数 `one` 是变量，而第二个参数 `29` 是常量值。
- 第 4 行中的表达式 `larger(38.45, 56.78)` 是函数调用。在此调用中，实际参数是 38.45 和 56.78。在此语句中，函数 larger 返回的值被赋给变量 `maxNum`。

> **注意：** 在函数调用中，只需指定实际参数，而不指定其数据类型。例如，在示例 6-2 中，第 1、2、3 和 4 行中的语句展示了如何使用实际参数调用函数 larger。然而，以下语句包含对函数 larger 的不正确调用，会导致语法错误。（假设所有变量都已正确声明。）

```cpp
x = larger(int one, 29);          //illegal
y = larger(int one, int 29);      //illegal
cout << larger(int one, int two); //illegal
```

一旦函数编写完成，就可以在程序中的任何位置使用它。函数 `larger` 比较两个数并返回两者中较大的数。现在让我们编写另一个函数，它使用此函数来确定三个数中的最大者。我们将此函数称为 `compareThree`。

```cpp
double compareThree(double x, double y, double z)
{
    return larger(x, larger(y, z));
}
```

在函数首部中，x、y 和 z 是形式参数。

让我们看一下表达式：

```
larger(x, larger(y, z))
```

它位于函数 compareThree 的定义中。此表达式包含两次对函数 larger 的调用。外部调用的实际参数是 x 和 larger(y, z)；内部调用的实际参数是 y 和 z。由此可知，首先计算表达式 larger(y, z)；也就是说，内部调用先执行，得到 y 和 z 中较大的数。假设 larger(y, z) 的计算结果为 t。（注意，t 是 y 或 z。）接下来，外部调用确定 x 和 t 中较大的数。最后，return 语句返回最大的数。因此可知，要执行函数调用，首先会计算参数。例如，外部调用的实际参数 larger(y, z) 会先计算。

注意，函数 larger 比函数 compareThree 通用得多。这里，我们只是说明：一旦编写好一个函数，就可以使用它来编写其他函数。本章后面将展示如何使用函数 larger 从一组数中确定最大数。

## 函数原型

现在你已经对如何在程序中编写和使用函数有了一些了解，下一个问题涉及用户自定义函数在程序中应出现的顺序。例如，你是将函数 larger 放在函数 main 之前还是之后？larger 应放在 compareThree 之前还是之后？遵循“必须先声明标识符才能使用它”的规则，并且知道函数 main 使用了标识符 larger，从逻辑上讲，必须将 larger 放在 main 之前。

实际上，C++ 程序员通常将函数 main 放在所有其他用户自定义函数之前。然而，这种组织方式可能产生编译器错误，因为函数是按照它们在程序中出现的顺序编译的。例如，如果将函数 main 放在函数 larger 之前，那么在编译函数 main 时，标识符 larger 是未定义的。为了解决未声明标识符的问题，我们将**函数原型**放在任何函数定义（包括 main 的定义）之前。

**函数原型：** 不带函数体的函数首部。
