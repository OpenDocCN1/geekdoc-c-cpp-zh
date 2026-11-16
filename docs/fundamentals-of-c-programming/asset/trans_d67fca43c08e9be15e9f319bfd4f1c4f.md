

### 图 11.6 包含三个元素的简单数组

```
int list[3];
list[0] = 5;
list[1] = -3;
list[2] = 12;
```

![](img/e84ad11adb18201d71595b31ce6c9eff_323_0.png)

```
int list[3]; // Declare list to be an array of three ints
list[0] = 5 ; // Make the first element 5
list[1] = -3 ; // Make the second element -3
list[2] = 12 ; // Make the last element 12
```

这段代码片段表明，在声明点之后使用的方括号允许我们根据元素在数组所分配内存块中的位置来访问单个元素。这种语法与用于 vector 对象的语法相同。与 vector 一样，数组中的第一个元素出现在索引 0 处。

执行这些赋值语句后，list 数组在概念上如图 11.6 所示。

数组方括号运算符根据上下文具有两种不同的含义：

- 1. 在数组声明时，例如，
  `double nums[10];`
  方括号内的数字指定数组可以容纳的元素数量。编译器使用该数字以及数组的类型来确定为数组分配多少内存。

- 2. 在数组声明之后，例如，
  `nums[3] = 10.45;`
  方括号内的数字表示一个索引，用于定位数组所分配内存中的特定元素。

![](img/e84ad11adb18201d71595b31ce6c9eff_323_1.png)

与 vector 不同，编译器会坚持要求程序员对索引使用整数值；例如，以下语句：

```
numbers[1.3] = 5;
```

如果 numbers 是数组，则该语句非法。与 vector 类似，程序员必须确保数组索引在数组的边界内。通过超出数组边界的索引访问元素会导致未定义行为。

我们可以将数组传递给函数，如清单 11.11（arraytofunc.cpp）所示，这是清单 11.7（vectortofunc.cpp）的数组版本。

```
Listing 11.11: arraytofunc.cpp
#include <iostream>
/*
 * print(a, n)
 *
 * Prints the contents of an int array
 * a is the array to print
 * n is the size of the array
 */
void print(int a[], int n) {
    for (int i = 0; i < n; i++) {
        std::cout << a[i] << " ";
    }
    std::cout << '\n';
}
/*
 * sum(a, n)
 *
 * Adds up the contents of an int array
 * a is the array to sum
 * n is the size of the array
 */
int sum(int a[], int n) {
    int result = 0;
    for (int i = 0; i < n; i++)
        result += a[i];
    return result;
}
int main() {
    int list[] = { 2, 4, 6, 8 };
    // Print the contents of the array
    print(list, 4);
    // Compute and display sum
    std::cout << sum(list, 4) << '\n';
    // Zero out all the elements of list
    for (int i = 0; i < 4; i++)
        list[i] = 0;
    // Reprint the contents of the array
    print(list, 4);
    // Compute and display sum
    std::cout << sum(list, 4) << '\n';
}
```

如 print 函数的定义所示：

void print(int a[], int n)

空方括号跟在数组形式参数的名称后面。程序员可以在方括号内提供一个数字，但编译器会忽略它。在调用接受数组参数的函数时，例如

```
print(list, 4);
```

程序员必须将数组的大小连同数组名称一起传递。这是因为数组只是引用一块内存，并且没有其大小的概念。

在 C++ 源代码中，未修饰的数组名称本身的行为类似于指向数组起始元素的常量指针。因此，当数组作为实际参数在函数调用中传递时，如清单 11.11（arrayfunc.cpp）所示：

```
print(list, 4);
```

函数接收数组的地址——数组的地址绑定到形式参数。因此，虽然函数不能影响数组本身的地址，但函数可以完全访问数组的内容。在清单 11.12（cleararray.cpp）中，clear 函数修改传递给它的任何数组的内容，使所有元素都为零。

### 清单 11.12：cleararray.cpp

```
#include <iostream>

/*
 * print(a, n)
 *
 * Prints the contents of an int array
 * a is the array to print
 * n is the size of the array
 */
void print(int a[], int n) {
    for (int i = 0; i < n; i++) {
        std::cout << a[i] << " ";
    }
    std::cout << '\n';
}

/*
 * clear(a, n)
 *
 * Makes all the elements of array a zero
 * a is the array to zero out
 * n is the size of the array
 */
void clear(int a[], int n) {
    for (int i = 0; i < n; i++)
        a[i] = 0;
}

int main() {
    int list[] = { 2, 4, 6, 8 };
    // Print the contents of the array
    print(list, 4);
    // Zero out the array
    clear(list, 4);
    // Reprint the contents of the array
    print(list, 4);
}
```

清单 11.12（cleararray.cpp）的输出是

```
2 4 6 8
0 0 0 0
```

clear 函数实际上修改了 main 的 list 数组的内容。该函数操作数组的实际元素，而不是其元素的副本。

因此，数组默认情况下按引用传递其包含的元素。默认情况下，数组的内容可能被错误的函数损坏。为了保护数组，使函数可以读取其内容但不能修改其内容，必须将参数声明为 const，例如

```
int sum(const int a[], int n)
```

在清单 11.11（arrayofunc.cpp）中，print 和 sum 函数没有理由能够修改其数组参数的内容，因此应将 const 说明符添加到它们的定义中。

作为一般规则，所有接受数组参数的函数都应将数组内容声明为 const，除非它们需要修改数组的元素。

> 作为一般规则，所有接受数组参数的函数都应将数组内容声明为 const，除非它们需要修改数组的元素。例如，如果 sum 函数必须能够检查数组的内容但不打算修改其内容，则应使用
> `int sum(const int a[], int n)`
> 而不是
> `int sum(int a[], int n)`

C++ 不直接支持空数组。物理数组必须至少包含一个元素。有时，考虑一个在概念上为空的数组是合适的：例如，如果我们希望将一个“空”数组传递给 sum 函数怎么办？我们可以将 0 作为第二个参数传递，因为空数组不包含任何元素，但第一个参数应该传递什么呢？任何数组都可以，但当不需要真正的数组时，没有必要创建一个真实的数组。相反，我们可以使用 nullptr：

```
quantity = sum(nullptr, 0);
```

如果你仔细检查 sum 函数的函数体，你会发现这次调用会将正确答案（即零）赋值给 quantity。

## 11.2.2 指针和数组

在 C++ 源代码中使用的数组名称引用内存中的一个位置，即数组中第一个元素（索引 0 处的元素）的地址。在这方面，数组名称类似于常量指针（有关 C++ 指针的更多信息，请参见第 10.7 节）。因此，我们可以在某种程度上将数组标识符视为指针。同样，我们可以指示指针指向数组，然后将指针本身视为数组。

清单 11.13（pointerprint.cpp）使用指针遍历数组。

```
Listing 11.13: pointerprint.cpp
#include <iostream>

int main() {
    int a[] = { 2, 4, 6, 8, 10, 12, 14, 16, 18, 20 },
        *p;

    p = &a[0]; // p points to first element of array a

    // Print out the contents of the array
    for (int i = 0; i < 10; i++) {
        std::cout << *p << ' '; // Print the element p points to
        p++; // Increment p so it points to the next element
    }
    std::cout << '\n';
}
```

语句
p = &a[0];
将 p 设置为指向数组 a 的第一个元素。完成同一件事的更简短的方法是
p = a；

因为 a 本身就是对数组内存位置的引用。这个赋值语句清楚地展示了数组变量和指针变量之间的关联。请注意，相反的赋值（a = p）是不可能的，因为上面声明的数组 a 不能单独出现在赋值运算符的左侧。

指针变量可以参与加法和减法表达式。语句
p++;
会更改 p 中存储的地址，因此随后指针将指向内存中的下一个整数位置。如果 p 被赋值给数组 a，则递增 p 会将其重定向到指向 a 的下一个元素。1 在图 11.7 中，指针 p 被赋值给数组 a，然后递增以引用 a 中的各种元素。

表达式
p[0]
是编写
*p

的另一种方式，因此数组索引运算符（[]）可以与指针一起使用。表达式
p[5]

1 内存中的每个字节都有一个唯一的数值地址。由于大多数 C++ 类型需要多于一个字节的存储空间，将指针递增 1 并不会简单地将其持有的地址加 1。添加的量取决于指针的类型，例如，在使用 32 位（4 字节）整数的系统上，将 1 加到整数指针变量会使其地址增加 4，而不是 1。编译器知道指针变量的类型，因为程序员必须声明所有变量。因此，编译器可以自动调整算术运算以使其正常工作。如果指针指向数组中的内存并且与数组的类型相同，则递增指针会正确地将指针重新定位到指向数组中的下一个元素。

