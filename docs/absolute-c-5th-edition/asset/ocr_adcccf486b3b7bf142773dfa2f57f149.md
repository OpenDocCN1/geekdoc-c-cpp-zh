# CHAPTER 10 Pointers and Dynamic Arrays

# Display 10.4 A Call-by-Value Pointer Parameter

```
//Program to demonstrate the way call-by-value parameters
//behave with pointer arguments.
#include <iostream>
using namespace std;

typef int* IntPointer;

void sneaky(IntPointer);

int main ()
{
    IntPointer p;
    p = new int;
    *p = 77;
    cout << "Before call to function *p == "
         << *p << endl;

sneaky(p);

return 0;
}
void sneaky(IntPointer temp)
{
    *temp = 99;
    cout << "Inside function call *temp == "
         << *temp << endl;
}
```

Sample Dialogue
Before call to function *p == 77
Inside function call *temp == 99
After call to function *p == 99

# Uses for Pointers

Chapter 17 discusses ways to use pointers to create a number of useful data structures. This chapter only discusses one of pointers, namely, to reference arrays, and in particular to create and reference a kind of array known as a dynamically allocated array. Dynamically allocated arrays are the topic of Section 10.2.