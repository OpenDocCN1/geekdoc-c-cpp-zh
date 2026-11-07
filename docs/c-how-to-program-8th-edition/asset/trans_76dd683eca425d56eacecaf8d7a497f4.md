
另一个源容器中的第一个元素，第四个参数是一个输出迭代器，用于指定变换后的值应放置的位置，最后一个参数是一个接受两个参数的通用函数。这个版本的 transform 从两个输入源中各取出一个元素，并对这对元素应用该通用函数，然后将变换后的值放置到第四个参数所指定的位置。

### 22.8.6 基本搜索和排序算法

图 22.31 演示了标准库的一些基本搜索和排序功能，包括 find、find_if、sort 和 binary_search。

```cpp
// Fig. 22.31: Fig22_31.cpp
// Standard Library search and sort algorithms.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <vector> // vector class-template definition
#include <iterator>
using namespace std;

bool greater10( int value ); // predicate function prototype

int main()
{
   const int SIZE = 10;
   int a[ SIZE ] = { 10, 2, 17, 5, 16, 8, 13, 11, 20, 7 };
   vector< int > v( a, a + SIZE ); // copy one array
   ostream_iterator< int > output( cout, " " );

   cout << "Vector v contains: ";
   copy( v.begin(), v.end(), output ); // display output vector

   // locate first occurrence of 16 in v
   vector< int >::iterator location;
   location = find( v.begin(), v.end(), 16 );

   if ( location != v.end() ) // found 16
      cout << "\n\nFound 16 at location " << ( location - v.begin() );
   else // 16 not found
      cout << "\n\n16 not found";

   // locate first occurrence of 100 in v
   location = find( v.begin(), v.end(), 100 );

   if ( location != v.end() ) // found 100
      cout << "\nFound 100 at location " << ( location - v.begin() );
   else // 100 not found
      cout << "\n\n100 not found";

   // locate first occurrence of value greater than 10 in v
   location = find_if( v.begin(), v.end(), greater10 );
}
```

**图 22.31** | 标准库的基本搜索和排序算法。（第 1 部分，共 2 部分。）

返回一个 bool 值，指示整数参数是否大于 10。函数 `find_if` 要求其两个迭代器参数至少是输入迭代器。该函数返回一个输入迭代器，它要么定位在第一个包含使谓词函数返回 true 的值的元素处，要么指示序列末尾。

第 48 行使用函数 `sort` 将 `v.begin()` 到（但不包括）`v.end()` 范围内的元素按升序排列。该函数要求其两个迭代器参数是随机访问迭代器。该函数的第二个版本接受第三个参数，这个参数是一个二元谓词函数，它接受两个参数（这两个参数是序列中的值），并返回一个指示排序顺序的 bool 值——如果返回值为 true，则被比较的两个元素处于有序顺序。

> **常见编程错误 22.5**
> 
> *尝试使用非随机访问迭代器对容器进行排序会导致编译错误。函数 sort 要求使用随机访问迭代器。*

第 53 行使用函数 `binary_search` 判断值 13 是否在 `v` 中从 `v.begin()` 到（但不包括）`v.end()` 的范围内。值序列必须首先按升序排序。函数 `binary_search` 要求其两个迭代器参数至少是前向迭代器。该函数返回一个 bool 值，指示是否在序列中找到该值。第 59 行演示了一次对函数 `binary_search` 的调用，其中未找到该值。该函数的第二个版本接受第四个参数，这个参数是一个二元谓词函数，它接受两个参数（这两个参数是序列中的值）并返回一个 bool 值。如果被比较的两个元素处于有序顺序，则该谓词函数返回 true。要获取搜索键在容器中的位置，请使用 `lower_bound` 或 `find` 算法。

### 22.8.7 swap、iter_swap 和 swap_ranges

图 22.32 演示了用于交换元素的算法 swap、iter_swap 和 swap_ranges。第 18 行使用函数 `swap` 交换两个值。在此示例中，数组 a 的第一个和第二个元素被交换。该函数接受对被交换的两个值的引用作为参数。

```cpp
// Fig. 22.32: Fig22_32.cpp
// Standard Library algorithms iter_swap, swap and swap_ranges.
#include <iostream>
#include <algorithm>  // algorithm definitions
#include <iterator>
using namespace std;

int main()
{
    const int SIZE = 10;
    int a[ SIZE ] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    ostream_iterator< int > output( cout, " " );

    cout << "Array a contains:\n    ";
    copy( a, a + SIZE, output ); // display array a

    // swap elements at locations 0 and 1 of array a
    swap( a[ 0 ], a[ 1 ] );

    cout << "\nArray a after swapping a[0] and a[1] using swap:\n   ";
    copy( a, a + SIZE, output ); // display array a

    // use iterators to swap elements at locations 0 and 1 of array a
    iter_swap( &a[ 0 ], &a[ 1 ] ); // swap with iterators
    cout << "\nArray a after swapping a[0] and a[1] using iter_swap:\n   ";
    copy( a, a + SIZE, output );

    // swap elements in first five elements of array a with
    // elements in last five elements of array a
    swap_ranges( a, a + 5, a + 5 );

    cout << "\nArray a after swapping the first five elements\n"
         << " with the last five elements:\n   ";
    copy( a, a + SIZE, output );
    cout << endl;
} // end main
```

```text
Array a contains:
  1 2 3 4 5 6 7 8 9 10
Array a after swapping a[0] and a[1] using swap:
  2 1 3 4 5 6 7 8 9 10
Array a after swapping a[0] and a[1] using iter_swap:
  1 2 3 4 5 6 7 8 9 10
Array a after swapping the first five elements
with the last five elements:
  6 7 8 9 10 1 2 3 4 5
```

**图 22.32** | 演示 `swap`、`iter_swap` 和 `swap_ranges`。（第 2 部分，共 2 部分。）

第 24 行使用函数 `iter_swap` 交换这两个元素。该函数接受两个前向迭代器参数（在此例中，是指向数组元素的指针），并交换这些迭代器所指向元素中的值。

第 30 行使用函数 `swap_ranges` 将数组 a 中从 a 到（但不包括）a + 5 的元素与从位置 a + 5 开始的元素交换。该函数要求三个前向迭代器参数。前两个参数指定第一个序列中要与第二个序列中的元素交换的元素范围，第二个序列从第三个参数中的迭代器开始。在此示例中，两个值序列位于同一个数组中，但这两个序列也可以来自不同的数组或容器。

### 22.8.8 copy_backward、merge、unique 和 reverse

图 22.33 演示了 STL 算法 copy_backward、merge、unique 和 reverse。第 26 行使用函数 `copy_backward` 将从 v1.begin() 到（但不包括）v1.end() 范围内的元素复制到 results 中，复制时从 results.end() 之前的元素开始，并向该向量的开头方向进行。该函数返回一个迭代器，它定位在最后一个被复制到 results 中的元素处（即 results 的开头，因为这是反向复制）。这些元素以与 v1 相同的顺序放置到 results 中。该函数要求两个双向迭代器参数（这些迭代器可以分别递增和递减，以便在序列中向前和向后迭代）。copy_backward 与 copy 的一个区别是：copy 返回的迭代器定位在最后一个被复制元素之后，而 copy_backward 返回的迭代器定位在最后一个被复制元素处（即序列中的第一个元素）。此外，只要要复制的第一个元素不在目标元素范围内，copy_backward 就可以操作容器中重叠的元素范围。

```cpp
// Fig. 22.33: Fig22_33.cpp
// Standard Library functions copy_backward, merge, unique and reverse.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <vector> // vector class-template definition
#include <iterator> // ostream_iterator
using namespace std;

int main()
{
   const int SIZE = 5;
   int a1[ SIZE ] = { 1, 3, 5, 7, 9 };
   int a2[ SIZE ] = { 2, 4, 5, 7, 9 };
   vector< int > v1( a1, a1 + SIZE ); // copy of a1
   vector< int > v2( a2, a2 + SIZE ); // copy of a2
   ostream_iterator< int > output( cout, " " );

   cout << "Vector v1 contains: ";
   copy( v1.begin(), v1.end(), output ); // display vector output
   cout << "\nVector v2 contains: ";
   copy( v2.begin(), v2.end(), output ); // display vector output

   vector< int > results( v1.size() );

   // place elements of v1 into results in reverse order
   copy_backward( v1.begin(), v1.end(), results.end() );
   cout << "\nAfter copy_backward, results contains: ";
   copy( results.begin(), results.end(), output );

   vector< int > results2( v1.size() + v2.size() );

   // merge elements of v1 and v2 into results2 in sorted order
   merge( v1.begin(), v1.end(), v2.begin(), v2.end(), results2.begin() );

   cout << "\nAfter merge of v1 and v2 results2 contains:\n";
   copy( results2.begin(), results2.end(), output );

   // eliminate duplicate values from results2
   vector< int >::iterator endLocation;
   endLocation = unique( results2.begin(), results2.end() );

   cout << "\nAfter unique results2 contains:\n";
   copy( results2.begin(), endLocation, output );
}
```

图 22.33 | 演示 copy_backward、merge、unique 和 reverse。（第 1 部分，共 2 部分。）
