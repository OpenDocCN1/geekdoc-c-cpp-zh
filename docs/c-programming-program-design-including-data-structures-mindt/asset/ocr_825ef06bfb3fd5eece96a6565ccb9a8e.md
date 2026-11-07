After this statement executes, the objects and static members are as shown in Figure 10-14.

![](bbox=[0.182, 0.128, 0.91, 0.274])

FIGURE 10-14  `illusObject1` and `illusObject2` after the statement `illustrate::count++;` executes

The output of the statements:

```
illusObject1.print();
illusObject2.print();
```

is:

```
x = 3, Y = 1, count = 2
x = 5, Y = 1, count = 2
```

Note that the function `print` outputs the same incremented value of `count` for both `illusObject1` and `illusObject2`.

The program in Example 10-13 further illustrates how static members of a class work.

# EXAMPLE 10-13

```
#include <iostream>                                      //Line 1
#include "illustrate.h"                                  //Line 2

using namespace std;                                      //Line 3

int main()                                                //Line 4
{
    illustrate illusObject1(3);                           //Line 6
    illustrate illusObject2(5);                           //Line 7

    illustrate::increment();                              //Line 8
    illustrate::count++;                                  //Line 9
    illusObject1.print();                                 //Line 10
    illusObject2.print();                                 //Line 11

    cout << "Line 12: ***Increment y using "
         << illusObject1 << endl;                         //Line 12
```