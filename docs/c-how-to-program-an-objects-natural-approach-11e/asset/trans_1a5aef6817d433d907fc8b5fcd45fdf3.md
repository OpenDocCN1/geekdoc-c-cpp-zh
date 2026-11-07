
## 19.6.12 通过成员函数 flags 设置和重置格式状态

你已经了解了如何使用流操纵器来更改输出格式特征，但在更改输出流的格式后，如何将其格式恢复到之前的状态呢？不带参数的成员函数 `flags` 返回当前格式状态设置，类型为 `fmtflags` 对象。带 `fmtflags` 参数的成员函数 `flags` 按参数指定设置格式状态，并返回先前的状态设置。`flags` 返回值的初始设置可能因编译器而异。图 19.18 使用成员函数 `flags` 保存流的原始格式状态（第 16 行），然后恢复原始格式设置（第 24 行）。在 C++20 文本格式化中，不再要求具备捕获格式状态并恢复它的能力。每次 `std::format` 调用的格式化仅用于该次调用，不会影响任何其他 `std::format` 调用，从而简化了输出格式化。

```cpp
// fig19_18.cpp
// flags member function.
#include <format>
#include <iostream>

int main() {
   int integerValue{1000};
   double doubleValue{0.0947628};

   // display flags value, int and double values (original format)
   std::cout << std::format("flags value: {}\n", std::cout.flags())
      << "int and double in original format:\n"
      << integerValue << '\t' << doubleValue << "\n\n";

   // save original format, then change the format
   auto originalFormat{std::cout.flags()};
   std::cout << std::showbase << std::oct << std::scientific;

   // display flags value, int and double values (new format)
   std::cout << std::format("flags value: {}\n", std::cout.flags())
      << "int and double in new format:\n"
      << integerValue << '\t' << doubleValue << "\n\n";

   std::cout.flags(originalFormat); // restore format

   // display flags value, int and double values (original format)
   std::cout << std::format("flags value: {}\n", std::cout.flags())
      << "int and double in original format:\n"
      << integerValue << '\t' << doubleValue << "\n";
}
```

**图 19.18** | flags 成员函数。（第 1 部分，共 2 部分。）

```text
flags value: 513
int and double in original format:
1000    0.0947628

flags value: 5129
int and double in new format:
01750    9.476280e-02

flags value: 513
int and double in original format:
1000    0.0947628
```

**图 19.18** | flags 成员函数。（第 2 部分，共 2 部分。）

## 19.7 流错误状态

每个流对象都包含一组表示流状态的状态位——粘性格式设置、错误指示符等。你可以利用这些信息来测试输入是否成功等。这些状态位定义在类 `ios_base` 中——它是流类的基类。如果输入的数据类型错误，流提取会把流的 `failbit` 设置为 true。类似地，如果操作以不可恢复的方式失败——例如，程序从磁盘读取文件时该磁盘发生故障——流提取会把流的 `badbit` 设置为 true。图 19.19 展示了如何使用 `failbit` 和 `badbit` 之类的位来确定流的状态。⁴ 有关位和位操作的更多信息，请参阅 https://deitel.com/cpphtp11 上的位操作附录。

```cpp
// fig19_19.cpp
// Testing error states.
#include <iostream>

int main() {
   int integerValue{0};

   // display results of cin functions
   std::cout << std::boolalpha << "Before a bad input operation:"
      << "\n  cin.rdstate(): " << std::cin.rdstate()
      << "\n  cin.eof(): " << std::cin.eof()
      << "\n  cin.fail(): " << std::cin.fail()
      << "\n  cin.bad(): " << std::cin.bad()
      << "\n  cin.good(): " << std::cin.good()
      << "\n\n expects an integer, but enter a character: ";

   std::cin >> integerValue; // enter character value
```

**图 19.19** | 测试错误状态。（第 1 部分，共 2 部分。）

```cpp
   // display results of cin functions after bad input
   std::cout << "\nAfter a bad input operation:"
             << "\n  cin.rdstate(): " << std::cin.rdstate()
             << "\n  cin.eof(): " << std::cin.eof()
             << "\n  cin.fail(): " << std::cin.fail()
             << "\n  cin.bad(): " << std::cin.bad()
             << "\n  cin.good(): " << std::cin.good();

   std::cin.clear(); // clear stream

   // display results of cin functions after clearing cin
   std::cout << "\nAfter cin.clear()"
             << "\n  cin.fail(): " << std::cin.fail()
             << "\n  cin.good(): " << std::cin.good() << "\n";
}
```

```text
Before a bad input operation:
  cin.rdstate(): 0
  cin.eof(): false
  cin.fail(): false
  cin.bad(): false
  cin.good(): true

 expects an integer, but enter a character: A

After a bad input operation:
  cin.rdstate(): 2
  cin.eof(): false
  cin.fail(): true
  cin.bad(): false
  cin.good(): false

After cin.clear()
  cin.fail(): false
  cin.good(): true
```

**图 19.19** | 测试错误状态。（第 2 部分，共 2 部分。）

### 成员函数 eof

程序首先显示在从用户接收任何输入之前流的状态（第 9～14 行）。第 11 行使用成员函数 `eof` 判断流上是否遇到了文件结束。在本例中，该函数返回 0（false）。该函数检查流的 `eofbit` 数据成员的值；对于输入流，在尝试提取超出流末尾的数据而遇到文件结束后，该位会被设置为 true。

### 成员函数 fail

第 12 行使用 `fail` 成员函数判断流操作是否失败。该函数检查流的 `failbit` 数据成员的值；当发生格式错误并因此没有输入任何字符时，该位会在流上被设置为 true。例如，当你尝试读取一个数字，而用户输入了字符串时，就可能发生这种情况。在本例中，该函数返回 0（false）。当输入发生此类错误时，字符不会丢失。通常，从这类输入错误中恢复是可能的。

### 成员函数 bad

第 13 行使用 `bad` 成员函数判断流操作是否失败。该函数检查流的 `badbit` 数据成员的值；当发生导致数据丢失的错误时，该位会在流上被设置为 true——例如，从文件读取时，存储该文件的磁盘发生故障。在本例中，该函数返回 0（false）。一般来说，这类严重故障是不可恢复的。

### 成员函数 good

第 14 行使用 `good` 成员函数；如果 `bad`、`fail` 和 `eof` 函数都返回 false，则该函数返回 true。该函数检查流的 `goodbit`；如果流中的 `eofbit`、`failbit` 或 `badbit` 均未设置为 true，则该位会在流上被设置为 true。在本例中，该函数返回 1（true）。只应在“good”流上执行 I/O 操作。

### 成员函数 rdstate

`rdstate` 成员函数（第 10 行）以整数值返回流的总体错误状态。例如，可以用 `switch` 语句检查该函数的返回值，以检查 `eofbit`、`badbit`、`failbit` 和 `goodbit`。测试流状态的首选方法是使用成员函数 `eof`、`bad`、`fail` 和 `good`——使用这些函数不需要你熟悉特定的状态位。

### 在输入流中引发错误并重新显示流的状态

第 17 行将一个值读入 `int` 变量。输入字符串而不是 `int`，以强制输入流中发生错误。此时，输入失败，第 20～25 行再次调用流的状态函数。在本例中，`fail` 返回 1（true），因为输入失败。函数 `rdstate` 也返回非零值（true），因为成员函数 `eof`、`bad` 和 `fail` 中至少有一个返回了 true。一旦流中发生错误，函数 `good` 就返回 0（false）。

### 清除错误状态，以便继续使用流

发生错误后，在重置流的错误状态之前，你不能再使用该流。`clear` 成员函数（第 27 行）用于将流的状态恢复为“good”，以便可以在该流上继续执行 I/O。第 30～32 行表明 `fail` 返回 0（false），`good` 返回 1（true），因此输入流可以再次使用。

`clear` 的默认参数是 `goodbit`，因此语句

```cpp
std::cin.clear();
```

清除 `cin` 并为该流设置 `goodbit`。语句

```cpp
std::cin.clear(ios::failbit)
```

设置 `failbit`。当你使用用户定义类型在 `cin` 上执行输入并遇到问题时，可能希望这样做。`clear` 这个名称在此上下文中可能显得不合适，但它是正确的。

⁴ 此程序输出的实际值可能因编译器而异。
