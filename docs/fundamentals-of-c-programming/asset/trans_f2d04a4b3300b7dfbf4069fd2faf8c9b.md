

| 3 | 3 |
|---|---|
| 3.08221 | 3.08221 |
| 3.16228 | 3.16228 |

显示结果中存在一些微小差异。显然，我们应该使用标准 sqrt 函数，而不是我们自己的函数。

每个 C++ 函数都有两个方面：

- **函数定义**。函数的定义指定了函数的返回类型和参数类型，并提供了决定函数行为的代码。在清单 9.1（customsquareroot.cpp）中，square_root 函数的定义出现在 main 函数之上。

- **函数调用**。程序员通过函数调用来使用函数。main 函数同时调用了我们的 square_root 函数和 sqrt 函数。每个函数都有且只有一个函数定义，但可能有多次调用。

函数定义由四部分组成：

- **名称**—C++ 中的每个函数都有一个名称。名称是一个标识符（参见第 3.3 节）。与变量名称一样，为函数选择的名称应准确描绘其预期用途或描述其功能。

- **类型**—每个函数都有一个返回类型。如果函数向其调用者返回一个值，则其类型对应于它返回的值的类型。特殊类型 void 表示函数不返回值。

- **参数**—每个函数都必须指定它从调用者处接受的参数类型。参数出现在带括号的逗号分隔列表中，类似于函数原型（参见第 8.1 节）。然而，与函数原型不同，参数通常与每个类型关联有名称。

- **函数体**—每个函数定义都有一个由花括号括起来的函数体。函数体包含在调用函数时要执行的代码。

图 9.1 剖析了我们的 square_root 函数定义。

最简单的函数不接受参数，也不向调用者返回值。清单 9.2（simplefunction.cpp）是清单 4.1（adder.cpp）的一个变体，包含了这样的简单函数定义。

### 清单 9.2：simplefunction.cpp

```cpp
#include <iostream>

// Definition of the prompt function
void prompt() {
    std::cout << "Please enter an integer value: ";
}

int main() {
    int value1, value2, sum;
    std::cout << "This program adds together two integers.\n";
    prompt(); // Call the function
    std::cin >> value1;
```

### 图 9.1 函数定义解剖

函数计算的值的类型

函数名称

函数要求调用者提供的值的类型

```cpp
double square_root(double x) {
    double diff;
    // Compute a provisional square root.
    double root = 1.0;
    do { // Loop until the p
    // is close enough to
    root = (root + x/root) / 2.0;
    // How bad is the approximation?
    diff = root * root - x;
} while (diff > 0.0001 || diff < -0.0001);
return root;
}
```

函数体

函数用于调用者提供的值的名称

```cpp
prompt(); // Call the function again
std::cin >> value2;
sum = value1 + value2;
std::cout << value1 << " + " << value2 << " = " << sum << '\n';
}
```

prompt 函数只是打印一条消息。程序的运行过程如下：

1. 程序的执行（与所有 C++ 程序一样）从名为 main 的函数中的第一条可执行语句开始。main 函数中的第一行只是声明编译器维护所需的一些变量，因此下一行才实际开始可执行代码。
2. 第一条可执行语句打印程序意图的消息。
3. 下一条语句是对 prompt 函数的调用。此时，程序的执行转移到 prompt 函数的函数体中。prompt 内部的代码将一直执行，直到函数体结束或遇到 return 语句。由于 prompt 不包含 return 语句，prompt 的整个函数体（那条打印语句）都将被执行。
4. prompt 执行完毕后，控制权会返回到 main 中紧随 prompt 调用之后的位置。
5. prompt 调用后的下一个操作是从键盘读取 value1 的值。
6. 第二次调用 prompt 将控制权转移回 prompt 函数内部的代码。它会再次打印其消息。
7. 第二次调用 prompt 结束后，控制权返回到 main 中第二条输入语句的位置，该语句从键盘为 value2 赋值。
8. main 中剩下的两条语句将被执行，然后程序执行终止。

作为另一个简单示例，请考虑清单 9.3（countto10.cpp）。

### 清单 9.3：countto10.cpp

```cpp
#include <iostream>
int main() {
for (int i = 1; i <= 10; i++)
std::cout << i << '\n';
}
```

它只是简单地数到十：

```
1
2
3
4
5
6
7
8
9
10
```

如果我们希望在程序中频繁以这种方式数到十，可以编写如清单 9.4（count10func.cpp）所示的函数，并根据需要调用任意多次。

### 清单 9.4：countto10func.cpp

```cpp
#include <iostream>

// Count to n and print each number on its own line
void count_to_10() {
    for (int i = 1; i <= 10; i++)
        std::cout << i << '\n';
}

int main() {
    std::cout << "Going to count to ten . . .";
    count_to_10();
    std::cout << "Going to count to ten again . . .";
    count_to_10();
}
```

我们的 prompt 和 countto10 函数有些令人失望。prompt 函数可以被删除，每次对 prompt 的调用都可以替换为其函数体中的语句。count_to_10 函数也是如此，尽管拥有一个简单的单行语句来隐藏循环的复杂性很方便。不过，使用 prompt 函数确实有一个优势。如果删除 prompt 并将两次对 prompt 的调用替换为 prompt 内部的打印语句，我们必须确保打印的两条消息相同。如果我们只是调用 prompt，我们知道打印的两条消息将相同，因为只能打印一条可能的消息（即 prompt 函数体中的那条）。

我们可以通过一种称为参数传递的机制来改变函数的行为。如果函数是为接受来自调用者的信息而编写的，则调用者必须提供信息才能使用该函数。调用者通过函数要求的一个或多个参数来传递信息。如果我们有时想要数到不同的数字，count_to_10 函数对我们帮助不大。清单 9.5（countton.cpp）将清单 9.4（count10func.cpp）推广为可以数到调用者需要的任意高度。

### 清单 9.5：countton.cpp

```cpp
#include <iostream>

// Count to n and print each number on its own line
void count_to_n(int n) {
    for (int i = 1; i <= n; i++)
        std::cout << i << '\n';
}

int main() {
    std::cout << "Going to count to ten . . .";
    count_to_n(10);
    std::cout << "Going to count to five . . .";
    count_to_n(5);
}
```

当调用者（在此例中为 main）发出调用时

```cpp
count_to_n(10);
```

参数 10 在函数语句开始执行之前被赋值给 n。

调用者在调用期间必须向 count_to_n 传递恰好一个整数参数（或与整数赋值兼容的其他类型）。否则将导致编译器错误或警告：

```cpp
count_to_n(); // Error, missing parameter during the call
count_to_n(3, 5); // Error, too many parameters during the call
count_to_n(3.2); // Warning, possible loss of data (double to int)
```

我们可以如清单 9.6（betterprompt.cpp）所示增强 prompt 函数的功能。

### 清单 9.6：betterprompt.cpp

```cpp
#include <iostream>

// Definition of the prompt function
int prompt() {
    int result;
    std::cout << "Please enter an integer value: ";
    std::cin >> result;
    return result;
}

int main() {
    int value1, value2, sum;
    std::cout << "This program adds together two integers.\n";
    value1 = prompt(); // Call the function
    value2 = prompt(); // Call the function again
    sum = value1 + value2;
    std::cout << value1 << " + " << value2 << " = " << sum << '\n';
}
```

在这个版本中，prompt 处理输入，因此 main 不需要使用任何输入语句。main 中的赋值语句：

```cpp
value1 = prompt();
```

这意味着 prompt 不再是 void 函数；它必须返回一个可以赋值给变量 value1 的值。此外，prompt 返回的值必须与 int 赋值兼容，因为 value1 的声明类型是 int。快速查看 prompt 定义的第一行可以证实我们的假设：

```cpp
int prompt()
```

这表明 prompt 返回一个 int 值。

因为 prompt 被声明为返回 int 值，所以它必须包含一个 return 语句。return 语句指定要返回给调用者的确切值。在函数执行期间遇到 return 时，控制权会立即返回给调用者。函数调用的值是 return 语句指定的值，因此语句

```cpp
value1 = prompt();
```

将 return 语句执行时指示的值赋给变量 value1。

