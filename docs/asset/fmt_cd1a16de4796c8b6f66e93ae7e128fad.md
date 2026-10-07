
```cpp
0: #include <bitset>
1: #include <iostream>
2: #include <string>
3:
4: int main ()
5: {
6:     using namespace std;
7:     
8:     // 初始化 bitset 为 0
9:     bitset<4> fourBits;
10:    cout << "Initial contents of fourBits: " << fourBits << endl;
11:
12:    // 使用字符串字面量初始化 bitset
13:    bitset<5> fiveBits("10101");
14:    cout << "Initial contents of fiveBits: " << fiveBits << endl;
15:
16:    // 使用二进制字面量初始化 bitset (C++14)
17:    bitset<6> sixBits(0b100001);
18:    cout << "Initial contents of sixBits: " << sixBits << endl;
19:
20:    // 将一个 bitset 拷贝到另一个
21:    bitset<8> eightBits(fiveBits);
22:    cout << "Initial contents of eightBits: " << eightBits << endl;
23:
24:    return 0;
25: }
```

# 使用 std::bitset 及其成员

# 输出

```
Initial contents of fourBits: 0000
Initial contents of fiveBits: 10101
Initial contents of sixBits: 100001
Initial contents of eightBits: 00101101
```

# std::bitset 中介绍的实用运算符

你已经在第 12 节“运算符类型与运算符重载”中学习了运算符，你还学习了运算符最重要的作用之一是增加类的易用性。`std::bitset` 了一了一些非常实用的运算符，如表 25.1 所示，这使得操作变得非常简单。下表使用你在列表（Listing） 25.1 中学到的示例 bitset `forbits` 对这些运算符进行了说明。

### 表 25.1 std::bitset 支持的运算符

| 运算符 | 说明 |
| :--- | :--- |
| `operator<<` | 将位序列的文本表示形式插入输出流 `cout << fourBits;` |
| `operator>>` | 将字符串插入 bitset 对象 `"0101" >> fourBits;` |
| `operator&` | 执行位按与（AND）操作 `bitset<4> result (fourBits1 & fourBits2);` |
| `operator|` | 执行位按或（OR）操作 `bitset<4> result (fourBits1 | fourBits2);` |
| `operator^` | 执行位按异或（XOR）操作 `bitset<4> result (fourBits1 ^ fourBits2);` |
| `operator-` | 执行位取反（NOT）操作 `bitset<4> result (-fourBits1);` |
| `operator>>=` | 执行位右移 `fourBits >>= (2); // 向右移动两个位` |
| `operator<<=` | 执行位左移 `fourBits << (2); // 向左移动两个位` |
| `operator[N]` | 返回序列中第 n 个位的引用 `fourBits[2] = 0; // 将第三个位设置为 0 bool bNum = fourBits[2]; // 读取第三个位` |

除了这些运算符外，`std::bitset` 还具有诸如 `|=`, `&=`, `^=` 和 `~=` 等运算符，有助于对 bitset 对象执行位操作。

# std::bitset 成员方法

位位（Bits）可以有两种状态——它们要么被置（1），要么被重置（0）。为了帮助操作 bitset 的内容，你可以使用表 25.2 列出的成员函数，这些函数可以帮助你处理单个位或处理 bitset 中的所有位。

### 表 25.2 std::bitset 的成员方法

| 函数 | 说明 |
| :--- | :--- |
| `set()` | 将序列中的所有位设置为 1 `fourBits.set(); // 序列包含: '1111'` |
| `set(N, val=1)` | 将第 M 个位设置为 val指定的的值（默认为 1） `fourBits.set(2, 0); // 将第三个位设置为 0` |
| `reset()` | 将序列中的所有位重置为 0 `fourBits.reset(); // 序列包含: '0000'` |
| `reset(N)` | 清除第 M 个位 `fourBits.reset(2); // 第三个位现在是 0` |
| `flip()` | 翻转序列中的所有位 `fourBits.flip(); // 0101 变为 1010` |
| `size()` | 返回序列中的位数 `size_t numBits = fourBits.size(); // 返回 4` |
| `count()` | 返回被置（1）的位数 `size_t numBitsSet = fourBits.count(); size_t numBitsReset = fourBits.size() - fourBits.count();` |

这些成员方法和运算符的使用在列表 25.2 中给出。

### 列表 25.2 使用 Bitset 执行逻辑操作

```cpp
0: #include <bitset>
1: #include <string>
2: #include <iostream>
3: 
4: int main ()
5: {
6:     using namespace std;
```

# 第 25 节：使用 STL 处理位标志

```cpp
7: bitset <8> inputBits;
8: cout << "Enter a 8-bit sequence: ";
9:
10: cin >> inputBits; // 将用户输入存储在 bitset 中
11:
12: cout << "Num is you supplied: " << inputBits.count() << endl;
13: cout << "Num Os supplied: ";
14:
15: cout << inputBits.size() - inputBits.count() << endl;
16:
17: bitset<8> inputFlipped(inputBits); // 拷贝
18: inputFlipped.flip(); // 翻转位
19:
20: cout << "Flipped version is: " << inputFlipped << endl;
21:
22: cout << "Result of AND, OR and XOR between the two:" << endl;
23: cout << inputBits << " & " << inputFlipped << " = ";
24: cout << (inputBits & inputFlipped) << endl; // 位按与
25:
26: cout << " | " << inputFlipped << " = ";
27: cout << (inputBits | inputFlipped) << endl; // 位按或
28:
29: cout << inputBits << " ^ " << inputFlipped << " = ";
30: cout << (inputBits ^ inputFlipped) << endl; // 位按异或
31:
32: } return 0;
```

## 输出

```
Enter a 8-bit sequence: 1010101

Num is you supplied: 5

Num Os supplied: 3

Flipped version is: 0100101

Result of AND, OR and XOR between the two:

1010101 & 0100101 = 0000000

1010101 | 0100101 = 1111111

1010101 ^ 0100101 = 1111111
```

## 分析

这个交互式程序演示了使用 `std::bitset` 在两个位序列之间执行位操作并不容易，但也展示了其流运算符的实用性。`std::bitset` 实现的移位运算符（`>>` 和 `<<`）使得向屏幕写入位序列以及从用户处读取位序列变成了一项简单的任务。`inputBits` 包含了在第 10 行输入的用户提供的序列，第 12 行用于显示序列中 1 的个数，而 0 的个数则是通过 `size()`（返回位数）与 `count()` 之间的差值来计算的。`inputFlipped` 在开头创建，然后使用 `flip()` 进行翻转，如第 17 行所示，每个位都被翻转了——即取反（0 变成 1）。

## 注意

`std::bitset` 的一个缺点是无法动态调整大小。你可以使用 bitset 只要在编译时就确定位数。

# vector<bool>

`vector<bool>` 是 `std::vector` 的一个特化版本，用于存储布尔数据。它可以动态调整大小。

## 提示

使用 `vector<bool>` 需要包含头文件：

`#include <vector>`

# 实例化 vector<bool>

`vector<bool>` 是 `std::vector` 的一个特化版本，用于存储布尔数据。它可以动态调整大小。

# 列表 25.3 vector<bool> 的实例化

```cpp
0: #include <vector>
1: #include <iostream>
2: using namespace std;
3:
4: int main ()
5: {
6:     vector<bool> boolFlags(3); // 初始化 3 个 bool 标志
7:     boolFlags[0] = true;
8:     boolFlags[1] = true;
9:     boolFlags[2] = false;
10:  boolFlags.push_back(true); // 在末插入第四个 bool
11:
12:  cout << "The contents of the vector are: " << endl;
13:  for (size_t index = 0; index < boolFlags.size(); ++ index) {
14:    cout << boolFlags[index] << ' ';
15:  }
16:
17:  cout << endl;
18:  boolFlags.flip();
19:
20:  cout << "The contents of the vector are: " << endl;
21:  for (size_t index = 0; index < boolFlags.size(); ++ index) {
22:    cout << boolFlags[index] << ' ';
23:  }
24:
25:  return 0;
26: }
```

## 分析

此示例展示了实例化 `vector<bool>` 的几种方式。第 7 行使用了默认构造函数。第 10 行展示了创建一个 10 个值为 true 的 vector。第 13 行展示了如何通过另一个对象来实例化 `vector<bool>`

# vector<bool> 函数与运算符

`vector<bool>` 具有 `flip()` 函数，可以翻转序列中布尔值的状态，类似于 `std::bitset` 的函数。

此外，该类在意义上与 `std::vector` 非常相似，例如你甚至可以序列中 `push_back` 标志。列表 25.4 详细演示了该类的用法。

### 列表 25.4 使用 vector<bool>

```cpp
0: #include <vector>
1: #include <iostream>
2: using namespace std;
3:
4: int main ()
5: {
6:     vector<bool> boolFlags(3); // 初始化持有 3 个 bool 标志
7:     boolFlags[0] = true;
8:     boolFlags[1] = true;
9:     boolFlags[2] = false;
10:  boolFlags.push_back(true); // 在结尾插入第四个 bool
11:
12:  cout << "The contents of the vector are: " << endl;
13:  for (size_t index = 0; index < boolFlags.size(); ++ index) {
14:    cout << boolFlags[index] << ' ';
15:  }
16:
17:  cout << endl;
18:  boolFlags.flip();
19:
20:  cout << "The contents of the vector are: " << endl;
21:  for (size_t index = 0; index < boolFlags.size(); ++ index) {
22:    cout << boolFlags[index] << ' ';
23:  }
24:
25:  return 0;
26: }
```

# 输出

```
The contents of the vector are:

1 1 0

The contents of the vector are:

0 0 1 0
```

![](img/ccb6520e9d7dbbb25f5e4ac7152a7c51_648_0.png)

## 总结

在本节中，你学习了处理位序列和位标志的最有效工具：`std::bitset` 类。你还学习了 `vector<bool>` 类的知识，该类允许你存储布尔标志——而这些标志的数量不需要在编译时就已确定。

## 问答

- 在 `std::bitset` 和 `vector<bool>` 均可以使用的情况下，你更倾向于使用哪一个类来存储你的二进制标志？

  首选 Bitset，因为它最符合这一需求。

- 我有一个名为 `myBitSet` 的 `std::bitset` 对象，它包含特定数量的存储位。我如何确定值为 0（或假）的位数？

  `bitset::count()` 提供值为 1 的位数。将此数字从 `bitset::size()`（指示存储的位位总数）中减去，即可得到序列中 0 的个数。

- 我可以使用迭代器访问 `vector<bool>` 中的单个元素吗？

  可以。因为 `vector<bool>` 是 `std::vector` 的部分特化版本，所以它支持迭代器。

- 我可以在编译时指定 `vector<bool>` 中持有的元素数量吗？

  可以，可以通过在重载的构造函数中指定数量，或者在稍后的实例中使用 `vector<bool>::resize()` 函数。

## 工作坊

工作坊包含测验题，帮助你巩固对涵盖内容的理解，并提供让你使用所学知识的练习。在检查附录 E 中的答案之前，尝试回答测验和练习题，并在进入下一节之前确保理解了答案。

## 测验

- bitset 可以扩展其内部缓冲区以容任意数量的元素吗？

- 为什么 bitset 不被归为 STL 容器类？

- 你会使用 `std::vector` 来存储在编译时固定且已知的位数吗？

## 练习

- 编写一个包含四个比特位的 bitset 类。将其初始化为一个数字，显示结果，并将其添加到另一个 bitset 对象中。（注意：Bitset 不允许 `bitsetA = bitsetX + bitsetY`）。

- 演示你如何翻转（即切换）bitset 中的位。

# 第 26 节

理解智能指针

C++ 程序员在管理堆内存（或自由存储）时，并不一定需要使用普通指针类型；他们可以使用智能指针。

在本节中，你将学习：

- 什么是智能指针以及你为什么需要它们

- 智能指针是如何实现的

- 不同的智能指针类型

- 为什么你不应该使用已废弃的 `std::auto_ptr`

- 标准库智能指针 `std::unique_ptr`

- 流行的智能指针库

# 什么是智能指针？

简单来说，C++ 中的智能指针是一个重载了运算符的类，它的行为类似于传统的指针。然而，它通过确保动态分配的数据被正确且及时地销毁，提供了额外的价值，并促进了定义良好的对象周期。

# 使用传统（原始）指针的问题
