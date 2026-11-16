```
a=6;
}
```

In this program, output will be 5, instead of the fact that we have changed the value of a to 6, in display1() function. This is called the function call by value. Here, one copy of the value of a is passed to display1() function. So, the value in the main() function remains unchanged because the value stored at the original address has not been changed rather the copy of value in the display1() function has been changed and this change will survive until and unless the function display1() function returns the handle to main().

If the above said is true then if we try to access the memory location of num in the following program, it should give two different values, which can be viewed easily.

![](bbox=[0.12, 0.3, 0.94, 0.57])

# Call by reference using pointers

When we call the function by reference either by using pointer or by using address, then the address of the variables are passed to the function. So, whatever the change we make in the function, the same changes occur at original memory location of the local variable.

Consider the following program:

```
#include<iostream>
using namespace std;
int display1(int*);
int main()
{
    int a=5;
    cout<<a;
```