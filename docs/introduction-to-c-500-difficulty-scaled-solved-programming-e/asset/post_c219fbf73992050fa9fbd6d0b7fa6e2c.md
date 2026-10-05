
# 8 • Pointers 207

```cpp
void make_rand(void (*ptr)(int, int), int num)
{
    int i, cnt;

    cnt = 0;
    while (1) {
        i = rand();
        cnt++;
        if (i >= 1000 && i <= 2000) {
            (*ptr)(cnt, i);
            return;
        }
    }
}
```

```cpp
void handle_event(int evt, int num)
{
    std::cout << "Times:" << evt << " Num:" << num << '\n';
}
```

At first, the main program (e.g., part A) calls make_rand(e.g., evt, part B), which takes parameter a pointer to a function which accepts two integer parameters and returns nothing. Notice that we write the name of handle_event(). When the name of a function is not followed by parentheses, the compiler uses a pointer to this function; it is careful not to call the function. To make sure you understand the difference, here is an example with two functions a and b:

```cpp
a(b); // The address of b is passed to a.
a(b()); // b is first called, then the return value of b is passed to a.
```

make_rand() generates random integers, once an integer within [1000, 2000] is generated, it uses the pointer to callback handle_event() and passes as arguments how many numbers were generated and the number in the specified interval. This example has no practical value; I just wanted to show you an implementation example of the callback mechanism. Also, the use of a function as argument can make your function to work in a generic way. Here is an example:

```cpp
#include <iostream> // Example 8.26
#include <vector>
using std::cout;
using std::vector;

int find_val(const vector<int>& v, int num, (*op)(int a, int b));
int max_val(int a, int b);
int min_val(int a, int b);

int main() {
    vector<int> vec(3, 8, 12, -5);

    cout << "Max:" << find_val(vec, max_val) << '\n';
    cout << "Min:" << find_val(vec, min_val) << '\n';
    return 0;
}
```

# 208 Introduction to C++

```cpp
int find_val(const vector<int>& v, int (*op)(int a, int b))
{
    int i, res;

    res = v[0];
    for(i = 1; i < v.size(); i++)
    {
        if(op(v[i], res))
            res = v[i];
    }
    return res;
}
```

```cpp
int max_val(int a, int b)
{
    return a > b;
}
```

```cpp
int min_val(int a, int b)
{
    return a < b;
}
```

In each call of find_val() the address of the respective function is passed and op points to that address. The program outputs the maximum and minimum value of the vector elements, that is, 12 and -5. As you see, find_val() works in a generic way, in the sense that the same function supports both operations. The function can be more generic and work for different types of data (i.e., not only for int), as you'll see when you learn about generic programming and function templates in Chapter 16. Instead of passing a function pointer we can pass a function object or a lambda expression, as we'll see in Chapter 26.

# ARRAY OF POINTERS TO FUNCTIONS

An array of pointers to functions is nothing more than an array whose elements are function pointers. Notice that all functions will have the same prototype. For example, the statement:

```cpp
void (*ptr[20])(int a);
```

declares an array of 20 elements, where each element is a pointer to a function that takes an integer parameter and returns nothing. In the following program, each element of the array ptr is a pointer to a function, which takes two parameters and returns an integer.

```cpp
#include <iostream> // Example 8.27

int f1(int a, int b);
int f2(int a, int b);
int f3(int a, int b);

int main()
{
    int (*ptr[3])(int a, int b);
    int i, j, k;
```

# 8 Pointers 209

```cpp
ptr[0] = f1; // ptr[0] points to the address of f1.
ptr[1] = f2;
ptr[2] = f3;

std::cout << "Enter numbers: ";
std::cin >> i >> j;

if(i > 0 && i < 10) {
    k = ptr[0](i, j); // Call the function that ptr[0] points to.
    We could also write k = (*ptr[0])(i, j);
} else if (i >= 10 && i < 20) {
    k = ptr[1](i, j); // Call the function that ptr[1] points to.
} else {
    k = ptr[2](i, j); // Call the function that ptr[2] points to.
}
return 0;
}

int f1(int a, int b) {
    return a + b;
}

int f2(int a, int b) {
    return a - b;
}

int f3(int a, int b) {
    return a * b;
}
```

The program reads two integers, checks the first one, and uses a function pointer to call the respective function. The program displays the return value. An array of pointers can be initialized when declared, like an ordinary array. For example, we could use:

```cpp
int (*ptr[3])(int a, int b) = {f1, f2, f3};
```

Suppose that the user enters the values 20 and 10. What does the following statement output?

```cpp
cout << ptr[0](ptr[1](i, j), ptr[2](i, j));
```

The expression ptr[1](i, j) calls f2(), which returns 10. Similarly, the expression ptr[2](i, j) calls f3(), which returns 200. Therefore, the expression is translated to ptr[0](10, 200), which displays the return value of f1(), which is 21. When using an array of pointers, we usually prefer to use the pointer name to call the function because it is easier to write and read the statement than to write: (*ptr[0])((*ptr[1](i, j)), (*ptr[2](i, j))).

And I know that you are curious, I'll show you an implementation where an array of pointers to functions can improve the program's performance. This example is coming from my experience in the implementation of Finite State Machines (FSMs) for network protocols. To give you an idea, an FSM is a mathematical concept using states and events to describe the operation of the protocol. For example, when an event occurs (e.g., data reception from the network), the program checks the state of the protocol, the event code, and calls the proper function to process that event. There are several ways to implement FSM; using the switch statement is one of them. For example:

```cpp
const int STATE_1 = 0;
const int STATE_2 = 1;
...
```

```cpp
const int EVT_1 = 0;
const int EVT_2 = 1;
...
```

```cpp
void evt_received(int evt_code)
{
    switch(state)
    {
        case STATE_1:
            switch(evt_code)
            {
                case EVT_1:
                    Handle_ST1_Evt1();
                    break;
                case EVT_2:
                    Handle_ST1_Evt2();
                    break;
                ..
                case EVT_N:
                    Handle_ST1_EvtN();
                    break;
                default:
                    std::cout << "Error: unexpected event " <<
                    evt_code << " received at state " << '\n';
                    break;
            }
        case STATE_2:
            switch(evt_code)
            {
                case EVT_1:
                    Handle_ST2_Evt1();
                    break;
                case EVT_2:
                    Handle_ST2_Evt2();
                    break;
                ..
                case EVT_N:
                    Handle_ST2_EvtN();
                    break;
            default:
                std::cout << "Error: unexpected event " <<
                evt_code << " received at state " << state << '\n';
                break;
    }
...
default:
    std::cout << "Time to panic: invalid state\n";
    break;
}
```

Alternatively, we can declare a two-dimensional array of pointers and use the pointers to call the event handlers. For example, if each function does not take parameters and returns the integer value. Then, we could declare an array of pointers like this:

```cpp
typedef void (*Func_Ptr)(); /* As we'll see in Chapter 2, we use typedef to create a synonym. */
Func_Ptr ptr[MAX_STATES][MAX_EVENTS] = {Handle_ST1_Evt1, Handle_ST1_Evt2,
Handle_ST1_EvtN, Handle_ST2_Evt1, ...};
```

See how the following code demonstrates:

```cpp
void evt_received(int evt_code)
{
    func_ptr[state][evt_code]();
}
```

Not only the code becomes simpler and easier to read, it is more flexible as well. With the array of pointers, we can easily remove a function (e.g., set the pointer to nullptr) or add new event handler function, if needed. And the most important, we gain in speed, since the proper function is directly called avoiding the time overhead of the switch statements.

I have good news and bad news. The good news is that a really tough chapter finished, at last. Close this book and get some rest, but the bad news is that the next chapter is bigger and even harder. Don't be scared, just kidding!

# UNSOLVED EXERCISES

U.8.1 Write a program that uses two pointer variables to read two double numbers and display the absolute value of their sum.

U.8.2 What is the output of the following program?

```cpp
#include <iostream>
int main()
{
    int *ptr, i = 10, j = 20, k = 30;

    ptr = &i;
    *ptr = 40;
```
