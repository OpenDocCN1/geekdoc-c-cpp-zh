

## 显示 2.8 循环中的 break 语句

```
#include <iostream>
using namespace std;

int main()
{
    int number, sum = 0, count = 0;
    cout << "Enter 4 negative numbers:\n";

    while (++count <= 4)
    {
        cin >> number;

        if (number >= 0)
        {
            cout << "ERROR: positive number"
                 << " or zero was entered as the "
                 << count << "th number! Input ends "
                 << "with the " << count << "th number.\n"
                 << count << "th number was not added in.\n";
            break;
        }

        sum = sum + number;
    }

    cout << sum << " is the sum of the first "
         << (count - 1) << " numbers.\n";

    return 0;
}
```

### 示例对话

Enter 4 negative numbers:
-1 -2 3 -4
ERROR: positive number or zero was entered as the
3rd number! Input ends with the 3rd number.
3rd number was not added in
-3 is the sum of the first 2 numbers.

## 显示 2.9 循环中的 continue 语句

```
#include <iostream>
using namespace std;

int main()
{
    int number, sum = 0, count = 0;
    cout << "Enter 4 negative numbers, ONE PER LINE:\n";

    while (count < 4)
    {
        cin >> number;

        if (number >= 0)
        {
            cout << "ERROR: positive number (or zero)!\n" << "Reenter that number and continue:\n";
            continue;
        }

        sum = sum + number;
        count++;
    }

    cout << sum << " is the sum of the " << count << " numbers.\n";
    return 0;
}
```

### 示例对话

Enter 4 negative numbers, ONE PER LINE:
1
ERROR: positive number (or zero)!
Reenter that number and continue:
-1
-2
3
ERROR: positive number!
Reenter that number and continue:
-3
-4
-10 is the sum of the 4 numbers.

请注意，你永远也不绝对需要 break 或 continue 语句。显示 2.8 和 2.9 中的程序可以重写，使其既不使用 break 也不使用 continue 语句。continue 语句尤其棘手，可能使你的代码难以阅读。最好完全避免使用 continue 语句，或者至少只在极少数情况下使用它。

## 嵌套循环

将一个循环语句嵌套在另一个循环语句内部是完全合法的。进行此操作时，请记住，任何 break 或 continue 语句都适用于包含该 break 或 continue 语句的最内层循环（或 switch）语句。最好通过将内层循环放在函数定义中，并在外层循环中放置函数调用来避免嵌套循环。函数将在第 3 章中介绍。

## 自测练习

- 36. break 语句做什么？在哪里合法放置 break 语句？
- 37. 预测以下嵌套循环的输出：

```
int n, m;
for (n = 1; n <= 10; n++)
  for (m = 10; m >= 1; m--)
    cout << n << " times " << m
         << " = " << n*m << endl;
```

## 章节总结

- 布尔表达式的求值方式与算术表达式的求值方式相似。
- C++ 的分支语句是 if-else 语句和 switch 语句。
- switch 语句是多路分支语句。你也可以通过嵌套 if-else 语句形成多路 if-else 语句来形成多路分支语句。
- switch 语句是为你的程序用户实现菜单的好方法。
- 循环可以用 `break` 语句提前结束。循环体的单次迭代可以用 `continue` 语句提前结束。最好谨慎使用 `break` 语句。最好完全避免使用 `continue` 语句，尽管一些程序员在极少数情况下确实会使用它们。

## 自测练习答案

- 1. a. **true.**
- b. **true.** 请注意表达式 `a` 和 `b` 完全相同。因为运算符 `==` 和 `<` 的优先级高于 `&&`，所以你不需要包含括号。括号确实使阅读更容易。大多数人会发现 `a` 中的表达式比 `b` 中的表达式更容易阅读，即使它们含义相同。
- c. **true.**
- d. **true.**
- e. **false.** 由于第一个子表达式 `(count == 1)` 的值为 false，你就知道整个表达式为 false，而无需费心求值第二个子表达式。因此，`x` 和 `y` 的值无关紧要。这是 *短路求值*。
- f. **true.** 由于第一个子表达式 `(count < 10)` 的值为 true，你就知道整个表达式为 true，而无需费心求值第二个子表达式。因此，`x` 和 `y` 的值无关紧要。这是 *短路求值*。
- g. **false.** 请注意，`g` 中的表达式包含 `f` 中的表达式作为子表达式。此子表达式使用我们对 `f` 描述的短路求值进行求值。`g` 中的整个表达式等价于：

```text
!((true || (x < y)) && true)
```

而它又等价于 `!(true && true)`，而后者等价于 `!(true)`，最终值为 **false**。

- h. 求值此表达式时会产生错误，因为第一个子表达式 `((limit/count) > 7)` 涉及除零。
- i. **true.** 由于第一个子表达式 `(limit < 20)` 的值为 true，你就知道整个表达式为 true，而无需费心求值第二个子表达式。因此，第二个子表达式

```text
((limit/count) > 7)
```

永远不会被求值，所以它涉及除零的事实永远不会被计算机注意到。这是 *短路求值*。
- j. 求值此表达式时会产生错误，因为第一个子表达式 `((limit/count) > 7)` 涉及除零。
- k. false. 由于第一个子表达式 `(limit < 0)` 的值为 false，你就知道整个表达式为 false，而无需费心求值第二个子表达式。因此，第二个子表达式

`((limit/count) > 7)`

永远不会被求值，所以它涉及除零的事实永远不会被计算机注意到。这是短路求值。

- l. 如果你认为此表达式毫无意义，你是对的。该表达式没有直观的含义，但 C++ 将 int 值转换为 bool，然后求值 `&&` 和 `!` 操作。因此，C++ 会求值这个混乱的东西。回想一下，在 C++ 中，任何非零整数都转换为 true，而 0 转换为 false，所以 C++ 会按如下方式求值

`(5 && 7) + (!6)`

在表达式 `(5 && 7)` 中，5 和 7 转换为 true；`true && true` 求值为 true，C++ 将其转换为 1。在表达式 `(!6)` 中，6 转换为 true，所以 `!` (true) 求值为 false，C++ 将其转换为 0。因此，整个表达式求值为 `1 + 0`，即 1。最终值因此为 1。C++ 会将数字 1 转换为 true，但作为 true 的答案几乎没有直观意义；最好只说答案是 1。没有必要熟练求值这些无意义的表达式，但做几个可以帮助你理解为什么编译器在你犯下在单个表达式中混合数值和布尔运算符的错误时不会给出错误消息。

- 2. 表达式 `2 < x < 3` 是合法的。然而，它并不意味着

`(2 < x) && (x < 3)`

正如许多人所希望的那样。它意味着 `(2 < x) < 3`。由于 `(2 < x)` 是一个布尔表达式，其值是 true 或 false，因此转换为 0 或 1，而两者都小于 3。所以，`2 < x < 3` 总是 true。结果与 x 的值无关，始终为 true。

- 3. `(x < −1 || (x > 2)`
- 4. `(x > 1 && (x < 3)`
- 5. 不会。在布尔表达式中，`(j > 0)` 为 false（`j` 刚刚被赋值为 −1）。`&&` 使用短路求值，如果可以根据第一个表达式确定真值，则不会求值第二个表达式。第一个表达式为 false，所以第二个无关紧要。
- 6. 如果 `(score > 100)`

```cpp
cout << "High";
else
    cout << "Low";
```

你可能想在上述引用的字符串末尾添加 `\n`，这取决于程序的其他细节。

