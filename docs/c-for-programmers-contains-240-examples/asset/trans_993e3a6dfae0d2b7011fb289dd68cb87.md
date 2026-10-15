

```
48  static const int daysPerMonth[ 13 ] =
49      { 0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };
50
51  // determine whether testDay is valid for specified month
52  if ( testDay > 0 && testDay <= daysPerMonth[ month ] )
53      return testDay;
54
55  // February 29 check for leap year
56  if ( month == 2 && testDay == 29 && ( year % 400 == 0 ||
57      ( year % 4 == 0 && year % 100 != 0 ) ) )
58      return testDay;
59
60  cout << "Invalid day (" << testDay << ") set to 1.\n";
61      return 1; // leave object in consistent state if bad value
62  } // end function checkDay
```

图 10.11 | Date 类成员函数定义。（第 2 部分，共 2 部分。）

```
1  // Fig. 10.12: Employee.h
2  // Employee class definition showing composition.
3  // Member functions defined in Employee.cpp.
4  #ifndef EMPLOYEE_H
5  #define EMPLOYEE_H
6
7  #include "Date.h" // include Date class definition
8
9  class Employee
10 {
11  public:
12      Employee( const char * const, const char * const,
13          const Date &, const Date & );
14      void print() const;
15      ~Employee(); // provided to confirm destruction order
16  private:
17      char firstName[ 25 ];
18      char lastName[ 25 ];
19      const Date birthDate; // composition: member object
20      const Date hireDate; // composition: member object
21  }; // end class Employee
22
23  #endif
```

图 10.12 | 显示组合的 Employee 类定义。

Class Date 和 class Employee 各自包含一个析构函数（图 10.11 的第 37–42 行和图 10.13 的第 51–55 行），该析构函数在所属类的对象被析构时打印一条消息。这使我们能够确认程序输出中对象是从内向外构造、从外向内以相反顺序销毁（即包含它们的 Employee 对象在 Date 成员对象之后被销毁）。请注意图 10.14 输出中的最后四行。最后两行是 Date 析构函数在 Date 对象 hire（第 12 行）和 birth（第 11 行）上运行的输出。这些输出证实了在 main 中创建的三个对象以与构造顺序相反的顺序被析构。（Employee 析构函数输出在倒数第五行。）输出窗口倒数第四行和倒数第三行显示了 Employee 的成员对象 hireDate（图 10.12，第 20 行）和 birthDate（图 10.12，第 19 行）的析构函数运行。这些输出证实 Employee 对象是从外向内析构的——即 Employee 析构函数先运行（输出显示在输出窗口倒数第五行），然后成员对象以与构造时相反的顺序被析构。同样，图 10.14 中的输出并未显示这些成员对象的构造函数运行，因为它们是 C++ 编译器提供的默认拷贝构造函数。

```
1  // Fig. 10.13: Employee.cpp
2  // Employee class member-function definitions.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  #include <cstring> // strlen and strncpy prototypes
8  using std::strlen;
9  using std::strncpy;
10
11 #include "Employee.h" // Employee class definition
12 #include "Date.h" // Date class definition
13
14 // constructor uses member initializer list to pass initializer
15 // values to constructors of member objects birthDate and hireDate
16 // [Note: This invokes the so-called "default copy constructor" which the
17 // C++ compiler provides implicitly.]
18 Employee::Employee( const char * const first, const char * const last,
19     const Date &dateOfBirth, const Date &dateOfHire )
20   : birthDate( dateOfBirth ), // initialize birthDate
21     hireDate( dateOfHire ) // initialize hireDate
22 {
23     // copy first into firstName and be sure that it fits
24     int length = strlen( first );
25     length = ( length < 25 ? length : 24 );
26     strncpy( firstName, first, length );
27     firstName[ length ] = '\0';
28
29     // copy last into lastName and be sure that it fits
30     length = strlen( last );
31     length = ( length < 25 ? length : 24 );
32     strncpy( lastName, last, length );
33     lastName[ length ] = '\0';
34
35     // output Employee object to show when constructor is called
36     cout << "Employee object constructor: "
37         << firstName << ' ' << lastName << endl;
38 } // end Employee constructor
```

图 10.13 | Employee 类成员函数定义，包括带成员初始化列表的构造函数。（第 1 部分，共 2 部分。）

```
40 // print Employee object
41 void Employee::print() const
42 {
43     cout << lastName << ", " << firstName << "  Hired: ";
44     hireDate.print();
45     cout << "  Birthday: ";
46     birthDate.print();
47     cout << endl;
48 } // end function print
49
50 // output Employee object to show when its destructor is called
51 Employee::~Employee()
52 {
53     cout << "Employee object destructor: "
54         << lastName << ", " << firstName << endl;
55 } // end ~Employee destructor
```

图 10.13 | Employee 类成员函数定义，包括带成员初始化列表的构造函数。（第 2 部分，共 2 部分。）

成员对象无需通过成员初始化器显式初始化。如果未提供成员初始化器，则成员对象的默认构造函数将被隐式调用。默认构造函数建立的任何值都可以通过 set 函数被覆盖。然而，对于复杂的初始化，这种方法可能需要额外的大量工作和时间。

```
1 // Fig. 10.14: fig10_14.cpp
2 // Demonstrating composition--an object with member objects.
3 #include <iostream>
4 using std::cout;
5 using std::endl;
6
7 #include "Employee.h" // Employee class definition
8
9 int main()
10 {
11     Date birth( 7, 24, 1949 );
12     Date hire( 3, 12, 1988 );
13     Employee manager( "Bob", "Blue", birth, hire );
14
15     cout << endl;
16     manager.print();
17
18     cout << "\nTest Date constructor with invalid values:\n";
19     Date lastDayOff( 14, 35, 1994 ); // invalid month and day
20     cout << endl;
21     return 0;
22 } // end main
```

图 10.14 | 演示组合——带成员对象的对象。（第 1 部分，共 2 部分。）

```
Date object constructor for date 7/24/1949
Date object constructor for date 3/12/1988
Employee object constructor: Bob Blue

Blue, Bob  Hired: 3/12/1988  Birthday: 7/24/1949

Test Date constructor with invalid values:
Invalid month (14) set to 1.
Invalid day (35) set to 1.
Date object constructor for date 1/1/1994

Date object destructor for date 1/1/1994
Employee object destructor: Blue, Bob
Date object destructor for date 3/12/1988
Date object destructor for date 7/24/1949
Date object destructor for date 3/12/1988
Date object destructor for date 7/24/1949
```

请注意，当构造一个 Employee 时实际上有三次构造函数调用——两次对 Date 类默认拷贝构造函数的调用（由图 10.13 的第 20–21 行调用）和对 Employee 类构造函数的调用。

## 图 10.14 | 演示组合——带成员对象的对象。（第 2 部分，共 2 部分。）

## 常见编程错误 10.6

如果成员对象未使用成员初始化器初始化，并且成员对象的类未提供默认构造函数（即成员对象的类定义了一个或多个构造函数，但没有默认构造函数），则会发生编译错误。

## 性能提示 10.2

通过成员初始化器显式初始化成员对象。这消除了“双重初始化”成员对象的开销——一次是在调用成员对象的默认构造函数时，另一次是在构造函数体中（或之后）调用 set 函数以初始化成员对象时。

## 软件工程观察 10.7

如果类的成员是另一个类的对象，使该成员对象变为 public 并不会违反该成员对象私有成员的封装和隐藏。然而，它确实违反了包含类的实现的封装和隐藏，因此类类型的成员对象仍应为 private，就像所有其他数据成员一样。

在图 10.11 的第 26 行，注意对 Date 成员函数 print 的调用。C++ 中类的许多成员函数不需要参数。这是因为每个成员函数都包含一个隐式句柄（以指针形式）指向其操作的那个对象。我们将在第 10.5 节讨论隐式指针，它由关键字 this 表示。

Class Employee 使用两个 25 字符的数组（图 10.12，第 17–18 行）来表示 Employee 的名字和姓氏。这些数组对于短于 24 个字符的名字会浪费空间。（记住，每个数组中的一个字符用于字符串的终止空字符 '\0'。）此外，长于 24 个字符的名字必须被截断以适应这些固定大小的字符数组。第 10.7 节介绍了另一个版本的 Employee 类，该类动态创建保存名字和姓氏所需的确切空间。

请注意，使用所需确切空间表示 Employee 的名字和姓氏的最简单方法是使用两个 string 对象（C++ 标准库类

