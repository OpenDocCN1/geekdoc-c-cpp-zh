

如果向量为空则返回 true，因为空向量包含相同数量的偶数和奇数（0）。该函数不会影响向量的内容。

```cpp
bool balanced(const std::vector<int>& v) {
    // Add your code...
}
```

- 5. 完成以下函数：如果向量 a 包含重复元素则返回 true；如果 a 中的所有元素都是唯一的则返回 false。例如，向量 2, 3, 2, 1, 9 包含重复项（2 出现多次），但向量 2, 1, 0, 3, 8, 4 不包含（没有元素出现多次）。
  - 空向量没有重复项。
  - 该函数不会影响向量的内容。

```cpp
bool has_duplicates(const std::vector<int>& v) {
    // Add your code...
}
```

- 6. 可以对未排序的向量使用二分查找吗？为什么或为什么不可以？

- 7. 可以对未排序的向量使用线性查找吗？为什么或为什么不可以？

- 8. 完成以下函数 is_ascending：如果整数向量中的元素按升序排列（更准确地说，如果向量包含重复项，则为非降序），则返回 true。例如，以下语句

```cpp
std::cout << is_ascending({3, 6, 2, 1, 7}) << '\n';
```

将打印 false，但以下语句

```cpp
std::cout << is_ascending({3, 6, 7, 12, 27}) << '\n';
```

将打印 true。空向量中不存在的元素被视为按升序排列，因为它们不可能出现顺序错误。

```cpp
bool is_ascending(std::vector<int>& v) {
    // Add your code...
}
```

- 9. 考虑一个使用上一题中 is_ascending 函数的排序函数。它使用循环来测试整数向量的排列。当它找到包含向量所有元素且按升序排列的排列时，它会退出循环。你认为这是一个好的排序算法吗？为什么或为什么不？

## 第 13 章

## 标准 C++ 类

在硬件领域，台式计算机是通过组装以下部件构建的：

- 主板（包含处理器和各种支持卡插槽的电路板），
- 处理器，
- 内存，
- 显卡，
- 输入/输出卡（USB 端口、并行端口和鼠标端口），
- 磁盘控制器，
- 磁盘驱动器，
- 机箱，
- 键盘，
- 鼠标，以及
- 显示器。

（其中一些组件，如 I/O、磁盘控制器和显卡，可能与主板集成。）

显卡本身是一件精密的硬件，包含视频处理器芯片、内存和其他电子元件。技术人员无需组装显卡；显卡是现成的现货，直接使用。显卡在标准封装中提供了大量功能。一个显卡可以被不同供应商的另一张显卡或功能不同的另一张显卡替换。无论使用哪张显卡，整台计算机都能正常工作（前提是操作系统有可用的驱动程序），因为标准接口允许组件协同工作。

当今的软件开发越来越基于组件。软件组件的使用方式类似于硬件组件。软件系统可以很大程度上通过组装预先存在的软件构建块来构建。C++ 支持各种软件构建块。其中最简单的是我们在第 8 章和第 9 章中探讨的函数。一种更强大的技术使用内置和用户设计的软件对象。

C++ 是面向对象的。它不是第一种面向对象编程语言，但却是第一种在各种应用领域获得广泛使用的面向对象语言。面向对象编程语言允许程序员定义、创建和操作对象。与 `ints` 和 `doubles` 等原始数值变量相比，表示对象的变量可以具有相当大的功能。与普通变量一样，每个 C++ 对象都有一个类型。我们说对象是特定类的实例，而 `class` 与 _类型_ 含义相同。对象的类型就是它的类。我们一直在使用 `std::cout` 和 `std::cin` 对象。`std::cout` 是 `std::ostream` 类的实例——也就是说，`std::cout` 的类型是 `std::ostream`。`std::cin` 是 `std::istream` 类的实例。

使用对象的代码是该对象的 _客户端_；例如，以下代码片段

```cpp
std::cout << "Hello\n";
```

使用 `std::cout` 对象，因此是 `std::cout` 的客户端。我们迄今看到的许多函数都是 `std::cout` 和/或 `std::cin` 对象的客户端。对象为其客户端提供服务。

### 13.1 字符串对象

字符串是字符序列，最常用于表示单词和名称。C++ 标准库提供了类 `string`，它指定了 _字符串对象_。要使用字符串对象，必须提供预处理器指令

```cpp
#include <string>
```

`string` 类是标准命名空间的一部分，这意味着它的全名是 `std::string`。如果在代码中使用

```cpp
using namespace std;
```

或

```cpp
using std::string;
```

语句，则可以使用缩写名称 `string`。

声明字符串对象就像声明任何其他变量一样：

```cpp
string name;
```

可以使用熟悉的字符串引号语法将字符序列赋值给 `string` 对象：

```cpp
string name = "joe";
std::cout << name << '\n';
name = "jane";
std::cout << name << '\n';
```

可以使用简单的赋值运算符将一个 `string` 对象赋值给另一个：

```cpp
string name1 = "joe", name2;
name2 = name1;
std::cout << name1 << " " << name2 << '\n';
```

在这种情况下，赋值语句将构成 name1 的字符复制到 name2。赋值后，name1 和 name2 各自拥有构成字符串的字符副本；它们不共享内容。赋值后，更改一个字符串不会影响另一个字符串。string 类中的代码定义了赋值运算符在字符串对象上下文中应如何工作。

与 vector 类（第 11.1.3 节）一样，string 类提供了许多方法。一些字符串方法包括：

- operator[]——提供访问字符串中给定索引处存储的值
- operator=——将一个字符串赋值给另一个
- operator+=——将字符串或单个字符追加到字符串对象末尾
- at——提供对给定索引处存储的字符的边界检查访问
- length——返回构成字符串的字符数
- size——返回构成字符串的字符数（与 length 相同）
- find——定位字符串对象中子字符串的索引
- substr——返回由现有字符串对象的子字符串组成的新字符串对象
- starts_with——如果一个字符串是另一个字符串的前缀，则返回 true
- ends_with——如果一个字符串是另一个字符串的后缀，则返回 true
- empty——如果字符串不包含任何字符，则返回 true；如果字符串包含一个或多个字符，则返回 false
- clear——从字符串中删除所有字符

以下代码片段

```cpp
string word = "computer";
std::cout << "\"" << word << "\" contains " << word.length()
          << " letters." << '\n';
```

打印

```
"computer" contains 8 letters.
```

表达式：

```cpp
word.length()
```

代表 word 对象调用 length 方法。string 类提供了一个名为 size 的方法，其行为与 length 方法完全相同。

string 类定义了一个名为 operator[] 的方法，允许程序员访问字符串中的字符，如下所示：

```cpp
std::cout << "The letter at index 3 is " << word.operator[](3) << '\n';
```

这里 operator[] 方法使用与 length 方法相同的语法，但 operator[] 方法期望一个整数参数。上述代码片段最好写成

```cpp
std::cout << "The letter at index 3 is " << word[3] << '\n';
```

表达式

```cpp
word.operator[](3)
```

与表达式

```cpp
word[3]
```

等价

可以看出，operator[] 的工作方式与 std::vector 类第 11.1.3 节中的同名方法完全相同。

以下代码片段演示了字符串对象可用的一些方法：

### 清单 13.1：stringoperations.cpp

```cpp
#include <iostream>
#include <string>

int main() {
  // Declare a string object and initialize it
  // string word = "fred";
  // Prints 4, since word contains four characters
  std::cout << word.length() << " \n";
  // Prints "not empty", since word is not empty
  if (word.empty())
    std::cout << " empty\n";
  else
    std::cout << " not empty\n";
  // Makes word empty
  word.clear();
  // Prints "empty", since word now is empty
  if (word.empty())
    std::cout << " empty\n";
  else
    std::cout << " not empty\n";
  // Assign a string using operator= method
  word = "good";
  // Prints "good"
  std::cout << word << " \n";
  // Append another string using operator+= method
  word += "-bye";
  // Prints "good-bye"
  std::cout << word << " \n";
  // Print first character using operator[] method
  std::cout << word[0] << " \n";
  // Print last character
  std::cout << word[word.length() - 1] << " \n";
  // Prints "od-by", the substring starting at index 2 of length 5
  std::cout << word.substr(2, 5);
  std::string first = "ABC", last = "XYZ";
  // Splice two strings with + operator
  std::cout << first + last + " \n";
  std::cout << "Compare " << first << " and ABC: ";
  if (first == "ABC")
    std::cout << " equal\n";
}

