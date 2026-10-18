
We are in outer block

m = 20
::m = 10
```

In the above program, the variable **m** is declared at three places, namely, outside the **main()** function, inside the **main()**, and inside the inner block.

> **NOTE:** *It is to be noted ::m will always refer to the global m. In the inner block, ::m refers to the value 10 and not 20.*

A major application of the scope resolution operator is in the classes to identify the class to which a member function belongs. This will be dealt in detail later when the classes are introduced.

## 3.16 Member Dereferencing Operators

As you know, C++ permits us to define a class containing various types of data and functions as members. C++ also permits us to access the class members through pointers. In order to achieve this, C++ provides a set of three pointer-to-member operators. [Table 3.5](#table-3.5) shows these operators and their functions.

### Table 3.5 Member dereferencing operators

| Operator | Function |
|---|---|
| `::*` | To declare a pointer to a member of a class |
| `.*` | To access a member using object name and a pointer to that member |
| `->*` | To access a member using a pointer to the object and a pointer to that member |

Further details on these operators will be meaningful only after we discuss classes, and therefore we defer the use of member dereferencing operators until then.

## 3.17 Memory Management Operators

C uses **malloc()** and **calloc()** functions to allocate memory dynamically at run time. Similarly, it uses the function **free()** to free dynamically allocated memory. We use dynamic allocation techniques when it is not known in advance how much of memory space is needed. Although C++ supports these functions, it also defines two unary operators **new** and **delete** that perform the task of allocating and freeing the memory in a better and easier way. Since these operators manipulate memory on the free store, they are also known as *free store* operators.

An object can be created by using **new**, and destroyed by using **delete**, as and when required. A data object created inside a block with **new**, will remain in existence until it is explicitly destroyed by using **delete**. Thus, the lifetime of an object is directly under our control and is unrelated to the block structure of the program.

The **new** operator can be used to create objects of any type. It takes the following general form:

```
pointer-variable = new data-type;
```

Here, *pointer-variable* is a pointer of type *data-type*. The **new** operator allocates sufficient memory to hold a data object of type *data-type* and returns the address of the object. The *data-type* may be any valid data type. The *pointer-variable* holds the address of the memory space allocated.

Examples:

Here, size specifies the number of elements in the array. For example, the statement

```cpp
int *p = new int[10];
```

creates a memory space for an array of 10 integers. **p[0]** will refer to the first element, **p[1]** to the second element, and so on.

When creating multi-dimensional arrays with **new**, all the array sizes must be supplied.

```cpp
array_ptr = new int[3][5][4];     // legal
array_ptr = new int[m][5][4];     // legal
array_ptr = new int[3][5][];       // illegal
array_ptr = new int[][5][4];       // illegal
```

The first dimension may be a variable whose value is supplied at runtime. All others must be constants.

Similar to the basic data type objects, the **new** operator can also be used for dynamically creating class objects. The size of the class object is automatically determined and the memory space is allocated accordingly. The general form of allocating class objects using **new** operator is:

```cpp
class sample
{
    private:
        data-type d1;
        data-type d2;
        .
        .
    public:
        .
        .
};
main()
```

will delete the entire array pointed to by **p**.

Program 3.2 demonstrates the use of new and delete operators for dynamic allocation and deallocation of memory.

# Program 3.2 — Use of new and delete Operators

```cpp
#include <iostream>
#include<conio.h>

using namespace std;

void main()
{

    int *arr;
    int size;

    cout<<"Enter the size of the integer array: ";
    cin>>size;

    cout<<"Creating an array of size "<<size<<"...";
    arr = new int[size];

    cout<<"\nDynamic allocation of memory for array arr is successful.";

    delete arr;
    getch();
}
```

The output of Program 3.2 would be:

Program 3.2 — Use of new and delete Operators

```cpp
#include <iostream>
#include<conio.h>

using namespace std;

void main()
{

    int *arr;
    int size;

    cout<<"Enter the size of the integer array: ";
    cin>>size;

    cout<<"Creating an array of size "<<size<<"...";
    arr = new int[size];

    cout<<"\nDynamic allocation of memory for array arr is successful.";

    delete arr;
    getch();
}
```

The output of Program 3.2 would be:

class sample
{
private:
int data1;
char data2;
public:
void set (int i,char c)
{
data1=i;
data2=c;
}
void display(void)
{
cout<<"Data1 = "<<data1;
cout<<"\nData2 = "<<data2;
}
};
int main()
{
sample *s_ptr;
try
{
s_ptr = new sample;
}
catch (bad_alloc ba)
{
cout<<"Bad Allocation occurred...the program will terminate
now..:";
return 1;
}
s_ptr->set(25,'A');
s_ptr->display();
```

delete s_ptr;
getch();
}
```

The **new** operator offers the following advantages over the function **malloc()**.

+   1. It automatically computes the size of the data object. We need not use the operator **sizeof**.
+   2. It automatically returns the correct pointer type, so that there is no need to use a type cast.
+   3. It is possible to initialize the object while creating the memory space.
+   4. Like any other operator, **new** and **delete** can be overloaded.

## 3.18 Manipulators

Manipulators are operators that are used to format the data display. The most commonly used manipulators are **endl** and **setw**.

The **endl** manipulator, when used in an output statement, causes a linefeed to be inserted. It has the same effect as using the newline character “\n”. For example, the statement

```
....
cout << □m = □ << m << endl
    << □n = □ << n << endl
    << □p = □ << p << endl;
....
....
```

would cause three lines of output, one for each variable. If we assume the values of the variables as 2597, 14, and 175 respectively, the output will appear as follows:

It is important to note that this form is not the ideal output. It should rather appear as under:

```
m = 2597
n = 14
p = 175
```

Here, the numbers are *right-justified*. This form of output is possible only if we can specify a common field width for all the numbers and force them to be printed right-justified. The **setw** manipulator does this job. It is used as follows:

```
cout << setw(5) << sum << endl;
```

The manipulator **setw(5)** specifies a field width 5 for printing the value of the variable *sum*. This value is right-justified within the field as shown below:

We can also write our own manipulators as follows:

```
```cpp
#include <iostream>
ostream & symbol(ostream & output)
{
    return output << "\tRs";
}
```
```

The **symbol** is the new manipulator which represents **Rs**. The identifier **symbol** can be used whenever we need to display the string **Rs**.

## 3.19 Type Cast Operator

C++ permits explicit type conversion of variables or expressions using the type cast operator.

Traditional C casts are augmented in C++ by a function-call notation as a syntactic alternative. The following two versions are equivalent:

```
(type-name) expression // C notation
type-name (expression) // C++ notation
```

Examples:

```
average = sum/(float)i; // C notation
average = sum/float(i); // C++ notation
```

A type-name behaves as if it is a function for converting values to a designated type. The function-call notation usually leads to simplest expressions. However, it can be used only if the type is an identifier. For example,

```
p = int * (q);
```

is illegal. In such cases, we must use C type notation.
