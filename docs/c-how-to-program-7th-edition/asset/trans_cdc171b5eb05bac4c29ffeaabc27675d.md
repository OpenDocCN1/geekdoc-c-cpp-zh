
```cpp
ptr = new int[ size ]; // create space for array copy
} // end if

for ( int i = 0; i < size; i++ )
    ptr[ i ] = right.ptr[ i ]; // copy array into object
} // end outer if

return *this; // enables x = y = z, for example
} // end function operator=

// determine if two Arrays are equal and
// return true, otherwise return false
bool Array::operator==( const Array& right ) const
{
    if ( size != right.size )
        return false; // arrays of different number of elements

    for ( int i = 0; i < size; i++ )
        if ( ptr[ i ] != right.ptr[ i ] )
            return false; // Array contents are not equal

    return true; // Arrays are equal
} // end function operator==

// overloaded subscript operator for non-const Arrays;
// reference return creates a modifiable lvalue
int &Array::operator[]( int subscript )
{
    // check for subscript out-of-range error
    if ( subscript < 0 || subscript >= size )
    {
        cerr << "\nError: Subscript " << subscript
             << " out of range" << endl;
        exit( 1 ); // terminate program; subscript out of range
    } // end if

    return ptr[ subscript ]; // reference return
} // end function operator[]

// overloaded subscript operator for const Arrays
// const reference return creates an rvalue
int Array::operator[]( int subscript ) const
{
    // check for subscript out-of-range error
    if ( subscript < 0 || subscript >= size )
    {
        cerr << "\nError: Subscript " << subscript
             << " out of range" << endl;
        exit( 1 ); // terminate program; subscript out of range
    } // end if

    return ptr[ subscript ]; // returns copy of this element
} // end function operator[]
```

*图 11.7 | Array 类的成员函数和友元函数定义。（第 2 部分，共 3 部分。）*

```cpp
107 // overloaded input operator for class Array;
108 // inputs values for entire Array
109 istream &operator>>( istream &input, Array & a )
110 {
111     for ( int i = 0; i < a.size; i++ )
112         input >> a.ptr[ i ];
113
114     return input; // enables cin >> x >> y;
115 } // end function
116
117 // overloaded output operator for class Array
118 ostream &operator<<( ostream &output, const Array & a )
119 {
120     int i;
121
122     // output private ptr-based array
123     for ( i = 0; i < a.size; i++ )
124     {
125         output << setw( 12 ) << a.ptr[ i ];
126
127         if ( ( i + 1 ) % 4 == 0 ) // 4 numbers per row of output
128             output << endl;
129     } // end for
130
131     if ( i % 4 != 0 ) // end last line of output
132         output << endl;
133
134     return output; // enables cout << x << y;
135 } // end function operator<<
```

*图 11.7 | Array 类的成员函数和友元函数定义。（第 3 部分，共 3 部分。）*

```cpp
1   // Fig. 11.8: fig11_08.cpp
2   // Array class test program.
3   #include <iostream>
4   #include "Array.h"
5   using namespace std;
6
7   int main()
8   {
9
10      Array integers1( 7 ); // seven-element Array
11      Array integers2; // 10-element Array by default
12
13      // print integers1 size and contents
14      cout << "Size of Array integers1 is "
15           << integers1.getSize()
16           << "\nArray after initialization:\n" << integers1;
17
18      // print integers2 size and contents
19      cout << "\nSize of Array integers2 is "
20           << integers2.getSize()
21           << "\nArray after initialization:\n" << integers2;
22
23      // input and print integers1 and integers2
24      cout << "\nEnter 17 integers: " << endl;
25      cin >> integers1 >> integers2;
26
27      cout << "\nAfter input, the Arrays contain:\n"
28           << "integers1:\n" << integers1
29           << "integers2:\n" << integers2;
30
31      // use overloaded inequality (!=) operator
32      cout << "\nEvaluating: integers1 != integers2" << endl;
33
34      if ( integers1 != integers2 )
35         cout << "integers1 and integers2 are not equal" << endl;
36
37      // create Array integers3 using integers1 as an
38      // initializer; print size and contents
39      Array integers3( integers1 ); // invokes copy constructor
40
41      cout << "\nSize of Array integers3 is "
42           << integers3.getSize()
43           << "\nArray after initialization:\n" << integers3;
44
45      // use overloaded assignment (=) operator
46      cout << "\nAssigning integers2 to integers1:" << endl;
47      integers1 = integers2; // note target Array is smaller
48
49      cout << "\nSize of integers1: " << integers1
50           << "\nintegers2:\n" << integers2;
51
52      // use overloaded equality (==) operator
53      cout << "\nEvaluating: integers1 == integers2" << endl;
54
55      if ( integers1 == integers2 )
56         cout << "integers1 and integers2 are equal" << endl;
57
58      // use overloaded subscript operator to create rvalue
59      cout << "\nintegers1[5] is " << integers1[ 5 ];
60
61      // use overloaded subscript operator to create lvalue
62      cout << "\nAssigning 1000 to integers1[5]" << endl;
63      integers1[ 5 ] = 1000;
64      cout << "\nintegers1:\n" << integers1;
65
66      // attempt to use out-of-range subscript
67      cout << "\nAttempting to assign 1000 to integers1[15]" << endl;
68      integers1[ 15 ] = 1000; // ERROR: out of range
69 } // end main
```

*图 11.8 | Array 类测试程序。（第 1 部分，共 3 部分。）*

```text
Size of Array integers1 is 7
Array after initialization:
        0          0          0          0
        0          0          0
        0          0          0

Size of Array integers2 is 10
Array after initialization:
        0          0          0          0
        0          0          0          0
        0          0          0          0
        0          0

Enter 17 integers:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

After input, the Arrays contain:
integers1:
        1          2          3          4
        5          6          7
integers2:
        8          9          10         11
        12         13         14         15
        16         17

Evaluating: integers1 != integers2
integers1 and integers2 are not equal

Size of Array integers3 is 7
Array after initialization:
        1          2          3          4
        5          6          7

Assigning integers2 to integers1:
integers1:
        8          9          10         11
        12         13         14         15
        16         17
integers2:
        8          9          10         11
        12         13         14         15
        16         17

Evaluating: integers1 == integers2
integers1 and integers2 are equal

integers1[5] is 13

Assigning 1000 to integers1[5]
integers1:
        8          9          10         11
        12         1000       14         15
        16         17

Attempting to assign 1000 to integers1[15]

Error: Subscript 15 out of range
```

*图 11.8 | Array 类测试程序。（第 3 部分，共 3 部分。）*

## 使用重载的下标运算符

第 58 行使用重载的下标运算符引用 `integers1[5]`——`integers1` 中一个范围内的元素。这个带下标的名称用作右值，打印存储在 `integers1[5]` 中的值。第 62 行将 `integers1[5]` 用作赋值语句左侧的可修改左值，将新值 1000 赋给 `integers1` 的第 5 个元素。我们将看到，`operator[]` 在确认 5 是 `integers1` 的有效下标后，返回一个引用以用作可修改的左值。

第 67 行试图将值 1000 赋给 `integers1[15]`——一个越界元素。在此示例中，`operator[]` 判断下标越界，打印一条消息并终止程序。我们在程序中将第 67 行标红，以强调访问越界元素是错误的。这是一个运行时逻辑错误。

有趣的是，数组下标运算符 `[]` 并不限于只与数组一起使用；例如，它还可以用于从其他类型的容器类（如链表、字符串和字典）中选择元素。此外，定义 `operator[]` 函数后，下标不再必须是整数——字符、字符串、浮点数甚至用户定义类的对象也可以使用。第 22 章将讨论允许非整数下标的 STL `map` 类。

## Array 类定义

现在我们已经了解了这个程序如何运行，接下来逐步讲解类头文件（图 11.6）。当我们提到头文件中的每个成员函数时，会讨论图 11.7 中该函数的实现。在图 11.6 中，第 34–35 行表示 `Array` 类的私有数据成员。每个 `Array` 对象由一个 `size` 成员（表示 `Array` 中元素的数量）和一个 `int` 指针——`ptr`——组成，该指针指向由 `Array` 对象管理的、动态分配的基于指针的整数数组。

## 将流插入运算符和流提取运算符重载为友元

图 11.6 的第 11–12 行将重载的流插入运算符和重载的流提取运算符声明为 `Array` 类的友元。当编译器看到像 `cout << arrayObject` 这样的表达式时，会通过以下调用调用全局函数 `operator<<`：

```cpp
operator<<( cout, arrayObject )
```

当编译器看到像 `cin >> arrayObject` 这样的表达式时，会通过以下调用调用全局函数 `operator>>`：

```cpp
operator>>( cin, arrayObject )
```

我们再次指出，这些流插入和流提取运算符函数不能是 `Array` 类的成员，因为 `Array` 对象总是出现在流插入运算符和流提取运算符的右侧。如果这些运算符函数是 `Array` 类的成员，则必须使用以下别扭的语句来输出和输入一个 `Array`：

```cpp
arrayObject << cout;
arrayObject >> cin;
```

对大多数熟悉 `cout` 和 `cin` 分别作为 `<<` 和 `>>` 左操作数出现的 C++ 程序员来说，这样的语句会令人困惑。

