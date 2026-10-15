
Retrieving single results via the function’s name was shown in Section 2.2 to be readily accomplished by a return statement specifying the value to be returned. Python takes this further by generalizing the mechanism and enabling the retrieval of several pieces of data through the function’s name. For illustration, we provide a classical example program in Listing 2.7, in which the function Swap is supposed to interchange the values of two variables. The parameters x and y acquire their initial values as copies of the arguments a and b, which are passed by value. At the same time, by virtue of the return statement, x and y become references to the elements in the list on the left-hand side of the call to Swap (in this particular case, still a and b), which receive the changed values by reference.

Thus, the process involves both the pass-by-value and pass-by-reference mechanisms and actually separates the arguments into two lists: the input list (on the right side), whose arguments are passed by value, and the output list (on the left side), whose arguments are passed by reference. This becomes particularly obvious if the interchanged values are returned to a different pair of arguments:

```
(c,d) = Swap(a,b)
```

Indeed, while, upon return from Swap, c and d receive by reference the interchanged input values, a and b remain unchanged, since they are passed by value.

The fact that the input and output lists are functionally disjoint is also clarified by the simplified version of the function Swap shown below, in which the parameters create an inverted correspondence between the input and output arguments.

```
def Swap(x, y):
    return (y, x)    # scalar arguments passed by value
                     # return interchanged values
```

An important point to make is that in Python, due to the characteristic dynamic typing, the same function can operate with arguments of different types, which actually determine the types of the corresponding parameters. In particular, the function Swap can equally well interchange numeric values or strings, so that the arguments in Program 2.7 might, as well, have been strings:

```
a = "1st"; b = "2nd"
```

Let us now replace the pair of arguments to be interchanged with the elements of a list, as in Program 2.8. Being a compound data type, the list alist is passed by default by reference. The function actually operates by means of its local alias xlist directly upon alist itself. Correspondingly, the mechanism of returning data via the function’s name is no longer applied and, therefore, a return statement becomes unnecessary.

## Listing 2.8 Returning Interchanged List Components from a Function (Python Coding)

```
# Returning swapped list elements from a function

def Swap(xlist):
    temp = xlist[0]; xlist[0] = xlist[1]; xlist[1] = temp    # list passed by reference

# main

alist = [1e0, 2e0]    # list of values to be swapped
Swap(alist)
print(alist)
```

## 2.4 Passing Arguments to C/C++ Functions

Retrieving a single result from a function via the function’s name was illustrated in Section 2.2. Unlike Python, in C/C++, this mechanism cannot be directly generalized for arbitrary data sets. The only way of returning data sets in compliance with modular programming, that is, through the parameter list, involves explicit or disguised use of *pointers*.

Pointers are particular types of variables, which are specialized in storing *memory addresses* (Kernighan and Ritchie 1988). As an immediate application, pointers can be used to reference variables by their addresses, rather than by their names, thus providing external aliases to variables and enabling the retrieval of data from functions via their parameters.

The address of an object in the memory (e.g., a variable or an array element) can be retrieved by applying the *address operator* `&`. Accordingly, the statement

```
p = &x;
```

assigns the address of the variable x to the pointer p, and p is said to *point to x* (see Figure 2.1). The address operator cannot be applied to constants or expressions.

To access the object a pointer points to, one applies the *indirection operator* `*`. Concretely, if p contains the address of the variable x, then *p precisely represents the *value* of x.

The declaration of pointers is similar to that of usual variables, `type *name`, specifying, notably, not the type of the pointer itself, but rather the type of the indirected pointer, or, in other words, of the variables the pointer is defined to point to. Hence, the declaration

```
double *p;
```

defines a pointer specialized in pointing to variables (locations) of type double. The type of variables pointed to is essential both in indirecting the pointer and in performing arithmetic operations therewith.

Incrementing a pointer, for example p++, yields the address of the next memory location of the type the pointer points to. Similarly, decrementing a pointer, p--, results in the address of the previous location. Incrementing, instead, the *variable* pointed to by pointer p is obtained by ++(*p).

Two of the major uses of pointers in scientific programming concern the mechanism of returning values from functions via their parameter lists (discussed in the following paragraph) and the dynamic memory allocation for arrays (discussed in the next section).

Since the only mechanism implemented in ANSI C for passing arguments to functions is the pass-by-value mechanism, called functions cannot directly modify variables defined in the calling function, thereby returning results. In other words, the transmission of data invariably occurs from the caller to the called function. Nevertheless, the use of pointers enables an indirect implementation of the pass-by-reference mechanism. The basic idea is to pass (again by value) the *addresses* of the locations where the calling function expects the called function to save the results, so as to “find” and use them subsequently. Obviously, to hold addresses of memory locations, the output parameters of the called function have to be pointers.

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_37_0.png)

**FIGURE 2.1** Pointers contain the addresses of the memory locations they point to.

## Listing 2.9 Function Returning Modified Argument Values (C Coding)

```
// Returning swapped arguments from a function (C syntax)
#include <stdio.h>

void Swap(double *x, double *y)            // formal arguments are pointers
{
    double temp;                          // temporary variable

    temp = *x; *x = *y; *y = temp;  // variable values accessed by indirection
}

int main()
{
    double a, b;

    a = 1e0; b = 2e0;                      // values to be swapped
    Swap(&a,&b);                          // actual arguments are addresses
    printf("%f %f\n",a,b);
}
```

For illustration of the described pass-by-reference mechanism, we refer again to the example of swapping variables, implemented in Python in Section 2.3. The ANSI C version shown in Listing 2.9 defines a function Swap for interchanging values of type double (similar to the swap function for integers defined in Kernighan and Ritchie 1988). As explained above, the main program does not pass to Swap the values of the arguments a and b, but rather their addresses, &a and &b, so that Swap can directly operate on the original locations. Correspondingly, to be able to receive the addresses of the operands, the parameters of Swap have to be declared pointers. Swap operates with the actual values of the arguments a and b from the main program by indirecting the pointers x and y, which contain their addresses.

Aside from returning results by the function’s name, the method based on pointer-type parameters represents the main technique for retrieving results from functions in the spirit of modular programming.

Not changing the essence of the standard mechanism based on pointers, C++ significantly simplifies the syntax related to the pass-by-reference mechanism, improving the readability of the code (see

## Listing 2.10 Function Returning Modified Argument Values (C++ Coding)

```
// Returning swapped arguments from a function (C++ syntax)
#include <stdio.h>

void Swap(double &x, double &y)            // arguments passed by reference
{
    double temp;                          // temporary variable

    temp = x; x = y; y = temp;
}

void main()
{
    double a, b;

    a = 1e0; b = 2e0;                      // values to be swapped
    Swap(a,b);
    printf("%f %f\n",a,b);
}
```
