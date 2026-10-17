
## Fig. 7.25: `fig07_25.cpp`

// Creates GradeBook object using a two-dimensional array of grades.

```cpp
#include "GradeBook.h" // GradeBook class definition

// function main begins program execution

int main()
{
   // two-dimensional array of student grades
   int gradesArray[GradeBook::students][GradeBook::tests] =
      { { 87, 96, 70 },
        { 68, 87, 90 },
        { 94, 100, 90 },
        { 100, 81, 82 },
        { 83, 65, 85 },
        { 78, 87, 65 },
        { 85, 75, 83 },
        { 91, 94, 100 },
        { 76, 72, 84 },
        { 87, 93, 73 } };

    GradeBook myGradeBook(
    "CS101 Introduction to C++ Programming", gradesArray );
    myGradeBook.displayMessage();
    myGradeBook.processGrades();
    return 0; // indicates successful termination
} // end main
```

**Fig. 7.25** | Creates a GradeBook object using a two-dimensional array of grades, then invokes member function `processGrades` to analyze them. (Part 1 of 2.)

欢迎使用成绩簿
CS101 Introduction to C++ Programming!

成绩如下：

|          | Test 1 | Test 2 | Test 3 | Average |
|----------|--------|--------|--------|---------|
| Student 1| 87     | 96     | 70     | 84.33   |
| Student 2| 68     | 87     | 90     | 81.67   |
| Student 3| 94     | 100    | 90     | 94.67   |
| Student 4| 100    | 81     | 82     | 87.67   |
| Student 5| 83     | 65     | 85     | 77.67   |
| Student 6| 78     | 87     | 65     | 76.67   |
| Student 7| 85     | 75     | 83     | 81.00   |
| Student 8| 91     | 94     | 100    | 95.00   |
| Student 9| 76     | 72     | 84     | 77.33   |
| Student 10| 87    | 93     | 73     | 84.33   |

成绩簿中最低成绩为 65
成绩簿中最高成绩为 100

总体成绩分布：
0-9:
10-19:
20-29:
30-39:
40-49:
50-59:
60-69: ***
70-79: ******
80-89: ************
90-99: *********
100: ***

图 7.25 | 使用二维成绩数组创建 GradeBook 对象，然后调用成员函数 `processGrades` 对其进行分析。 (第 2 部分，共 2 部分。)

## 7.11 C++ 标准库类模板 `vector` 的介绍

我们现在介绍 C++ 标准库类模板 `vector`，它表示一种更强大的数组类型，具有许多额外的功能。正如你在后面的章节中会看到的那样，C 风格的基于指针的数组（即迄今为止介绍的数组类型）存在很大的错误风险。例如，如前所述，程序很容易“走出”数组的两端，因为 C++ 不会检查下标是否超出数组的范围。两个数组不能使用相等运算符或关系运算符有意义地进行比较。正如你在第 8 章中会看到的那样，指针变量（更 commonly 称为指针）包含其值作为内存地址。数组名只是指向内存中数组开始位置的指针，当然，两个数组总是在不同的内存位置。当一个数组被传递给设计用于处理任意大小数组的通用函数时，数组的大小必须作为额外的参数传递。此外，一个数组不能使用赋值运算符赋给另一个数组——数组名是 `const` 指针，正如你在第 8 章中会看到的那样，常量指针不能用作赋值运算符的左侧。这些和其他功能对于处理数组来说似乎是“自然的”，但 C++ 并未提供此类功能。然而，C++ 标准库提供了类模板 `vector`，允许程序员创建比数组更强大且出错率更低的替代方案。在第 11 章《运算符重载；字符串和数组对象》中，我们介绍了实现此类数组功能的方法，如 `vector` 所提供的功能。你将看到如何为自己的类自定义运算符（这种技术称为运算符重载）。

`vector` 类模板可供任何使用 C++ 构建应用程序的人使用。`vector` 示例使用的记法可能对你来说不熟悉，因为 `vector` 使用模板记法。回想一下，第 6.18 节讨论了函数模板。在第 14 章中，我们讨论类模板。目前，你应该能够通过模仿本节中示例的语法来舒适地使用类模板 `vector`。随着我们在第 14 章研究类模板，你的理解会加深。第 20 章详细介绍了类模板 `vector`（以及其他几个标准 C++ 容器类）。

图 7.26 的程序演示了 C++ 标准库类模板 `vector` 提供的功能，这些功能对于 C 风格的基于指针的数组是不可用的。标准类模板 `vector` 提供了与我们在第 11 章《运算符重载；字符串和数组对象》中构建的 `Array` 类相同的许多功能。标准类模板 `vector` 在头文件 `<vector>` 中定义（第 11 行）并属于命名空间 `std`（第 12 行）。第 20 章讨论了标准类模板 `vector` 的完整功能。

第 19-20 行创建了两个存储类型为 `int` 的 `vector` 对象——`integers1` 包含七个元素，`integers2` 包含 10 个元素。默认情况下，每个 `vector` 对象的元素都设置为 0。请注意，`vector` 可以定义为存储任何数据类型，只需将 `vector<int>` 中的 `int` 替换为适当的数据类型即可。这种指定 `vector` 中存储类型的记法与第 6.18 节中用函数模板引入的模板记法类似。再次强调，第 14 章详细讨论了这种语法。

### Fig. 7.26: `fig07_26.cpp`

```cpp
// Demonstrating C++ Standard Library class template vector.
#include <iostream>
using std::cout;
using std::cin;
using std::endl;

#include <iomanip>
using std::setw;

#include <vector>
using std::vector;

void outputVector( const vector< int > & ); // display the vector
void inputVector( vector< int > & ); // input values into the vector

int main()
{
    vector< int > integers1( 7 ); // 7-element vector< int >
    vector< int > integers2( 10 ); // 10-element vector< int >

    // print integers1 size and contents
    cout << "Size of vector integers1 is " << integers1.size()
        << "\nvector after initialization:" << endl;
    outputVector( integers1 );

    // print integers2 size and contents
    cout << "\nSize of vector integers2 is " << integers2.size()
        << "\nvector after initialization:" << endl;
    outputVector( integers2 );

    // input and print integers1 and integers2
    cout << "\nEnter 17 integers:" << endl;
    inputVector( integers1 );
    inputVector( integers2 );

    cout << "\nAfter input, the vectors contain:\n"
        << "integers1:" << endl;
    outputVector( integers1 );
    cout << "integers2:" << endl;
    outputVector( integers2 );

    // use inequality (!=) operator with vector objects
    cout << "\nEvaluating: integers1 != integers2" << endl;

    if ( integers1 != integers2 )
        cout << "integers1 and integers2 are not equal" << endl;

    // create vector integers3 using integers1 as an
    // initializer; print size and contents
    vector< int > integers3( integers1 ); // copy constructor

    cout << "\nSize of vector integers3 is " << integers3.size()
        << "\nvector after initialization:" << endl;
    outputVector( integers3 );

    // use overloaded assignment (=) operator
    cout << "\nAssigning integers2 to integers1:" << endl;
    integers1 = integers2; // assign integers2 to integers1

    cout << "integers1:" << endl;
    outputVector( integers1 );
    cout << "integers2: " << endl;
    outputVector( integers2 );

    // use equality (==) operator with vector objects
    cout << "\nEvaluating: integers1 == integers2" << endl;
    if ( integers1 == integers2 )
       cout << "integers1 and integers2 are equal" << endl;

    // use square brackets to create rvalue
    cout << "\nintegers1[5] is " << integers1[ 5 ];

    // use square brackets to create lvalue
    cout << "\n\nAssigning 1000 to integers1[5]" << endl;
    integers1[ 5 ] = 1000;
    cout << "integers1: " << endl;
    outputVector( integers1 );

    // attempt to use out-of-range subscript
    cout << "\nAttempt to assign 1000 to integers1.at( 15 )" << endl;
    integers1.at( 15 ) = 1000; // ERROR: out of range
    return 0;
} // end main

// output vector contents
void outputVector( const vector< int > &array )
{
   size_t i; // declare control variable
   for ( i = 0; i < array.size(); i++ )
   {
      cout << setw( 12 ) << array[ i ];
      if ( ( i + 1 ) % 4 == 0 ) // 4 numbers per row of output
         cout << endl;
   } // end for
   if ( i % 4 != 0 )
      cout << endl;
} // end function outputVector

// input vector contents
void inputVector( vector< int > &array )
{
   for ( size_t i = 0; i < array.size(); i++ )
      cin >> array[ i ];
} // end function inputVector
```

图 7.26 | C++ 标准库类模板 `vector`。 (第 1 部分，共 4 部分。)

**图 7.26** | C++ 标准库类模板 `vector`。 (第 3 部分，共 4 部分。)

```
Size of vector integers1 is 7
vector after initialization:
             0             0             0             0
             0             0             0
```

```
Size of vector integers2 is 10
vector after initialization:
                 0                 0                 0                 0
                 0                 0                 0                 0
                 0                 0
Enter 17 integers:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17
After input, the vectors contain:
integers1:
                 1                 2                 3                 4
                 5                 6                 7
integers2:
                 8                 9                10                11
                12                13                14                15
                16                17
Evaluating: integers1 != integers2
integers1 and integers2 are not equal
Size of vector integers3 is 7
vector after initialization:
                 1                 2                 3                 4
                 5                 6                 7
Assigning integers2 to integers1:
integers1:
                 8                 9                10                11
```

