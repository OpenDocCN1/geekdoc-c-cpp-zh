
C++标准。假设存在 int v[5]，其第一个元素位于内存位置 3000，且 int 占四个字节。同时，假设指针 vPtr 已初始化为指向 v[0]（即 vPtr 的值为 3000）。下图展示了在整数为四字节的机器上的这种情况：

![](img/7b5e2088e71c7f78681d4ddbcf104c06_390_0.png)

变量 vPtr 可以用以下任一语句初始化为指向 v（因为内置数组的名称会隐式转换为其第零个元素的地址）：

```cpp
int* vPtr{v};
int* vPtr{&v[0]};
```

### 7.9.1 向指针加整数和从指针减整数

在常规算术中，加法 3000 + 2 得到值 3002。指针算术通常不是这样：

- 向指针加一个整数会使指针增加该整数乘以指针所指向类型的大小。
- 从指针减一个整数会使指针减少该整数乘以指针所指向类型的大小。

字节数取决于对象的数据类型。例如，语句

```cpp
vPtr += 2;
```

将产生 3008（3000 + 2 * 4），假设一个 int 存储在四个字节的内存中。在内置数组 v 中，vPtr 现在将指向 v[2]，如下图所示：

![](img/7b5e2088e71c7f78681d4ddbcf104c06_390_1.png)

如果 vPtr 已增加到 3016（指向 v[4]），则语句

```cpp
vPtr -= 4;
```

会将 vPtr 设回 3000——内置数组的开头。要使指针增加或减少一个元素，分别使用递增（++）或递减（--）运算符。语句

```cpp
++vPtr;
vPtr++;
```

使指针递增以指向内置数组的下一个元素。语句

```cpp
--vPtr;
vPtr--;
```

使指针递减以指向内置数组的前一个元素。

**指针算术没有边界检查，因此 C++ 核心准则建议改用 `std::span`，我们将在第 7.10 节演示。** 你必须确保每个向指针加整数或从指针减整数的指针算术运算，都使指针引用内置数组边界内的元素。正如你将看到的，**`std::span` 具有边界检查，这有助于你避免错误。**

### 7.9.2 从一个指针减去另一个指针

指向同一内置数组的指针变量可以相互相减。例如，如果 vPtr 包含地址 3000，v2Ptr 包含地址 3008，则表达式

```cpp
v2Ptr - vPtr;
```

将确定从 vPtr 到 v2Ptr 的内置数组元素个数——在本例中为 2。我们不能假设同一类型的两个变量在内存中连续存储，除非它们是内置数组的相邻元素。对不指向同一内置数组元素的两个指针进行相减或比较是逻辑错误。

### 7.9.3 指针赋值

如果两个指针类型相同，则可以将一个指针赋值给另一个指针。¹⁷ 此外，任何指向基本类型或类类型的指针都可以在不进行强制转换的情况下赋值给 `void*`（指向 `void` 的指针）。然而，`void*` 类型的指针不能直接赋值给其他类型的指针——`void*` 类型的指针必须首先用 `static_cast` 转换为合适的指针类型。例如，要将名为 ptr 的 `void*` 强制转换为 `int*`，你会使用

```cpp
int* intPtr{static_cast<int*>(ptr)};
```

### 7.9.4 不能解引用 void* 指针

`void*` 指针不能被解引用。例如，编译器“知道”在整数为四字节的机器上，`int*` 指向四个字节的内存。解引用 `int*` 会创建一个左值，该左值是内存中该 `int` 四个字节的别名。然而，`void*` 包含一个未知数据类型的存储地址。你不能在指针算术中使用 `void*`，也不能解引用 `void*`，因为编译器不知道指针所指向数据的类型或大小。

对 `void*` 指针允许的操作有：

- 将 `void*` 指针与其他指针比较，
- 将 `void*` 指针强制转换为其他指针类型，以及
- 将其他指针类型转换为 `void*` 指针。

对 `void*` 指针的所有其他操作都是编译错误。

17. 当然，`const` 指针不能被修改。

### 函数 displayArray

将内置数组传递给函数通常需要数组的名称和大小。尽管参数 items（第 12 行）使用 [] 声明，但它只是一个指向 int 的指针。它并不“知道”函数实参包含多少个元素。这种方法存在各种问题。例如，调用 displayArray 的代码可能为 size 传递错误的值。在这种情况下，函数

- 可能不会处理 items 的所有元素，或者
- 可能访问 items 边界之外的元素——这是逻辑错误，也是潜在的安全问题。

此外，我们之前讨论了外部迭代的缺点，如第 13–15 行所使用的那样。Visual Studio 中的 C++ 核心准则检查器会针对 displayArray 以及将内置数组传递给函数发出若干警告。我们在本示例中包含函数 displayArray，只是为了将其与在函数 displaySpan 中传递 span 进行比较，后者是推荐的方法。

```cpp
// items parameter is treated as a const int* so we also need the size to
// know how to iterate over items with counter-controlled iteration
void displayArray(const int items[], size_t size) {
    for (size_t i{0}; i < size; ++i) {
        std::cout << std::format("{}", items[i]);
    }
}
```

### 函数 displaySpan

C++ 核心准则指出，指针应只指向一个对象，而不是一个数组。它们还指出，像 displayArray 这样接收指针和大小的函数容易出错。要解决这些问题，应使用 span 将数组传递给函数。函数 displaySpan（第 20–24 行）接收一个包含 const int 的 span——之所以是 const，是因为该函数不需要修改数据。

```cpp
// span parameter contains both the location of the first item
// and the number of elements, so we can iterate using range-based for
void displaySpan(std::span<const int> items) {
    for (const auto& item : items) { // spans are iterable
        std::cout << std::format("{}", item);
    }
}
```

span 同时封装了一个指针和一个表示元素个数的 size_t。当你将内置数组（或 std::array 或 std::vector）传递给 displaySpan 时，C++ 会隐式创建一个 span，其中包含指向数组第一个元素的指针及其大小，大小由编译器根据数组声明确定。这个 span 视图查看你作为实参传入的原始数组中的数据。C++ 核心准则指出，可以按值传递 span，因为它与分别传递指针和大小一样高效，²¹ 正如我们在 displayArray 中所做的那样。

19. C++ 核心准则，“ES.42：保持指针的使用简单直接。”访问于 2023 年 4 月 14 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#es-42

20. C++ 核心准则，“I.13：不要将数组作为单个指针传递。”访问于 2023 年 4 月 14 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#R-arrays

span 具有许多类似于数组和 vector 的能力，例如通过基于范围的 for 语句进行迭代。由于 span 是基于编译器确定的数组原始大小创建的，基于范围的 for 保证我们无法访问数组边界之外的元素。这修复了与 displayArray 相关的各种问题，并有助于防止缓冲区溢出等安全问题。

### 函数 `times2`

因为 span 是对现有容器的视图，所以更改 span 的元素会更改容器的原始数据。函数 times2 将其 span<int> 中的每个项乘以 2。注意，我们使用非 const 引用来修改 span 视图查看的每个元素。

```cpp
// spans can be used to modify elements in the original data structure
void times2(std::span<int> items) {
    for (int& item : items) {
        item *= 2;
    }
}
```

### 将数组传递给函数以显示内容

第 34–36 行创建 int 内置数组 values1、std::array values2 和 std::vector values3。每个都有五个元素，并在内存中连续存储其元素。第 41 行调用 displayArray 显示 values1 的内容。displayArray 函数的第一个参数是指向 int 的指针，因此我们不能使用 std::array 或 std::vector 的名称将这些对象传递给 displayArray。

```cpp
int main() {
    int values1[] = { 1, 2, 3, 4, 5 };
    std::array values2{6, 7, 8, 9, 10};
    std::vector values3{11, 12, 13, 14, 15};

    // must specify size because the compiler treats displayArray’s items
    // parameter as a pointer to the first element of the argument
    std::cout << "values1 via displayArray: ";
    displayArray(values1, 5);
}
```

```text
values1 via displayArray: 1 2 3 4 5
```

21. C++ 核心准则，“F.24：使用 span<T> 或 span_p<T> 来指定半开序列。”访问于 2023 年 4 月 14 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rf-range.

