

步骤 1：在 main 调用 cubeByValue 之前：

```c
int main()
{
    int number = 5;
    number = cubeByValue( number );
}

// number: 5
```

```c
int cubeByValue( int n )
{
    return n * n * n;
}

// n: undefined
```

步骤 2：cubeByValue 收到调用后：

```c
int main()
{
    int number = 5;
    number = cubeByValue( number );
}

// number: 5
```

```c
int cubeByValue( int n )
{
    return n * n * n;
}

// n: 5
```

步骤 3：cubeByValue 对参数 n 求立方后，且在 cubeByValue 返回 main 之前：

```c
int main()
{
    int number = 5;
    number = cubeByValue( number );
}

// number: 5
```

```c
int cubeByValue( int n )
{
    return n * n * n;   // 125
}

// n: 5
```

步骤 4：cubeByValue 返回 main 后，且在将结果赋给 number 之前：

```c
int main()
{
    int number = 5;
    number = cubeByValue( number );   // 125
}

// number: 5
```

```c
int cubeByValue( int n )
{
    return n * n * n;
}

// n: undefined
```

步骤 5：main 完成对 number 的赋值后：

```c
int main()
{
    int number = 5;
    number = cubeByValue( number );
}

// number: 125
// returned value: 125
```

```c
int cubeByValue( int n )
{
    return n * n * n;
}

// n: undefined
```

**图 8.8** | 图 8.6 中程序的按值传递分析。

第 6 章解释过，当实参按值传递时，函数调用中的实参副本会被创建并传递给函数。如果副本在函数中被修改，调用方中的原始值不会改变。在许多情况下，传递给函数的值会在该函数中被修改。然而，在某些情况下，即使被调用函数只操作原始值的副本，该值也不应在被调用函数中被更改。

考虑一个函数，它接收一维数组及其大小作为实参，然后打印该数组。这样的函数应循环遍历数组并逐个输出每个元素。数组的大小在函数体中用于确定数组的最高下标，以便在打印完成时循环可以终止。数组的大小不需要在函数体中改变，因此应将其声明为 const 以确保它不会改变。因为数组只是被打印，所以它也应被声明为 const。这一点尤其重要，因为数组总是按引用传递，并且很容易在被调用函数中被更改。如果尝试修改 const 值，就会发生错误。

> **软件工程观察 8.2**
> 
> *如果一个值在它被传递到的函数体中不会（或不应）改变，则该参数应声明为 const。*

![](img/bfd978e7e9b192bab46ec2a89e481263_373_0.png)

> **防错提示 8.2**
> 
> *在使用函数之前，检查其函数原型，以确定它可以修改和不能修改的参数。*

![](img/bfd978e7e9b192bab46ec2a89e481263_373_1.png)

将指针传递给函数有四种方式：指向非常量数据的非常量指针、指向常量数据的非常量指针（图 8.10）、指向非常量数据的常量指针（图 8.11）以及指向常量数据的常量指针（图 8.12）。每种组合提供不同级别的访问权限。

## 指向非常量数据的非常量指针

最高访问权限由指向非常量数据的非常量指针授予——可以通过解引用后的指针修改数据，并且可以修改指针使其指向其他数据。此类指针的声明（例如 `int *countPtr`）不包含 const。

## 指向常量数据的非常量指针

指向常量数据的非常量指针是一种可以修改为指向适当类型的任何数据项的指针，但不能通过该指针修改它所指向的数据。这样的指针可用于接收传递给函数的数组实参，该函数将处理每个数组元素，但不应允许修改数据。在函数中任何修改数据的尝试都会导致编译错误。此类指针的声明将 const 放在指针类型的左侧，如下所示

```cpp
const int *countPtr;
```

该声明从右到左读作“countPtr 是一个指向整型常量的指针”。图 8.10 展示了尝试编译一个函数时产生的编译错误消息，该函数接收指向常量数据的非常量指针，然后试图使用该指针修改数据。

```cpp
// Fig. 8.10: fig08_10.cpp
// Attempting to modify data through a
// nonconstant pointer to constant data.

void f( const int * ); // prototype

int main()
{
    int y;

    f( &y ); // f attempts illegal modification
} // end main

// xPtr cannot modify the value of constant variable to which it points
void f( const int *xPtr )
{
    *xPtr = 100; // error: cannot modify a const object
} // end function f
```

*Microsoft Visual C++ 编译器错误消息：*

```text
c:\cpphtp8_examples\ch08\Fig08_10\fig08_10.cpp(17) :
    error C3892: 'xPtr' : you cannot assign to a variable that is const
```

*GNU C++ 编译器错误消息：*

```text
fig08_10.cpp: In function 'void f(const int*)':
fig08_10.cpp:17: error: assignment of read-only location
```

**图 8.10** | 尝试通过指向常量数据的非常量指针修改数据。

如你所知，数组是聚合数据类型，它们在同一个名称下存储相同类型的相关数据项。当以数组作为实参调用函数时，数组会按引用传递给函数。然而，默认情况下，对象按值传递——传递整个对象的副本。这需要执行时开销：复制对象中的每个数据项并将其存储在函数调用栈上。当传递指向对象的指针时，只需复制对象的地址——对象本身不会被复制。

![](img/bfd978e7e9b192bab46ec2a89e481263_374_0.png)

> **性能提示 8.1**
> 
> *如果大型对象不需要被调用函数修改，请使用指向常量数据的指针或对常量数据的引用传递它们，以获得按引用传递的性能优势。*

![](img/bfd978e7e9b192bab46ec2a89e481263_374_1.png)

> **软件工程观察 8.3**
> 
> *使用指向常量数据的指针或对常量数据的引用传递大型对象，以获得按值传递的安全性。*

## 指向非常量数据的常量指针

指向非常量数据的常量指针是一种始终指向同一内存位置的指针；可以通过该指针修改该位置的数据。通过该指针修改数据的一个示例。数组应以这种方式传递给一个*只读取*该数组（使用数组下标表示法）且*不修改*该数组的函数。图 8.12 的程序将指针变量 `ptr` 声明为 `const int * const` 类型（第 13 行）。该声明从*右到左*读作“ptr 是一个指向整型常量的常量指针”。该图展示了在尝试修改 ptr 所指向的数据时（第 17 行）以及尝试修改指针变量中存储的地址时（第 18 行）所产生的错误消息。当程序尝试解引用 `ptr`（第 15 行）时，或当程序尝试输出 ptr 所指向的值时，不会发生错误，因为在此语句中，指针及其指向的数据都没有被修改。

```cpp
// Fig. 8.12: fig08_12.cpp
// Attempting to modify a constant pointer to constant data.
#include <iostream>
using namespace std;

int main()
{
   int x = 5, y;

   // ptr is a constant pointer to a constant integer.
   // ptr always points to the same location; the integer
   // at that location cannot be modified.
   const int *const ptr = &x;

   cout << *ptr << endl;

   *ptr = 7; // error: *ptr is const; cannot assign new value
   ptr = &y; // error: ptr is const; cannot assign new address
} // end main
```

*Microsoft Visual C++ 编译器错误消息：*

```text
c:\cpphtp8_examples\ch08\Fig08_12\fig08_12.cpp(17) : error C3892: 'ptr' :
   you cannot assign to a variable that is const
c:\cpphtp8_examples\ch08\Fig08_12\fig08_12.cpp(18) : error C3892: 'ptr' :
   you cannot assign to a variable that is const
```

*GNU C++ 编译器错误消息：*

```text
fig08_12.cpp: In function ‘int main()’:
fig08_12.cpp:17: error: assignment of read-only location
fig08_12.cpp:18: error: assignment of read-only variable ‘ptr’
```

**图 8.12** | 尝试修改指向常量数据的常量指针。

## 8.6 使用按引用传递的选择排序

在本节中，我们定义一个排序程序，以演示按引用传递数组和单个数组元素。我们使用**选择排序**算法，这是一种易于编写但遗憾的是效率较低的排序算法。该算法的第一次迭代

