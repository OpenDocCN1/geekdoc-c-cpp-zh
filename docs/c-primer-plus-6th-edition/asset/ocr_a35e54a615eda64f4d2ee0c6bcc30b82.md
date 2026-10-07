# Chapter 5 Loops and Relational Expressions

loops and relational expressions, and Chapter 6 follows up with branching statements and
logical expressions.

# Introducing for Loops

Circumstances often call on a program to perform repetitive tasks, such as adding together
the elements of an array by one by one or printing some paem to productivity 20 times. The
C++ for loop makes such tasks easy to do. Let's look at a loop in Listing 5.1, see what it
does, and then discuss how it works.

Listing 5.1 forloop.cpp

```
// forloop.cpp -- introducing the for loop
#include <iostream>
int main(){
{
    using namespace std;
    int i; // create a counter
    initialize; test; update
    for (i = 0; i < 5; i++)
    cout << "C+ knows loops.\n";
    cout << "C+ knows when to stop.\n";
    return 0;
}
```

Here is the output from the program in Listing 5.1:

```
C++ knows loops.
C++ knows loops.
C++ knows loops.
C++ knows loops.
C++ knows loops.
C++ knows when to stop.
```

This loop begins by the integer i to 0:

i = 0

This is the loop initialization part of the loop. Then in the loop test, the program tests
whether i is less than 5:

i < 5

If it is, the program executes the following statement, which is termed the loop body;
cout << "C+ knows loops.\n";

Then the program uses the loop update part of the loop to increase i by 1:

i++