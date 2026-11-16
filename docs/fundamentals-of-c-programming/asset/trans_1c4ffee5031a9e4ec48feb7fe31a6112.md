

编译器会提醒我们这一事实。要了解为什么不应该轻视此警告，请考虑以下我们预期不会打印任何内容的代码：

```
unsigned u = 0;
int i = 0;
while (i < u - 1) {
    std::cout << i << '\n';
    i++;
}
```

但相反，它会打印出系统支持的尽可能多的无符号值！这是因为尽管 0 不小于 -1，但 -1 是有符号值，而不是无符号值。无符号数据类型无法表示有符号数。在 32 位系统上尝试计算无符号 0 减 1 会产生 4,294,967,295，这肯定不小于零。为保险起见，请将 size 方法的值赋给 int 变量，或使用无符号变量来控制循环迭代。更好的做是，尽可能使用基于范围的 for 语句。

empty 方法是一个便捷方法；如果 vec 是一个向量，表达式 vec.empty() 等价于布尔表达式 vec.size() == 0。请注意，empty 方法并不会使向量为空；它只是在向量为空时返回 true，否则返回 false。

clear 方法会移除向量中的所有元素，使其为空。在最初为空的向量上调用 clear 没有任何效果。清空向量后，向量的 size 方法将返回零，其 empty 方法将返回 true，而对其 operator[] 方法使用任何值（包括零）作为索引的调用将表现出未定义行为。

## 11.1.4 向量与函数

函数可以将向量作为参数接受，如清单 11.7（vectortofunc.cpp）所示。

```
Listing 11.7: vectortofunc.cpp
#include <iostream>
#include <vector>

/*
 * print(v)
 *   Prints the contents of an int vector
 *   v is the vector to print
 */
void print(std::vector<int> v) {
    for (int elem : v) {
        std::cout << elem << " ";
    }
    std::cout << '\n';
}

/*
 * sum(v)
 *   Adds up the contents of an int vector
 *   v is the vector to sum
 *   Returns the sum of all the elements
 *   or zero if the vector is empty.
 */
int sum(std::vector<int> v) {
    int result = 0;
    for (int elem : v)
        result += elem;
    return result;
}

int main() {
  std::vector<int> list{ 2, 4, 6, 8, };
  // Print the contents of the vector
  print(list);
  // Compute and display sum
  std::cout << sum(list) << '\n';
  // Zero out all the elements of list
  for (int i = 0; i < list.size(); i++)
    list[i] = 0;
  // Reprint the contents of the vector
  print(list);
  // Compute and display sum
  std::cout << sum(list) << '\n';
}
```

清单 11.7（vectortofunc.cpp）生成：

```
2 4 6 8
20
0 0 0 0
0
```

print 函数的定义：

```
void print(std::vector<int> v) {
```

这表明向量形式参数的声明方式与非向量形式参数相同。在此例中，print 函数使用按值传递，因此在程序执行期间，对 print 的调用会将实际参数（list）中的数据复制到形式参数（v）中。由于向量可能非常大，因此如上所示按值传递向量通常效率低下。按值传递要求函数调用为形式参数创建一个新的向量对象，并将实际参数的所有元素复制到该局部于函数的新向量中。更好的方法是使用按引用传递，但有一个变体：

```
void print(const std::vector<int>& v) {
  for (int elem : v)
    std::cout << elem << " ";
  std::cout << '\n';
}
```

& 符号表示调用 print 的调用者将按引用传递 v（参见第 10.9 节）。这会将实际参数（由调用者拥有）的地址复制到形式参数 v，而不是复制调用者向量中的所有数据。传递地址效率高得多，因为在大多数系统上，地址的大小与单个 int 相同，而向量例如可能包含 1,000,000 个 int。使用按值传递时，函数调用将不得不从调用者的实际参数中复制所有这 1,000,000 个整数到函数的形式参数中。

第 10.9 节指出，按值传递参数优于按引用传递参数。这是因为使用按值传递的函数无法修改调用者传递给它的实际变量。请仔细观察，我们的新 print 函数将其形式参数 v 声明为 const 引用。这意味着该函数无法修改调用者传递的实际参数。将向量对象作为常量引用传递，使我们能够在获得按值传递安全性的同时，实现按引用传递的效率。

不过，按常量引用传递与按值传递不同。接收按值传递参数的函数可以修改该参数并返回其修改后的副本。使用按常量引用传递的函数无法修改传递给它的参数。

与 print 函数一样，清单 11.7（vectortofunc.cpp）中的 sum 函数也不打算修改其向量参数的内容。由于 sum 函数只需查看向量的内容，因此其向量参数应声明为 const 引用。一般来说，如果函数的目的是修改向量，则引用不应为 const。清单 11.8（makerandomvector.cpp）使用一个名为 make_random 的函数，该函数用伪随机整数值填充向量。

```
Listing 11.8: makerandomvector.cpp

#include <iostream>
#include <vector>
#include <cstdlib> // For rand

/*
 * print(v)
 * Prints the contents of an int vector
 * v is the vector to print; v is not modified
 */
void print(const std::vector<int>& v) {
    for (int elem : v)
        std::cout << elem << " ";
    std::cout << "\n";
}

/*
 * make_random(v)
 * Fills an int vector with pseudorandom numbers
 * v is the vector to fill; v is modified
 * size is the maximum size of the vector
 */
void make_random(std::vector<int>& v, int size) {
    v.clear(); // Empties the contents of vector
    int n = rand() % size + 1; // Random size for v
    for (int i = 0; i < n; i++)
        v.push_back(rand()); // Populate with random values
}

int main() {
    srand(2); // Set pseudorandom number generator seed
    std::vector<int> list;
    // Print the contents of the vector
    std::cout << "Vector initially: ";
    print(list);
    print(list);
    make_random(list, 5);
    std::cout << "2nd random vector: ";
    print(list);
    make_random(list, 10);
    std::cout << "3rd random vector: ";
    print(list);
}
```

清单 11.8（makerandomvector.cpp）中的 make_random 函数调用向量方法 clear，该方法使向量为空。我们先调用 clear 是因为我们希望在添加更多元素之前确保向量为空。然后该函数会向空向量中添加随机数量的随机整数。

函数可以返回向量对象。清单 11.9（primelist.cpp）是一个返回向量的函数的实际示例。

Listing 11.9: primelist.cpp

```
#include <iostream>
#include <vector>
#include <cmath>

/*
print(v)
*
* Prints the contents of an int vector
* v is the vector to print; v is not modified
*/
void print(const std::vector<int>& v) {
    for (int elem : v)
        std::cout << elem << " ";
    std::cout << '\n';
}

/*
is_prime(n)
*
* Determines the primality of a given value
* n an integer to test for primality
* Returns true if n is prime; otherwise, returns false
*/
bool is_prime(int n) {
    if (n < 2)
        return false;
    else {
        bool result = true; // Provisionally, n is prime
        double r = n, root = sqrt(r);
        // Try all possible factors from 2 to the square
        // root of n
        for (int trial_factor = 2; result && trial_factor <= root;
             trial_factor++)
            result = (n % trial_factor != 0);
        return result;
    }
}

/*
* primes(begin, end)
*
* Returns a vector containing the prime
* numbers in the range begin...end.
*
* begin is the first number in the range
* end is the last number in the range
*/
std::vector<int> primes(int begin, int end) {
    std::vector<int> result;
    for (int i = begin; i <= end; i++)
        if (is_prime(i))
            result.push_back(i);
    return result;
}

int main() {
    int low, high;
    std::cout << "Please enter lowest and highest values in "
              << "the range: ";
    std::cin >> low >> high;
    std::vector<int> prime_list = primes(low, high);
    print(prime_list);
}
```

primes 函数声明了一个名为 result 的局部向量变量。该函数检查 begin...end 范围内的每个值（包含两端）。primes 函数将 is_prime 用作辅助函数。如果 is_prime 函数将某个值分类为素数，primes 函数中的代码会将该值添加到 result 向量中。在 primes 考虑了所提供范围内的所有值后，result 将包含该范围内的所有素数。最终，primes 返回包含指定范围内所有素数的向量。

当返回像 int、double、char 等内置标量类型的局部变量时，C++ 函数通常会复制该局部变量以返回给调用者。之所以需要复制，是因为局部变量仅在声明它们的函数正在执行期间存在。当函数执行完毕并返回给调用者时，运行时环境会回收函数局部变量和参数所占用的内存，以便其他函数可以使用这些空间。

primes 中的返回值不是简单的标量类型——它是一个对象，可能非常大，尤其是当调用者传入一个大范围时。现代 C++ 编译器生成机器代码，消除了复制局部向量 result 的必要性。这种技术称为返回值优化，当函数返回在函数内声明的对象时会发挥作用。使用返回值优化时，编译器“知道”该变量将消失且该变量要返回给调用者；因此，它生成机器语言代码，在调用者的内存空间中为结果分配空间，而不是在被调用函数中。由于调用者维护着对象的空间，该对象在函数返回后仍然存在。正因为有返回值优化，你可以在类似这种情况下按值返回向量，而无需担心耗时的复制操作。

