
对 bitset `b` 和 `b1` 逐位执行逻辑 AND。结果存储在 `b` 中。按位逻辑 OR 和按位逻辑 XOR 通过以下语句执行

```cpp
b |= b1;
b ^= b2;
```

表达式

```cpp
b >>= n;
```

将 bitset `b` 中的位向右移动 `n` 个位置。表达式

```cpp
b <<= n;
```

将 bitset `b` 中的位向左移动 `n` 个位置。表达式

```cpp
b.to_string()
b.to_ulong()
```

分别将 bitset `b` 转换为字符串和无符号长整型。

### 使用 bitset 的埃拉托斯特尼筛法

图 22.40 重新讨论我们在练习 7.29 中讨论过的用于寻找素数的埃拉托斯特尼筛法。该算法使用 bitset 而不是数组来实现。程序显示从 2 到 1023 的所有素数，然后允许用户输入一个数，以判断该数是否为素数。

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
   sieve.flip(); // flip all bits in bitset sieve
   sieve.reset( 0 ); // reset first bit (number 0)
   sieve.reset( 1 ); // reset second bit (number 1)

   // perform Sieve of Eratosthenes
   int finalBit = sqrt( static_cast<double >( sieve.size() ) ) + 1;

   // determine all prime numbers from 2 to 1024
   for ( int i = 2; i < finalBit; i++ )
   {
      if ( sieve.test( i ) ) // bit i is on
      {
```

**图 22.40** | 类 bitset 与埃拉托斯特尼筛法。（第 1 部分，共 3 部分。）

```text
Enter a value from 2 to 1023 (-1 to end): 389
389 is a prime number

Enter a value from 2 to 1023 (-1 to end): 88
88 is not a prime number

Enter a value from 2 to 1023 (-1 to end): -1
```

**图 22.40** | 类 bitset 与埃拉托斯特尼筛法。（第 3 部分，共 3 部分。）

第 13 行创建一个包含 `SIZE` 位的 bitset（本例中大小为 1024）。默认情况下，bitset 中的所有位都设置为“关”。第 14 行调用函数 flip 将所有位设置为“开”。数字 0 和 1 不是素数，因此第 15—16 行调用函数 reset 将第 0 位和第 1 位设置为“关”。第 22—29 行确定从 2 到 1023 的所有素数。整数 finalBit（第 19 行）用于确定算法何时完成。基本算法是：如果一个数除了 1 和它本身之外没有其他约数，那么它就是素数。从数字 2 开始，我们可以消除该数字的所有倍数。数字 2 只能被 1 和它本身整除，因此它是素数。因此，我们可以消除 4、6、8 等。数字 3 只能被 1 和它本身整除。因此，我们可以消除 3 的所有倍数（请记住，所有偶数都已经被消除）。

## 22.7 函数对象

许多 STL 算法允许你向算法传入函数指针，以帮助算法执行任务。例如，我们在 22.5.6 节讨论的 binary_search 算法有一个重载版本，它要求第四个参数是一个指向函数的指针，该函数接受两个参数并返回 bool 值。binary_search 算法使用这个函数将搜索键与集合中的元素进行比较。如果搜索键与被比较的元素相等，该函数返回 true；否则返回 false。这使得 binary_search 能够搜索这样的元素集合：其元素类型没有提供重载的相等 `==` 运算符。

STL 的设计者通过允许任何可接收函数指针的算法接收一个类对象，使算法更加灵活；该类重载了圆括号运算符，函数名为 `operator()`，前提是该重载运算符满足算法的要求——对于 binary_search 来说，它必须接收两个参数并返回 bool。这种类的对象称为函数对象，可以在语法和语义上像函数或函数指针一样使用——通过使用函数对象的名称后跟包含函数实参的圆括号来调用重载的圆括号运算符。函数对象与所使用的函数统称为仿函数。大多数算法可以互换使用函数对象和函数。

与函数指针相比，函数对象具有若干优点。由于函数对象通常实现为类模板，并被包含到每个使用它们的源代码文件中，因此编译器可以内联重载的 `operator()` 以提高性能。此外，由于它们是类的对象，函数对象可以拥有数据成员，`operator()` 可以使用这些数据成员来执行任务。

### 标准模板库的预定义函数对象

许多预定义函数对象可在头文件 `<functional>` 中找到。图 22.41 列出了若干 STL 函数对象，它们都实现为类模板。我们在 set、multiset 和 priority_queue 示例中使用了函数对象 less<T>，以指定容器中元素的排序顺序。

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

### 使用 STL accumulate 算法

图 22.42 演示了 accumulate 数值算法（在图 22.30 中讨论过）来计算 vector 中元素的平方和。accumulate 的第四个参数是一个二元函数对象（即其 `operator()` 接受两个参数的函数对象）或指向二元函数的函数指针（即接受两个参数的函数）。函数 accumulate 被演示了两次——一次使用函数指针，一次使用函数对象。

```cpp
1  // Fig. 22.42: Fig22_42.cpp
2  // Demonstrating function objects.
3  #include <iostream>
4  #include <vector> // vector class-template definition
5  #include <algorithm> // copy algorithm
6  #include <numeric> // accumulate algorithm
7  #include <functional> // binary_function definition
8  #include <iterator> // ostream_iterator
9  using namespace std;
10
11 // binary function adds square of its second argument and the
12 // running total in its first argument, then returns the sum
13 int sumSquares( int total, int value )
14 {
15    return total + value * value;
16 } // end function sumSquares
17
```

**图 22.42** | 二元函数对象。（第 1 部分，共 2 部分。）

第 13—16 行定义了一个函数 sumSquares，它将其第二个参数 value 平方，将该平方与其第一个参数 total 相加，并返回和。在示例中，函数 accumulate 会将它所迭代序列的每个元素作为第二个参数传递给 sumSquares。第一次调用 sumSquares 时，第一个参数将是 total 的初始值（作为 accumulate 的第三个参数提供；本程序中为 0）。随后对 sumSquares 的所有调用都会将上一次调用 sumSquares 返回的累计和作为第一个参数。当 accumulate 完成时，它返回序列中所有元素的平方和。

第 21—30 行定义了一个类 SumSquaresClass，它继承自类模板 **binary_function**（位于头文件 `<functional>` 中）——这是一个空基类，用于创建 `operator()` 接受两个参数并返回值的函数对象。类 binary_function 接受三个类型参数，分别表示 `operator()` 的第一个参数、第二个参数和返回值的类型。在此示例中，这些参数的类型为 T（第 22 行）。第一次调用该函数对象时，第一个参数将是 total 的初始值（作为 accumulate 的第三个参数提供：本程序中为 0），第二个参数将是 vector integers 中的第一个元素。随后对 `operator()` 的所有调用都会将上一次调用该函数对象返回的结果作为第一个参数，第二个参数将是 vector 中的下一个元素。当 accumulate 完成时，它返回 vector 中所有元素的平方和。

第 45—46 行调用函数 accumulate，并将指向函数 sumSquares 的指针作为其最后一个参数。第 53—54 行的语句调用函数 accumulate，并将类 SumSquaresClass 的对象作为最后一个参数。表达式 `SumSquaresClass< int >()` 创建类 SumSquaresClass 的一个实例（一个函数对象），该实例被传递给 accumulate，accumulate 向该对象发送消息（调用函数）`operator()`。该语句可以写成两条单独的语句，如下所示：

```cpp
SumSquaresClass< int > sumSquaresObject;
result = accumulate( integers.begin(), integers.end(),
    0, sumSquaresObject );
```

第一行定义类 SumSquaresClass 的一个对象。然后该对象被传递给函数 accumulate。

## 22.8 小结

本章中，我们介绍了标准模板库，并讨论了它的三个关键组成部分——容器、迭代器和算法。你学习了 STL 序列容器 vector、deque 和 list，它们表示线性数据结构。我们讨论了关联容器 set、multiset、map 和 multimap，它们表示非线性数据结构。你还了解到，容器适配器 stack、queue 和 priority_queue 可用于限制序列容器的操作，以实现容器适配器所表示的专用数据结构。随后，我们演示了许多 STL 算法，包括数学算法、基本搜索和排序算法以及集合操作。你学习了每种算法所需的迭代器类型，以及每种算法都可以与任何支持该算法所需最低迭代器功能的容器一起使用。你还学习了类 bitset，它使以容器方式创建和操作位变得容易。最后，我们介绍了
