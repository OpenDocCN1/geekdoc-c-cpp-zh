
```cpp
44    cout << "\n\nVector v1 after reverse: ";
45    reverse( v1.begin(), v1.end() ); // reverse elements of v1
46    copy( v1.begin(), v1.end(), output );
47    cout << endl;
48  } // end main
```

```text
Vector v1 contains: 1 3 5 7 9
Vector v2 contains: 2 4 5 7 9

After copy_backward, results contains: 1 3 5 7 9

After merge of v1 and v2 results2 contains:
1 2 3 4 5 5 7 7 9 9

After unique results2 contains:
1 2 3 4 5 7 9

Vector v1 after reverse: 9 7 5 3 1
```

**图 22.33** | 演示 copy_backward、merge、unique 和 reverse。（第 2 部分，共 2 部分。）

第 33 行使用函数 **merge** 将两个按升序排序的值序列合并为第三个按升序排序的序列。该函数需要五个迭代器实参。前四个必须至少是输入迭代器，最后一个必须至少是输出迭代器。前两个实参指定第一个已排序序列（v1）中元素的起始位置，接下来的两个实参指定第二个已排序序列（v2）中元素的范围，最后一个实参指定元素将合并到的第三个序列（results2）中的起始位置。该函数的第二个版本将指定排序顺序的二元谓词函数作为其第六个实参。

第 30 行创建 vector results2，其元素个数为 v1.size() + v2.size()。如这里所示使用 merge 函数要求存储结果的序列至少具有被合并的两个序列的大小。如果你不想在合并操作之前为结果序列分配元素数量，可以使用以下语句：

```cpp
vector< int > results2;
merge( v1.begin(), v1.end(), v2.begin(), v2.end(),
       back_inserter( results2 ) );
```

实参 back_inserter(results2) 为容器 results2 使用函数模板 **back_inserter**（头文件 <iterator>）。back_inserter 调用容器的默认 push_back 函数，在容器末尾插入一个元素。如果向已无更多可用空间的容器插入元素，容器大小会增长。因此，不必预先知道容器中元素的数量。另外还有两个插入器——**front_inserter**（用于在作为其实参指定的容器开头插入元素）和 **inserter**（用于在作为第一个实参提供的容器中、在作为第二个实参提供的迭代器之前插入元素）。

第 40 行对 results2 中从 results2.begin() 到（但不包括）results2.end() 范围内的已排序元素序列使用函数 **unique**。将该函数应用于含重复值的已排序序列后，序列中每个值只保留一份副本。该函数接受两个实参，它们必须至少是前向迭代器。该函数返回一个迭代器，指向唯一值序列中最后一个元素之后的位置。容器中最后一个唯一值之后的所有元素的值都是未定义的。该函数的第二个版本接受第三个实参，即指定如何比较两个元素是否相等的二元谓词函数。

第 46 行使用函数 `reverse` 反转 `v1` 中从 `v1.begin()` 到（但不包括）`v1.end()` 范围内的所有元素。该函数接受两个实参，它们必须至少是双向迭代器。

## 22.8.9 inplace_merge、unique_copy 和 reverse_copy

图 22.34 演示算法 `inplace_merge`、`unique_copy` 和 `reverse_copy`。第 22 行使用函数 `inplace_merge` 合并同一容器中的两个已排序元素序列。在此示例中，从 `v1.begin()` 到（但不包括）`v1.begin() + 5` 的元素与从 `v1.begin() + 5` 到（但不包括）`v1.end()` 的元素合并。该函数要求其三个迭代器实参至少是双向迭代器。该函数的第二个版本将用于比较两个序列中元素的二元谓词函数作为第四个实参。

```cpp
// Fig. 22.34: Fig22_34.cpp
// Standard Library algorithms inplace_merge,
// reverse_copy and unique_copy.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <vector> // vector class-template definition
#include <iterator> // back_inserter definition
using namespace std;

int main()
{
   const int SIZE = 10;
   int a1[ SIZE ] = { 1, 3, 5, 7, 9, 1, 3, 5, 7, 9 };
   vector< int > v1( a1, a1 + SIZE ); // copy of a1
   ostream_iterator< int > output( cout, " " );

   cout << "\nVector v1 contains: ";
   copy( v1.begin(), v1.end(), output );

   // merge first half of v1 with second half of v1 such that
   // v1 contains sorted set of elements
   inplace_merge( v1.begin(), v1.begin() + 5, v1.end() );

   cout << "\nAfter inplace_merge, v1 contains: ";
   copy( v1.begin(), v1.end(), output );

   vector< int > results1;

   // copy only unique elements of v1 into results1
   unique_copy( v1.begin(), v1.end(), back_inserter( results1 ) );
   cout << "\nAfter unique_copy results1 contains: ";
32    copy( results1.begin(), results1.end(), output );
33
34    vector< int > results2;
35
36    // copy elements of v1 into results2 in reverse order
37    reverse_copy( v1.begin(), v1.end(), back_inserter( results2 ) );
38    cout << "\nAfter reverse_copy, results2 contains: ";
39    copy( results2.begin(), results2.end(), output );
40    cout << endl;
41 } // end main
```

图 22.34 | 算法 inplace_merge、unique_copy 和 reverse_copy。（第 1 部分，共 2 部分。）

```text
Vector v1 contains: 1 3 5 7 9 1 3 5 7 9
After inplace_merge, v1 contains: 1 1 3 3 5 5 7 7 9 9
After unique_copy results1 contains: 1 3 5 7 9
After reverse_copy, results2 contains: 9 9 7 7 5 5 3 3 1 1
```

*图 22.34* | 算法 inplace_merge、unique_copy 和 reverse_copy。（第 2 部分，共 2 部分。）

第 30 行使用函数 `unique_copy` 复制从 `v1.begin()` 到（但不包括）`v1.end()` 的已排序值序列中所有唯一元素。复制的元素被放入 `results1`。前两个实参必须至少是输入迭代器，最后一个必须至少是输出迭代器。在此示例中，我们没有在 `results1` 中预分配足够的元素来存储从 `v1` 复制的所有元素。相反，我们使用函数 `back_inserter`（定义在头文件 `<iterator>` 中）将元素添加到 `results1` 的末尾。`back_inserter` 利用 vector 类在 vector 末尾插入元素的能力。因为 `back_inserter` 插入元素而不是替换现有元素的值，所以 vector 能够增长以容纳额外元素。`unique_copy` 函数的第二个版本将用于比较元素是否相等的二元谓词函数作为第四个实参。

第 37 行使用函数 `reverse_copy` 创建从 `v1.begin()` 到（但不包括）`v1.end()` 范围内元素的反序副本。复制的元素使用 `back_inserter` 对象插入到 `results2` 中，以确保 vector 能够增长以容纳复制元素的数量。函数 `reverse_copy` 要求其前两个迭代器实参至少是双向迭代器，第三个实参至少是输出迭代器。

## 22.8.10 集合运算

图 22.35 演示用于操作已排序值集合的函数 `includes`、`set_difference`、`set_intersection`、`set_symmetric_difference` 和 `set_union`。为了演示 STL 函数可应用于数组和容器，此示例仅使用数组（请记住，指向数组的指针是随机访问迭代器）。

第 25 行和第 31 行调用函数 `includes`。函数 includes 比较两个已排序值集合，以确定第二个集合的每个元素是否都在第一个集合中。如果是，includes 返回 true；否则返回 false。前两个迭代器实参必须至少是输入迭代器，并且必须描述第一个值集合。在第 25 行中，第一个集合由从 a1 到（但不包括）a1 + SIZE1 的元素组成。最后两个迭代器实参必须至少是输入迭代器，并且必须描述第二个值集合。在此示例中，第二个集合由从 a2 到（但不包括）a2
