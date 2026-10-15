
第 26 行使用函数 iter_swap 交换两个元素。该函数接受两个正向迭代器参数（本例中是指向数组元素的指针），并交换这两个迭代器所引用的元素中的值。

第 32 行使用函数 swap_ranges 将从 a 到 a + 5（但不包括 a + 5）的元素与从位置 a + 5 开始的元素进行交换。该函数需要三个正向迭代器参数。前两个参数指定第一个序列中要与第二个序列中的元素进行交换的元素范围，第二个序列从第三个参数中的迭代器所指示的位置开始。在本例中，两个值序列位于同一个数组中，但这两个序列也可以来自不同的数组或容器。

## 20.5.8 copy_backward、merge、unique 和 reverse

图 20.33 演示了 STL 算法 copy_backward、merge、unique 和 reverse。第 28 行使用函数 copy_backward 将从 v1.begin() 到 v1.end()（但不包括 v1.end()）范围内的元素复制到 results 中，复制时从 results.end() 之前的元素开始，向 vector 的开头方向进行。该函数返回一个迭代器，指向复制到 results 中的最后一个元素（由于是向后复制，因此也就是 results 的开头）。这些元素按与 v1 相同的顺序放入 results 中。该函数需要三个双向迭代器参数（这类迭代器既可以递增也可以递减，从而分别向前和向后遍历序列）。copy_backward 与 copy 的一个区别是：copy 返回的迭代器位于最后被复制的元素之后，而 copy_backward 返回的迭代器位于最后被复制的元素处（即序列中的第一个元素）。此外，只要要复制的第一个元素不在目标元素范围内，copy_backward 就可以处理容器中重叠的元素范围。

```
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

```
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

第 35–36 行使用函数 **merge** 将两个已按升序排列的值序列合并为第三个已按升序排列的序列。该函数需要五个迭代器参数。前四个至少必须是输入迭代器，最后一个至少必须是输出迭代器。前两个参数指定第一个已排序序列（v1）中的元素范围，后两个参数指定第二个已排序序列（v2）中的元素范围，最后一个参数指定第三个序列（results2）中元素合并的起始位置。该函数的另一个版本将二元谓词函数作为第六个参数，用于指定排序顺序。

请注意，第 32 行创建的 vector results2 的元素个数为 v1.size() + v2.size()。如此处所示使用 merge 函数时，存储结果的目标序列必须至少与要合并的两个序列的总大小一样大。如果不想在合并操作前为目标序列分配元素个数，可以使用以下语句：

```
std::vector< int > results2;
std::merge ( v1.begin(), v1.end(), v2.begin(), v2.end(),
    std::back_inserter( results2 ) );
```

参数 std::back_inserter( results2 ) 为容器 results2 使用了函数模板 back_inserter（头文件 `<iterator>`）。back_inserter 会调用容器的默认 push_back 函数，将元素插入到容器末尾。更重要的是，如果向已经没有可用空间的容器插入元素，容器会增大。因此，不需要预先知道容器中的元素个数。另外还有两个插入器——front_inserter（用于在其参数指定的容器开头插入元素）和 inserter（用于在第一个参数指定的容器中、第二个参数提供的迭代器之前插入元素）。

第 43 行对 results2 中从 results2.begin() 到 results2.end()（但不包括 results2.end()）的有序元素序列使用函数 unique。在将此函数应用于含有重复值的有序序列后，序列中每个值仅保留一个副本。该函数接受两个参数，它们至少必须是正向迭代器。该函数返回一个迭代器，指向唯一值序列中最后一个元素之后的位置。容器中最后一个唯一值之后的所有元素的值是未定义的。该函数的另一个版本接受第三个参数，即一个二元谓词函数，用于指定如何比较两个元素是否相等。

第 49 行使用函数 reverse 反转 v1 中从 v1.begin() 到 v1.end()（但不包括 v1.end()）范围内的所有元素。该函数接受两个参数，它们至少必须是双向迭代器。

## 20.5.9 inplace_merge、unique_copy 和 reverse_copy

图 20.34 演示了 STL 算法 inplace_merge、unique_copy 和 reverse_copy。第 24 行使用函数 inplace_merge 合并同一容器中两个已排序的元素序列。在本例中，从 v1.begin() 到 v1.begin() + 5（但不包括 v1.begin() + 5）的元素与从 v1.begin() + 5 到 v1.end()（但不包括 v1.end()）的元素合并。该函数要求其三个迭代器参数至少是双向迭代器。该函数的另一个版本接受第四个参数作为二元谓词函数，用于比较两个序列中的元素。

```
1  // Fig. 20.34: fig20_34.cpp
2  // Standard Library algorithms inplace_merge,
3  // reverse_copy and unique_copy.
4  #include <iostream>
5  using std::cout;
6  using std::endl;
```

```
7
8 #include <algorithm> // algorithm definitions
9 #include <vector> // vector class-template definition
10 #include <iterator> // back_inserter definition
11
12 int main()
13 {
14     const int SIZE = 10;
15     int a1[ SIZE ] = { 1, 3, 5, 7, 9, 1, 3, 5, 7, 9 };
16     std::vector< int > v1( a1, a1 + SIZE ); // copy of a
17     std::ostream_iterator< int > output( cout, " " );
18
19     cout << "Vector v1 contains: ";
20     std::copy( v1.begin(), v1.end(), output );
21
22     // merge first half of v1 with second half of v1 such that
23     // v1 contains sorted set of elements after merge
24     std::inplace_merge( v1.begin(), v1.begin() + 5, v1.end() );
25
26     cout << "\nAfter inplace_merge, v1 contains: ";
27     std::copy( v1.begin(), v1.end(), output );
28
29     std::vector< int > results1;
30
31     // copy only unique elements of v1 into results1
32     std::unique_copy(
33         v1.begin(), v1.end(), std::back_inserter( results1 ) );
34     cout << "\nAfter unique_copy results1 contains: ";
35     std::copy( results1.begin(), results1.end(), output );
36
37     std::vector< int > results2;
38
39     // copy elements of v1 into results2 in reverse order
40     std::reverse_copy(
41         v1.begin(), v1.end(), std::back_inserter( results2 ) );
42     cout << "\nAfter reverse_copy, results2 contains: ";
43     std::copy( results2.begin(), results2.end(), output );
44     cout << endl;
45     return 0;
46 } // end main
```

Vector v1 contains: 1 3 5 7 9 1 3 5 7 9
After inplace_merge, v1 contains: 1 1 3 3 5 5 7 7 9 9
After unique_copy results1 contains: 1 3 5 7 9
After reverse_copy, results2 contains: 9 9 7 7 5 5 3 3 1 1

图 20.34 | 演示 inplace_merge、unique_copy 和 reverse_copy。（第 2 部分，共 2 部分。）

第 32–33 行使用函数 unique_copy 复制从 v1.begin() 到 v1.end()（但不包括 v1.end()）的有序值序列中的所有唯一元素。复制的元素被放入 vector results1 中。前两个参数至少必须是输入迭代器，最后一个参数至少必须是输出迭代器。在本例中，我们没有在 results1 中预分配足够的元素来存储从 v1 复制来的所有元素。相反，
