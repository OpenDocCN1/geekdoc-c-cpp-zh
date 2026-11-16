
- Except in case 4, the initial array elements are undefined. Once an IntArray object has been created, its size cannot be changed, and each object should use just enough storage to hold its elements, plus a fixed amount of space for bookkeeping information.

- Elements of an IntArray are accessed using the standard C style array indexing notation. If the index falls outside the legal range, an error message should be printed, and the program should simulate a halt.

- IntArray objects may be assigned to each other if they have the same number of elements. The indices need not match, and the indices of the target object will not change; only the elements will be copied. If the sizes of objects being assigned don't match, an error message should be printed, and the program should simulate a halt.

- Two IntArray objects can be compared using the == and != operators. If the arrays have the same number of elements and each of the corresponding elements match, the objects are equal and the comparison operator (==) should return a non-zero value, even if their indices are different. Comparing IntArray objects with different number of elements is legal, and the result is always zero. The != operator should return zero whenever == would return non-zero, and vice versa.

- Class IntArray should also overload the operators below. An error should be generated if the arrays are of a different size.

| Operator | Description |
|---|---|
| [] | - allows index range checking |
| + | - allows the sum of two arrays to be assigned to a third array |
| += | - allows the sum of two arrays to be assigned to the first array |
| << | - allows the contents of an array to be output |

- The IntArray class should have high() and low() member functions that return the maximum and minimum legal index for a given array as defined by the driver (user).

- The `IntArray` class should also contain a private data member that will hold the name of the `IntArray` object when instantiated. This data member should be initialized with a call to a `setName()` member function.

I will supply a driver program, `iadrv.cpp`, that demonstrates the use of the `IntArray` class. The driver will demonstrate all operation and error condition features separately. Each test will note what feature is being demonstrated and output each array name, index, and corresponding element using the overloaded `<<` operator.

Note that for each array test data, the driver will simply multiply the array index by 10 immediately after each array is initialized or modified and output its contents. When your program encounters a run-time error, you should "simulate" a halt with appropriate diagnostics rather than actually halting the program. Be sure that all error messages sent to the terminal window are also sent to the `csis.txt` output file.

When elements of an array are output, the array name should be output, a left bracket, an index value, a right bracket, an equal sign, and finally a value. For example:

```
a[3] = 30
```

Note that the driver program outputs array elements vertically down the page. This behavior should not be changed. Be sure that you include a destructor for the `IntArray` class. The driver program will include the following tests:

- 1. Test array declared with single integer:

```
IntArray a(10);
```

- 2. Test array declared with two integers, one of which is negative:

```
IntArray b(-3, 6);
```

- 3. Test array declared with two non-negative integers:

```
IntArray c(6, 8);
```

- 4. Test array declared with two identical integers:

```
IntArray d(5, 5);
```

- 5. Test array declared with no integers:

```
IntArray z;
```

- 6. Test array declared with another object of type IntArray:

```
IntArray c(6, 8);
IntArray e(c);
```

- 7. Test array assigned to another array with different indices:

```
IntArray f(1, 4);
IntArray g(5, 8);
f = g;
```

- 8. Test multiple array assignment with different indices:

```
IntArray j(3, 6);
IntArray k(6, 9);
IntArray l(1, 4);
j = k = l;
```

- 9. Test overloaded equality operator (identical elements):

```
IntArray m(3, 7);
IntArray n(1, 5);
m == n
```

- 10. Test overloaded equality operator (different elements):

```
IntArray o(3, 7);
IntArray p(1, 5);
o == p
```

- 11. Test overloaded equality operator (different size arrays):

```
IntArray q(1, 3);
IntArray r(1, 4);
q == r
```

- 12. Test overloaded inequality operator (identical elements):

```
IntArray s(3, 7);
IntArray t(1, 5);
s != t;
```

- 13. Test overloaded inequality operator (different elements):

```
IntArray u(3, 7);
IntArray v(1, 5);
u != v
```

- 14. Test overloaded inequality operator (different size arrays):

```
IntArray w(1, 3);
IntArray x(1, 4);
w != x
```

- 15. Test sum of two arrays assigned to third array (note that corresponding array elements get added to each other and assigned to the corresponding element in the third array):

```
IntArray a(1, 5);
IntArray b(4, 8);
IntArray c = a+b;
```

Note that IntArray c should take on the indices of the invoking IntArray object, in this case a.

- 16. Test sum of two arrays assigned to first array (note that corresponding array elements get added to each other and assigned to the corresponding element in the first array):

```
IntArray d(10, 13);
IntArray e(30, 33);
d += e;
```

- 17. Test array declared with illegal array bounds:

```
IntArray f(5, 2);
```

- 18. Test array for index out of range:

```
IntArray g(10);
num = g[10];
```

- 19. Test arrays for length mismatch:

```
IntArray m(1, 4);
IntArray n(3, 7);
m = n;
```

- 20. Test array subscript operator as an lvalue and rvalue:

```
IntArray o(7, 8);
o[7] = 25;
o[8] = o[7];
```

```
// iadrv.h

#ifndef _IADRV_H
#define _IADRV_H

#include "intarray.h"

int main();
void test1();
void test2();
void test3();
void test4();
void test5();
void test6();
void test7();
void test8();
void test9();
void test10();
void test11();
void test12();
void test13();
void test14();
void test15();
void test16();
void test17();
void test18();
void test19();
void test20();
void wait();

#endif
```

```
// iadrv.cpp - driver program for testing IntArray class

#include <iostream>
#include <iomanip>
#include <fstream>
#include <stdlib.h>
#include "iadrv.h"

using namespace std;

ofstream csis;

int main()
{
    csis.open("csis.txt");
    test1();
    test2();
    test3();
    test4();
    test5();
    test6();
    test7();
    test8();
    test9();
    test10();
    test11();
    test12();
    test13();
    test14();
    test15();
    test16();
    test17();
    test18();
    test19();
    test20();
    csis.close();
}
```

```
void test1() {
    cout << "*. Array declared with single integer: IntArray a(10);" << endl << endl;
    csis << "*. Array declared with single integer: IntArray a(10);" << endl << endl;
    IntArray a(10);
    for(int i = a.low(); i <= a.high(); i++)
        a[i] = i * 10;
    a.set_name("a");
    cout << a << endl;
    csis << a << endl;
    wait();
}
```

```
void test2() {
    cout << "*. Array declared with two integers: IntArray b(-3, 6);" << endl << endl;
    csis << "*. Array declared with two integers: IntArray b(-3, 6);" << endl << endl;
    IntArray b(-3, 6);
    for(int i = b.low(); i <= b.high(); i++)
        b[i] = i * 10;
    b.set_name("b");
    cout << b << endl;
    csis << b << endl;
    wait();
}
```

```
void test3() {
    cout << "*. Array declared with two integers: IntArray c(6, 8);" << endl << endl;
    csis << "*. Array declared with two integers: IntArray c(6, 8);" << endl << endl;
    IntArray c(6, 8);
    for(int i = c.low(); i <= c.high(); i++)
        c[i] = i * 10;
    c.set_name("c");
    cout << c << endl;
    csis << c << endl;
    wait();
}
```

```
void test4() {
    cout << "*. Array declared with two identical integers: IntArray d(5, 5);" << endl << endl;
    csis << "*. Array declared with two identical integers: IntArray d(5, 5);" << endl << endl;
    IntArray d(5, 5);
    for(int i = d.low(); i <= d.high(); i++)
        d[i] = i * 10;
    d.set_name("d");
    cout << d << endl;
    csis << d << endl;
    wait();
}
```
