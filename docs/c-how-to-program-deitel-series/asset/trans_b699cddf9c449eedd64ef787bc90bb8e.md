

```cpp
cout << "\nThe maximum of 'G' and 'Z' is: " << max( 'G', 'Z' );

// determine which argument is the min and which is the max
auto result1 = minmax( { 12, 7 } );
cout << "\nThe minimum of 12 and 7 is: " << result1.first
     << "\nThe maximum of 12 and 7 is: " << result1.second;

array< int, 10 > items = { 3, 100, 52, 77, 22, 31, 1, 98, 13, 40 };
ostream_iterator<int> output( cout, " " );

cout << "\nArray items contains:";
copy( items.cbegin(), items.cend(), output );

auto result2 = minmax_element( items.cbegin(), items.cend() );
cout << "\nThe minimum element in items is: " << *result2.first
     << "\nThe maximum element in items is: " << *result2.second
     << endl;
} // end main
```

```text
The minimum of 12 and 7 is: 7
The maximum of 12 and 7 is: 12
The minimum of 'G' and 'Z' is: G
The maximum of 'G' and 'Z' is: Z

The minimum of 12 and 7 is: 7
The maximum of 12 and 7 is: 12

Array items contains: 3 100 52 77 22 31 1 98 13 40
The minimum element in items is: 1
The maximum element in items is: 100
```

图 16.13 | 算法 min、max、minmax 和 minmax_element。（第 2 部分，共 2 部分。）

### 两个参数版本的算法 min 和 max

算法 min 和 max（在第 10–13 行演示）分别确定两个元素的最小值和最大值。

### C++11：带 initializer_list 参数的 min 和 max 算法

C++11 现在包含了 min 和 max 算法的重载版本，每个版本接收一个 initializer_list 参数，并返回列表初始化器参数中的最小或最大项。例如，以下语句返回 7：

```cpp
int minimum = min( { 10, 7, 14, 21, 17 } );
```

这些新的 min 和 max 算法每个都还有一个重载版本，该版本将二元谓词函数作为第二个参数，用于比较值。

### C++11：minmax 算法

C++11 现在包含 minmax 算法（第 16 行），它接收两个项，并返回一个 pair，其中较小的项存储在 first 中，较大的项存储在 second 中。该算法的第二个版本将二元谓词函数作为第三个参数，用于比较值。

![](img/b42ba5cd262b1358d16610173f975e4d_761_0.png)

### C++11：`minmax_element` 算法

C++11 现在包含 `minmax_element` 算法（第 26 行），它接收两个输入迭代器，表示元素的范围，并返回一对迭代器，其中 first 指向范围内最小的元素，second 指向最大的元素。该算法的第二个版本将二元谓词函数作为第三个参数，用于比较值。

## 16.4 函数对象

许多标准库算法允许您将*函数指针*传递到算法中，以帮助算法执行其任务。例如，我们在 16.3.6 节讨论的 `binary_search` 算法有一个重载版本，要求其第四个参数是一个*函数指针*，该函数指针接受两个参数并返回一个 `bool` 值。算法使用此函数将搜索键与集合中的元素进行比较。如果搜索键与被比较的元素相等，则该函数返回 true；否则返回 false。这使 `binary_search` 能够搜索元素类型未提供重载的相等性 `==` 运算符的元素集合。

任何能够接收*函数指针*的算法也可以接收一个类的对象，该类使用名为 `operator()` 的函数重载函数调用运算符（括号），前提是重载的运算符满足算法的要求——对于 `binary_search`，它必须接收两个参数并返回一个 `bool`。这种类的对象称为*函数对象*，在语法和语义上可以像函数或*函数指针*一样使用——通过使用函数对象的名称后跟包含函数参数的括号来调用重载的括号运算符。大多数算法可以互换使用函数对象和函数。正如您将在 16.5 节中学到的，C++11 的 lambda 表达式也可以在函数指针和函数对象使用的地方使用。

### 函数对象相对于函数指针的优势

函数对象比函数指针有几个优势。编译器可以内联函数对象的重载 `operator()` 以提高性能。此外，由于它们是类的对象，函数对象可以拥有 `operator()` 用来执行其任务的数据成员。

### 标准模板库的预定义函数对象

在头文件 `<functional>` 中可以找到许多预定义的函数对象。图 16.14 列出了几十个标准库函数对象中的几个，它们都以类模板的形式实现。C++ 标准的 20.8 节包含函数对象的完整列表。我们在 `set`、`multiset` 和 `priority_queue` 示例中使用了函数对象 `less<T>` 来指定容器中元素的排序顺序。

### 使用 `accumulate` 算法

图 16.15 使用 accumulate 数值算法（在 图 16.5 中引入）计算数组中元素平方和。accumulate 的第四个参数是一个二元函数对象（即 `operator()` 接受两个参数的函数对象）或一个指向二元函数的函数指针（即接受两个参数的函数）。函数 accumulate 被演示了两次——一次使用函数指针，一次使用函数对象。

```cpp
ostream_iterator<int> output(cout, " ");
cout << "array integers contains:\n";
copy(integers.cbegin(), integers.cend(), output);

// calculate sum of squares of elements of array integers
// using binary function sumSquares
int result = accumulate(integers.cbegin(), integers.cend(),
   0, sumSquares);

cout << "\n\nSum of squares of elements in integers using "
   << "binary\nfunction sumSquares: " << result;

// calculate sum of squares of elements of array integers
// using binary function object
result = accumulate(integers.cbegin(), integers.cend(),
   0, SumSquaresClass<int>());

cout << "\n\nSum of squares of elements in integers using "
   << "\n\nfunction object of type "
   << "SumSquaresClass<int>: " << result << endl;
} // end main
```

```text
array integers contains:
1 2 3 4 5 6 7 8 9 10

Sum of squares of elements in integers using binary
function sumSquares: 385

Sum of squares of elements in integers using binary
function object of type SumSquaresClass<int>: 385
```

**图 16.15** | 二元函数对象。（第 2 部分，共 2 部分。）

### 函数 sumSquares

第 13–16 行定义了一个函数 sumSquares，它将第二个参数值平方，将该平方与第一个参数 total 相加，并返回总和。在示例中，函数 accumulate 将遍历的序列中的每个元素作为第二个参数传递给 sumSquares。第一次调用 sumSquares 时，第一个参数将是 total 的初始值（该值作为第三个参数提供给 accumulate；在本程序中为 0）。之后对 sumSquares 的所有调用都接收前一次 sumSquares 调用返回的累计和作为第一个参数。当 accumulate 完成时，它返回序列中所有元素的平方和。

### 类 SumSquaresClass

第 21–30 行定义了类模板 SumSquaresClass，其中包含一个重载的 operator()，它有两个参数并返回一个值——这是二元函数对象的要求。第一次调用该函数对象时，第一个参数将是 total 的初始值（该值作为第三个参数提供给 accumulate；在本程序中为 0），第二个参数将是数组 integers 中的第一个元素。之后对 operator() 的所有调用都接收前一次调用函数对象返回的结果作为第一个参数，第二个参数将是数组中的下一个元素。当 accumulate 完成时，它返回数组中所有元素的平方和。

### 将函数指针和函数对象传递给算法 accumulate

第 43–44 行调用函数 accumulate，以其最后一个参数为指向函数 sumSquares 的指针。类似地，第 51–52 行的语句调用 accumulate，以类 SumSquaresClass 的对象作为最后一个参数。表达式 `SumSquaresClass<int>()` 创建（并调用默认构造函数）一个类 SumSquaresClass 的实例（一个函数对象），该实例被传递给 accumulate，进而调用函数 operator()。第 51–52 行可以写成两条独立的语句，如下所示：

```cpp
SumSquaresClass<int> sumSquaresObject;
result = accumulate( integers.cbegin(), integers.cend(),
                     0, sumSquaresObject );
```

第一行定义了一个 SumSquaresClass 类的对象。然后该对象被传递给 accumulate。

## 16.5 Lambda 表达式

如您在本章中所见，许多算法可以接收函数指针或函数对象作为参数。在您能将函数指针或函数对象传递给算法之前，必须先声明相应的函数或类。

C++11 的 **Lambda 表达式**（或 **lambda 函数**）使您能够在*传递给函数的位置*定义匿名函数对象。它们在函数内部局部定义，可以“捕获”（按值或按引用）外围函数的局部变量，然后在 lambda 主体中操作这些变量。图 16.16 演示了一个简单的 lambda 表达式示例，该示例将 `int` 数组中的每个元素的值加倍。

```cpp
// Fig. 16.16: fig16_16.cpp
// Lambda expressions.
#include <iostream>
#include <array>
#include <algorithm>
using namespace std;

int main()
{
   const size_t SIZE = 4; // size of array values
   array<int, SIZE> values = { 1, 2, 3, 4 }; // initialize values

   // output each element multiplied by two
   for_each( values.cbegin(), values.cend(),
      []( int i ) { cout << i * 2 << endl; } );

   int sum = 0; // initialize sum to zero

   // add each element to sum
   for_each( values.cbegin(), values.cend(),
      [&sum] ( int i ) { sum += i; } );
}
```

**图 16.16** | *Lambda 表达式。（第 1 部分，共 2 部分。）*

