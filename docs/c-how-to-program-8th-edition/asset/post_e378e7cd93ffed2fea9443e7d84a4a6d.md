
```text
Enter the side length of your cube: 3.5
Volume of cube with side 3.5 is 42.875
```

**Fig. 6.18** | *inline function that calculates the volume of a cube. (Part 2 of 2.)*

## 6.14 References and Reference Parameters

Two ways to pass arguments to functions in many programming languages are **pass-by-value** and **pass-by-reference**. When an argument is passed by value, a copy of the argument’s value is made and passed (on the function call stack) to the called function. Changes to the copy do **not** affect the original variable’s value in the caller. This prevents the accidental side effects that so greatly hinder the development of correct and reliable software systems. Each argument in this chapter has been passed by value.

![](img/bfd978e7e9b192bab46ec2a89e481263_260_0.png)

> **Performance Tip 6.4**
>
> *One disadvantage of pass-by-value is that, if a large data item is being passed, copying that data can take a considerable amount of execution time and memory space.*

### Reference Parameters

This section introduces **reference parameters**—the first of the two means C++ provides for performing pass-by-reference. With pass-by-reference, the caller gives the called function the ability to access the caller’s data directly, and to modify that data.

![](img/bfd978e7e9b192bab46ec2a89e481263_260_1.png)

> **Performance Tip 6.5**
>
> *Pass-by-reference is good for performance reasons, because it can eliminate the pass-by-value overhead of copying large amounts of data.*

![](img/bfd978e7e9b192bab46ec2a89e481263_260_2.png)

> **Software Engineering Observation 6.1**
>
> *Pass-by-reference can weaken security; the called function can corrupt the caller’s data.*

Later, we’ll show how to achieve the performance advantage of pass-by-reference while simultaneously achieving the software engineering advantage of protecting the caller’s data from corruption.

A reference parameter is an alias for its corresponding argument in a function call. To indicate that a function parameter is passed by reference, simply follow the parameter’s type in the function prototype by an ampersand (&); use the same convention when listing the parameter’s type in the function header. For example, the following declaration in a function header

```cpp
int &count
```

when read from *right to left* is pronounced “count is a reference to an int.” In the function call, simply name the variable by name to pass it by reference. Then, mentioning the variable by its parameter name in the body of the called function actually refers to the original variable in the calling function, and the original variable can be modified directly by the called function. As always, the function prototype and header must agree.

### Passing Arguments by Value and by Reference

Figure 6.19 compares pass-by-value and pass-by-reference with reference parameters. The “styles” of the arguments in the calls to function squareByValue and function squareByReference are identical—both variables are simply mentioned by name in the function calls. Without checking the function prototypes or function definitions, it isn’t possible to tell from the calls alone whether either function can modify its arguments. Because function prototypes are mandatory, the compiler has no trouble resolving the ambiguity.

> **Common Programming Error 6.9**
>
> *Because reference parameters are mentioned only by name in the body of the called function, you might inadvertently treat reference parameters as pass-by-value parameters. This can cause unexpected side effects if the original variables are changed by the function.*

![](img/bfd978e7e9b192bab46ec2a89e481263_261_0.png)

```cpp
// Fig. 6.19: fig06_19.cpp
// Comparing pass-by-value and pass-by-reference with references.
#include <iostream>
using namespace std;

int squareByValue( int ); // function prototype (value pass)
void squareByReference( int & ); // function prototype (reference pass)

int main()
{
   int x = 2; // value to square using squareByValue
   int z = 4; // value to square using squareByReference

   // demonstrate squareByValue
   cout << "x = " << x << " before squareByValue\n";
   cout << "Value returned by squareByValue: "
        << squareByValue( x ) << endl;
   cout << "x = " << x << " after squareByValue\n" << endl;

   // demonstrate squareByReference
   cout << "z = " << z << " before squareByReference" << endl;
   squareByReference( z );
   cout << "z = " << z << " after squareByReference" << endl;
} // end main

// squareByValue multiplies number by itself, stores the
// result in number and returns the new value of number
int squareByValue( int number )
{
   return number *= number; // caller's argument not modified
} // end function squareByValue

// squareByReference multiplies numberRef by itself and stores the result
// in the variable to which numberRef refers in function main
void squareByReference( int &numberRef )
{
   numberRef *= numberRef; // caller's argument modified
} // end function squareByReference
```

**Fig. 6.19** | Passing arguments by value and by reference. (Part 1 of 2.)

```text
x = 2 before squareByValue
Value returned by squareByValue: 4
x = 2 after squareByValue

z = 4 before squareByReference
z = 16 after squareByReference
```

**Fig. 6.19** | Passing arguments by value and by reference. (Part 2 of 2.)

Chapter 8 discusses pointers; pointers enable an alternate form of pass-by-reference in which the style of the call clearly indicates pass-by-reference (and the potential for modifying the caller’s arguments).

![](img/bfd978e7e9b192bab46ec2a89e481263_262_0.png)

> **Performance Tip 6.6**
>
> *For passing large objects, use a constant reference parameter to simulate the appearance and security of pass-by-value and avoid the overhead of passing a copy of the large object.*

To specify a reference to a constant, place the `const` qualifier before the type specifier in the parameter declaration. Note the placement of `&` in function `squareByReference`’s parameter list (line 35, Fig. 6.19). Some C++ programmers prefer to write the equivalent form `int& numberRef`.

### References as Aliases within a Function

References can also be used as aliases for other variables within a function (although they typically are used with functions as shown in Fig. 6.19). For example, the code

```cpp
int count = 1; // declare integer variable count
int &cRef = count; // create cRef as an alias for count
++cRef; // increment count (using its alias cRef)
```

increments variable count by using its alias cRef. Reference variables must be initialized in their declarations (see Fig. 6.20 and Fig. 6.21) and cannot be reassigned as aliases to other variables. Once a reference is declared as an alias for another variable, all operations supposedly performed on the alias (i.e., the reference) are actually performed on the original variable. The alias is simply another name for the original variable. Unless it’s a reference to a constant, a reference argument must be an lvalue (e.g., a variable name), not a constant or expression that returns an rvalue (e.g., the result of a calculation). See Section 5.9 for definitions of the terms lvalue and rvalue.

```cpp
// Fig. 6.20: fig06_20.cpp
// Initializing and using a reference.
#include <iostream>
using namespace std;

int main()
{
   int x = 3;
   int &y = x; // y refers to (is an alias for) x

   cout << "x = " << x << endl << "y = " << y << endl;
   y = 7; // actually modifies x
   cout << "x = " << x << endl << "y = " << y << endl;
} // end main
```

**Fig. 6.20** | Initializing and using a reference. (Part 1 of 2.)

```text
x = 3
y = 3
x = 7
y = 7
```

**Fig. 6.20** | Initializing and using a reference. (Part 2 of 2.)

```cpp
// Fig. 6.21: fig06_21.cpp
// References must be initialized.
#include <iostream>
using namespace std;

int main()
{
   int x = 3;
   int &y; // Error: y must be initialized

   cout << "x = " << x << endl << "y = " << y << endl;
   y = 7;
   cout << "x = " << x << endl << "y = " << y << endl;
} // end main
```

*Microsoft Visual C++ compiler error message:*

```text
C:\cpphtp8_examples\ch06\Fig06_21\fig06_21.cpp(9) : error C2530: 'y' :
   references must be initialized
```

*GNU C++ compiler error message:*

```text
fig06_21.cpp:9: error: 'y' declared as a reference but not initialized
```

**Fig. 6.21** | Uninitialized reference causes a syntax error.

### Returning a Reference from a Function

Functions can return references, but this can be dangerous. When returning a reference to a variable declared in the called function, unless that variable is declared static, the reference refers to an automatic variable that’s discarded when the function terminates. Such a variable is said to be “undefined,” and the program’s behavior is unpredictable. References to undefined variables are called **dangling references**.

> **Common Programming Error 6.10**
>
> *Returning a reference to an automatic variable in a called function is a logic error. Some compilers issue a warning when this occurs.*
