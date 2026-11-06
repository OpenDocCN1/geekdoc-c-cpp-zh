
```cpp
// swap elements at locations 0 and 1 of array a
swap( a[ 0 ], a[ 1 ] );

cout << "\nArray a after swapping a[0] and a[1] using swap:\n    ";
copy( a, a + SIZE, output ); // display a

// use iterators to swap elements at locations 0 and 1 of array a
iter_swap( a, a + 1 ); // swap with iterators
cout << "\nArray a after swapping a[0] and a[1] using iter_swap:\n    ";
copy( a, a + SIZE, output );

// swap elements in first five elements of array a with
// elements in last five elements of array a
swap_ranges( a, a + 5, a + 5 );

cout << "\nArray a after swapping the first five elements\n"
     << " with the last five elements:\n    ";
copy( a, a + SIZE, output );
cout << endl;
} // end main
```

```
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

_图 22.32_ | 演示 swap、iter_swap 和 swap_ranges。（第 2 部分，共 2 部分。）

第 24 行使用函数 **iter_swap** 交换这两个元素。该函数接受两个前向迭代器实参（在本例中是指向数组元素的指针），并交换这些迭代器所引用元素中的值。

第 30 行使用函数 **swap_ranges** 将从 a 到（但不包括）a + 5 的元素与从位置 a + 5 开始的元素交换。该函数要求三个前向迭代器实参。前两个实参指定第一个序列中要与第二个序列中的元素交换的元素范围，第二个序列从第三个实参中的迭代器开始。在本例中，两个值序列位于同一数组中，但序列也可以来自不同的数组或容器。

## 22.5.8 copy_backward、merge、unique 和 reverse

图 22.33 演示 STL 算法 copy_backward、merge、unique 和 reverse。第 26 行使用函数 **copy_backward** 将范围从 v1.begin() 到（但不包括）v1.end() 的元素复制到 results 中，放置元素时从 results.end() 之前的元素开始，向 vector 的开头方向进行。该函数返回一个迭代器，它定位在最后一个被复制到 results 中的元素处（即由于反向复制，位于 results 的开头）。这些元素按与 v1 相同的顺序放入 results。该函数要求两个双向迭代器实参（这些迭代器可以分别递增和递减，以便在序列中向前和向后迭代）。copy_backward 与 copy 的一个区别是：copy 返回的迭代器定位在最后一个被复制元素之后，而 copy_backward 返回的迭代器定位在最后一个被复制元素处（即序列中的第一个元素）。此外，只要要复制的第一个元素不在目标元素范围内，copy_backward 就可以操作容器中重叠的元素范围。

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

   cout << "Vector v1 contains:\n";
   copy( v1.begin(), v1.end(), output ); // display vector output
   cout << "\nVector v2 contains:\n";
   copy( v2.begin(), v2.end(), output ); // display vector output

   vector< int > results( v1.size() );

   // place elements of v1 into results in reverse order
   copy_backward( v1.begin(), v1.end(), results.end() );
   cout << "\nAfter copy_backward, results contains:\n";
   copy( results.begin(), results.end(), output );

   vector< int > results2( v1.size() + v2.size() );

   // merge elements of v1 and v2 into results2 in sorted order
   merge( v1.begin(), v1.end(), v2.begin(), v2.end(), results2.begin() );

   cout << "\n\nAfter merge of v1 and v2 results2 contains:\n";
   copy( results2.begin(), results2.end(), output );

   // eliminate duplicate values from results2
   vector< int >::iterator endLocation;
   endLocation = unique( results2.begin(), results2.end() );

   cout << "\n\nAfter unique results2 contains:\n";
   copy( results2.begin(), endLocation, output );
}
```

图 22.33 | 演示 copy_backward、merge、unique 和 reverse。（第 1 部分，共 2 部分。）

值保留在序列中。该函数接受两个实参，它们至少必须是前向迭代器。该函数返回一个迭代器，它定位在唯一值序列中最后一个元素之后。容器中最后一个唯一值之后所有元素的值都是未定义的。该函数的第二个版本接受一个二元谓词函数作为第三个实参，用于指定如何比较两个元素是否相等。

第 46 行使用函数 `reverse` 将 `v1` 中从 `v1.begin()` 到（但不包括）`v1.end()` 范围内的所有元素反转。该函数接受两个实参，它们至少必须是双向迭代器。

## 22.5.9 inplace_merge、unique_copy 和 reverse_copy

图 22.34 演示算法 `inplace_merge`、`unique_copy` 和 `reverse_copy`。第 22 行使用函数 `inplace_merge` 合并同一容器中的两个已排序元素序列。在本例中，从 `v1.begin()` 到（但不包括）`v1.begin() + 5` 的元素与从 `v1.begin() + 5` 到（但不包括）`v1.end()` 的元素合并。该函数要求其三个迭代器实参至少为双向迭代器。该函数的第二个版本接受一个二元谓词函数作为第四个实参，用于比较两个序列中的元素。

```cpp
 1  // Fig. 22.34: Fig22_34.cpp
 2  // Standard Library algorithms inplace_merge,
 3  // reverse_copy and unique_copy.
 4  #include <iostream>
 5  #include <algorithm> // algorithm definitions
 6  #include <vector> // vector class-template definition
 7  #include <iterator> // back_inserter definition
 8  using namespace std;
 9
10  int main()
11  {
12      const int SIZE = 10;
13      int a1[ SIZE ] = { 1, 3, 5, 7, 9, 1, 3, 5, 7, 9 };
14      vector< int > v1( a1, a1 + SIZE ); // copy of a1
15      ostream_iterator< int > output( cout, " " );
16
17      cout << "Vector v1 contains: ";
18      copy( v1.begin(), v1.end(), output );
19
20      // merge first half of v1 with second half of v1 such that
21      // v1 contains sorted set of elements after merge
22      inplace_merge( v1.begin(), v1.begin() + 5, v1.end() );
23
24      cout << "\nAfter inplace_merge, v1 contains: ";
25      copy( v1.begin(), v1.end(), output );
26
27      vector< int > results1;
28
29      // copy only unique elements of v1 into results1
30      unique_copy( v1.begin(), v1.end(), back_inserter( results1 ) );
31      cout << "\nAfter unique_copy results1 contains: ";
32      copy( results1.begin(), results1.end(), output );
33
34      vector< int > results2;
35
36      // copy elements of v1 into results2 in reverse order
37      reverse_copy( v1.begin(), v1.end(), back_inserter( results2 ) );
38      cout << "\nAfter reverse_copy, results2 contains: ";
39      copy( results2.begin(), results2.end(), output );
40      cout << endl;
41  } // end main
```

图 22.34 | 算法 inplace_merge、unique_copy 和 reverse_copy。（第 1 部分，共 2 部分。）

```
Vector v1 contains: 1 3 5 7 9 1 3 5 7 9
After inplace_merge, v1 contains: 1 1 3 3 5 5 7 7 9 9
After unique_copy results1 contains: 1 3 5 7 9
After reverse_copy, results2 contains: 9 9 7 7 5 5 3 3 1 1
```

图 22.34 | 算法 inplace_merge、unique_copy 和 reverse_copy。（第 2 部分，共 2 部分。）

第 30 行使用函数 **unique_copy** 复制从 v1.begin() 到（但不包括）v1.end() 的已排序值序列中的所有唯一元素。被复制的元素放入 vector results1 中。前两个实参至少必须是输入迭代器，最后一个至少必须是输出迭代器。在本例中，我们没有在 results1 中预先分配足够的元素来存储从 v1 复制的所有元素。相反，我们使用函数 back_inserter（定义在头文件 <iterator> 中）向 v1 的末尾添加元素。back_inserter 使用类 vector 在 vector 末尾插入元素的能力。由于 back_inserter 插入元素而不是替换现有元素的值，因此 vector 能够增长以容纳额外元素。unique_copy 函数的第二个版本接受一个二元谓词函数作为第四个实参，用于比较元素是否相等。

第 37 行使用函数 **reverse_copy** 复制从 v1.begin() 到（但不包括）v1.end() 范围内元素的反向副本。被复制的元素使用 back_inserter 对象插入到 results2 中，以确保 vector 能够增长以容纳所复制的适当数量的元素。函数 reverse_copy 要求其前两个迭代器实参至少为双向迭代器，第三个至少为输出迭代器。

## 22.5.10 集合操作

图 22.35 演示用于操作已排序值集合的函数 includes、set_difference、set_intersection、set_symmetric_difference 和 set_union。为了演示 STL 函数可以应用于数组和容器，本例只使用数组（请记住，指向数组的指针是随机访问迭代器）。

第 25 行和第 31 行调用函数 **includes**。函数 includes 比较两个已排序值集合，以确定第二个集合的每个元素是否都在第一个集合中。如果是，includes 返回 true；否则返回 false。前两个迭代器实参至少必须是输入迭代器，并且必须描述第一个值集合。在第 25 行中，第一个集合由从 a1 到（但不包括）a1 + SIZE1 的元素组成。最后两个迭代器实参至少必须是输入迭代器，并且必须描述第二个值集合。在本例中，第二个集合由从 a2 到（但不包括）a2 的元素组成
