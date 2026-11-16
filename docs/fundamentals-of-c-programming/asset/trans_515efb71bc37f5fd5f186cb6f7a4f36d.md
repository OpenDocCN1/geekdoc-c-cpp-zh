

请注意，在清单 9.6（betterprompt.cpp）中，我们在 prompt 函数内部声明了一个名为 result 的变量。该变量是函数的局部变量，这意味着我们不能在 prompt 之外使用这个特定变量。这也意味着我们可以在 prompt 函数之外的不同上下文中自由使用相同的名称，而该用法不会干扰 prompt 中的 result 变量。我们说 result 是一个局部变量。

我们可以进一步增强 prompt 函数。目前 prompt 始终打印相同的消息。使用参数，我们可以自定义 prompt 打印的消息。清单 9.7（evenbetterprompt.cpp）展示了如何使用参数在 prompt 中提供自定义消息。

```
Listing 9.7: evenbetterprompt.cpp

#include <iostream>

// Definition of the prompt function
int prompt(int n)
{
    int result;
    std::cout << "Please enter integer #" << n << ": ";
    std::cin >> result;
    return result;
}

int main()
{
    int value1, value2, sum;
    std::cout << "This program adds together two integers.\n";
    value1 = prompt(1); // Call the function
    value2 = prompt(2); // Call the function again
    sum = value1 + value2;
    std::cout << value1 << " + " << value2 << " = " << sum << '\n';
}
```

在清单 9.7（evenbetterprompt.cpp）中，参数影响打印的消息。现在用户被提示输入值 #1 或值 #2。调用

value1 = prompt(1);

将值 1 传递给 prompt 函数。由于 prompt 的参数名为 n，该过程的工作方式就好像赋值语句

n = 1;

作为 prompt 内部的第一个动作被执行一样。

在函数定义的第一行：

int prompt(int n)

n 被称为形式参数。形式参数在函数体内像变量一样使用，但它是在函数的参数列表中声明的；它不是在函数体中声明的。形式参数是函数正式定义中使用的参数。

在函数调用时：

value1 = prompt(1);

传递给函数的参数（或实参）1 被称为实际参数。实际参数是函数调用过程中实际使用的参数。当调用函数时，任何实际参数都会被赋值给其对应的形式参数，然后函数开始执行。另一种说法是，在函数调用期间，实际参数被绑定到其对应的形式参数。

函数定义中使用的参数称为形式参数。形式参数在函数体内表现为局部变量；因此，形式参数的名称不会与其他函数中的任何局部变量或形式参数名称冲突。这意味着作为函数开发者，你可以选择最能代表参数在函数中作用的参数名称。

![](img/e84ad11adb18201d71595b31ce6c9eff_220_0.png)

如果你正在编写函数，无法预测调用者的实际参数。你必须能够处理调用者发送的任何值。编译器将确保调用者参数的类型与你形式参数的声明类型兼容。

要记住形式参数和实际参数之间的区别，请记住：

- 形式参数是在函数的正式定义中声明和使用的参数。
- 实际参数是调用者在实际使用（调用或呼叫）函数时提供的参数。

当调用 `value1 = prompt(1);` 在 main 中执行，并且 prompt 函数体内的语句 `std::cout << "Please enter integer #" << n << ": ";` 被执行时，n 将具有值 1。同样，当调用 `value2 = prompt(2);` 在 main 中执行，并且 prompt 函数体内的语句 `std::cout << "Please enter integer #" << n << ": ";` 被执行时，n 将具有值 2。在 `value1 = prompt(1);` 的情况下，prompt 中的 n 绑定到 1，在 `value2 = prompt(2);` 的情况下，prompt 中的 n 绑定到 2。

函数定义要求所有形式参数都必须在函数名称后面的括号中声明。调用者在调用函数时不提供实际参数类型声明。鉴于清单 9.1（countersquareroot.cpp）中定义的 square_root 函数，以下调用者代码片段是非法的：

```
double number = 25.0;
// Legal, pass the variable's value to the function
std::cout << square_root(number) << '\n';
// Illegal, do not declare the parameter during the call
std::cout << square_root(double number) << '\n';
```

函数定义负责声明其参数的类型，而不是调用者。

## 9.2 使用函数

函数定义的一般形式是

```
type name( parameterlist ) {
    body
}
```

- 函数的类型指示函数返回的值的类型。通常，函数会执行计算，计算结果必须传回调用函数的位置。特殊类型 void 表示函数不返回值。
- 函数的名称是一个标识符（参见第 3.3 节）。函数的名称应指示函数的用途。
- 参数列表是逗号分隔的形式为
    类型 名称

的对列表，其中 类型 是 C++ 类型，名称 是表示参数的标识符。调用者通过参数将信息传递给函数。函数定义的参数列表中指定的参数称为形式参数。参数也称为实参。参数列表可以为空；空参数列表表示调用者无法向函数传递任何信息。
- 函数体是用花括号括起来的语句序列，用于定义函数要执行的操作。语句可以包含变量声明，在函数体中声明的任何变量都是该函数的局部变量。

函数体可能只包含一条语句、多条语句，或者根本不包含任何语句；无论如何，花括号始终是必需的。

请注意，可以通过多个参数将多个信息传递给函数，但只能通过返回值将一个信息从函数传出。回顾初等数学中的最大公约数（也称为最大公因数）。

![](img/e84ad11adb18201d71595b31ce6c9eff_222_0.png)
![](img/e84ad11adb18201d71595b31ce6c9eff_222_1.png)

要确定 24 和 18 的 GCD，我们列出它们所有的公因数并选择最大的一个：

- 24: 1, 2, 3, 4, 6, 8, 12, 24
- 18: 1, 2, 3, 6, 9, 18

最大公约数函数在将分数化简为最简分数时很有用；例如，考虑分数 18/24。18 和 24 的最大公约数是 6，因此我们将分数的分子和分母都除以 6：18/6 / 24/6 = 3/4。GCD 函数除了用于将分数化简为最简分数外，还有其他应用领域。

考虑将一块长 24 英寸、宽 18 英寸的胶合板切割成最大尺寸的正方形块，且不浪费任何材料的问题。由于 GCD(24, 18) = 6，我们可以将胶合板切割成十二块 6 英寸 x 6 英寸的正方形，如图 9.2 所示。

如果我们将胶合板切割成任何其他尺寸且不浪费任何材料的正方形，那么这些正方形必须小于 6 英寸 x 6 英寸；例如，我们可以制作四十八块 3 英寸 x 3 英寸的正方形，如图 9.3 所示。

如果我们切割的正方形大于 6 英寸 x 6 英寸，那么并非所有胶合板都可以用来制作正方形。

## 图 9.4 正方形过大

![](img/e84ad11adb18201d71595b31ce6c9eff_223_0.png)

图 9.4 显示了一些较大正方形的情况。

除了基本算术和几何之外，GCD 函数在密码学中发挥着至关重要的作用，使得在不安全的网络上进行安全通信成为可能。

## 清单 9.8: gcdprog.cpp

```cpp
#include <iostream>

int main() {
    // Prompt user for input
    int num1, num2;
    std::cout << "Please enter two integers: ";
    std::cin >> num1 >> num2;

    // Determine the smaller of num1 and num2
    int min = (num1 < num2) ? num1 : num2;

    // 1 is definitely a common factor to all ints
    int largestFactor = 1;
    for (int i = 2; i <= min; i++)
```

