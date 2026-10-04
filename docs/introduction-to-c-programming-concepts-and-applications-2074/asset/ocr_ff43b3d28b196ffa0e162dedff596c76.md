# // USING REFERENCES

References allow you to share information without making needless copies.

A reference is a way of describing a particular variable. Normally, when you define a variable, it gets its own box of memory. If you do something to that box of memory, such as assign a value to it, it's not going to affect any other box.

The same thing b is to a (8). This means that b is going to refer to the exact same box of memory as a. When you print out the values of a and b, both show up as 1.

With a reference, though, you don't create a new box of memory for your variable. Instead, you use an alias that refers to that memory. Basically, your variable becomes another name for some box of memory that already exists; anything you do to that new variable must affect the original memory;

You can assign a new value, 2, to a (10). When you do so, the value changes in that box of memory. When you print out both a and b now, both show up as 2.

The way you specify a reference is by putting an ampersand (&) after the type when you declare it. Then you initialize your new variable to refer to some other variable.

The same thing happens if you assign a new value, 3, to b (12). The box of memory b refers to has its value changed to 3. Printing out the values of a and b indicates both have the value 3.

```
// Program 13_7
// Reference example
#include <iostream>
using namespace std;
int main() {
    int a = 1;
    int &b = a;
    cout << a << " " " << b << endl;
    a = 3;
    cout << a << " " " << b << endl;
}
```

First, create a variable, a, that you initialize to a value of 1 (7).

Next, create a variable, b, that is a reference to an integer. So, you must make this reference to something; you can't just leave it there,

The most common way references are used is calling functions. That's you can declare any of the parameters in a function to be a reference. This means that the parameter will not be a copy of the argument that comes in; it'll be a reference to the argument so the reference parameter will be like changing the original.

The term used to describe this is passing by reference. This is distinguished from what you previously did, which is when you pass by value, you're copying the value of the argument into the new box of memory set up for the parameter. When you pass by reference, you don't copy anything; you just let the parameter refer back to a shared variable of input.

Lecture 13 | Expanding Your Functions Can Do in C++