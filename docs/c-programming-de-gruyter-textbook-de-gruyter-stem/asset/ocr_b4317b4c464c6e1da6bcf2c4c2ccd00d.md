# 6.2.6 Using Pointers to Process Array Elements

The addition and subtraction characteristics of pointers make them especially suitable for processing the same type of data that is stored in a continuous memory space. An array is a set of same-type variables that have some ordinal relation; array elements are stored continuously physically; the array name is the starting address of the array. We can use pointers to do convenient and quick operations on arrays and array elements. For example,

```
int array[5];
```

declares a one-dimensional array that stores five int-type elements. The array name is the starting address of the array (the address of its first element). That is, array is the same as &array[0]. Five integers in the array are stored orderly, so we can access array elements by using the array name and some arithmetic operations. The array element whose address is i (*array+i). For example, *array is array[0], and *(array+3) is array[3].

**Example 6.7:** Suppose there is an array a of the int type, which has 10 elements. Use three methods to output all the elements.

Program 1: Using array name and subscripts

```
//6_7_1.cpp
#include <iostream>
using namespace std;
int main() {
    int a[10]={1,2,3,4,5,6,7,8,9,0};
    int i;
    for(i=0; i<10; i++)
        cout<<a[i]<<" ";
    cout<<endl;
}
```

Program 2: Using array name and pointer operations

```
//6_7_2.cpp
#include <iostream>
using namespace std;
int main() {
    int a[10]={1,2,3,4,5,6,7,8,9,0};
    int i;
    for(i=0; i<10; i++)
        cout<<*(a+i)<<" ";
```