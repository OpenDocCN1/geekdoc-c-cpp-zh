
Fig. 11.5 | Overloaded stream insertion and stream extraction operators. (Part 1 of 2.)

`PhoneNumber` 对象可以与对其他 `PhoneNumber` 对象或其他数据类型对象的输入操作一起级联。例如，程序可以在一个语句中输入两个 `PhoneNumber` 对象，如下所示：

```
cin >> phone1 >> phone2;
```

首先，表达式 `cin >> phone1` 通过进行全局函数调用执行

```
operator>>( cin, phone1 );
```

此调用然后将对 `cin` 的引用作为 `cin >> phone1` 的值返回，因此表达式的剩余部分被简单地解释为 `cin >> phone2`。这通过进行全局函数调用执行

```
operator>>( cin, phone2 );
```

流插入运算符函数（图 11.4，第 12–17 行）接受一个 `ostream` 引用（output）和一个 `const PhoneNumber` 引用（number）作为参数并返回一个 `ostream` 引用。函数 `operator<<` 显示 `PhoneNumber` 类型的对象。当编译器看到图 11.5 第 25 行的表达式

```
cout << phone
```

时，编译器会生成全局函数调用

```
operator<<( cout, phone );
```

函数 `operator<<` 将电话号码的各部分作为字符串显示，因为它们存储为字符串对象。

# 错误预防提示 11.1

> 从重载的 `<<` 或 `>>` 运算符函数返回引用通常是成功的，因为 `cout`、`cin` 和大多数流对象都是全局的，或至少是长寿命的。返回对自动变量或其他临时对象的引用是危险的——这会创建指向不存在对象的“悬空引用”。

请注意，函数 `operator>>` 和 `operator<<` 在 `PhoneNumber` 中声明为全局友元函数（图 11.3，第 15–16 行）。它们是全局函数，因为 `PhoneNumber` 类的对象在每种情况下都作为运算符的右操作数出现。记住，二元运算符的重载运算符函数只有当左操作数是函数所属类的对象时才能是成员函数。重载的输入和输出运算符如果需要直接访问非公共类成员以提高性能或因为类可能没有提供适当的 get 函数，则声明为友元。此外，请注意函数 `operator<<` 的参数列表中的 `PhoneNumber` 引用（图 11.4，第 12 行）是 `const`，因为 `PhoneNumber` 只会被输出，而函数 `operator>>` 的参数列表中的 `PhoneNumber` 引用（第 22 行）是非 `const` 的，因为 `PhoneNumber` 对象必须被修改以将输入的电话号码存储在对象中。

# 软件工程观察 11.3

> 在不修改标准输入/输出库类的情况下，为用户定义类型添加新的输入/输出功能。这是 C++ 可扩展性的又一例证。

## 11.6 重载一元运算符

类的一个一元运算符可以重载为无参数的非静态成员函数，或重载为一个参数的全局函数；该参数必须是类的对象或对类的对象的引用。实现重载运算符的成员函数必须是非静态的，以便它们可以访问类的每个对象的非静态数据。记住，静态成员函数只能访问类的静态成员。

本章后面，我们将重载一元运算符 `!` 来测试我们创建的 `String` 类（第 11.10 节）的对象是否为空并返回一个 `bool` 结果。考虑表达式 `!s`，其中 `s` 是 `String` 类的对象。当一元运算符如 `!` 被重载为无参数的成员函数时，编译器看到表达式 `!s` 时，会生成函数调用 `s.operator!()`。操作数 `s` 是调用 `String` 类成员函数 `operator!` 的类对象。函数在类定义中声明如下：

```
class String
{
public:
   bool operator!() const;
   ...
}; // end class String
```

一元运算符如 `!` 可以重载为一个参数的全局函数，有两种不同的方式——参数可以是对象（这需要对象的拷贝，因此函数的副作用不会应用于原始对象），或参数可以是对对象的引用（不会对原始对象进行拷贝，因此该函数的任何副作用都会应用于原始对象）。如果 `s` 是 `String` 类对象（或对 `String` 类对象的引用），则 `!s` 被视为已编写调用 `operator!()`，调用声明如下的全局 `operator!` 函数：

```
bool operator!( const String & );
```

## 11.7 重载二元运算符

二元运算符可以重载为一个参数的非静态成员函数，或重载为两个参数的全局函数（其中一个参数必须是类对象或对类对象的引用）。

本章后面，我们将重载 `<` 来比较两个 `String` 对象。当将二元运算符 `<` 重载为 `String` 类的一个参数的非静态成员函数时，如果 `y` 和 `z` 是 `String` 类对象，则 `y < z` 被视为已编写 `y.operator<(z)`，调用下面声明的 `operator<` 成员函数

```
class String
public:
   bool operator<( const String & ) const;
}; // end class String
```

如果二元运算符 `<` 要重载为全局函数，它必须采用两个参数——其中一个必须是类对象或对类对象的引用。如果 `y` 和 `z` 是

`String`-class objects or references to `String`-class objects, then `v < z` is treated as if the call `operator<( y, z )` had been written in the program, invoking global-function `operator<` declared as follows:

```
bool operator<( const String &, const String & );
```

## 11.8 Case Study: Array Class

基于指针的数组存在许多问题。例如，程序很容易“走出”数组的两端，因为 C++ 不会检查下标是否超出数组范围（你仍然可以显式地这样做）。大小为 *n* 的数组必须将元素编号为 0, …, *n* − 1；不允许使用其他下标范围。整个非字符数组不能一次输入或输出；每个数组元素必须单独读取或写入。两个数组不能通过相等运算符或关系运算符进行有意义的比较（因为数组名只是指向内存中数组开始位置的指针，当然两个数组总是在不同的内存位置）。当数组传递给设计用于处理任意大小数组的通用函数时，数组的大小必须作为额外参数传递。一个数组不能用赋值运算符赋给另一个数组（因为数组名是 const 指针，常量指针不能用在赋值运算符的左侧）。这些和其他功能对于处理数组来说似乎是“自然的”，但基于指针的数组不提供此类功能。然而，C++ 通过使用类和运算符重载提供了实现此类数组功能的方法。

在此示例中，我们创建了一个功能强大的数组类，该类执行范围检查以确保下标保持在 `Array` 的边界内。该类允许使用赋值运算符将一个数组对象赋给另一个数组。`Array` 类的对象知道自己的大小，因此在将 `Array` 传递给函数时，无需将大小单独作为参数传递。整个数组都可以用流提取运算符和流插入运算符分别进行输入或输出。可以使用相等运算符 `==` 和 `!=` 对数组进行比较。

此示例将加深你对数据抽象的理解。你可能希望建议对此 `Array` 类的其他增强。类开发是一项有趣、富有创造性且智力上具有挑战性的活动——始终以“打造有价值的类”为目标。

图 11.6–11.8 的程序演示了类 `Array` 及其重载的运算符。首先我们遍历 main（图 11.8）。然后我们考虑类定义（图 11.6）以及类的每个成员函数和友元函数定义（图 11.7）。

### Fig. 11.6 | Array class definition with overloaded operators. (Part 1 of 2.)

// Fig. 11.6: Array.h
// Array class definition with overloaded operators.
#ifndef ARRAY_H
#define ARRAY_H

```
#include <iostream>
using std::ostream;
using std::istream;
class Array
{
    friend ostream &operator<<( ostream &, const Array & );
    friend istream &operator>>( istream &, Array & );
public:
    Array( int = 10 ); // default constructor
    Array( const Array & ); // copy constructor
    ~Array(); // destructor
    int getSize() const; // return size
    const Array &operator=( const Array & ); // assignment operator
    bool operator==( const Array & ) const; // equality operator
    // inequality operator; returns opposite of == operator
    bool operator!=( const Array &right ) const
    {
        return ! ( *this == right ); // invokes Array::operator==
    } // end function operator!=
    // subscript operator for non-const objects returns modifiable lvalue
    int &operator[]( int );
    // subscript operator for const objects returns rvalue
    int operator[]( int ) const;
private:
    int size; // pointer-based array size
    int *ptr; // pointer to first element of pointer-based array
}; // end class Array
#endif
```

Fig. 11.6 | Array class definition with overloaded operators. (Part 2 of 2.)

### Fig. 11.7 | Array class member- and friend-function definitions. (Part 1 of 4.)

// Fig 11.7: Array.cpp
// Array class member- and friend-function definitions.
#include <iostream>
using std::cerr;
using std::cout;
using std::cin;
using std::endl;

#include <iomanip>
using std::setw;

#include <cstdlib> // exit function prototype
using std::exit;

Fig. 11.7 | Array class member- and friend-function definitions. (Part 1 of 4.)

```
65      for ( int i = 0; i < size; i++ )
66          ptr[ i ] = right.ptr[ i ]; // copy array into object
67      } // end outer if
68
69      return *this; // enables x = y = z, for example
70  } // end function operator=
71
72  // determine if two Arrays are equal and
73  // return true, otherwise return false
74  bool Array::operator==( const Array &right ) const
75  {
76      if ( size != right.size )
77          return false; // arrays of different number of elements
78
79      for ( int i = 0; i < size; i++ )
80          if ( ptr[ i ] != right.ptr[ i ] )
81              return false; // Array contents are not equal
82
83      return true; // Arrays are equal
84  } // end function operator==
85
86  // overloaded subscript operator for non-const Arrays;
87  // reference return creates a modifiable lvalue
88  int &Array::operator[]( int subscript )
89  {
90      // check for subscript out-of-range error
91      if ( subscript < 0 || subscript >= size )
92      {
93          cerr << "\nError: Subscript " << subscript
94              << " out of range" << endl;
95          exit( 1 ); // terminate program; subscript out of range
96      } // end if
97
98      return ptr[ subscript ]; // reference return
99  } // end function operator[]
100
101  // overloaded subscript operator for const Arrays
102  // const reference return creates an rvalue
103  int Array::operator[]( int subscript ) const
104  {
105      // check for subscript out-of-range error
106      if ( subscript < 0 || subscript >= size )
107      {
108          cerr << "\nError: Subscript " << subscript
109              << " out of range" << endl;
110          exit( 1 ); // terminate program; subscript out of range
111      } // end if
112
113      return ptr[ subscript ]; // returns copy of this element
114  } // end function operator[]
115
```

Fig. 11.7 | Array class member- and friend-function definitions. (Part 3 of 4.)

```
// overloaded input operator for class Array;
// inputs values for entire Array
istream &operator>>( istream &input, Array &a )
{
   for ( int i = 0; i < a.size; i++ )
      input >> a.ptr[ i ];
   return input; // enables cin >> x >> y;
} // end function
// overloaded output operator for class Array
ostream &operator<<( ostream &output, const Array &a )
{
   int i;
   // output private ptr-based array
   for ( i = 0; i < a.size; i++ )
   {
      output << setw( 12 ) << a.ptr[ i ];
      if ( ( i + 1 ) % 4 == 0 ) // 4 numbers per row of output
         output << endl;
   } // end for
   if ( i % 4 != 0 ) // end last line of output
      output << endl;
