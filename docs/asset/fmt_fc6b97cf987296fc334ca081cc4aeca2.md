
In this example, the `do-while` loop is used to execute the block of code 10 times. The block of code is executed once before the condition `x < 10` is checked. If the condition is true, the block of code is executed again and the value of `x` is incremented by 1. This will cause the loop to execute 10 times, with the value of `x` increasing by 1 each time. The output of this program will be the numbers 0 through 9, each on a separate line.

The `do-while` loop

### for statement

In C++, the `for` loop is a type of iteration statement that is used to execute a block of code a specific number of times. The syntax for the `for` loop is as follows:

```
for (initialization; condition; increment) {
    // code to be executed
}
```

The `initialization` clause is used to initialize a loop variable, the `condition` clause is used to specify a condition that is checked before each iteration of the loop, and the `increment` clause is used to modify the loop variable at the end of each iteration.

以下是 C++ 中使用 `for` 循环的示例：

```cpp
#include <iostream>
int main() {
    for (int i = 0; i < 10; i++) {
        std::cout << i << std::endl;
    }
    return 0;
}
```

在此示例中，`for` 循环用于执行代码块 10 次。循环变量 `i` 初始化为 0，并在每次迭代前检查条件 `i < 10`。如果条件为真，则执行代码块并将循环变量递增 1。这将导致循环执行 10 次，`i` 的值每次增加 1。该程序的输出将是 0 到 9 的数字，每行一个。

`for` 循环是执行特定次数的代码块的有用工具，常在迭代次数已知时使用。重要的是在循环中包含一个最终会使条件变为假的语句，否则循环将成为无限循环。

### 基于范围的 for 语句

在 C++ 中，基于范围的 `for` 循环是一种用于遍历范围内元素的迭代语句。基于范围的 `for` 循环的语法如下：

```
for (range_declaration : range_expression) {
    // code to be executed
}
```

`range_declaration` 是为范围中的每个元素声明的变量，而 `range_expression` 是指定要遍历范围的表达式。

以下是 C++ 中使用基于范围的 `for` 循环的示例：

```cpp
#include <iostream>
#include <vector>
int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    for (int number : numbers) {
        std::cout << number << std::endl;
    }
    return 0;
}
```

在此示例中，基于范围的 `for` 循环用于遍历 `numbers` 向量中的元素。循环变量 `number` 为范围中的每个元素声明，而范围表达式 `numbers` 指定要遍历的范围。这将导致循环执行 5 次，`number` 的值依次设置为 `numbers` 向量中的每个元素。该程序的输出将是 1 到 5 的数字，每行一个。

基于范围的 `for` 循环是遍历范围内元素的有用工具，常用于简化使用传统 `for` 循环的代码。重要的是确保范围表达式指定的范围在循环期间未被修改，否则可能导致未定义行为。

## 第十章

### 跳转语句

在 C++ 中，跳转语句用于将控制转移到程序中的不同位置。C++ 中有四种跳转语句：`break` 语句、`continue` 语句、`goto` 语句和 `return` 语句。

`break` 语句用于终止循环或 `switch` 语句并将控制转移到循环或 `switch` 之后下一个语句。`break` 语句的语法如下：

```
break;
```

以下是 C++ 中使用 `break` 语句的示例：

```cpp
#include <iostream>
int main() {
    for (int i = 0; i < 10; i++) {
        if (i == 5) {
            break;
        }
        std::cout << i << std::endl;
    }
    return 0;
}
```

在此示例中，`break` 语句用于在 `i` 的值为 5 时终止 `for` 循环。循环将执行 5 次，`i` 的值每次增加 1。当 `i` 的值变为 5 时，`break` 语句将被执行，循环将被终止。该程序的输出将是 0 到 4 的数字，每行一个。

`continue` 语句用于跳过当前循环迭代的剩余部分并将控制转移到下一次迭代。`continue` 语句的语法如下：

```
continue;
```

以下是 C++ 中使用 `continue` 语句的示例：

```cpp
#include <iostream>
int main() {
    for (int i = 0; i < 10; i++) {
        if (i % 2 == 0) {
            continue;
        }
        std::cout << i << std::endl;
    }
    return 0;
}
```

在此示例中，`continue` 语句用于在 `i` 的值为偶数时跳过 `for` 循环当前迭代的剩余部分。循环将执行 10 次，`i` 的值每次增加 1。如果 `i` 的值为偶数，则执行 `continue` 语句并跳过当前迭代的剩余部分。该程序的输出将是 1 到 9 的奇数，每行一个。

`goto` 语句用于将控制转移到同一函数中的带标签语句。`goto` 语句的语法如下：

```
goto label;
...
label:
// code to be executed
```

`return` 语句用于终止函数并返回一个值

### break 语句

在 C++ 中，`break` 语句是一种跳转语句，用于终止循环或 `switch` 语句并将控制转移到循环或 `switch` 之后下一个语句。`break` 语句的语法如下：

```
break;
```

以下是 C++ 中使用 `break` 语句的示例：

```cpp
#include <iostream>
int main() {
    for (int i = 0; i < 10; i++) {
        if (i == 5) {
            break;
        }
        std::cout << i << std::endl;
    }
    return 0;
}
```

在此示例中，`break` 语句用于在 `i` 的值为 5 时终止 `for` 循环。循环将执行 5 次，`i` 的值每次增加 1。当 `i` 的值变为 5 时，`break` 语句将被执行，循环将被终止。该程序的输出将是 0 到 4 的数字，每行一个。

`break` 语句常用于在满足特定条件时提前终止循环或 `switch` 语句。重要的是仅在循环或 `switch` 语句的主体中使用 `break` 语句，因为在这些上下文之外使用它将导致编译时错误。

### continue 语句

在 C++ 中，`continue` 语句是一种跳转语句，用于跳过当前循环迭代的剩余部分并将控制转移到下一次迭代。`continue` 语句的语法如下：

```
continue;
```

以下是 C++ 中使用 `continue` 语句的示例：

```cpp
#include <iostream>
int main() {
    for (int i = 0; i < 10; i++) {
        if (i % 2 == 0) {
            continue;
        }
        std::cout << i << std::endl;
    }
    return 0;
}
```

在此示例中，`continue` 语句用于在 `i` 的值为偶数时跳过 `for` 循环当前迭代的剩余部分。循环将执行 10 次，`i` 的值每次增加 1。如果 `i` 的值为偶数，则执行 `continue` 语句并跳过当前迭代的剩余部分。该程序的输出将是 1 到 9 的奇数，每行一个。

`continue` 语句常用于在满足特定条件时跳过循环的某些迭代。重要的是仅在循环的主体中使用 `continue` 语句，因为在循环之外使用它将导致编译时错误。

### return 语句

在 C++ 中，`return` 语句是一种跳转语句，用于终止函数并将值返回给调用函数。`return` 语句的语法如下：

```
return expression;
```

`expression` 是一个可选表达式，指定要返回给调用函数的值。如果省略 `expression`，则函数返回函数返回类型的默认值。

以下是 C++ 中使用 `return` 语句的示例：

```cpp
#include <iostream>
int add(int x, int y) {
    return x + y;
}
int main() {
    int result = add(2, 3);
    std::cout << result << std::endl;
    return 0;
}
```

在此示例中，`return` 语句用于将 `add` 函数的结果返回给调用函数。`add` 函数接受两个参数 `x` 和 `y`，并返回它们的和。`return` 语句在调用 `add` 函数时执行，`x + y` 的值被返回给调用函数。在 this case, the value 5 is returned and printed to the screen.

The `return` statement is used to terminate a function and return a value to the calling function. It is important to ensure that the return type of the function is compatible with the value being returned, as attempting to return a value of the wrong type will result in a compile-time error.

### goto statement

In C++, the `goto` statement is a jump statement that is used to transfer control to a labeled statement in the same function. The syntax for the `goto` statement is as follows:

```
goto label;
...
label:
  // code to be executed
```

The `label` is a user-defined identifier that is used to mark a point in the code to which control can be transferred.

Here is an example of using the `goto` statement in C++:

```cpp
#include <iostream>
int main() {
    int x = 0;
    while (true) {
        x++;
        if (x % 2 == 0) {
            goto even;
        }
        std::cout << x << std::endl;
    }
    even:
        std::cout << "Even number: " << x << std::endl;
    return 0;
}
```
