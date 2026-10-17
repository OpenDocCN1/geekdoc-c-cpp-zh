
Fig. 20.31 | Basic searching and sorting algorithms of the Standard Library. (Part 3 of 3.)

Line 25 uses function `find` to locate the value 16 in the range from `v.begin()` up to, but not including, `v.end()` in `v`. The function requires its two iterator arguments to be at least input iterators and returns an input iterator that either is positioned at the first element containing the value or indicates the end of the sequence (as is the case in line 33).

Line 41 uses function `find_if` to locate the first value in the range from `v.begin()` up to, but not including, `v.end()` in `v` for which the unary predicate function `greater10` returns true. Function `greater10` (defined in lines 71–74) takes an integer and returns a `bool` value indicating whether the integer argument is greater than 10. Function `find_if` requires its two iterator arguments to be at least input iterators. The function returns an input iterator that either is positioned at the first element containing a value for which the predicate function returns true or indicates the end of the sequence.

Line 50 uses function `sort` to arrange the elements in the range from `v.begin()` up to, but not including, `v.end()` in `v` in ascending order. The function requires its two iterator arguments to be random-access iterators. A second version of this function takes a third argument that is a binary predicate function taking two arguments that are values in the sequence and returning a `bool` indicating the sorting order—if the return value is true, the two elements being compared are in sorted order.

### Common Programming Error 20.5

> Attempting to sort a container by using an iterator other than a random-access iterator is a compilation error. Function `sort` requires a random-access iterator.

Line 55 uses function `binary_search` to determine whether the value 13 is in the range from `v.begin()` up to, but not including, `v.end()` in `v`. The sequence of values must be sorted in ascending order first. Function `binary_search` requires its two iterator arguments to be at least forward iterators. The function returns a `bool` indicating whether the value was found in the sequence. Line 61 demonstrates a call to function `binary_search` in which the value is not found. A second version of this function takes a fourth argument that is a binary predicate function taking two arguments that are values in the sequence and returning a `bool`. The predicate function returns true if the two elements being compared are in sorted order. To obtain the location of the search key in the container, use the `lower_bound` or `find` algorithms.

## 20.5.7 `swap`, `iter_swap` and `swap_ranges`

Figure 20.32 demonstrates algorithms `swap`, `iter_swap` and `swap_ranges` for swapping elements. Line 20 uses function `swap` to exchange two values. In this example, the first and second elements of array `a` are exchanged. The function takes as arguments references to the two values being exchanged.

```cpp
// Fig. 20.32: fig20_32.cpp
// Standard Library algorithms iter_swap, swap and swap_ranges.
#include <iostream>
using std::cout;
using std::endl;

#include <algorithm> // algorithm definitions
#include <iterator>

int main()
{
    const int SIZE = 10;
    int a[ SIZE ] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    std::ostream_iterator< int > output( cout, " " );

    cout << "Array a contains:\n    ";
    std::copy( a, a + SIZE, output ); // display array a

    // swap elements at locations 0 and 1 of array a
    std::swap( a[ 0 ], a[ 1 ] );

    cout << "\nArray a after swapping a[0] and a[1] using swap:\n    ";
    std::copy( a, a + SIZE, output ); // display array a

    // use iterators to swap elements at locations 0 and 1 of array a
    std::iter_swap( &a[ 0 ], &a[ 1 ] ); // swap with iterators
    cout << "\nArray a after swapping a[0] and a[1] using iter_swap:\n    ";
    std::copy( a, a + SIZE, output );

    // swap elements in first five elements of array a with
    // elements in last five elements of array a
    std::swap_ranges( a, a + 5, a + 5 );

    cout << "\nArray a after swapping the first five elements\n"
         << "with the last five elements:\n    ";
    std::copy( a, a + SIZE, output );
    cout << endl;
    return 0;
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

Fig. 20.32 | Demonstrating `swap`, `iter_swap` and `swap_ranges`.

第 26 行使用函数 `iter_swap` 交换两个元素。该函数接受两个正向迭代器参数（本例中是指向数组元素的指针），并交换这两个迭代器所引用的元素中的值。

第 32 行使用函数 `swap_ranges` 将从 `a` 到 `a + 5`（但不包括 `a + 5`）的元素与从位置 `a + 5` 开始的元素进行交换。该函数需要三个正向迭代器参数。前两个参数指定第一个序列中要与第二个序列中的元素进行交换的元素范围，第二个序列从第三个参数中的迭代器所指示的位置开始。在本例中，两个值序列位于同一个数组中，但这两个序列也可以来自不同的数组或容器。

## 20.5.8 `copy_backward`、`merge`、`unique` 和 `reverse`

图 20.33 演示了 STL 算法 `copy_backward`、`merge`、`unique` 和 `reverse`。第 28 行使用函数 `copy_backward` 将从 `v1.begin()` 到 `v1.end()`（但不包括 `v1.end()`）范围内的元素复制到 `results` 中，复制时从 `results.end()` 之前的元素开始，向 `vector` 的开头方向进行。该函数返回一个迭代器，指向复制到 `results` 中的最后一个元素（由于是向后复制，因此也就是 `results` 的开头）。这些元素按与 `v1` 相同的顺序放入 `results` 中。该函数需要三个双向迭代器参数（这类迭代器既可以递增也可以递减，从而分别向前和向后遍历序列）。`copy_backward` 与 `copy` 的一个区别是：`copy` 返回的迭代器位于最后被复制的元素之后，而 `copy_backward` 返回的迭代器位于最后被复制的元素处（即序列中的第一个元素）。此外，只要要复制的第一个元素不在目标元素范围内，`copy_backward` 就可以处理容器中重叠的元素范围。

```cpp
1  // Fig. 20.33: fig20_33.cpp
2  // Standard Library functions copy_backward, merge, unique and reverse.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  #include <algorithm> // algorithm definitions
8  #include <vector> // vector class-template definition
9  #include <iterator> // ostream_iterator
10
11  int main()
12  {
13      const int SIZE = 5;
14      int a1[ SIZE ] = { 1, 3, 5, 7, 9 };
15      int a2[ SIZE ] = { 2, 4, 5, 7, 9 };
16      std::vector< int > v1( a1, a1 + SIZE ); // copy of a1
17      std::vector< int > v2( a2, a2 + SIZE ); // copy of a2
18      std::ostream_iterator< int > output( cout, " " );
19
20      cout << "Vector v1 contains: ";
21      std::copy( v1.begin(), v1.end(), output ); // display vector output
22      cout << "\nVector v2 contains: ";
23      std::copy( v2.begin(), v2.end(), output ); // display vector output
```

```cpp
std::vector< int > results( v1.size() );

// place elements of v1 into results in reverse order
std::copy_backward( v1.begin(), v1.end(), results.end() );

cout << "\n\nAfter copy_backward, results contains: ";
std::copy( results.begin(), results.end(), output );

std::vector< int > results2( v1.size() + v2.size() );

// merge elements of v1 and v2 into results2 in sorted order
std::merge( v1.begin(), v1.end(), v2.begin(), v2.end(),
    results2.begin() );

cout << "\n\nAfter merge of v1 and v2 results2 contains:\n";
std::copy( results2.begin(), results2.end(), output );

// eliminate duplicate values from results2
std::vector< int >::iterator endLocation;
endLocation = std::unique( results2.begin(), results2.end() );

cout << "\n\nAfter unique results2 contains:\n";
std::copy( results2.begin(), endLocation, output );

cout << "\n\nVector v1 after reverse: ";
std::reverse( v1.begin(), v1.end() ); // reverse elements of v1
std::copy( v1.begin(), v1.end(), output );

cout << endl;
return 0;
} // end main
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_856_0.png)

第 35–36 行使用函数 `merge` 将两个已按升序排列的值序列合并为第三个已按升序排列的序列。该函数需要五个迭代器参数。前四个至少必须是输入迭代器，最后一个至少必须是输出迭代器。前两个参数指定第一个已排序序列（`v1`）中的元素范围，后两个参数指定第二个已排序序列（`v2`）中的元素范围，最后一个参数指定第三个序列（`results2`）中元素合并的起始位置。该函数的另一个版本将二元谓词函数作为第六个参数，用于指定排序顺序。

请注意，第 32 行创建的 `vector` `results2` 的元素个数为 `v1.size() + v2.size()`。如此处所示使用 `merge` 函数时，存储结果的目标序列必须至少与要合并的两个序列的总大小一样大。如果不想在合并操作前为目标序列分配元素个数，可以使用以下语句：

```cpp
std::vector< int > results2;

std::merge ( v1.begin(), v1.end(), v2.begin(), v2.end(),
    std::back_inserter( results2 ) );
```
