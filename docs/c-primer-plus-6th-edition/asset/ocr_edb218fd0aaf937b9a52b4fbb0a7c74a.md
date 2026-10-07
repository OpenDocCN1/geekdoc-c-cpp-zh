# Chapter 8 Adventures in Functions

How do you establish a default value?You must use the function prototype. Because the compiler looks at the prototype to see how many arguments a function uses, the prototype also has to tell the program to the possibility of default arguments. The method is to assign a value to the argument in the prototype. For example, here's the prototype fitting this description of left():

```
char * left(const char * str, int n = 1);
```

You want the function to return a new string, so its type is char*, or pointer-to-char. You want to leave the original string unaltered, so use the const qualifier for the first argument You want to have a default value of 1, so you assign that to n.A default argument value is an initialization value.Thus, the preceding prototype initializes n to the value 1. If you leave n alone, the value 1, but if you pass an argument, the new value overwrites it.

When you use a function with an argument list, you must add defaults from right to left. That is, you can't provide a default value for a particular argument unless you provide defaults for all the arguments to its right:

```
int harpo(int n, int m = 4, int j = 5);      // VALID
int chico(int n, int m = 6, int j);                   // INVALID
int groucho(int k = 1, int m = 2, int n = 3);         // VALID
```

For example, the harpo() prototype calls with one, two, or three arguments:

```
beeps = harpo(2);                          // same as harpo(2,4,5)
beeps = harpo(1,8);                          // same as harpo(1,8,5)
beeps = harpo(8,7,6);                        // no default arguments used
```

The actual arguments are assigned to the corresponding formal arguments from left to right; you can't skip them. Thus, the following isn't allowed:

```
beeps = harpo(3, .8);                   // invalid, doesn't set m to 4
```

Default arguments aren't a major programming breakthrough; rather, they are a convenience. When you are working with class, you'll find they can reduce the number of constructors, methods, and method overloads you have to define.
Listing 8.9 puts default arguments to use. Note that only the prototype identifies the function. The definition remains the same as it would be without arguments.

# Listing 8.9 left.cpp

```
// left.cpp
#include <iostream>
const int ArSize = 80;
char * left(const char * str, int n = 1);
int main() {
    using namespace std;
    char sample[ArSize];
    cout << "Enter a string:\n";
```