# 10.8. PASS BY REFERENCE

r = y;

Does not bind r to the y variable. The declaration of r binds r to the x variable for the life of r. This statement simply assigns y's value to x via the reference r. In contrast, we may freely bind pointer variables to any variables we choose at any time.

A reference variable, therefore, in the examples provided here works like pointer that may be bound to a variable and may not be redirected to point anywhere else. Also, unlike pointers, nullptr may not be assigned to a reference variable. There are some other differences between references and pointers that we will not explore. Reference variables provide a simpler syntax than pointers that we do not need to use the pointer dereferencing operator (*) when working with references.

There is one other major difference between pointers and references—C++ adopted pointers as is in the C programming language, but C does not have references. C++ programmers often use library functions written in C, so it is important not to mix references with C code.

Section 10.8 reveals a very important practical application of pointers and references in their role of enabling pass by reference.

# 10.8 Pass by Reference

The default technique for passing parameters to functions is pass by value (see Section 9.3). C++ also supports pass by reference, also known as call by reference, which allows functions to alter the values of formal parameters passed by callers.

Consider Listing 10.16 (faultyswap.cpp), which uses a function that attempts to interchange the values of its integer parameters.

Listing 10.16: faultyswap.cpp
#include <iostream>

using namespace std;

/*
* swap(a, b)
* Attempts to interchange the values of
* its parameters a and b. That it does, but
* unfortunately it affects the local
* copies.
*/
void swap(int a, int b) {
int temp = a;
a = b;
b = temp;
}

/*
* main
* Attempts to interchange the values of
* two variables using a faulty swap function.
*/
int main() {