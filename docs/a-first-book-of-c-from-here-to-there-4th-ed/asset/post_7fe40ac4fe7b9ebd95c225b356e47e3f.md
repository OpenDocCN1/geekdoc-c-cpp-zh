
## 16. (Program)

- a. The following is a useful programming algorithm for rounding a real number to *n* decimal places:

  - Step 1: Multiply the number by 10ⁿ.
  - Step 2: Add 0.5.
  - Step 3: Delete the fractional part of the result.
  - Step 4: Divide by 10ⁿ.

  For example, using this algorithm to round the number 78.374625 to three decimal places yields:

  - Step 1: 78.374625 × 10³ = 78374.625
  - Step 2: 78374.625 + 0.5 = 78375.125
  - Step 3: Retaining the integer part = 78375
  - Step 4: 78375 divided by 10³ = 78.375

  Using this algorithm, write a C++ function that accepts a user-entered value and returns the result rounded to two decimal places.

- b. Include the function written in Exercise 16a in a working program. Make sure your function is called from main() and returns a value to main() correctly. Have main() use a cout statement to display the returned value. Test the function by passing various data to it and verifying the returned value.

## 6.3 Returning Multiple Values

In a typical function invocation, the called function receives values from its calling function, stores and manipulates the passed values, and directly returns at most one value. When data is passed in this manner, it’s referred to as a pass by value.

Calling a function and passing arguments by value is a distinct advantage of C++. It allows functions to be written as independent entities that can use any variable or parameter name without concern that other functions might be using the same name. It also alleviates any concern that altering a parameter or variable in one function could inadvertently alter a parameter or variable’s value in another function. In this approach, parameters can be considered initialized variables, or variables assigned values when the function is executed. At no time, however, does the called function have direct access to any variable defined in the calling function, even if the variable is used as an argument in the function call.

At times, however, you need to modify this approach by giving a called function direct access to its calling function’s variables. This approach allows one function—the called function—to use and change the value of variables that have been defined in the calling function. Doing so requires passing the variable’s address to the called function. After the called function has the variable’s address, it “knows where the variable lives,” so to speak, and can access and change the value stored there.

Passing addresses is referred to as a function pass by reference¹³ because the called function can reference, or access, the variable whose address has been passed. C++ provides two types of address parameters: references and pointers. The next section describes the method that uses reference parameters.

### Passing and Using Reference Parameters

As always, when exchanging data between two functions, you must be concerned with both the sending and receiving sides. From the sending side, calling a function and passing an address as an argument that’s accepted as a reference parameter on the receiving side is the same as calling a function and passing a value; the called function is summoned into action by giving its name and a list of arguments. For example, the statement newval(firstnum, secnum); calls the function named newval() and passes two arguments to it. Whether a value or an address is actually passed depends on the parameter types declared for newval(). Now take a look at writing the newval() function and prototype so that it receives the addresses rather than the values of the variables firstnum and secnum, which are assumed to be double-precision variables.

One of the first requirements in writing the newval() is to declare two reference parameters for accepting passed addresses. In C++, a reference parameter is declared with this syntax:

```
dataType& referenceName
```

For example, the reference declaration

```
double& num1;
```

declares that num1 is a reference parameter used to store the address of a double. Similarly, `int& secnum;` declares that secnum is a reference to an integer, and `char& key;` declares that key is a reference to a character.

The ampersand, &, in C++ means "the address of." Additionally, when & is used in a declaration, it refers to "the address of" the preceding data type. Using this information, declarations such as double& num1 and int& secnum are sometimes more clearly understood if they’re read backward. Reading the declaration double& num1 in this manner yields the information "num1 is the address of a double-precision value." (This topic is discussed in more detail in Section 8.1.)

Because you need to accept two addresses in the parameter list for newval(), the declarations double& num1 and double& num2 can be used. Including these declarations in the parameter list for newval(), and assuming the function returns no value (void), the function header for newval() becomes the following:

```
void newval(double& num1, double& num2)
```

For this function header, the following is a suitable function prototype:

```
void newval(double&, double&);
```

This prototype and function header are included in Program 6.8, which uses a newval() function body that displays and alters the values stored in these reference variables from within the called function.

### Program 6.8

```cpp
#include <iostream>
using namespace std;

void newval(double&, double&);  // prototype with two reference parameters

int main()
{
    double firstnum, secnum;

    cout << "Enter two numbers: ";
    cin >> firstnum >> secnum;
    cout << "\nThe value in firstnum is: " << firstnum << endl;
    cout << "The value in secnum is: " << secnum << "\n\n";

    newval(firstnum, secnum);    // call the function

    cout << "The value in firstnum is now: " << firstnum << endl;
    cout << "The value in secnum is now: " << secnum << endl;

    return 0;
}

void newval(double& xnum, double& ynum)
{
    cout << "The value in xnum is: " << xnum << endl;
    cout << "The value in ynum is: " << ynum << "\n\n";
    xnum = 89.5;
    ynum = 99.5;

    return;
}
```

In calling the newval() function in Program 6.8, you need to understand the connection between the arguments used in the function call, firstnum and secnum, and the parameters used in the function header, xnum and ynum. Both refer to the same data items. The significance is that the values in the arguments (firstnum and secnum) can now be altered from within newval() by using the parameter names (xnum and ynum). Therefore, the parameters xnum and ynum don't store copies of the values in firstnum and secnum; instead, they access the locations in memory set aside for these two arguments.

Figure 6.7 shows the equivalence of argument names in Program 6.8, which is the essence of a pass by reference. The argument names and their matching parameter names are simply different names referring to the same memory storage areas. In main(), these memory locations are referenced by the argument names firstnum and secnum, and in newval(), the same locations are referenced by the parameter names xnum and ynum.

![](img/e9bf940282dfb289356f077151cc69dd_279_0.png)

### Figure 6.7 The equivalence of arguments and parameters in Program 6.8

The following is a sample run of Program 6.8:

```
Enter two numbers: 22.5 33.0

The value in firstnum is: 22.5
The value in secnum is: 33

The value in xnum is: 22.5
The value in ynum is: 33
The value in firstnum is now: 89.5
The value in secnum is now: 99.5
```

In reviewing this output, notice that the values initially displayed for the parameters xnum and ynum are the same as those displayed for the arguments firstnum and secnum. Because xnum and ynum are reference parameters, however, newval() now has direct access to the arguments firstnum and secnum. Therefore, any change to xnum in newval() alters the value of firstnum in main(), and any change to ynum changes secnum's value. As the final displayed values show, the assignment of values to xnum and ynum in newval() is reflected in main() as the altering of firstnum's and secnum's values.

The equivalence between actual calling arguments and function parameters shown in Program 6.8 provides the basis for returning multiple values from within a function. For example, say you want to write a function to accept three values, compute these values' sum
