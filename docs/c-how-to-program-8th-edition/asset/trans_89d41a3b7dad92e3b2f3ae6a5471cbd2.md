

![](img/bfd978e7e9b192bab46ec2a89e481263_901_0.png)

## 性能提示 22.9

出于性能原因，应在循环之前捕获循环结束值，并与该值进行比较，而不是在每次迭代中调用（可能开销很大的）函数。

## vector 元素操作函数

图 22.15 演示了可用于获取和操作 vector 元素的函数。第 15 行使用重载的 vector 构造函数，该构造函数接受两个迭代器作为参数来初始化 integers。请记住，指向数组的指针可以用作迭代器。第 15 行用 array 中从位置 array 开始、直到（但不包括）位置 array + SIZE 的内容初始化 integers。

```cpp
// Fig. 22.15: Fig22_15.cpp
// Testing Standard Library vector class template
// element-manipulation functions.
#include <iostream>
#include <vector> // vector class-template definition
#include <algorithm> // copy algorithm
#include <iterator> // ostream_iterator iterator
#include <stdexcept> // out_of_range exception
using namespace std;

int main()
{
   const int SIZE = 6;
   int array[ SIZE ] = { 1, 2, 3, 4, 5, 6 };
   vector< int > integers( array, array + SIZE );
   ostream_iterator< int > output( cout, " " );

   cout << "Vector integers contains: ";
   copy( integers.begin(), integers.end(), output );

   cout << "\nFirst element of integers: " << integers.front()
        << "\nLast element of integers: " << integers.back();

   integers[ 0 ] = 7; // set first element to 7
   integers.at( 2 ) = 10; // set element at position 2 to 10

   // insert 22 as 2nd element
   integers.insert( integers.begin() + 1, 22 );

   cout << "\nContents of vector integers after changes: ";
   copy( integers.begin(), integers.end(), output );

   // access out-of-range element
   try
   {
      integers.at( 100 ) = 777;
   } // end try
```

**图 22.15** | vector 类模板元素操作函数。（第 1 部分，共 2 部分。）

```cpp
38  catch ( out_of_range &outOfRange )  // out_of_range exception
39  {
40      cout << "\n\nException: " << outOfRange.what();
41  } // end catch

43  // erase first element
44  integers.erase( integers.begin() );
45  cout << "\n\nVector integers after erasing first element: ";
46  copy( integers.begin(), integers.end(), output );

48  // erase remaining elements
49  integers.erase( integers.begin(), integers.end() );
50  cout << "\n\nAfter erasing all elements, vector integers "
51       << ( integers.empty() ? "is" : "is not" ) << " empty";

53  // insert elements from array
54  integers.insert( integers.begin(), array, array + SIZE );
55  cout << "\n\nContents of vector integers before clear: ";
56  copy( integers.begin(), integers.end(), output );

58  // empty integers; clear calls erase to empty a collection
59  integers.clear();
60  cout << "\n\nAfter clear, vector integers "
61       << ( integers.empty() ? "is" : "is not" ) << " empty" << endl;
62 } // end main
```

```text
Vector integers contains: 1 2 3 4 5 6
First element of integers: 1
Last element of integers: 6

Contents of vector integers after changes: 7 22 2 10 4 5 6

Exception: invalid vector<T> subscript

Vector integers after erasing first element: 22 2 10 4 5 6
After erasing all elements, vector integers is empty

Contents of vector integers before clear: 1 2 3 4 5 6
After clear, vector integers is empty
```

**图 22.15** | vector 类模板元素操作函数。（第 2 部分，共 2 部分。）

第 16 行定义了一个名为 output 的 ostream_iterator，可用于通过 cout 输出以单个空格分隔的整数。ostream_iterator<int> 是一种类型安全的输出机制，只输出 int 类型或兼容类型的值。构造函数的第一个参数指定输出流，第二个参数是一个字符串，用于指定输出值之间的分隔符——在本例中，该字符串包含一个空格字符。在本例中，我们使用 ostream_iterator（定义在头文件 <iterator> 中）输出 vector 的内容。

第 19 行使用标准库中的算法 copy 将 vector integers 的全部内容输出到标准输出。算法 copy 从第一个参数中的迭代器所指定的位置开始，复制容器中的每个元素，直到（但不包括）第二个参数中的迭代器所指定的位置。第一个和第二个参数必须满足输入迭代器要求——它们必须是可以从容器中读取值的迭代器。此外，对第一个迭代器应用 ++ 最终必须使其到达容器中的第二个迭代器。元素被复制到最后一个参数指定的输出迭代器（即可以通过其存储或输出值的迭代器）所指定的位置。在本例中，输出迭代器是附加到 `cout` 的 `ostream_iterator (output)`，因此元素被复制到标准输出。要使用标准库的算法，必须包含头文件 `<algorithm>`。

第 21–22 行使用函数 front 和 back（适用于所有序列容器）分别确定 vector 的第一个和最后一个元素。请注意函数 front 与 begin 之间的区别。函数 front 返回对 vector 中第一个元素的引用，而函数 begin 返回指向 vector 中第一个元素的随机访问迭代器。另请注意函数 back 与 end 之间的区别。函数 back 返回对 vector 中最后一个元素的引用，而函数 end 返回指向 vector 末尾（最后一个元素之后的位置）的随机访问迭代器。

> **常见编程错误 22.3**
>
> *vector 不能为空；否则，front 和 back 函数的结果将是未定义的。*

第 24–25 行演示了两种通过下标访问 vector 的方式（这些方式也可用于 deque 容器）。第 24 行使用重载的下标运算符，根据容器是否为常量，返回对指定位置值的引用或对该值的常量引用。函数 at（第 25 行）执行相同的操作，但会进行边界检查。函数 at 首先检查作为参数提供的值，并确定它是否在 vector 的边界内。如果不在，函数 at 会抛出定义在头文件 `<stdexcept>` 中的 `out_of_range` 异常（如第 34–41 行所示）。图 22.16 展示了一些 STL 异常类型。（标准库异常类型将在第 16 章讨论。）

| STL 异常类型 | 描述 |
|---|---|
| `out_of_range` | 表示下标超出范围——例如，当向 vector 成员函数 at 指定无效下标时。 |
| `invalid_argument` | 表示向函数传递了无效参数。 |
| `length_error` | 表示尝试创建过长的容器、字符串等。 |
| `bad_alloc` | 表示使用 new（或分配器）分配内存的尝试因可用内存不足而失败。 |

**图 22.16** | 一些 STL 异常类型

第 28 行使用每个序列容器提供的三个重载 `insert` 函数之一。第 28 行将值 22 插入到第一个参数中的迭代器所指定位置的元素之前。在本例中，该迭代器指向 vector 的第二个元素，因此 22 被插入为第二个元素，原来的第二个元素成为 vector 的第三个元素。`insert` 的其他版本允许插入

```cpp
// Fig. 22.17: Fig22_17.cpp
// Standard library list class template test program.
#include <iostream>
#include <list> // list class-template definition
#include <algorithm> // copy algorithm
#include <iterator> // ostream_iterator
using namespace std;

// prototype for function template printList
template < typename T > void printList( const list< T > &listRef );

int main()
{
   const int SIZE = 4;
   int array[ SIZE ] = { 2, 6, 4, 8 };
   list< int > values; // create list of ints
   list< int > otherValues; // create list of ints

   // insert items in values
   values.push_front( 1 );
   values.push_front( 2 );
   values.push_back( 4 );
   values.push_back( 3 );

   cout << "\nvalues contains: ";
   printList( values );

   values.sort(); // sort values
   cout << "\nAfter sorting contains: ";
   printList( values );

   // insert elements of array into otherValues
   otherValues.insert( otherValues.begin(), array, array + SIZE );
   cout << "\nAfter insert, otherValues contains: ";
   printList( otherValues );

   // remove otherValues elements and insert at end of values
   values.splice( values.end(), otherValues );
   cout << "\nAfter splice, values contains: ";
   printList( values );

   values.sort(); // sort values
   cout << "\nAfter sort, values contains: ";
   printList( values );

   // insert elements of array into otherValues
   otherValues.insert( otherValues.begin(), array, array + SIZE );
   otherValues.sort();
   cout << "\nAfter insert and sort, otherValues contains: ";
   printList( otherValues );

   // remove otherValues elements and insert into values in sorted order
   values.merge( otherValues );
```

**图 22.17** | 标准库 list 类模板。（第 1 部分，共 3 部分。）

