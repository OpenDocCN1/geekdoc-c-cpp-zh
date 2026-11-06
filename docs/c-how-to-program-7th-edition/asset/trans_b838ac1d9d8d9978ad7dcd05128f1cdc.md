

### 22.5.3 remove、remove_if、remove_copy 和 remove_copy_if

图 22.28 演示了使用算法 remove、remove_if、remove_copy 和 remove_copy_if 从序列中删除值。

```cpp
// Fig. 22.28: Fig22_28.cpp
// Standard Library functions remove, remove_if,
// remove_copy and remove_copy_if.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <vector> // vector class-template definition
#include <iterator> // ostream_iterator
using namespace std;

bool greater9( int ); // prototype

int main()
{
   const int SIZE = 10;
   int a[ SIZE ] = { 10, 2, 10, 4, 16, 6, 14, 8, 12, 10 };
   ostream_iterator< int > output( cout, " " );
   vector< int > v( a, a + SIZE ); // copy of a
   vector< int >::iterator newLastElement;

   cout << "Vector v before removing all 10s:\n   ";
   copy( v.begin(), v.end(), output );

   // remove all 10s from v
   newLastElement = remove( v.begin(), v.end(), 10 );
   cout << "\nVector v after removing all 10s:\n   ";
   copy( v.begin(), newLastElement, output );

   vector< int > v2( a, a + SIZE ); // copy of a
   vector< int > c( SIZE, 0 ); // instantiate vector c
   cout << "\n\nVector v2 before removing all 10s and copying:\n   ";
   copy( v2.begin(), v2.end(), output );

   // copy from v2 to c, removing 10s in the process
   remove_copy( v2.begin(), v2.end(), c.begin(), 10 );
   cout << "\nVector c after removing all 10s from v2:\n   ";
   copy( c.begin(), c.end(), output );

   vector< int > v3( a, a + SIZE ); // copy of a
   cout << "\n\nVector v3 before removing all elements"
      << "\ngreater than 9:\n   ";
   copy( v3.begin(), v3.end(), output );

   // remove elements greater than 9 from v3
   newLastElement = remove_if( v3.begin(), v3.end(), greater9 );
   cout << "\nVector v3 after removing all elements"
      << "\ngreater than 9:\n   ";
   copy( v3.begin(), newLastElement, output );

        vector< int > v4( a, a + SIZE ); // copy of a
        vector< int > c2( SIZE, 0 ); // instantiate vector c2
        cout << "\n\nVector v4 before removing all elements"
             << "\ngreater than 9 and copying:\n  ";
        copy( v4.begin(), v4.end(), output );

        // copy elements from v4 to c2, removing elements greater
        // than 9 in the process
        remove_copy_if( v4.begin(), v4.end(), c2.begin(), greater9 );
        cout << "\nVector c2 after removing all elements"
             << "\ngreater than 9 from v4:\n  ";
        copy( c2.begin(), c2.end(), output );
        cout << endl;
    } // end main

    // determine whether argument is greater than 9
    bool greater9( int x )
    {
        return x > 9;
    } // end function greater9
```

图 22.28 | 算法 remove、remove_if、remove_copy 和 remove_copy_if（第 1 部分，共 2 部分）

```text
Vector v before removing all 10s:
    10 2 10 4 16 6 14 8 12 10
Vector v after removing all 10s:
    2 4 16 6 14 8 12

Vector v2 before removing all 10s and copying:
    10 2 10 4 16 6 14 8 12 10
Vector c after removing all 10s from v2:
    2 4 16 6 14 8 12 0 0 0

Vector v3 before removing all elements
greater than 9:
    10 2 10 4 16 6 14 8 12 10
Vector v3 after removing all elements
greater than 9:
    2 4 6 8

Vector v4 before removing all elements
greater than 9 and copying:
    10 2 10 4 16 6 14 8 12 10
Vector c2 after removing all elements
greater than 9 from v4:
    2 4 6 8 0 0 0 0 0 0
```

图 22.28 | 算法 remove_if、remove_copy 和 remove_copy_if（第 2 部分，共 2 部分）

第 24 行使用函数 remove 将 v 中从 v.begin() 到 v.end()（但不包括 v.end()）范围内所有值为 10 的元素删除。前两个迭代器参数必须是前向迭代器，以便算法能够修改序列中的元素。该函数不会修改 vector 中的元素数量，也不会销毁被删除的元素，但它会将所有未被删除的元素移到 vector 的前面。函数返回一个迭代器，指向未被删除的最后一个 vector 元素之后的位置。从该迭代器位置到 vector 末尾的元素具有未定义的值（在本例中，每个“未定义”位置的值都是 0）。

```cpp
int a[ SIZE ] = { 10, 2, 10, 4, 16, 6, 14, 8, 12, 10 };
ostream_iterator< int > output( cout, " " );

vector< int > v1( a, a + SIZE ); // copy of a
cout << "Vector v1 before replacing all 10s:\n  ";
copy( v1.begin(), v1.end(), output );

// replace all 10s in v1 with 100
replace(v1.begin(), v1.end(), 10, 100 );
cout << "\nVector v1 after replacing 10s with 100s:\n  ";
copy( v1.begin(), v1.end(), output );

vector< int > v2( a, a + SIZE ); // copy of a
vector< int > c1( SIZE ); // instantiate vector c1
cout << "\n\nVector v2 before replacing all 10s and copying:\n  ";
copy( v2.begin(), v2.end(), output );

// copy from v2 to c1, replacing 10s with 100s
replace_copy( v2.begin(), v2.end(), c1.begin(), 10, 100 );
cout << "\nVector c1 after replacing all 10s in v2:\n  ";
copy( c1.begin(), c1.end(), output );

vector< int > v3( a, a + SIZE ); // copy of a
cout << "\n\nVector v3 before replacing values greater than 9:\n  ";
copy( v3.begin(), v3.end(), output );

// replace values greater than 9 in v3 with 100
replace_if( v3.begin(), v3.end(), greater9, 100 );
cout << "\nVector v3 after replacing all values greater than 9\n"
     << "than 9 with 100s:\n  ";
copy( v3.begin(), v3.end(), output );

vector< int > v4( a, a + SIZE ); // copy of a
vector< int > c2( SIZE ); // instantiate vector c2
cout << "\n\nVector v4 before replacing all values greater "
     << "than 9 and copying:\n  ";
copy( v4.begin(), v4.end(), output );

// copy v4 to c2, replacing elements greater than 9 with 100
replace_copy_if( v4.begin(), v4.end(), c2.begin(), greater9, 100 );
cout << "\nVector c2 after replacing all values greater"
     << "than 9 in v4:\n  ";
copy( c2.begin(), c2.end(), output );
cout << endl;
} // end main

// determine whether argument is greater than 9
bool greater9( int x )
{
   return x > 9;
} // end function greater9
```

图 22.29 | 算法 replace、replace_if、replace_copy 和 replace_copy_if（第 2 部分，共 3 部分）

### 22.5.5 数学算法

图 22.30 演示了 STL 中的几个常见数学算法，包括 `random_shuffle`、`count`、`count_if`、`min_element`、`max_element`、`accumulate`、`for_each` 和 `transform`。

```cpp
// Fig. 22.30: Fig22_30.cpp
// Mathematical algorithms of the Standard Library.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <numeric> // accumulate is defined here
#include <vector>
#include <iterator>
using namespace std;

bool greater9( int ); // predicate function prototype
void outputSquare( int ); // output square of a value
int calculateCube( int ); // calculate cube of a value

int main()
{
   const int SIZE = 10;
   int a1[ SIZE ] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
   vector< int > v( a1, a1 + SIZE ); // copy of a1
   ostream_iterator< int > output( cout, " " );

   cout << "Vector v before random_shuffle: ";
   copy( v.begin(), v.end(), output );

   random_shuffle( v.begin(), v.end() ); // shuffle elements of v
   cout << "\nVector v after random_shuffle: ";
   copy( v.begin(), v.end(), output );

   int a2[ SIZE ] = { 100, 2, 8, 1, 50, 3, 8, 8, 9, 10 };
   vector< int > v2( a2, a2 + SIZE ); // copy of a2
   cout << "\n\nVector v2 contains: ";
   copy( v2.begin(), v2.end(), output );

   // count number of elements in v2 with value 8
   int result = count( v2.begin(), v2.end(), 8 );
   cout << "\nNumber of elements matching 8: " << result;

   // count number of elements in v2 that are greater than 9
   result = count_if( v2.begin(), v2.end(), greater9 );
   cout << "\nNumber of elements greater than 9: " << result;

   // locate minimum element in v2
   cout << "\n\nMinimum element in Vector v2 is: "
      << *( min_element( v2.begin(), v2.end() ) );

   // locate maximum element in v2
   cout << "\nMaximum element in Vector v2 is: "
      << *( max_element( v2.begin(), v2.end() ) );
```

图 22.30 | 标准库的数学算法（第 1 部分，共 2 部分）

