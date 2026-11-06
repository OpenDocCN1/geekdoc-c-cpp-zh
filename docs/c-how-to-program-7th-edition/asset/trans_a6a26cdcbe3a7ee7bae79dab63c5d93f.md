
```cpp
// calculate sum of elements in v
cout << "\nThe total of the elements in Vector v is: "
     << accumulate( v.begin(), v.end(), 0 );

// output square of every element in v
cout << "\nThe square of every integer in Vector v is:\n";
for_each( v.begin(), v.end(), outputSquare );

vector< int > cubes( SIZE ); // instantiate vector cubes

// calculate cube of each element in v; place results in cubes
transform( v.begin(), v.end(), cubes.begin(), calculateCube );
cout << "\nThe cube of every integer in Vector v is:\n";
copy( cubes.begin(), cubes.end(), output );
cout << endl;
} // end main

// determine whether argument is greater than 9
bool greater9( int value )
{
   return value > 9;
} // end function greater9

// output square of argument
void outputSquare( int value )
{
   cout << value * value << ' ';
} // end function outputSquare

// return cube of argument
int calculateCube( int value )
{
   return value * value * value;
} // end function calculateCube
```

```
Vector v before random_shuffle: 1 2 3 4 5 6 7 8 9 10
Vector v after random_shuffle: 5 4 1 3 7 8 9 10 6 2

Vector v2 contains: 100 2 8 1 50 3 8 8 9 10
Number of elements matching 8: 3
Number of elements greater than 9: 3

Minimum element in Vector v2 is: 1
Maximum element in Vector v2 is: 100

The total of the elements in Vector v is: 55

The square of every integer in Vector v is:
25 16 1 9 49 64 81 100 36 4

The cube of every integer in Vector v is:
125 64 1 27 343 512 729 1000 216 8
```

**图 22.30** | 标准库的数学算法。（第 2 部分，共 2 部分。）

另一个源容器中的第一个元素，第四个参数是一个输出迭代器，指定转换后的值应放置的位置，最后一个参数是接受两个参数的通用函数。这个版本的 transform 从两个输入源中各取一个元素，将通用函数应用于这对元素，然后将转换后的值放置在第四个参数指定的位置。

## 22.5.6 基本搜索和排序算法

图 22.31 演示标准库的一些基本搜索和排序功能，包括 find、find_if、sort 和 binary_search。

```cpp
// Fig. 22.31: Fig22_31.cpp
// Standard Library search and sort algorithms.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <vector>    // vector class-template definition
#include <iterator>
using namespace std;

bool greater10( int value ); // predicate function prototype

int main()
{
   const int SIZE = 10;
   int a[ SIZE ] = { 10, 2, 17, 5, 16, 8, 13, 11, 20, 7 };
   vector< int > v( a, a + SIZE ); // copy of a
   ostream_iterator< int > output( cout, " " );

   cout << "Vector v contains: ";
   copy( v.begin(), v.end(), output ); // display output vector

   // locate first occurrence of 16 in v
   vector< int >::iterator location;
   location = find( v.begin(), v.end(), 16 );

   if ( location != v.end() ) // found 16
      cout << "\nFound 16 at location " << ( location - v.begin() );
   else // 16 not found
      cout << "\n16 not found";

   // locate first occurrence of 100 in v
   location = find( v.begin(), v.end(), 100 );

   if ( location != v.end() ) // found 100
      cout << "\nFound 100 at location " << ( location - v.begin() );
   else // 100 not found
      cout << "\n100 not found";

   // locate first occurrence of value greater than 10 in v
   location = find_if( v.begin(), v.end(), greater10 );

   if ( location != v.end() ) // found value greater than 10
      cout << "\nThe first value greater than 10 is " << *location
           << "\nfound at location " << ( location - v.begin() );
   else // value greater than 10 not found
      cout << "\nNo values greater than 10 were found";

   // sort elements of v
   sort( v.begin(), v.end() );
   cout << "\n\nVector v after sort: ";
   copy( v.begin(), v.end(), output );

   // use binary_search to locate 13 in v
   if ( binary_search( v.begin(), v.end(), 13 ) )
      cout << "\n\n13 was found in v";
   else
      cout << "\n\n13 was not found in v";

   // use binary_search to locate 100 in v
   if ( binary_search( v.begin(), v.end(), 100 ) )
      cout << "\n\n100 was found in v";
   else
      cout << "\n\n100 was not found in v";

   cout << endl;
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

**图 22.31** | 标准库的基本搜索和排序算法。（第 2 部分，共 2 部分。）

第 23 行使用函数 find 在 v 中从 v.begin() 到（但不包括）v.end() 的范围内定位值 16。该函数要求其两个迭代器参数至少是输入迭代器，并返回一个输入迭代器，该迭代器要么定位到第一个包含该值的元素，要么指示序列末尾（如第 31 行的情况）。

第 39 行使用函数 find_if 在 v 中从 v.begin() 到（但不包括）v.end() 的范围内定位第一个使一元谓词函数 greater10 返回 true 的值。函数 greater10（在第 71–74 行定义）接受一个整数并返回一个 bool 值，指示该整数参数是否大于 10。函数 find_if 要求其两个迭代器参数至少是输入迭代器。该函数返回一个输入迭代器，该迭代器要么定位到第一个包含使谓词函数返回 true 的值的元素，要么指示序列末尾。

第 48 行使用函数 sort 将 v 中从 v.begin() 到（但不包括）v.end() 范围内的元素按升序排列。该函数要求其两个迭代器参数是随机访问迭代器。该函数的第二个版本接受第三个参数，该参数是一个二元谓词函数，接受两个序列中的值作为参数，并返回一个指示排序顺序的 bool——如果返回值为 true，则被比较的两个元素处于已排序顺序。

> **常见编程错误 22.5**
>
> *尝试使用非随机访问迭代器对容器排序是编译错误。函数 sort 要求随机访问迭代器。*

第 53 行使用函数 binary_search 判断值 13 是否在 v 中从 v.begin() 到（但不包括）v.end() 的范围内。值序列必须首先按升序排序。函数 binary_search 要求其两个迭代器参数至少是前向迭代器。该函数返回一个 bool，指示是否在序列中找到该值。第 59 行演示了一次未找到值的函数 binary_search 调用。该函数的第二个版本接受第四个参数，该参数是一个二元谓词函数，接受两个序列中的值作为参数并返回一个 bool。如果被比较的两个元素处于已排序顺序，则该谓词函数返回 true。要获得搜索键在容器中的位置，请使用 lower_bound 或 find 算法。

## 22.5.7 swap、iter_swap 和 swap_ranges

图 22.32 演示用于交换元素的算法 swap、iter_swap 和 swap_ranges。第 18 行使用函数 swap 交换两个值。在此示例中，数组 a 的第一个和第二个元素被交换。该函数接受对被交换的两个值的引用作为参数。

```cpp
// Fig. 22.32: Fig22_32.cpp
// Standard Library algorithms iter_swap, swap and swap_ranges.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <iterator>
using namespace std;

int main()
{
   const int SIZE = 10;
   int a[ SIZE ] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
   ostream_iterator< int > output( cout, " " );

   cout << "Array a contains:\n   ";
   copy( a, a + SIZE, output ); // display array a
```

**图 22.32** | 演示 swap、iter_swap 和 swap_ranges（第 1 部分，共 2 部分。）
