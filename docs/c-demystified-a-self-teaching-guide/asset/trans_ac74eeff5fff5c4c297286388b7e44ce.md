
循环的第十次迭代，执行顺序如下：

- 1. 将 num 的当前值 10 与 10 进行比较。
- 2. 由于比较结果为真（10 小于或等于 10），输出 num 的当前值 10。
- 3. num 的值加1，将 num 的当前值 11 与 10 进行比较。由于比较结果为假（11 不小于或等于 10），循环结束。`for` 循环内部的代码不再执行，num 的值不再加1，并开始执行 `for` 循环之后的代码。在这个示例中，`for` 循环之后的代码是 `return 0;` 语句，因此程序结束。

之前的示例使用了递增运算符。然而，你也可以使用递减运算符。将括号和关键字改为 `(int num = 10; num >= 1; num--)` 将导致 1 到 10 之间的数字按倒序输出：注意关系运算符已从 `>` 更改为 `>=`。

在 1 到 10 之间的输出示例中，只有一个语句属于循环。然而，与结构相同，如果有多个语句属于 `for` 循环，这些语句必须包含在花括号内。

```cpp
for (int num = 1; num < 10; num++) {
    cout << num << " ";
    cout << "Next loop ";
}
```

同样，与结构相同，如果括号后面跟着一个分号，且该分号被解释为空语句，那么关键字和后面的语句将不会执行。因此，在下面的代码段中，只有对应的数字会被输出：

```cpp
for (int num = 1; num <= 10; num++)
    cout << num << " ";
```

如果循环继续，结果将是 11，因为空语句会执行，直到 `num` 为 11 时条件失败。该语句不是循环的一部分，它在 `for` 循环完成时执行，输出 11，即循环结束后 `num` 的值。

表达式不需要在循环的括号内。在程序中，`num` 在循环之前进行初始化，并在循环体内部进行递增。

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int num = 1;
    for (; num <= 10;) {
        cout << num << " ";
        num++;
    }
    return 0;
}
```

尽管初始化和递增没有在括号内完成，但仍然需要两个分号来分隔三个表达式。虽然表达式可以为空，但分号是必须的。

## 警惕死循环

在之前的程序中，如果省略了 `num++` 语句，循环将永远不会停止：

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int num = 1;
    for (; num <= 10;)
    {
        cout << num << " ";
    }
    return 0;
}
```

原因是条件 `num <= 10` 永远不会变为假，因为 `num` 将从 1 开始，且由于省略了 `num++` 语句，它的值永远不会改变。

这种永不停执行的循环被称为死循环。通常，它通过在控制窗口中快速连续的字符来标识，且应用程序永远不会结束。

你并不希望在代码中编写死循环，但错误确实会发生；我以前也犯过很多这种错误。如果这种情况发生你身上，不要慌慌。你可以使用 CTRL-BREAK 组合键来结束程序。一旦你遇到了死循环，就可以纠正导致它的错误。

## 阶乘示例

到为止，循环的使用相对简单，即按升序或倒序计数数字。然而，循环可以用于更复杂的程序。

下面的程序计算用户输入的数字的阶乘。阶乘是从 1 到该数字所有正整数的乘积。例如，3 的阶乘是 3*2，等于 6；5 的阶乘是 5*4*3*2*1，等于 120。

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int num, counter, total = 1;
    cout << "Enter a number: ";
    cin >> num;
    cout << "The factorial of " << num << " is: ";
    for (int counter = 1; counter <= num; counter++)
        total *= counter;
    cout << total;
    return 0;
}
```

输入和输出可能是：
4
The factorial of 4 is 24

## 跳出循环

我们之前在 `switch` 语句中使用过 `break` 关键字。你也可以在 `for` 循环中使用 `break` 关键字。`break` 关键字用于 `for` 循环的代码内部，通常位于 `if / else` 结构中。如果遇到了 `break` 关键字，`for` 循环将终止，尽管条件仍然为真。

例如，在下面的程序中，用户有三次机会猜一个 1 到 10 之间的数字（恰好是 3）。然而，如果用户在第一次或第二次尝试就猜中了数字，那么让他们再次猜就没有意义了。因此，如果用户猜中了数字，则使用 `break` 语句跳出循环。

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int num, counter, secret = 3;
    cout << "Guess a number between 1 and 10\n";
    cout << "You have 3 tries\n";
    for (int counter = 1; counter <= 3; counter++) {
        cout << "Enter the number now: ";
        cin >> num;
        if (num == secret) {
            cout << "You guessed the secret number!";
            break;
        }
    }
    cout << "Program over;";
    return 0;
}
```

这里有两个示例输入和输出。在第一个中，用户尝试了三次但都没有猜对。在第二个中，用户在第二次尝试时就猜对了，所以没有到达 `break` 关键字的第三次迭代。

```
Guess a number between 1 and 10
You have 3 tries
Enter the number now: 2
Enter the number now: 4
Enter the number now: 6
Program over
```

Guess a number between 1 and 10
You have 3 tries
Enter the number now: 2
Enter the number now: 3
You guessed the secret number!
```

如果没有 `break` 关键字，循环将是无限的。虽然 `break` 关键字是 C++ 语言的一部分，但我建议谨慎使用它。通常，每次迭代只有一个出口点。然而，当你使用多个 `break` 语句时，会变得难以理解，并可能导致逻辑错误。

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int num = 1;
    for (num <= 10) {
        break;
    } else {
        cout << num << " ";
        num++;
    }
}
```

## Continue 关键字

你也可以在 `for` 循环中使用 `continue` 关键字。`continue` 关键字和 `break` 关键字一样，用于 `for` 循环的代码内部，通常位于 `if / else` 结构中。如果遇到了 `continue` 语句，当前迭代结束，并在下次迭代。

例如，在下面的程序中，用户每个商品 3 元，但第 13 个商品不收费。换句话说，每 13 个商品是免费的。

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int num, counter, total = 0;
    cout << "How many items you want to buy: ";
    cin >> num;
    for (int counter = 1; counter <= num; counter++) {
        if (counter % 13 == 0)
            continue;
        total += 3;
    }
    cout << "Total for " << num << " items is $" << total;
    return 0;
}
```

这里有三个示例输入和输出，说明了 12 个或 13 个商品的价格没有变化，但在第 14 个商品时用户需要额外支付 3 元。

How many items you want to buy: 12
Total for 12 items is $36

How many items you want to buy: 13
Total for 13 items is $36

How many items you want to buy: 14
Total for 14 items is $39

在下面的程序中，逻辑运算符 `!`（非）是使用 `continue` 关键字的另一个示例。

