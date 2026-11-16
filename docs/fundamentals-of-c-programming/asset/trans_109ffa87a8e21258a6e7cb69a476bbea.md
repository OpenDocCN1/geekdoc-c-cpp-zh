

如果您的程序正在使用 vector，并且以此类消息终止，您应仔细检查其源代码，查找可能发生越界 vector 访问的位置。

以下代码片段展示了一些正确和不正确的 vector 访问：

```cpp
std::vector<int> numbers(10); // Declare the vector
numbers[0] = 5; // Put value 5 first
numbers[9] = 2; // Put value 2 last
numbers[-1] = 5; // Out of bounds; first valid index is 0
numbers[10] = 5; // Out of bounds; last valid index is 9
numbers[1.3] = 5; // Compiler warning, 1.3 is not an int
```

在使用 for 循环进行 vector 遍历时，例如

```cpp
for (int i = 0; i < SIZE; i++)
std::cout << a[i] << '\n';
```

在知道 SIZE 是 vector 中元素数量的情况下，很容易确保 i 不会超出 vector a 的边界，但在使用任意索引值之前应先检查它。在以下代码中：

```cpp
int x;
std::vector<int> a(10); // Make a vector with 10 spaces available
std::cin >> x; // User enters x at run time
// Ensure x is within the bounds of the vector
if (0 <= x && x < 10)
    a[x] = 1; // This is safe now
else
    std::cout << "Index provided is out of range\n";
```

if 语句确保 vector 访问在 vector 的边界内。

C++11 支持 for 语句的一种变体，它为支持遍历的对象（如 vector）使用特殊语法。通常称为基于范围的 for 或 "foreach" 语句，这个版本的 for 语句允许在不使用索引变量跟踪位置的情况下进行 vector 遍历。以下代码片段使用基于范围的 for 语句打印名为 vec 的整数 vector 的内容：

```cpp
for (int n : vec)
    std::cout << n << ' ';
```

您可以将此语句读作“对 vec 中的每个 int n，std::cout << n << ' '。”因此，冒号 (:) 读作“in”。在这个基于范围的 for 循环的第一次迭代中，变量 n 代表 vector vec 中的第一个元素。在第二次迭代中，n 代表第二个元素。第三次迭代时，n 是第三个元素，依此类推。声明的变量在循环的每次迭代中都扮演不同 vector 元素的角色。请注意，基于范围的 for 循环不需要控制变量来跟踪 vector 中的当前索引；循环本身处理该细节，使程序员免于此项任务。

这个基于范围的 for 语句的一般形式是

```cpp
for ( type element variable : vector variable ) statement
```

如果基于范围的 for 循环中的元素变量被声明为引用，则循环体内的代码可以修改 vector 的元素。清单 11.5 (foreachreference.cpp) 允许用户用 10 个数字填充 vector，然后打印 vector 的内容。

```cpp
Listing 11.5: foreachreference.cpp
#include <iostream>
#include <vector>
int main() {
  // Declare a vector of ten numbers
  std::vector<double> vec(10);
  // Allow the user to populate the vector
  std::cout << "Please enter 10 numbers: ";
  for (double& elem : vec)
    std::cin >> elem;
  // Print the vector's contents
  for (double elem : vec)
    std::cout << elem << '\n';
}
```

请注意，清单 11.5 (foreachreference.cpp) 中的第一个基于范围的 for 语句使用引用变量来为 vector 中的每个元素赋值。第二个基于范围的 for 语句不需要使用引用变量，因为它不会更改 vector vec 的任何内容。

在遍历 vector 时，并不总是可以使用基于范围的 for 语句。基于范围的 for 语句按顺序遍历 vector 元素，不能向后移动。此外，如果您只想考虑 vector 中的一部分元素，基于范围的 for 语句也不方便。示例包括访问 vector 中的每隔一个元素，或仅考虑前三分之一的元素。在这些特殊情况下，您可以使用带有整数控制变量的标准 for 循环。第 20.5 节探讨了以创造性方式遍历 vector 的其他一些选项。

## 11.1.3 Vector 方法

vector 是一个对象，对象与 int、double 和 bool 等简单类型在多个方面有所不同。大多数对象都可以访问称为方法的特殊函数。C++ 程序员通常将方法称为成员函数。方法是与对象类相关联的函数。方法调用涉及与函数调用略有不同的语法；例如，如果 obj 是一个支持名为 f 且不接受参数的方法的对象，我们可以使用以下语句代表 obj 调用 f：

```cpp
obj.f();
```

点运算符将对象与要调用的方法连接起来。除了这种特殊的调用语法外，方法的工作方式与第 8 章介绍的全局函数非常相似。方法可以接受参数并可以返回值。

vector 支持多种方法，但我们将重点介绍其中七种：

- push_back—在 vector 末尾插入新元素
- pop_back—从 vector 中删除最后一个元素
- operator[]—提供访问 vector 中给定索引处存储的值
- at—提供对 vector 中给定位置处存储的值的边界检查访问
- size—返回 vector 中当前存储的值的数量
- empty—如果 vector 不包含元素，则返回 true；如果 vector 包含一个或多个元素，则返回 false
- clear—使 vector 为空。

我们已经了解了如何声明特定大小的 vector 并使用提供的空间；但是，我们不受 vector 初始大小的限制。要向 vector 添加元素，我们使用 push_back 方法，如下所示：

```cpp
std::vector<int> list; // Make an empty vector that can hold integers
list.push_back(5); // Add 5 to the end of list
list.push_back(-3); // Add -3 to the end of the list
list.push_back(12); // Add 12 to the end of list
```

执行上述三个 push_back 调用后，list vector 在概念上就像图 11.2 所示。随着新元素插入到末尾，vector 的大小会自动调整。每次 push_back 方法调用都会使 vector 中的元素数量增加一个。

pop_back 方法执行与 push_back 相反的操作。调用 pop_back 会从 vector 中删除最后一个元素，实际上将 vector 中的元素数量减少一个。以下代码片段生成一个名为 list 的 vector，其中仅包含元素 5。

```cpp
std::vector<int> list; // Declare list to be a vector
list.push_back(5); // Add 5 to the end of list
list.push_back(-3); // Add -3 to the end of the list
list.push_back(12); // Add 12 to the end of list
list.pop_back(); // Removes 12 from the list
list.pop_back(); // Removes -3 from the list
```

我们一直在使用 operator[] 方法来访问 vector 中的元素。单词 operator 在 C++ 中是保留字，这使得这个方法更加有趣。表达式

```cpp
vec.operator[](2)
```

是编写

```cpp
vec[2]
```

的长形式。程序员专门使用较短的语法，但较长的表达式更好地说明了方括号 ([ ]) 运算符确实是 std::vector 对象类中的一个方法。

正如我们所看到的，程序员必须保持警惕，避免在 operator[] 方法中使用越界索引。vector 类提供了一个额外的方法 at，它提供索引边界检查。表达式 vec[x] 本身不提供边界检查，因此可能表示未定义行为。功能等效的表达式 vec.at(x) 会检查以确保索引 x 在 vector 的边界内。如果 x 在可接受的索引范围之外，该方法保证会产生运行时错误。清单 11.6 (vectoroutofbounds2.cpp) 是清单 11.4 (vectorofbounds.cpp) 的一个变体，它使用 at 方法而不是 operator[] 方法。

### 清单 11.6: vectoroutofbounds2.cpp

```cpp
#include <iostream>
#include <vector>

int main() {
  const int SIZE = 3;
  std::vector<int> a(5, 5);
  // Print the contents of the vector
  std::cout << "a contains ";
  for (int i = 0; i < SIZE; i++)
    std::cout << a.at(i) << " ";
    std::cout << '\n';
  std::cout << '\n';
  // Change all the 5s in vector a to 8s
  for (int i = 0; i <= SIZE; i++) // Bug: <= should be <
    a.at(i) = 8;
  // Reprint the contents of the vector
  std::cout << "a contains ";
  for (int i = 0; i < SIZE; i++)
    std::cout << a.at(i) << " ";
  std::cout << '\n';
}
```

编译并执行清单 11.6 (vectoroutofbounds2.cpp) 时，保证会产生运行时错误。运行时错误很糟糕，但未定义行为更糟，因为它可能表现为不可预测的运行时错误，并且程序在多个平台上的行为可能不同。

size 方法返回 vector 中的元素数量。以下代码片段打印 vector list 的内容：

```cpp
int n = list.size();
for (int i = 0; i < n; i++)
  std::cout << "list[" << i << "] ";
std::cout << '\n';
```

size 方法在此返回的确切类型是 std::vector<int>::size_type。该类型在 std::vector<int> 类中定义。它与 unsigned 类型兼容，并可以像上面所示一样赋值给 int 变量。我们可以避免额外的局部变量 n，如下所示：

```cpp
for (unsigned i = 0; i < list.size(); i++)
  std::cout << "list[" << i << "] ";
std::cout << '\n';
```

请注意，i 的声明类型是 unsigned，而不是 int。这在将 i 与 list.size() 进行比较时可以防止警告。有符号和无符号整数类型之间的比较可能很危险，并且

