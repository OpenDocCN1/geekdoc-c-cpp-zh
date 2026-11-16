
## 清单 10.16: referencevar.cpp

```
#include <iostream>

int main() {
    int x = 5;
    int y = x;
    int& r = x;

    std::cout << "x = " << x << '\n';
    std::cout << "y = " << y << '\n';
    std::cout << "r = " << r << '\n';

    std::cout << "Assign 7 to x\n";
    x = 7;

    std::cout << "x = " << x << '\n';
    std::cout << "y = " << y << '\n';
    std::cout << "r = " << r << '\n';

    std::cout << "Assign 8 to y\n";
    y = 8;

    std::cout << "x = " << x << '\n';
    std::cout << "y = " << y << '\n';
    std::cout << "r = " << r << '\n';

    std::cout << "Assign 2 to r\n";
    r = 2;

    std::cout << "x = " << x << '\n';
    std::cout << "y = " << y << '\n';
    std::cout << "r = " << r << '\n';
}
```

清单 10.16 (referencevar.cpp) 的输出：

```
x = 5
y = 5
r = 5
Assign 7 to x
x = 7
y = 7
r = 7
Assign 8 to y
x = 8
y = 8
r = 8
Assign 2 to r
x = 2
y = 8
r = 2
```

清楚地表明，变量 x 和 r 表示同一量。重新赋值 x 会以完全相同的方式改变 r，重新赋值 r 也会以完全相同的方式改变 x。另一方面，变量 y 与 x 和 r 都独立。重新赋值 x 或 r 都不会影响 y，重新赋值 y 也不会影响 x 或 r。

声明引用变量时使用的 & 符号周围的空格无关紧要；具体来说，语句

```
int& r = x;
```

等效于

```
int &r = x;
```

引用变量与指针变量相似，但存在一些重要区别。引用语法比指针语法更简单，因为无需解引用引用变量即可分配其所指的内存位置。如果 num 是 int，ptr 是指向 int 的指针，ref 是指向 int 的引用，请考虑以下语句：

```
num = ref; // Assign num from ref, no need to dereference
num = *ptr; // Assign num from ptr, must dereference with *
```

与指针变量相比，引用变量有两个重大限制：

- 引用变量在声明时必须用实际变量进行初始化。指针变量可以在没有初始值的情况下声明，稍后再赋值。请考虑以下语句：

```
int *p; // Legal, we will assign p later
int& r; // Illegal, we must initialize r when declaring it
```

在 Visual C++ 下尝试编译此代码会提示编译器发出错误

```
error C2350: 'r': references must be initialized
```

- 引用变量在其生命周期内无法绑定到不同的变量。请考虑以下代码片段：

```
int x = 5, y = 7;
int *p = &x; // Binds p to point to x
int& r = x; // Binds r to x
p = &y; // Reassign p to point to y
r = y; // Assign y's value to x (via r)
```

语句

```
r = y;
```

不将 r 绑定到 y 变量。r 的声明将 r 绑定到 x 变量，直至 r 的生命周期结束。此语句仅通过引用 r 将 y 的值赋给 x。相比之下，我们可以随时自由地将指针变量绑定到任意选择的变量。

因此，在本示例中，引用变量的工作方式类似于必须绑定到变量且不能重定向到其他位置的指针。此外，与指针不同，尝试将 nullptr 赋给引用变量是非法的。引用与指针之间还有其他一些区别，此处不再深入探讨。引用变量提供的语法比指针变量更简单，因为在使用引用时不需要使用指针解引用运算符 (*)。

指针和引用之间还有一个重大区别——C++ 从 C 编程语言原样采用了指针，但 C 不提供引用。C++ 程序员经常使用用 C 编写的库函数，因此不应将引用与 C 代码混用非常重要。

第 10.9 节揭示了指针和引用在实现向函数传递引用方面的一个非常重要的实际应用。

## 10.9 按引用传递

向函数传递参数的默认技术是按值传递（参见第 9.3 节）。C++ 还支持按引用传递，也称为按引用调用，这允许函数修改调用者传递的形参的值。

请考虑清单 10.17 (faultyswap.cpp)，它使用一个函数，该函数试图交换其两个整数参数的值。

```
Listing 10.17: faultySwap.cpp

#include <iostream>

/* swap(a, b)
 * Attempts to interchange the values of
 * its parameters a and b. That it does, but
 * unfortunately it only affects the local
 * copies.
 */
void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}

/* main
 * Attempts to interchange the values of
 * two variables using a faulty swap function.
 */
int main() {
    int var1 = 5, var2 = 19;
    std::cout << "var1 = " << var1 << ", var2 = " << var2 << '\n';
    swap(var1, var2);
    std::cout << "var1 = " << var1 << ", var2 = " << var2 << '\n';
}
```

清单 10.17 (faultyswap.cpp) 的输出是

```
var1 = 5, var2 = 19
var1 = 5, var2 = 19
```

不幸的是，swap 函数仅交换实际参数的副本，而非实际参数本身。我们真正希望编写一个交换调用者变量的函数。

要实现所需效果，必须使用按引用传递。C++ 可以通过两种方式实现按引用传递：指针参数和引用参数。

### 10.9.1 通过指针按引用传递

指针（参见第 10.7 节）允许我们访问变量的内存位置。我们可以利用此功能，允许函数修改其调用者拥有的变量的值。清单 10.18 (swapwithpointers.cpp) 提供了我们变量交换程序的正确版本。

## 清单 10.18: swapwithpointers.cpp

```
#include <iostream>
/*
 * swap(a, b)
 *   Interchanges the values of memory
 *   referenced by its parameters a and b.
 *   It effectively interchanges the values
 *   of variables in the caller's context.
 */
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
/*
 * main
 *   Interchanges the values of two variables
 *   using the swap function.
 */
int main() {
    int var1 = 5, var2 = 19;
    std::cout << "var1 = " << var1 << ", var2 = " << var2 << '\n';
    swap(&var1, &var2);
    std::cout << "var1 = " << var1 << ", var2 = " << var2 << '\n';
}
```

清单 10.18 (swapwithpointers.cpp) 的输出是

```
var1 = 5, var2 = 19
var1 = 19, var2 = 5
```

这就是我们试图实现的结果。swap 函数可以直接操作 main 的变量，因为我们将这些变量的指针传递给了它。

在清单 10.18 (swapwithpointers.cpp) 中：

- swap 的形参 a 和 b 是指向整数的指针，它们本身不是整数。为了访问名为 a 的指针所指向的整数，必须对其进行解引用。这就是为什么在 swap 的函数体中对 a 的任何使用都要加上指针解引用运算符 * 的原因。语句 `int temp = *a;` 将 a 所指向的变量的值赋给局部变量 temp。由于 main 在调用 swap 时将 var1 的地址作为第一个参数传递，在此例中 a 指向 var1，因此 *a 实际上是访问 main 中 var1 内存位置的另一种方式。因此，该函数将 main 的 var1 变量的值赋给 temp。

- 在 swap 的语句中：
  `*a = *b;`
  由于 *a 实际上是 main 的 var1 变量，*b 实际上是 main 的 var2 变量，因此该语句将 main 的 var2 的值赋给其 var1 变量。

- swap 函数的 `*b = temp;` 语句将局部 temp 值赋给 main 的 var2 变量，因为 swap 的 b 参数指向 main 的 var2。

- 在 main 中，调用 `swap(&var1, &var2);` 将其局部变量的地址传递给 swap。

实际上，使用指针的按引用传递仍然使用按值传递。我们传递的不是值的副本，而是地址的副本。例如，在清单 10.18 (swapwithpointers.cpp) 中，var1 和 var2 的地址值被复制到形参 a 和 b。区别在于，我们并非试图重新赋值 a 或 b，而是重新赋值 a 和 b 所指向的内存。无论使用原始地址还是地址的副本，它仍然是同一个地址——内存中相同的数值位置。

### 10.9.2 通过引用按引用传递

C 和 C++ 都支持使用指针进行按引用传递（参见第 10.9.1 节）。由于 C++ 程序经常使用 C 库，C++ 程序员必须熟悉按引用传递的指针技术。然而，C++ 提供了一种使用 _引用参数_ 实现按引用传递的更简单方法。（有关引用变量的介绍，请参见第 10.8 节。）清单 10.19 (swapwithreferences.cpp) 在我们的变量交换程序中使用了引用参数。

```
Listing 10.19: swapwithreferences.cpp

#include <iostream>

/*
 * swap(a, b)
 *  Interchanges the values of memory
 *  referenced by its parameters a and b.
 *  It effectively interchanges the values
 *  of variables in the caller's context.
 */
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

/*
 * main
 *  Interchanges the values of two variables
 *  using the swap function.
 */
int main() {
    int var1 = 5, var2 = 19;
    std::cout << "var1 = " << var1 << ", var2 = " << var2 << '\n';
    swap(var1, var2);
    std::cout << "var1 = " << var1 << ", var2 = " << var2 << '\n';
}
```
