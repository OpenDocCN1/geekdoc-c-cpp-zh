

# 表 10.1: 变量作用域与存储类型

| 存储类型 | 作用域 | 周期 | 内存分配 |
| --- | --- | --- | --- |
| Auto | 局部 | 函数/块执行 | 栈 |
| register | 局部 | 函数/块执行（如果存储在寄存器中） | CPU 寄存器（如果可用），否则使用栈 |
| static (局部) | 局部 | 贯穿整个函数调用 | 数据段 |
| static (全局) | 全局 | 整个程序执行 | 数据段 |
| extern | 取决于变量的原始声明 | 取决于变量的原始声明 | 取决于变量的原始声明 |

## 局部变量

局部变量局限于特定的函数，并且只能定义它们的代码块中使用。例如，在 `setup` 函数中声明的局部变量在 `loop` 函数中可见也无法使用。

在函数或块内声明的变量被视为该函数或块的局部变量。任何在大括号 `{}` 内部的内容都形成一个块。局部变量只存在于它们所在的块中。

这意味着它们无法在那个块的作用域之外被访问。

```
// 使用局部变量的错误方法
#include <stdio.h>

void display() {
    int age = 19; // 此变量是 display 函数的局部变量
}

int main() {
    // 编译错误
    printf("Age is: %d\n", age);

    return 0;
}
```

在此代码中：

- age 是在 display 函数内部声明的局部变量，仅在 display 内部可见。
- 尝试从 main 访问 localVar 将导致编译错误，因为超出了作用域。

## 10.3. 变量作用域与存储类型

以下代码修复了此错误：

```
#include <stdio.h>

void display() {
    int age = 19; // 此变量是 display 函数的局部变量
    printf("Age is %d\n", age);
}

int main() {
    display();
    return 0;
}
```

变量在任何代码块中都具有作用域，而不仅仅是在函数内部。在接以下程序中，变量 `i` 只存在于循环内部。尝试在循环外部访问 `i` 将导致编译错误。

```
#include <stdio.h>

int main() {
    int sum = 0;

    for (int i=0; i<5; i++) {
        sum += i;
    }
    printf("i = %d, sum = %d\n", i, sum); // 编译错误

    return 0;
}
```

总结来说，局部变量可以具有块作用域或函数作用域，这意味着它们只在声明它们的块或函数中存在并可以使用。尝试在这些这些块之外访问它们会导致编译错误。

## 全局变量

全局变量顾如其名，可以从程序的任何部分访问。它们声明在所有函数之外。它们在整个程序执行期间都是可用的。

通常不建议过度使用全局变量，因为可能会导致命名冲突、代码段之间的紧耦合，以及程序维护和测试的困难。

```
// 全局变量声明
int globalVar = 20;
```

```
void myFunction() {
    printf("%d\n", globalVar);
}
```

```
int main() {
  display();
  globalVar = 23; // 从 main 中修改全局变量的值
  → function
  display();
  return 0;
}
```

在此程序中，变量 `globalVar` 声明在任何函数之外，使其可以在程序的任何地方访问。

局部变量促进模块化和信息隐藏，使代码更容易理解和维护。全局变量应该谨慎使用，因为它们会引入依赖并使你的代码缺乏灵活性和重用性。

总结，变量作用域和存储类型是 C 语言中两个独立但密切相关的概念。变量作用域决定了变量的可见性，而存储类型决定了它跨函数和块的周期以及行为。理解这些概念对于编写高效、可维护且可移植的 C 代码至关重要。

## 静态变量

静态变量是一种特殊的变量，结合了局部和全局变量的特点。与局部变量一样，它们在整个程序执行期间存在，而是一个函数。与全局变量不同，它们声明在函数内部，将其可见性限制在该函数内（局部作用域）。

静态变量在函数中使用 `static` 关键字定义。静态变量可以实现计数器、维护历史数据以及在函数内部存储持久值。这里有一个演示静态变量的简单 C 代码：

```
#include <stdio.h>

void incrementCounter() {
  static int counter = 0; // 静态变量初始化
  counter++;              // 每次函数调用增加计数
  printf("Counter: %d\n", counter);
}

int main() {
  // 调用函数来增加并打印计数器
  incrementCounter();
  incrementCounter();
```

## 10.4. 函数调用过程中的类型转换

```
incrementCounter();
```

在此示例中，我们定义了一个名为 `incrementCounter` 的函数，它声明并定义了一个静态局部变量 `counter`。第一次调用该函数时，`counter` 变量被初始化为 0，对其值进行增加并打印。当再次调用函数时，由于 `counter` 是静态变量，它保留了之前的值，其值再次被增加并打印。该程序的输出将是：

```
Counter: 1
Counter: 2
Counter: 3
```

这表明 `counter` 在对 `incrementCounter` 的函数调用之间保留了其值。

在 C 中，当参数类型与参数类型不完全匹配时，在函数调用过程中可能会发生类型转换。以下是几个示例：

```
void print_value(double value) {
    printf("Value: %f\n", value);
}
```

```
int num = 10;

// 在传递之前将 int 转换为 double
print_value(num);
```

在此示例中，`print_value` 期望一个 `double` 参数，但传递的是 `int` 类型 `num`。这导致 `num` 被转换为 `double`。

```
void print_value(int value) {
    printf("Value: %d\n", value);
}
```

```
double another_num = 10.5;

// 在传递之前将 double 转换为 int
print_value(another_num);
```

在此示例中，`print_value` 期望一个 `int` 参数，但传递的是 `double` 类型 `another_num`。这导致 `another_num` 在传递给函数之前被转换为 `int`（截断为 10）。

```
int calculate_ratio(int a, int b) {
    // 将结果转换为 int
    return (float)a / b;
}
```

```
int ratio = calculate_ratio(10, 3);

printf("Ratio: %d\n", ratio); // 输出: 3
```

在此示例中，`calculate_ratio` 使用浮点操作数进行除法。然而，结果被隐式转换为 `int`，函数返回类型为 `int`，丢弃了小数部分。结果输出为 3 是因为小数部分被丢弃了。

这些示例演示了 C 如何处理函数调用和返回时的隐式转换。隐式转换可能会导致精度丢失或截断。理解隐式转换对于避免意外行为非常重要。如果需要，可以使用强制转换来执行手动类型转换，而不是依赖隐式转换。

## 10.5 向函数传递数组

C 中的数组用于存储和处理数据集合。当数组传递给函数时，函数只接收第一个元素的指针。多种方法指示数组的大小，例如作为独立参数传递、使用哨兵值或使用第一个元素作为大小指示。

### 10.5.1 作为独立参数传递数组大小

向函数传递数组大小常用的方法是使用独立参数。这显式地指定了数组的大小，并允许函数根据提供的大小遍历元素。

以下是作为独立参数传递大小的示例：

```
#include <stdio.h>

int sum(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i];
    }
    return sum;
}
```

```
int main() {
    int numbers[] = {1, 2, 3, 4, 5};
    int size = sizeof(numbers) / sizeof(numbers[0]);
}
```

