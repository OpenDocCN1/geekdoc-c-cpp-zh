
必须在编译时就已经确定。这在 `array` 中表现得为明显。你可能想尝试以下操作之一：

```cpp
void calculateImArray(int n) {
    array<int,n> data();      // n 必须是常量
    // ...
}
```

```cpp
long sumArray(array<int,n> data) { // 这个 n 从哪里来？
    int sum = 0;
    for(int e : data) {
        sum += e;
    }
    return sum;
}
```

这两种都是可能的，因为 `n` 是一个只在运行时确定的变量。你最多只能使用像 `3+4` 这样的简单计算或 `constexpr`。

关于 `array` 作为参数化类型语言特性的预览就够了。我最好现在进入具体细节。

## 省略元素类型

在 C++17 中，你通常省略角括号之间的类型参数。编译器可以使用构造函数参数确定容器的元素类型：

```cpp
std::vector vec { 1, 2, 3 };
```

这仍然是一个 `vector<int>`，只是你可以少写一些代码。然而，这并不总是明智的（或可能的）：

```cpp
std::vector<std::string> elves { "Elrond", "Galadriel" };
using namespace std::literals;
std::vector dwarves { "Oin"s, "Glin"s };
```

通过后缀 "s"，你强制使用了字符串构造函数参数，并为矮人也获得了一个 `vector<string>`。

## 6.4 简单序列容器

- std::array
  你在创建时指定该容器应持有的元素数量。它既不增长也不收缩；你通过索引或遍历范围来访问其元素。

- std::vector
  这种全能容器连续存储其元素。你通过数值索引访问其元素，或遍历范围。此外，当你添加元素时，它会自动增长。

我努力不使用歧义的术语 `arrays`（数组），而是总是编写 `array`、`std::array` 或 `C-array`。在其他来源中，后者通常被称为 `array`——或者，在某些文本中被称为 `field[13]`。

> 当你知道你需要多少个元素时，就使用数组。正如你在 `main()` 的第一行所示，你在声明中指定了元素的数量。它之后无法更改。

```cpp
// https://godbolt.org/z/cd1dW7T1
#include <array>
#include <iostream>

using std::cout; using std::array; using std::string;

int main() {
    array<string,7> wday = {"Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" };
```

### 6.4.1 "array"

```cpp
    cout << "The week starts with " << wday[0] << "."; // 读取值
    cout << "It ends with " << wday.at(6) << "."; // 安全读取
    /* 还要吗？ */
    wday[5] = "Saturday"; // 修改
}
```

### 列表 6.7 使用 "array" 在方括号中存储固定数量的元素。

你通过数字索引使用 `wday[]` 和 `wday[5]` 访问元素；你既可以读取也可以写入值。另一种方法 `at(index)` 稍微安全一些：使用 `[]` 时，没有检查你是否使用了过大或过小的索引，你的程序可能会崩溃或更糟（它带有错误的值继续运行），而 `at()` 包含一个检查，你可以通过它捕获错误——或至少在程序结束前接收错误消息。

`wday` 声明中的元素数量可以是一个常量。你不能使用之前已经确定了值的变量。作为一个数字字面量，`7` 显然是常量。然而，预先将此类数字声明为常量是一个良好的习惯。

```cpp
// https://godbolt.org/z/fe7dmM4ex
#include <array>
#include <iostream>
constexpr size_t MONTHS = 12; /* 一年的月份数 */

int main() {
    std::array<unsigned, MONTHS> wday = {
        31,28,31,30,31,31,30,31,30,30,30,31};
    unsigned age = 0;
    std::cout << "How old are you? " << std::cin >> age;

    std::array<int, 10> jan; // 数组大小不由变量决定
} 
```

### 列表 6.8 数组大小必须是常量。

图 6.1 一个 "array" 既不增长也不收缩。它的元素紧凑排列。

如果你想将数组作为参数传递给函数，它的类型必须精确匹配数组定义。因为 `array<int,4>` 与 `array<int,5>` 以及 `array<short,4>` 是不同的类型，它无法匹配此类参数类型。经常，为了避免重复代码，你应该预先使用 `using`（或 `typedef`）语句为数组类型赋予自己的名称。

```cpp
// https://gdbbolt.org/z/a4xzbd99z
#include <array>
#include <algorithm>
#include <numeric>
using January = std::array<int, 10>; // 别名

void init(January& jan) { // 数组参数
    std::iota(jan.begin(), jan.end(), 1); // 从1开始填充
}

int main() {
    January jan; // 声明
    init(jan);
}
```

| value | value | value | value | value |
|---|---|---|---|---|


