

置于变量之前（前缀）的递增或递减运算符分别称为前缀递增或前缀递减运算符。置于变量之后（后缀）的递增或递减运算符分别称为后缀递增或后缀递减运算符。

使用前缀递增（或递减）运算符将变量加 1（或减 1）称为对变量进行前递增（或前递减）。变量先被递增（或递减）1，然后其新值用于所在表达式。

使用后缀递增（或递减）运算符将变量加 1（或减 1）称为对变量进行后递增（或后递减）。变量在递增（或递减）之前的值用于表达式。与二元运算符不同，按惯例，一元递增和递减运算符应紧邻其操作数，中间不留空格。

### 前缀递增与后缀递增

图 3.4 演示了 `++` 递增运算符的前缀递增和后缀递增版本之间的区别。递减运算符（`--`）的工作原理类似。

```cpp
// fig03_04.cpp
// Prefix increment and postfix increment operators.
#include <iostream>
using namespace std;

int main() {
    // demonstrate postfix increment operator
    int c{5};
    cout << "c before postincrement: " << c << "\n"; // prints 5
    cout << "    postincrementing c: " << c++ << "\n"; // prints 5
    cout << "c after postincrement: " << c << "\n"; // prints 6

    cout << "\n"; // skip a line

    // demonstrate prefix increment operator
    c = 5;
    cout << "c before preincrement: " << c << "\n"; // prints 5
    cout << "    preincrementing c: " << ++c << "\n"; // prints 6
    cout << "c after preincrement: " << c << "\n"; // prints 6
}
```

```text
c before postincrement: 5
    postincrementing c: 5
c after postincrement: 6

c before preincrement: 5
    preincrementing c: 6
c after preincrement: 6
```

**图 3.4** | 前缀递增和后缀递增运算符。

第 8 行将变量 c 初始化为 5，第 9 行输出 c 的初始值。第 10 行输出表达式 c++ 的值。该表达式对变量 c 进行后递增，因此先输出 c 的原始值（5），然后将 c 的值递增（为 6）。因此，第 10 行再次输出 c 的初始值（5）。第 11 行输出 c 的新值（6），以证明变量的值在第 10 行被递增。第 16 行将 c 的值重置为 5，第 17 行输出 c 的值。第 18 行输出表达式 ++c 的值。该表达式对 c 进行前递增，因此其值先被递增，然后输出新值（6）。第 19 行再次输出 c 的值，以表明执行第 18 行后 c 仍为 6。

### 使用算术复合赋值运算符、递增和递减运算符简化语句

算术复合赋值运算符以及递增和递减运算符可用于简化程序语句。例如，图 3.3 中的三条赋值语句（第 21、24 和 28 行）

```cpp
passes = passes + 1;
failures = failures + 1;
studentCounter = studentCounter + 1;
```

可以使用复合赋值运算符更简洁地写成

```cpp
passes += 1;
failures += 1;
studentCounter += 1;
```

使用前缀递增运算符写成

```cpp
++passes;
++failures;
++studentCounter;
```

或使用后缀递增运算符写成

```cpp
passes++;
failures++;
studentCounter++;
```

当在语句中单独递增或递减变量时，前缀递增和后缀递增形式的效果相同，前缀递减和后缀递减形式的效果也相同。只有当变量出现在更大的表达式中时，前递增或后递增变量才会产生不同的效果（前递减或后递减也是如此）。

尝试对不是可赋值表达式的表达式使用递增或递减运算符会导致编译错误。例如，编写 `++(x + 1)` 是语法错误，因为 `(x + 1)` 不是变量。

### 运算符优先级与结合性

下表显示了到目前为止介绍的运算符的优先级和结合性。运算符按优先级从高到低自上而下排列。第二列表示每个优先级级别下运算符的结合性。注意，条件运算符（`?:`）、一元运算符前递增（`++`）、前递减（`--`）、正（`+`）和负（`-`），以及赋值运算符 `+=`、`-=`、`*=`、`/=` 和 `%=` 从右到左结合。此表中的所有其他运算符从左到右结合。

| 运算符 | 结合性 |
|---|---|
| `++ (后缀)` `-- (后缀)` | 从左到右 |
| `+` `-` `++ (前缀)` `-- (前缀)` | 从右到左 |
| `*` `/` `%` | 从左到右 |
| `+` `-` | 从左到右 |
| `<<` `>>` | 从左到右 |
| `<` `<=` `>` `>=` | 从左到右 |
| `==` `!=` | 从左到右 |
| `?:` | 从右到左 |
| `=` `+=` `-=` `*=` `/=` `%=` | 从右到左 |

### 检查点

- **1. （代码）** 假设 `int` 变量 `counter` 的值为 10。执行以下语句后，`result` 和 `counter` 的值分别是多少？

  ```cpp
  int result{counter--};
  ```

  **答案：** 初始化表达式使用了后缀递减运算符，因此 `result` 将包含 10，`counter` 将包含 9。

- **2. （代码）** 假设 `int` 变量 `counter` 的值为 10。执行以下语句后，`result` 和 `counter` 的值分别是多少？

  ```cpp
  int result{++counter};
  ```

  **答案：** 初始化表达式使用了前缀递增运算符，因此 `result` 和 `counter` 都将包含 11。

## 3.13 基本类型不可移植

你可以在以下网址查看 C++ 基本类型的完整列表及其典型范围：

https://en.cppreference.com/w/cpp/language/types

在 C 和 C++ 中，一台机器上的 `int` 可能由 16 位（2 字节）内存表示，第二台机器上由 32 位（4 字节）表示，另一台机器上由 64 位（8 字节）表示。因此，使用整数的代码并不总是跨平台可移植的。你可以编写多个版本的程序，在不同平台上使用不同的整数类型。或者使用各种技术来实现不同程度的可移植性。⁶ 在下一节中，我们将展示实现可移植性的一种方法。

C++ 的整数类型包括 `int`、`long` 和 `long long`。C++ 标准要求 `int` 类型至少为 16 位，`long` 类型至少为 32 位，`long long` 类型至少为 64 位。标准还要求 `int` 的大小小于或等于 `long` 的大小，并且 `long` 的大小小于或等于 `long long` 的大小。这种“弹性”要求带来了可移植性挑战，但允许编译器实现者通过将基本类型大小与机器硬件相匹配来优化性能。

### 检查点

- **1. （对/错）** 所有计算机都以相同的字节数表示 `int`。

  **答案：** 错。一台机器上的 `int` 可能由 16 位（2 字节）内存表示，第二台机器上由 32 位（4 字节）表示，另一台机器上由 64 位（8 字节）表示。

- **2. （对/错）** C++ 标准要求 `int` 的大小小于或等于 `long` 的大小，并且 `long` 的大小小于或等于 `long long` 的大小。

  **答案：** 对。

## 3.14 对象自然案例研究：超大整数

互联网通信和联网设备上数据存储的爆炸式增长，极大地提高了隐私和安全的重要性。密码学已被使用了数千年，用于对数据进行编码，使未经授权的用户难以（并希望不可能）读取。⁷,⁸ 这在当今互联世界中至关重要。大多数网站（包括 deitel.com）现在都使用 HTTPS（超文本传输安全协议）来加密和解密你的互联网交互。

### 某些应用需要超出 `long long` 整数范围的整数

许多密码学算法使用的整数远大于我们甚至可以用 C++ 的 `long long` 类型存储的整数。在大多数系统上，`long long` 整数可以存储的范围是 −9,223,372,036,854,775,808 到 9,223,372,036,854,775,807——最多 19 个十进制数字（可以表示千亿亿数量级的整数）。

最流行的加密/解密方案之一是 RSA 公钥密码学，通常用于保护通过互联网传输的数据。⁹,¹⁰,¹¹ 工业级强度的 RSA 实现使用由数百位数字组成的巨大素数。

RSA 如此安全的一个关键原因是，即使对于当今最强大的超级计算机来说，分解这些素数的乘积所需的时间也是巨大的。公钥密码学也用于保护比特币等加密货币背后的区块链技术。¹² 在本书后面，我们将讨论并实现使用 RSA 的公钥密码学。

- 7. “Cryptography.” January 15, 2023. https://en.wikipedia.org/wiki/Cryptography#History.

- 8. Binance Academy, “History of Cryptography.” Accessed April 14, 2023. https://www.binance.vision/security/history-of-cryptography.

- 9. “RSA (Cryptosystem).” Accessed April 14, 2023. https://en.wikipedia.org/wiki/RSA_(cryptosystem).

- 10. “RSA Algorithm.” Accessed April 14, 2023. https://simple.wikipedia.org/wiki/RSA_algorithm.

- 11. K. Moriarty, B. Kaliski, J. Jonsson and A. Rusch, “PKCS #1: RSA Cryptography Specifications Version 2.2,” November 2016. Accessed April 14, 2023. https://tools.ietf.org/html/rfc8017.

- 12. Sarah Rothrie, “How Blockchain Cryptography Is Fighting the Rise of Quantum Machines,” December 28, 2018. Accessed April 14, 2023. https://coincentral.com/blockchain-cryptography-quantum-machines/.

