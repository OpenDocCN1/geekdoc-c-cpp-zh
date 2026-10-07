
```cpp
    a %= 3; // 等同于: a = a % 3;

    std::cout << "Updated value of 'a': " << a << std::endl;

    return 0;

}
```

在上述代码中，变量 `a` 初始值为 5。复合赋值运算符通过执行算术运算并将结果赋值回 `a` 来修改 `a` 的值。然后使用 `std::cout` 显示更新后的 `a` 值。

## 运算符的优先级和结合性

C++ 中的运算符具有不同的优先级和结合性，这决定了当表达式中存在多个运算符时的计算顺序。理解运算符优先级对于编写产生预期结果的表达式至关重要。

下表显示了 C++ 中一些常用运算符的优先级和结合性，从高到低排序：

| 运算符 | 结合性 | 说明 |
| :--- | :--- | :--- |
| `()` | 从左到右 | 括号 |
| `++`, `--` | 从左到右 | 后置递增、递减 |
| `++`, `--` | 从右到左 | 前置递增、递减 |
| `+`, `-` | 从右到左 | 一元加、减 |
| `!`, `~` | 从右到左 | 逻辑取反和位反 |
| `*`, `/`, `%` | 从左到右 | 乘法、除法、取模 |
| `+`, `-` | 从左到右 | 加法、减法 |
| `<<`, `>>` | 从左到右 | 位左移、位右移 |
| `<`, `<= `>`, `>=` | 从左到右 | 关系运算符 |
| `==`, `!=` | 从左到右 | 等运算符 |
| `&` | 从左到右 | 位与 |
| `^` | 从左到右 | 位异异 |
| `|` | 从左到右 | 位或 |
| `&&` | 从左到右 | 逻辑与 |
| `||` | 从左到右 | 逻辑或 |
| `=` | 从左到右 | 赋值 |
| `+=`, `-=`, `*=`, `/=`, `%=` | 从左到右 | 复合赋值 |

```cpp
include <iostream>

int main() {

    for (int i = 0; i < 5; i++) {

        std::cout << "Count: " << i << std::endl;

    }

    return 0;

}
```

在这个示例中，`for` 循环将变量 `i` 初始化为 0。然后它检查 `i` 是否小于 5。如果条件为真，则执行块中的代码，然后将 `i` 加 1。这个过程会重复进行，直到条件变为假。

## 控制流语句：Break 和 Continue

除了条件语句和循环之外，`break` 和 `continue` 等控制流语句为循环内部的执行流提供了额外的控制。

`break` 语句用于终止当前循环并继续执行循环之外的下一个语句。它在某些条件下提前退出循环非常有用。这里有一个示例：

```cpp
#include <iostream>

int main() {

    for (int i = 0; i < 5; i++) {

        if (i == 3) {

            break;

        }

        std::cout << "Count: " << i << std::endl;

    }

    return 0;

}
```

在这个示例中，`for` 循环遍历 `i` 从 0 到 4 的值。然而，当 `i` 变为 3 时，遇到了 `break` 语句，终止了循环。结果是只显示了计数 0、1 和 2。

`continue` 语句用于跳过当前迭代的剩余部分并继续循环的下一次迭代。当我们想要根据特定条件跳过某些迭代时，它非常有用。这里有一个示例：

```cpp
#include <iostream>

int main() {

    for (int i = 0; i < 5; i++) {

        if (i == 2) {

            continue;

        }

        std::cout << "Count: " << i << std::endl;

    }

    return 0;

}
```

在这个示例中，当 `i` 变为 2 时，遇到了 `continue` 语句，跳过了该迭代下方的代码。结果是跳过了计数 2，并显示了剩余的计数 0、1、3 和 4。

## 结论

在本章中，我们探索了 C++ 中的控制流和决策结构。我们学习了条件语句，例如 `if-else` 语句，它允许我们根据某些条件执行不同的代码块。我们还探索了循环，包括只要条件为真就重复执行代码块的 `while` 循环，以及用于对值范围迭代或执行特定次数迭代的 `for` 循环。

此外，我们还涵盖了 `break` 和 `continue` 等控制流语句，它们为循环内部的执行流提供了额外的控制。这些语句允许我们根据特定条件提前终止循环或跳过某些迭代。

通过理解和利用控制流以及决策结构，你可以在 C++ 中创建更具动态性和交互性的程序。你可以控制执行流，根据用户输入或其他条件做出决策，并根据需要重复代码。

# 第 6 章：数组与字符串

在第 5 章中，我们探索了 C++ 中的控制流和决策结构。在本章中，我们将深入研究数组和字符串，这是是两个基础性概念，它们允许我们高效地处理元素集合。

## 数组

数组是一种数据结构，允许我们在连续的内存块中存储相同数据类型的多个元素。数组中的每个元素都通过索引访问，索引代表该元素在数组中的位置。数组为处理相关数据集合提供了一种方便的方法。

### 声明和访问数组

在 C++ 中声明数组时，我们指定元素的数据类型，紧接着是数组名和方括号中的大小。这里有一个示例：

```cpp
int numbers[5]; // 声明一个名为 'numbers' 的大小为 5 的整数数组
```

一旦声明，我们就可以使用索引访问数组的单个元素。第一个元素的索引为 0，第二个元素的索引为 1，以此此类推。这里有一个示例：

```cpp
int numbers[5]; // 声明一个名为 'numbers' 的大小为 5 的整数数组
numbers[0] = 10; // 给 'numbers' 的第一个元素赋值值 10
numbers[1] = 20; // 给 'numbers' 的第二个元素赋值值 20
numbers[2] = 30; // 给 'numbers' 的第三个元素赋值值 30
```

我们还可以在声明时使用初始化列表来初始化数组。这里有一个示例：

```cpp
int numbers[] = {10, 20, 30, 40, 50}; // 声明并初始化整数数组 'numbers'
```

### 访问数组元素

要访问数组的元素，我们使用数组名加上索引。这里有一个示例：

```cpp
int numbers[] = {10, 20, 30, 40, 50};
std::cout << numbers[0] << std::endl;
std::cout << numbers[1] << std::endl;
std::cout << numbers[2] << std::endl;
```

### 数组大小与边界

数组的大小决定了它可以包含的元素数量。注意索引从 0 开始到 size-1。访问范围之外的元素会导致未定义行为。这里有一个示例：

```cpp
int numbers[] = {10, 20, 30, 40, 50};
int size = sizeof(numbers) / sizeof(numbers[0]);
std::cout << "Array大小: " << size << std::endl;
```

### 多维数组

C++ 还支持多维数组，即数组的数组。多维数组可以用于表示矩阵、表格或任何具有多个维结构。这里有一个二维数组的示例：

```cpp
int matrix[3][3];
matrix[0][0] = 1; // 给第 0 行第 0 列赋值值 1
matrix[1][2] = 3; // 给第 1 行第 2 列赋值值 3
```

### 字符串

在 C++ 中，字符串被表示为字符数组。字符串是包含在双引号("")内的字符序列。C++ 在 `<string>` 头文件中提供了 `string` 类来高效处理字符串。这里有一个声明和初始化字符串的示例：

```cpp
#include <iostream>
#include <string>
int main() {
    std::string greeting = "Hello, world!"; // 声明并初始化字符串
    std::cout << greeting << std::endl; // 将字符串打印到控制台
    return 0;
}
```

### 字符串操作

C++ 提供了许多操作来处理字符串。以下是一些常用的字符串操作：

- 拼接：可以使用 `+` 运算符或 `+=` 复合赋值运算符拼接字符串。这里有一个示例：

```cpp
std::string firstName = "John";
std::string lastName = "Doe";
std::string fullName = firstName + " " + lastName; // 拼接字符串
std::cout << "Full name: " << fullName << std::endl;
```

- 长度：可以使用 `length()` 或 `size()` 成员函数获取字符串的长度。这里有一个示例：

```cpp
std::string message = "Hello, world!";
std::cout << "Length of message: " << message.length() << std::endl;
```

```cpp
int length = message.length();   // 获取字符串的
length
```

```cpp
std::cout << "Length of the string: " << length << std::endl;
```

- 访问字符：可以使用类似数组的索引表示法来访问字符串的单个字符。这里是一个示例：

```cpp
std::string message = "Hello, world!";
char firstCharacter = message[0]; // 访问第一个字符
```

```cpp
char lastCharacter = message[message.length() - 1]; // 访问最后一个字符
```

```cpp
std::cout << "First character: " << firstCharacter << std::endl;
std::cout << "Last character: " << lastCharacter << std::endl;
```

- 子字符串：可以使用 `substr()` 成员函数从字符串中提取子字符串。这是一个示例：

```cpp
std::string message = "Hello, world!";
std::string substring = message.substr(7, 5); // 提取从索引 7 开始长度为 5 的子字符串
```

```cpp
std::cout << "Substring:" << substring << std::endl;
```

## 结论

在本章中，我们探索了 C++ 中的数组和字符串。数组允许我们高效地存储和访问相同数据类型的多个元素，为处理相关数据集合提供了方便的方法。我们学习了如何声明数组、访问其元素以及计算它们的大小。我们还探索了用于表示多维度数据的多维数组。

此外，我们还讨论了字符串，它们在 C++ 中被表示为字符数组。我们学习了如何声明和初始化字符串，执行拼接和子字符串提取等字符串操作，以及获取字符串的长度。

数组和字符串是强大的工具，使我们能够在 C++ 中有效地处理和操作数据。通过掌握这些概念，你可以开发出高效管理和处理元素集合的程序。

# 第7 章：函数与模块化编程

在第 6 章中，我们探索了 C++ 中的数组和字符串。在本章中，我们将深入研究函数和模块化编程。函数允许我们将复杂的程序分解为更小、易于管理的代码块，使我们的程序更有组织、模块化且具复用性。

## 函数

函数是一个命名的代码块，用于执行特定任务或一组相关任务。函数通过将一系列语句封装到单个单元中，提供了一种代码模块化的方法。它们促进了代码的重用、可读性和维护性。

### 函数的声明与定义

在 C++ 中定义函数，我们需要提供函数的签名，其中包含返回类型、名称以及它接受的任何参数。函数体包含调用函数时执行的语句。这里是一个函数声明和定义的示例：

```cpp
// 函数声明
int addNumbers(int a, int b);
// 函数定义
int addNumbers(int a, int b) {
    int sum = a + b;
    return sum;
}
```

在这个示例中，我们声明并定义了一个名为 `addNumbers` 的函数，它接受两个整数参数 `a` 和 `b` 并返回一个整数值。函数计算 `a` 和 `b` 的和并使用 `return` 语句返回结果。

### 函数调用

要使用函数，我们需要通过名称调用它并提供必要的参数（如果有）。这里是调用 `addNumbers` 函数的示例：

```cpp
int result = addNumbers(5, 3);
```

在这个示例中，使用参数 5 和 3 调用了 `addNumbers` 函数。函数的返回值（两个数字之和）被存储在变量 `result` 中。

### 函数参数

函数参数允许我们将值传递到函数中。参数在函数的作用范围内充当变量，其值可以在函数执行期间使用。这里是一个示例：

```cpp
int multiplyNumbers(int a, int b) {
    int product = a * b;
    return product;
}
```

在这个示例中，`multiplyNumbers` 函数接受两个整数参数 `a` 和 `b`。它计算 `a` 和 `b` 的积并返回结果。

### 函数返回值

函数的返回类型指定了函数返回值的类型。它可以是任何有效的数据类型，包括基本类型、用户定义类型，或者如果函数不返回结果，可以是 `void`。这里是一个示例：

```cpp
void greet() {
  std::cout << "Hello, world!" << std::endl;
}
```

在这个示例中，`greet` 函数的返回类型为 `void`，表示它不返回值。它只是向控制台打印 "Hello, world!"。

### 函数重载

函数重载允许我们定义多个具有相同但参数列表不同的函数。C++ 根据调用时提供的参数来确定调用哪个函数。这里是一个示例：

```cpp
int square(int number) {
    return number * number;
}
double square(double number) {
    return number * number;
}
```

在这个示例中，我们定义了两个 `square` 函数。一个接受整数，另一个接受双精度。

## 模块化编程

模块化编程是一种强调将程序分解为称为函数的自包含单元的方法。每个函数执行特定的任务。

### 模块化编程的优势

模块化编程具有若干优点：

- **代码重用性**：函数可以在程序的多个部分被重用。
- **可读性**：将程序分解为函数使代码更易读、更容易理解。
- **易维护性**：通过模块化编程，修复程序中的错误变得更容易。
- **扩展性**：可以添加新函数或修改现有函数而不影响程序的其他部分。

### 示例：使用函数的模块化编程

让我们考虑这样一个示例：我们需要计算矩形的面积和周长。我们可以通过为每个任务定义单独的来实现程序的模块化：

```cpp
#include <iostream>
// 计算矩形面积的函数
double calculateArea(double length, double width) {
    return length * width;
}
// 计算矩形周长的函数
double calculatePerimeter(double length, double width) {
    return 2 * (length + width);
}
int main() {
    double length, width;
    std::cout << "Enter the length of the rectangle: ";
    std::cin >> length;
    std::cout << "Enter the width of the rectangle: ";
    std::cin >> width;
    double area = calculateArea(length, width);
    double perimeter = calculatePerimeter(length, width);
    std::cout << "Area: " << area << std::endl;
    std::cout << "Perimeter: " << perimeter << std::endl;
    return 0;
}
```
