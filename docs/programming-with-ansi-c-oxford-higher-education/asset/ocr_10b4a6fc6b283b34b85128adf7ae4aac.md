signature remains the same for all the four functions, except the name of the function. Program 6.8 uses (non-member) function pointers, whereas Program 6.9 uses function objects, which is the focus of this chapter.

# PROGRAM 6.8 Solution using function pointers

```
//UsingFunctionPointer.cpp
#include <iostream>
using namespace std;

int Plus (int TempX, int TempY)
{
cout << "Plus() function is called\n";
return TempX + TempY;
}

int Minus (int TempX, int TempY)
{
cout << "Minus() function is called\n";
return TempX - TempY;
}

int FunctionPointer(int(*FunPtr)(int, int), int Arg1, int Arg2)
{
return FunPtr(Arg1, Arg2);
}

void main()
{
int Arg1 = 20;
int Arg2 = 5;
/* The function itself is passed as an argument in the following statements */
cout << FunctionPointer(Plus, Arg1, Arg2) << "\n";
cout << FunctionPointer(Minus, Arg1, Arg2) << "\n";
}
```

# Output

```
Plus() function is called
25
Minus() function is called
15
```

# How the Program Works

The program is simple enough except for the use of a function pointer in calling the function. Observe the call

cout << FunctionPointer(Plus, Arg1, Arg2) << "\n";

The first argument is the name of a function. Any function can be called here by name and arguments.

# Advantage

The advantage of this mechanism is that we do not need a switch statement and the large number of comparisons in it. The function to be called is the first argument. Such a technique is very handy for those who are writing programs for compilers and have to generate object codes for a number of similar function calls. The header of the function that is called must have the argument consisting of the function pointer.

int FunctionPointer(int(*FunPtr)(int, int), int Arg1,int Arg2)
{