Suppose you have a savings account balance and you'd like to increase the balance by some percentage to account for earning interest.

You can create a function named increase_percentage that will take 2 parameters:
the value that you want to increase and the percentage to increase by. The key thing here is that you are going to modify the balance so that the first parameter will be a reference, not just a basic parameter. So, you will write float& value for the first parameter.

So, when the function is called, with arguments savings_balance and 10, the first argument, savings_balance, is passed by reference. In the function's memory, the parameter value just refers to the exact same block of memory as savings_balance from the main function. The second argument, 10, is passed by value, so a new box of memory named percentage is created in the function's memory area, and 10 is copied into there.

Thus, when you modify the variable named value in the function, you're actually modifying the same box of memory as savings_balance in the main function. After the function returns, you'll find that the value in savings_balance has in fact been changed.

Passing by reference makes it possible to modify a value. It also has the advantage of not having to go through the process of copying the variable.

Copying is not a big deal in most cases, but if the variable is something really large, such as an entire video file, you don't want to take the computational time and memory of going through and copying it.

The ability to not have to copy information needlessly is an advantage, so why wouldn't you always do that? Why wouldn't you always just pass by reference?

There are 2 main reasons:

+   1 One is if you know you want to modify the parameter in your function but don't want it affected back in the main program. You'd like the function to be as disconnected from where it was called as possible, so you don't want to needlessly tie things together that shouldn't be tied. Passing by value is the right solution when you want your function to be as much of a black box as possible, because you need to make a copy of that data regardless.

+   2 The other reason for passing by value is a little subtler: If you pass by reference, then the argument that you call with needs to be a variable. It can't be a literal—because there's no box of memory to refer to. If you try to pass in a string literal, you will get a compiler error.

```
// Program 13_8
// Passing by Reference
#include<iostream>
using namespace std;

void increase_percentage(float& value, float percentage) {
    value += value * (percentage / 100.0);
}

int main() {
    float savings_balance = 1000.0;
    cout << savings_balance << endl;
    increase_percentage(savings_balance, 10);
    cout << savings_balance << endl;
}
```

# Exercise

Suppose you have a really long string and want to do a search-and-replace for some word in the string, finding every occurrence of that word and replacing it with a different word. Can you come up with a header for a function that will modify the string in that way? (Don't worry about the body of the function.)

Click here to see the solution.