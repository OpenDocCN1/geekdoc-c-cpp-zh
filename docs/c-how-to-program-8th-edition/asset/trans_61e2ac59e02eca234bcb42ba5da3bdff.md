
语句

```cpp
b.reset( bitNumber );
```

将 bitset b 的第 bitNumber 位置为“关闭”。表达式 `b.reset()` 将 b 中的所有位置为“关闭”。语句

```cpp
b.flip( bitNumber );
```

“翻转” bitset b 的第 bitNumber 位（例如，如果该位为开，则 flip 将其置为关）。表达式 `b.flip()` 翻转 b 中的所有位。语句

```cpp
b[ bitNumber ];
```

返回对 bitset b 的第 bitNumber 位的引用。类似地，

```cpp
b.at( bitNumber );
```

首先对 bitNumber 执行范围检查。然后，如果 bitNumber 在范围内，`at` 返回对该位的引用。否则，`at` 抛出 `out_of_range` 异常。语句

```cpp
b.test( bitNumber );
```

首先对 bitNumber 执行范围检查。如果 bitNumber 在范围内，则如果该位为开，`test` 返回 true；如果该位为关，返回 false。否则，`test` 抛出 `out_of_range` 异常。表达式

```cpp
b.size()
```

返回 bitset b 中的位数。表达式

```cpp
b.count()
```

返回 bitset b 中被置位的位数。表达式

```cpp
b.any()
```

如果 bitset b 中任一位被置位，则返回 true。表达式

```cpp
b.none()
```

如果 bitset b 中没有任何位被置位，则返回 true。表达式

```cpp
b == b1
b != b1
```

分别比较两个 bitset 是否相等和不等。

每个按位赋值运算符 `&=`, `|=` 和 `^=` 都可用于组合 bitset。例如，

```cpp
b &= b1;
```

在 bitset b 和 b1 之间执行逐位逻辑与。结果存储在 b 中。按位逻辑或和按位逻辑异或由以下语句执行：

```cpp
b |= b1;
b ^= b2;
```

表达式

```cpp
b >>= n;
```

将 bitset b 中的位右移 n 个位置。表达式

```cpp
b <<= n;
```

将 bitset b 中的位左移 n 个位置。表达式

```cpp
b.to_string()
b.to_ulong()
```

分别将 bitset b 转换为字符串和无符号长整型。

## 使用 bitset 的埃拉托斯特尼筛法

图 22.40 重新讨论了我们在练习 7.29 中讨论过的用于寻找质数的埃拉托斯特尼筛法。该算法使用 bitset 而不是数组来实现。程序显示从 2 到 1023 的所有质数，然后允许用户输入一个数，以确定该数是否为质数。

```cpp
// Fig. 22.40: Fig22_40.cpp
// Using a bitset to demonstrate the Sieve of Eratosthenes.
#include <iostream>
#include <iomanip>
#include <cmath>
#include <bitset> // bitset class definition
using namespace std;

int main()
{
   const int SIZE = 1024;
   int value;
   bitset<SIZE> sieve; // create bitset of 1024 bits
   sieve.flip(); // fill all bits in bitset with 1
   sieve.reset( 0 ); // reset first bit (number 0)
   sieve.reset( 1 ); // reset second bit (number 1)

   // perform Sieve of Eratosthenes
   int finalBit = sqrt( static_cast<double >( sieve.size() ) ) + 1;

   // determine all prime numbers from 2 to 1024
   for ( int i = 2; i < finalBit; ++i )
   {
      if ( sieve.test( i ) ) // bit i is on
      {
         for ( int j = 2 * i; j < SIZE; j += i )
            sieve.reset( j ); // set bit j off
      } // end if
   } // end for

   cout << "The prime numbers in the range 2 to 1023 are:\n";

   // display prime numbers in range 2–1023
   for ( int k = 2, counter = 1; k < SIZE; ++k )
   {
```

**图 22.40** | bitset 类与埃拉托斯特尼筛法。（第 1 部分，共 2 部分。）

第 13 行创建一个包含 SIZE 位的 bitset（本例中 SIZE 为 1024）。默认情况下，bitset 中的所有位都被置为“关闭”。第 14 行调用函数 `flip` 将所有位置为“开启”。数字 0 和 1 不是质数，因此第 15–16 行调用函数 `reset` 将第 0 位和第 1 位置为“关闭”。第 22–29 行确定从 2 到 1023 的所有质数。整数 `finalBit`（第 19 行）用于确定算法何时完成。基本算法是：如果一个数除了 1 和它本身之外没有其他约数，那么它就是质数。从数字 2 开始，我们可以消除该数字的所有倍数。数字 2 只能被 1 和它本身整除，所以它是质数。因此，我们可以消除 4、6、8 等。数字 3 只能被 1 和它本身整除。因此，我们可以消除 3 的所有倍数（请记住，所有偶数都已经被消除了）。

## 22.10 函数对象

许多 STL 算法允许将函数指针传入算法，以帮助算法完成其任务。例如，我们在 22.8.6 节讨论过的 `binary_search` 算法有一个重载版本，其第四个参数要求是一个指向函数的指针，该函数接受两个参数并返回 bool 值。`binary_search` 算法使用该函数将搜索键与集合中的元素进行比较。如果搜索键与正在比较的元素相等，该函数返回 true；否则，该函数返回 false。这使得 `binary_search` 能够搜索元素类型未提供重载相等运算符 `==` 的元素集合。

STL 的设计者通过允许任何可接收函数指针的算法也接收这样一种类的对象，使算法更加灵活：该类重载了括号运算符，其函数名为 `operator()`，前提是该重载运算符满足算法的要求——对于 `binary_search`，它必须接收两个参数并返回 bool。这种类的对象称为函数对象，在语法和语义上可以像函数或函数指针一样使用——调用重载括号运算符的方式是使用函数对象的名称，后跟包含函数参数的括号。函数对象和函数一起被称为仿函数（functors）。大多数算法可以互换地使用函数对象和函数。

与函数指针相比，函数对象具有若干优点。由于函数对象通常实现为类模板，并被包含到使用它们的每个源代码文件中，因此编译器可以内联重载的 `operator()` 以提高性能。此外，由于它们是类的对象，函数对象可以拥有数据成员，供 `operator()` 用来执行其任务。

### 标准模板库的预定义函数对象

许多预定义函数对象可在头文件 `<functional>` 中找到。图 22.41 列出了若干 STL 函数对象，它们都实现为类模板。我们在 set、multiset 和 priority_queue 示例中使用了函数对象 `less<T>`，以指定容器中元素的排序顺序。

| STL 函数对象 | 类型 | STL 函数对象 | 类型 |
|---|---|---|---|
| `divides<T>` | 算术 | `logical_or<T>` | 逻辑 |
| `equal_to<T>` | 关系 | `minus<T>` | 算术 |
| `greater<T>` | 关系 | `modulus<T>` | 算术 |
| `greater_equal<T>` | 关系 | `negate<T>` | 算术 |
| `less<T>` | 关系 | `not_equal_to<T>` | 关系 |
| `less_equal<T>` | 关系 | `plus<T>` | 算术 |
| `logical_and<T>` | 逻辑 | `multiplies<T>` | 算术 |
| `logical_not<T>` | 逻辑 |  |  |

**图 22.41** | 标准库中的函数对象。

### 使用 STL 的 accumulate 算法

图 22.42 演示了 accumulate 数值算法（在图 22.30 中讨论过），用于计算 vector 中元素的平方和。accumulate 的第四个参数是一个二元函数对象（即其 `operator()` 接受两个参数的函数对象），或指向**二元函数**（即接受两个参数的函数）的函数指针。函数 accumulate 演示了两次——一次使用函数指针，一次使用函数对象。

```cpp
// Fig. 22.42: Fig22_42.cpp
// Demonstrating function objects.
#include <iostream>
#include <vector> // vector class-template definition
#include <algorithm> // copy algorithm
#include <numeric> // accumulate algorithm
#include <functional> // binary_function definition
#include <iterator> // ostream_iterator
using namespace std;

// binary function adds square of its second argument and the
// running total in its first argument, then returns the sum
int sumSquares( int total, int value )
{
   return total + value * value;
} // end function sumSquares

// binary function class template defines overloaded operator()
// that adds the square of its second argument and running
// total in its first argument, then returns the sum
template< typename T >
class SumSquaresClass : public binary_function< T, T, T >
{
public:
   // add square of value to total and return result
   T operator()( const T &total, const T &value )
   {
      return total + value * value;
   } // end function operator()
}; // end class SumSquaresClass
```

**图 22.42** | 二元函数对象。（第 1 部分，共 2 部分）
