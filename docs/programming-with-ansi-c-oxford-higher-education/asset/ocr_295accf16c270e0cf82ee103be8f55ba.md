One just passes variables as parameters while using reference variables and receives them in reference variables.

the function as pointers, the code in the first version is far better and easier to understand. This is the advantage of reference variables.

In the function SwapInt(), FirstVariable and SecondVariable are passed to the function and are accepted as int& First and int& Second. Henceforth, First is a reference to FirstVariable and Second is a reference to SecondVariable. As they are reference variables, whatever manipulation is done to First and Second will be reflected in FirstVariable and SecondVariable, respectively, in the main program. Thus, the function using reference variables achieves the same effect as that using pointers, but in a simpler way. This makes the function code more readable.

Passing a non-pointer argument in C++ does not guarantee passing the value as in C and thus the value returning from the function may be altered. One will have to check the prototype of the function to be sure.

However, a problem arises while using reference variables as function dummy parameters, as in the example shown. Suppose the Swap() function is a library function; then its definition will not be directly visible. Passing these two variables as value parameters is safe in C. It is known that the function called cannot change the values of the variables inadvertently or maliciously. In order to get the values changed, the addresses of these variables have to be passed. However, in C++, in order to ensure that the values of the variables are not changed, the prototype of the function has to be checked. This is because whether one passes value or reference parameters, the calling function is the same, that is, variables, and not addresses of variables, are being passed in both the cases.

# 2.5.3 Reference Variables as Return Types

Consider Program 2.4.

# PROGRAM 2.4 Return a reference variable

```
//ReturnRef.cpp
#include <iostream>
using namespace std;

void main()
{
    int FirstInt = 10, SecondInt = 20;
    int ThirdInt, FourthInt = 100;
    int& RetRefTest(int, int);
    ThirdInt = RetRefTest(FirstInt, SecondInt);

    // The following is a special use of returning as reference
    RetRefTest(FirstInt, SecondInt) = FourthInt;
    int& RetRefTest(int i, int j)
    {
        return(i>j?i:j);
    }
}
```

# How the Program Works

It is very easy to understand this code except the line following the comment. The line preceding the comment is the normal way of calling a function in C, where a variable is passed from a function as a return value. This value is accepted in the left-hand side (LHS)