

```
// 1. number of stars on left side of tree
// = current row value
// 2. exactly one star in the center of tree
// 3. number of stars on right side of tree
// = current row value
count = 0;
while (count < 2*row + 1) {
    std::cout << "*";
    count++;
}
// Move cursor down to next line
std::cout << '\n';
// Change to the next row
row++;
}
```

当用户运行清单 6.21（startree.cpp）并输入 7 时，程序显示

![](img/e84ad11adb18201d71595b31ce6c9eff_160_0.png)

清单 6.21（startree.cpp）使用两个顺序 while 循环，两者都嵌套在一个 while 循环中。外部 while 循环负责在每次执行其循环体时绘制一行树：

- 只要用户输入的值大于零，程序就会执行外部 while 循环的循环体；如果用户输入零或更小的值，程序将终止且不执行任何操作。这是预期的行为。

- 外部 while 循环体中的最后一条语句：

  row++;

  确保变量 row 在每次循环中增加一；因此，它最终将等于 height（因为最初必须小于 height 才能进入循环），循环将终止。这里不可能出现无限循环。

- 外部循环的循环体包含多条语句；因此，循环体必须用花括号括起来。每当一组语句用花括号括起来时，就会形成一个块。在块中声明的任何变量都是该块的局部变量。变量的作用域（变量存在且可以使用的源代码部分）从其声明点到其所在块的结束。例如，变量 height 和 row 在 main 的函数体块中声明；因此，它们是 main 的局部变量。变量 count 在外部 while 语句的循环体块中声明；因此，count 是外部 while 语句的局部变量。尝试在外部 while 语句的循环体之外使用 count 将是一个错误。

变量 x 对特定代码段来说是局部的，是什么意思？这意味着 x 在其作用域之外不存在。程序中可能有其他名为 x 的变量，但它们是不同的变量。如果在同一个程序中可以有两个同名的不同变量听起来很奇怪，请考虑这样一个事实：同一个房间里可以有两个同名的人。他们是不同的人，但名字相同。同样，变量的含义取决于其上下文，其名称不一定是唯一的。

两个内部循环扮演不同的角色：

- 第一个内部循环打印空格。第一次通过外部循环时打印的空格数等于树的高度，并且每次迭代都会减少。这是正确的行为，因为向下的每一行都包含更少的前导空格但更多的星号。
- 第二个内部循环打印构成树的星号行。第一次通过外部循环时，row 为零，因此不打印左侧星号，打印一个中央星号（树的顶部），不打印右侧星号。每次通过循环时，要打印的左侧和右侧星号数量都增加一，并且打印相同的中央星号；因此，树向下每一行在两侧各宽一。观察 2*row + 1 值如何完美地表达所需的星号数量。
- 虽然看起来不对称，请注意，不需要第三个内部循环来打印星号打印后行尾的空格。空格是不可见的，所以没有理由打印它们！

## 6.5.2 打印素数

素数是大于一且只有因子（也称为除数）为一和其本身的整数。例如，29 是素数（只有 1 和 29 能整除它），但 28 不是（2、4、7 和 14 是 28 的因子）。素数曾经仅仅是数学家的智力好奇心，但现在它们在密码学和计算机安全中发挥着重要作用。

任务是编写一个程序，显示用户输入的值以内的所有素数。

清单 6.22（printprimes.cpp）提供了一个解决方案。

```cpp
Listing 6.22: printprimes.cpp

#include <iostream>

int main() {
    int max_value;
    std::cout << "Display primes up to what value? ";
    std::cin >> max_value;
    int value = 2; // Smallest prime number
    while (value <= max_value) {
        // See if value is prime
        bool is_prime = true; // Provisionally, value is prime
        // Try all possible factors from 2 to value - 1
        int trial_factor = 2;
        while (trial_factor < value) {
            if (value % trial_factor == 0) {
                is_prime = false; // Found a factor
                break; // No need to continue; it is NOT prime
            }
            trial_factor++;
        }
        if (is_prime)
            std::cout << value << " "; // Display the prime number
        value++; // Try the next potential prime number
    }
    std::cout << '\n'; // Move cursor down to next line
}
```

清单 6.22（printprimes.cpp），输入 90 时，产生：

```
Display primes up to what value? 90
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89
```

清单 6.22（printprimes.cpp）的逻辑比清单 6.21（startree.cpp）的逻辑稍微复杂一些。用户为 max_value 提供一个值。主循环（外部 while）遍历从两到 max_value 的所有值：

- 引入了两个新变量，局部于外部循环的循环体：trial_factor 和 is_prime。is_prime 初始化为 true，意味着除非我们的测试证明否则，否则假设 value 是素数。trial_factor 在内部循环中取从两到 value - 1 的所有值：

```
int trial_factor = 2;
while (trial_factor < value) {
    if (value % trial_factor == 0) {
        is_prime = false; // Found a factor
        break; // No need to continue; it is NOT prime
    }
    trial_factor++;
}
```

当 trial_factor 能整除 value（即没有余数）时，表达式 value % trial_factor 为零——正好是 trial_factor 是 value 的因子时。如果执行的程序确定 trial_factor 的任何值是 value 的因子，则它将 is_prime 设置为 false 并通过 break 退出循环。如果循环继续到完成，程序永远不会将 is_prime 设置为 false，这意味着它没有找到因子，value 确实是素数。

- 内部循环后的 if 语句：

```
if (is_prime)
    std::cout << value << " "; // Display the prime number
```

只需检查 is_prime 的状态。如果 is_prime 为 true，则 value 必须是素数，因此它打印 value 以及一个额外的空格，以便与后续迭代中可能产生的输出分隔。

我们可以提出的一些重要问题包括：

- 1. 如果用户输入 2，它会被打印吗？

在这种情况下，max_value = value = 2，因此外部循环的条件

```
value <= max_value
```

为真，因为 2 <= 2。is_prime 被设置为 true，但内部循环的条件

```
trial_factor < value
```

不为真（2 不小于 2）。因此，跳过内部循环，is_prime 保持不变为 true，并打印 2。这种行为是正确的，因为 2 是最小的素数（也是唯一的偶素数）。

- 2. 如果用户输入小于 2 的数字，会打印任何内容吗？

while 条件确保不考虑小于二的值。while 的循环体永远不会被进入。只打印换行符，不显示任何数字。这种行为是正确的。

- 3. 内部循环是否保证始终终止？

要进入内部循环的循环体，trial_factor 必须小于 value。value 在循环中任何地方都不会改变，trial_factor 在循环内的 if 语句中任何地方都不会被修改，并且在 if 语句之后立即在循环中递增。因此，trial_factor 在循环的每次迭代中都会递增。最终，trial_factor 将等于 value，循环将终止。

- 4. 外部循环是否保证始终终止？

要进入外部循环的循环体，value 必须小于或等于 max_value。max_value 在循环中任何地方都不会改变。value 在外部循环循环体的最后一条语句中增加，并且 value 在其他任何地方都不会被修改。由于内部循环如上一答案所示保证终止，最终 value 将超过 max_value，循环将结束。

我们可以重新排列内部 while 的逻辑以避免 break 语句。当前版本是：

```
while (trial_factor < value) {
    if (value % trial_factor == 0) {
        is_prime = false; // Found a factor
        break; // No need to continue; it is NOT prime
    }
    trial_factor++;
}
```

我们可以将其重写为：

```
while (is_prime && trial_factor < value) {
    is_prime = (value % trial_factor != 0);
    trial_factor++; // Try next factor
}
```

这个没有 break 的版本为 while 引入了稍微复杂的条件，但删除了其循环体中的 if 语句。is_prime 在循环前初始化为 true。每次通过循环时，它都会被重新赋值。如果 value % trial_factor 为零，trial_factor 将变为 false。这正是 trial_factor 是 value 的因子时。如果 is_prime 变为 false，循环无法继续；如果 is_prime 永不变为 false，当 trial_factor 等于 value 时循环结束。由于运算符优先级，括号不是必需的。括号确实提高了可读性，因为包含 == 和 != 的表达式对人类来说解析起来很别扭。当括号放在不需要的地方时，例如

```
x = (y + 2);
```

