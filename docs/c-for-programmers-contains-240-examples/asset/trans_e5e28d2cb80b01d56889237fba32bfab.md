

我们使用函数 back_inserter（在头文件 <iterator> 中定义）将元素添加到 v1 的末尾。back_inserter 使用类 vector 在 vector 末尾插入元素的 capability。因为 back_inserter 是插入一个元素而不是替换现有元素的值，所以 vector 能够增长以容纳额外的元素。unique_copy 函数的第二个版本以一个二元谓词函数作为第四个参数来比较元素的相等性。

第 40–41 行使用函数 reverse_copy 来制作从 v1.begin() 起到但不包括 v1.end() 的元素范围的反向副本。复制的元素使用 back_inserter 对象插入到 results2 中，以确保 vector 能够增长以容纳适当数量的复制元素。函数 reverse_copy 要求其前两个迭代器参数至少是双向迭代器，其第三个参数至少是输出迭代器。

## 20.5.10 Set Operations

图 20.35 演示了标准库函数 includes、set_difference、set_intersection、set_symmetric_difference 和 set_union 用于操作已排序值的集合。为了演示标准库函数可以应用于数组和容器，本示例仅使用数组（请记住，指向数组的指针是随机访问迭代器）。

第 27 行和第 33 行在 if 语句的条件中调用函数 includes。函数 includes 比较两个已排序值的集合，以确定第二个集合的每个元素是否都在第一个集合中。如果是，includes 返回 true；否则返回 false。前两个迭代器参数必须至少是输入迭代器，并且必须描述第一个值的集合。在第 27 行中，第一个集合由从 a1 起到但不包括 a1 + SIZE1 的元素组成。后两个迭代器参数必须至少是输入迭代器，并且必须描述第二个值的集合。在本示例中，第二个集合由从 a2 起到但不包括 a2 + SIZE2 的元素组成。函数 includes 的第二个版本接受一个第五个参数，即用于比较元素相等性的二元谓词函数。

```
// Fig. 20.35: fig20_35.cpp
// Standard Library algorithms includes, set_difference,
// set_intersection, set_symmetric_difference and set_union.
#include <iostream>
using std::cout;
using std::endl;

#include <algorithm> // algorithm definitions
#include <iterator> // ostream_iterator

int main()
{
    const int SIZE1 = 10, SIZE2 = 5, SIZE3 = 20;
    int a1[ SIZE1 ] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int a2[ SIZE2 ] = { 4, 5, 6, 7, 8 };
    int a3[ SIZE2 ] = { 4, 5, 6, 11, 15 };
    std::ostream_iterator< int > output( cout, " " );

Fig. 20.35 | set operations of the Standard Library. (Part 1 of 3.)

cout << "a1 contains: ";
std::copy( a1, a1 + SIZE1, output ); // display array a1
cout << "\na2 contains: ";
std::copy( a2, a2 + SIZE2, output ); // display array a2
cout << "\na3 contains: ";
std::copy( a3, a3 + SIZE2, output ); // display array a3

// determine whether set a2 is completely contained in a1
if ( std::includes( a1, a1 + SIZE1, a2, a2 + SIZE2 ) )
    cout << "\n\na1 includes a2";
else
    cout << "\n\na1 does not include a2";

// determine whether set a3 is completely contained in a1
if ( std::includes( a1, a1 + SIZE1, a3, a3 + SIZE2 ) )
    cout << "\na1 includes a3";
else
    cout << "\na1 does not include a3";

int difference[ SIZE1 ];

// determine elements of a1 not in a2
int *ptr = std::set_difference( a1, a1 + SIZE1,
    a2, a2 + SIZE2, difference );
cout << "\n\nset_difference of a1 and a2 is: ";
std::copy( difference, ptr, output );

int intersection[ SIZE1 ];

// determine elements in both a1 and a2
ptr = std::set_intersection( a1, a1 + SIZE1,
    a2, a2 + SIZE2, intersection );
cout << "\n\nset_intersection of a1 and a2 is: ";
std::copy( intersection, ptr, output );

int symmetric_difference[ SIZE1 + SIZE2 ];

// determine elements of a1 that are not in a2 and
// elements of a2 that are not in a1
ptr = std::set_symmetric_difference( a1, a1 + SIZE1,
    a3, a3 + SIZE2, symmetric_difference );
cout << "\n\nset_symmetric_difference of a1 and a3 is: ";
std::copy( symmetric_difference, ptr, output );

int unionSet[ SIZE3 ];

// determine elements that are in either or both sets
ptr = std::set_union( a1, a1 + SIZE1, a3, a3 + SIZE2, unionSet );
cout << "\n\nset union of a1 and a3 is: ";
std::copy( unionSet, ptr, output );
cout << endl;
return 0;
} // end main

a1 contains: 1 2 3 4 5 6 7 8 9 10
a2 contains: 4 5 6 7 8
a3 contains: 4 5 6 11 15

a1 includes a2
a1 does not include a3

set_difference of a1 and a2 is: 1 2 3 9 10

set_intersection of a1 and a2 is: 4 5 6 7 8

set_symmetric_difference of a1 and a3 is: 1 2 3 7 8 9 10 11 15

set_union of a1 and a3 is: 1 2 3 4 5 6 7 8 9 10 11 15

Fig. 20.35 | set operations of the Standard Library. (Part 3 of 3.)

第 41–42 行使用函数 set_difference 来查找第一个已排序值集合中不在第二个已排序值集合中的元素（两个集合的值都必须按升序排列）。不同的元素被复制到第五个参数中（在本例中为数组 difference）。前两个迭代器参数必须至少是第一个值集合的输入迭代器。接下来的两个迭代器参数必须至少是第二个值集合的输入迭代器。第五个参数必须至少是输出迭代器，指示存储不同值的副本的位置。该函数返回一个输出迭代器，其位置在第五个参数指向的集合中复制的最后一个值之后。函数 set_difference 的第二个版本接受一个第六个参数，即指示元素最初排序顺序的二元谓词函数。两个序列必须使用相同的比较函数进行排序。

第 49–50 行使用函数 set_intersection 来确定第一个已排序值集合中存在于第二个已排序值集合中的元素（两个集合的值都必须按升序排列）。两个集合共有的元素被复制到第五个参数中（在本例中为数组 intersection）。前两个迭代器参数必须至少是第一个值集合的输入迭代器。接下来的两个迭代器参数必须至少是第二个值集合的输入迭代器。第五个参数必须至少是输出迭代器，指示存储相同值的副本的位置。该函数返回一个输出迭代器，其位置在第五个参数指向的集合中复制的最后一个值之后。函数 set_intersection 的第二个版本接受一个第六个参数，即指示元素最初排序顺序的二元谓词函数。两个序列必须使用相同的比较函数进行排序。

第 58–59 行使用函数 set_symmetric_difference 来确定第一个集合中不在第二个集合中的元素以及第二个集合中不在第一个集合中的元素（两个集合都必须按升序排列）。不同的元素从两个集合复制到第五个参数中（数组 symmetric_difference）。前两个迭代器参数必须至少是第一个值集合的输入迭代器。接下来的两个迭代器参数必须至少是第二个值集合的输入迭代器。第五个参数必须至少是输出迭代器，指示存储不同值的副本的位置。该函数返回一个输出迭代器，其位置在第五个参数指向的集合中复制的最后一个值之后。函数 set_symmetric_difference 的第二个版本接受一个第六个参数，即指示元素最初排序顺序的二元谓词函数。

