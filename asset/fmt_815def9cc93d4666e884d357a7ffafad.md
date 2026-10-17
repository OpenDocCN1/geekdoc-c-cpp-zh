
![](img/4fc2e1ee5600ca1ada5e16b9e1397269_850_0.png)

**Fig. 20.30** | 标准库的数学算法。 (Part 3 of 3.)

第 26 行使用函数 `random_shuffle` 随机重新排列范围从 `v.begin()` 到但不包括 `v.end()` 的元素在 `v` 中的顺序。此函数接受两个随机访问迭代器参数。

第 36 行使用函数 `count` 统计范围从 `v2.begin()` 到但不包括 `v2.end()` 的值为 8 的元素在 `v2` 中。此函数要求其两个迭代器参数至少为输入迭代器。

第 40 行使用函数 `count_if` 统计范围从 `v2.begin()` 到但不包括 `v2.end()` 的元素在 `v2` 中，对于这些元素谓词函数 `greater9` 返回 true。函数 `count_if` 要求其两个迭代器参数至少为输入迭代器。

第 45 行使用函数 `min_element` 定位范围从 `v2.begin()` 到但不包括 `v2.end()` 的最小元素。函数返回位于最小元素处的前向迭代器，如果范围为空则返回 `v2.end()`。函数的两个迭代器参数必须至少为输入迭代器。此函数的第二个版本将其第三个参数作为一个比较序列中两个元素的二进制函数。此函数如果第一个参数小于第二个则返回布尔值 true。

# Good Programming Practice 20.2

> 在对 `min_element` 的调用中指定范围时，检查范围是否为空并且返回值是否不是“超出末尾”迭代器是一个良好的做法。

第 49 行使用函数 `max_element` 定位范围从 `v2.begin()` 到但不包括 `v2.end()` 的最大元素在 `v2` 中。函数返回位于最大元素处的输入迭代器。函数的两个迭代器参数必须至少为输入迭代器。此函数的第二个版本将其第三个参数作为一个比较序列中元素的二进制谓词函数。二进制函数接受两个参数并返回布尔值 true，如果第一个参数小于第二个。

第 53 行使用函数 `accumulate`（其模板在头文件 `<numeric>` 中）对范围从 `v.begin()` 到但不包括 `v.end()` 的值在 `v` 中求和。函数的两个迭代器参数必须至少为输入迭代器，其第三个参数表示总和的初始值。此函数的第二个版本将其第四个参数作为一个确定元素如何累积的通用函数。通用函数必须接受两个参数并返回一个结果。第一个参数对这个

function is the current value of the accumulation. The second argument is the value of the current element in the sequence being accumulated.

Line 57 uses function `for_each` to apply a general function to every element in the range from `v.begin()` up to, but not including, `v.end()`. The general function takes the current element as an argument and may modify that element (if it is received by reference). Function `for_each` requires its two iterator arguments to be at least input iterators.

Line 62 uses function `transform` to apply a general function to every element in the range from `v.begin()` up to, but not including, `v.end()` in `v`. The general function (the fourth argument) should take the current element as an argument, should not modify the element and should return the transformed value. Function `transform` requires its first two iterator arguments to be at least input iterators and its third argument to be at least an output iterator. The third argument specifies where the transformed values should be placed. Note that the third argument can equal the first. Another version of `transform` accepts five arguments—the first two arguments are input iterators that specify a range of elements from one source container, the third argument is an input iterator that specifies the first element in another source container, the fourth argument is an output iterator that specifies where the transformed values should be placed and the last argument is a general function that takes two arguments. This version of `transform` takes one element from each of the two input sources and applies the general function to that pair of elements, then places the transformed value at the location specified by the fourth argument.

## 20.5.6 Basic Searching and Sorting Algorithms

Figure 20.31 demonstrates some basic searching and sorting capabilities of the Standard Library, including `find`, `find_if`, `sort` and `binary_search`.

```
// Fig. 20.31: fig20_31.cpp
// Standard Library search and sort algorithms.
#include <iostream>
using std::cout;
using std::endl;
#include <algorithm> // algorithm definitions
#include <vector> // vector class-template definition
#include <iterator>
bool greater10( int value ); // predicate function prototype
int main()
{
    const int SIZE = 10;
    int a[ SIZE ] = { 10, 2, 17, 5, 16, 8, 13, 11, 20, 7 };
    std::vector< int > v( a, a + SIZE ); // copy of a
    std::ostream_iterator< int > output( cout, " " );
    cout << "Vector v contains: ";
    std::copy( v.begin(), v.end(), output ); // display output vector
```

```
// Locate first occurrence of 16 in v
std::vector< int >::iterator location;
location = std::find( v.begin(), v.end(), 16 );
if ( location != v.end() ) // found 16
    cout << "\n\nFound 16 at location " << ( location - v.begin() );
else // 16 not found
    cout << "\n\n16 not found";
// Locate first occurrence of 100 in v
location = std::find( v.begin(), v.end(), 100 );
if ( location != v.end() ) // found 100
    cout << "\nFound 100 at location " << ( location - v.begin() );
else // 100 not found
    cout << "\n100 not found";
// Locate first occurrence of value greater than 10 in v
location = std::find_if( v.begin(), v.end(), greater10 );
if ( location != v.end() ) // found value greater than 10
    cout << "\n\nThe first value greater than 10 is " << *location
         << "\nfound at location " << ( location - v.begin() );
else // value greater than 10 not found
    cout << "\n\nNo values greater than 10 were found";
// sort elements of v
std::sort( v.begin(), v.end() );
cout << "\n\nVector v after sort: ";
std::copy( v.begin(), v.end(), output );
// use binary_search to locate 13 in v
if ( std::binary_search( v.begin(), v.end(), 13 ) )
    cout << "\n\n13 was found in v";
else
    cout << "\n13 was not found in v";
// use binary_search to locate 100 in v
if ( std::binary_search( v.begin(), v.end(), 100 ) )
    cout << "\n100 was found in v";
else
    cout << "\n100 was not found in v";
cout << endl;
return 0;
} // end main
// determine whether argument is greater than 10
bool greater10( int value )
{
  return value > 10;
} // end function greater10
```

```
Vector v contains: 10 2 17 5 16 8 13 11 20 7
Found 16 at location 4
100 not found
The first value greater than 10 is 17
found at location 2
Vector v after sort: 2 5 7 8 10 11 13 16 17 20
13 was found in v
100 was not found in v
```
