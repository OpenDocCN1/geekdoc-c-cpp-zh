
The *function call stack* (sometimes referred to as the *program execution stack*)—working “behind the scenes”—supports the function call/return mechanism. It also supports the creation, maintenance and destruction of each called function’s automatic variables. As we’ll see in Figs. 6.13–6.15, this LIFO behavior is exactly what a function does when returning to the function that called it.

As each function is called, it may, in turn, call other functions, which may, in turn, call other functions—all before any of the functions returns. Each function eventually must return control to the one that called it. So, somehow, we must keep track of the return addresses that each function needs to return control to its caller. The function call stack is the perfect data structure for handling this information. Each time a function is called, an entry is pushed onto the stack. This entry, called a *stack frame* or an *activation record*, contains the return address that the called function needs to return to the calling function. When the called function returns, the stack frame for the function call is popped, and control transfers to the return address in the popped stack frame.

The beauty of the call stack is that each called function always finds the information it needs to return to its caller at the top of the call stack. And, if a function makes a call to another function, a stack frame for the new function call is simply pushed onto the call stack. Thus, the return address required by the newly called function to return to its caller is now located at the top of the stack.

The stack frames have another important responsibility. Most functions have automatic variables—parameters and any local variables the function declares. Automatic variables need to exist while a function is executing. They need to remain active if the function makes calls to other functions. But when a called function returns to its caller, the called function’s automatic variables need to “go away.” The called function’s stack frame is a perfect place to store the function’s automatic variables. That stack frame exists as long as the called function is active. When that function returns—and no longer needs its local automatic variables—its stack frame is popped from the stack, and those local automatic variables are no longer known to the program.

Of course, the amount of memory in a computer is finite, so only a certain amount of memory can be used to store activation records on the function call stack. If more function calls occur than can have their activation records stored on the function call stack, an error known as *stack overflow* occurs.

## *Function Call Stack in Action*

So, as we’ve seen, the call stack and activation records support the function call/return mechanism and the creation and destruction of automatic variables. Now let’s consider how the call stack supports the operation of a square function called by main (lines 11–17 of Fig. 6.12). First the operating system calls main—this pushes an activation record onto the stack (shown in Fig. 6.13). The activation record tells main how to return to the

```
1  // Fig. 6.12: fig06_12.cpp
2  // square function used to demonstrate the function
3  // call stack and activation records.
4  #include <iostream>
```

Fig. 6.12 | square function used to demonstrate the function call stack and activation records. (Part 1 of 2.)

```
using std::cin;
using std::cout;
using std::endl;

int square( int ); // prototype for function square

int main()
{
    int a = 10; // value to square (local automatic variable in main)
    cout << a << " squared: " << square( a ) << endl; // display a squared
    return 0; // indicate successful termination
} // end main

// returns the square of an integer
int square( int x ) // x is a local variable
{
    return x * x; // calculate square and return result
} // end function square
```

10 squared: 100

Fig. 6.12 | square function used to demonstrate the function call stack and activation records. (Part 2 of 2.)

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_237_0.png)

Fig. 6.13 | Function call stack after the operating system invokes main.

operating system (i.e., transfer to return address R1) and contains the space for main’s automatic variable (i.e., a, which is initialized to 10).

Function main—before returning to the operating system—now calls function square in line 15 of Fig. 6.12. This causes a stack frame for square (lines 20–23) to be pushed onto the function call stack (Fig. 6.14). This stack frame contains the return address that square needs to return to main (i.e., R2) and the memory for square’s automatic variable (i.e., x).

After square calculates the square of its argument, the function needs to return to main—and no longer needs the memory for its automatic variable x. So the stack is popped—giving square the return location in main (i.e., R2) and losing square’s automatic variable. Figure 6.15 shows the function call stack after square’s activation record has been popped.

Function main now displays the result of calling square (line 15), then executes the return statement (line 16). This causes the activation record for main to be popped from the stack. This gives main the address it needs to return to the operating system (i.e., R1 in Fig. 6.13) and causes the memory for main’s automatic variable (i.e., a) to become unavailable.

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_238_0.png)

Fig. 6.14 | Function call stack after main invokes function square to perform the calculation.

Fig. 6.15 | Function call stack after function square returns to main.

## 6.12 Functions with Empty Parameter Lists

In C++, an empty parameter list is specified by writing either void or nothing at all in parentheses. The prototype

```
void print();
```

specifies that function print does not take arguments and does not return a value. Figure 6.16 demonstrates both ways to declare and use functions with empty parameter lists.

```
1  // Fig. 6.16: fig06_16.cpp
2  // Functions that take no arguments.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  void function1(); // function that takes no arguments
8  void function2( void ); // function that takes no arguments
```

Fig. 6.16 | Functions that take no arguments. (Part 1 of 2.)

```
9
10 int main()
11 {
12     function1(); // call function1 with no arguments
13     function2(); // call function2 with no arguments
14     return 0; // indicates successful termination
15 } // end main
16
17 // function1 uses an empty parameter list to specify that
18 // the function receives no arguments
19 void function1()
20 {
21     cout << "function1 takes no arguments" << endl;
22 } // end function1
23
24 // function2 uses a void parameter list to specify that
25 // the function receives no arguments
26 void function2( void )
27 {
28     cout << "function2 also takes no arguments" << endl;
29 } // end function2
```

```
function1 takes no arguments
function2 also takes no arguments
```

Fig. 6.16 | Functions that take no arguments. (Part 2 of 2.)

### Portability Tip 6.2

> The meaning of an empty function parameter list in C++ is dramatically different than in C. In C, it means all argument checking is disabled (i.e., the function call can pass any arguments it wants). In C++, it means that the function explicitly takes no arguments. Thus, C programs using this feature might cause compilation errors when compiled in C++.

### Common Programming Error 6.13

> C++ programs do not compile unless function prototypes are provided for every function or each function is defined before it is called.

## 6.13 Inline Functions

Implementing a program as a set of functions is good from a software engineering standpoint, but function calls involve execution-time overhead. C++ provides inline functions to help reduce function call overhead—especially for small functions. Placing the qualifier inline before a function’s return type in the function definition “advises” the compiler to generate a copy of the function’s code in place (when appropriate) to avoid a function call. The trade-off is that multiple copies of the function code are inserted in the program (often making the program larger) rather than there being a single copy of the function to which control is passed each time the function is called. The compiler can ignore the inline qualifier and typically does so for all but the smallest functions.
