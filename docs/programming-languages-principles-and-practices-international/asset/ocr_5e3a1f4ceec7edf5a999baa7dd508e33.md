defining block via references to nonlocal variables. It has no way of directly accessing the variables in its calling environment. In the sample C code, procedure B cannot directly access the local variable x of procedure A. Nevertheless, it may need the value of x in A to perform its computations.

The method of communication of a procedure with its calling environment is through parameters. A parameter list is declared along with the definition of the procedure, as in the max procedure of the previous section:

```
int max (int x, int y){
  return x > y ? x : y;
}
```

Here, x and y are parameters to the max function. They do not take on any value until max is called, when they are replaced by the arguments from the calling environment, as in:

```
z = max(a+b,10);
```

In this call to max, the parameter x is replaced by the argument a + b, and the parameter y is replaced by the argument 10. To emphasize the fact that parameters have no value until they are replaced by arguments, parameters are sometimes called formal parameters, while arguments are called actual parameters.

A strong case can be made that procedures should communicate with the rest of the program using only the parameters—that is, a procedure or function should never use or change a nonlocal variable. After all, such use or change represents a dependency (in the case of a use) or a side effect (in the case of a change) that is invisible from a reading of the procedure specification—it can only be determined from examining the body of the procedure (which could be very long, or even missing in the case of a library procedure). While this rule is generally a good one with regard to variables (e.g., a global variable should still be a parameter if it is changed), it is too much to expect with regard to functions and constants. In general, the body of a procedure will need to call other procedures in the program and library procedures, and may also need to use constants (such as PI). These are all nonlocal references, but we would not want to clutter up the parameter list with all such references (particularly since they are all essentially constants). Thus, nonlocal uses cannot be avoided.

Nevertheless, some procedures may depend only on parameters and fixed language features. These are said to be in closed form, since they contain no nonlocal dependencies. An example is the max function above, which has no dependencies on nonlocal definitions—it depends entirely on fixed language features and its parameters.

On the other hand, a polymorphic definition of the same function in C++ (using templates):

```
template <typename T>
T max (T x, T y)
{ return x > y ? x : y ; }
```

is not in closed form, since the “>” operator can be overloaded for non-built-in types. Thus, to write this function in closed form, we would have to include the “>” operation in the parameter list:

```
template <typename T>
T max (T x, T y, bool (*gt)(T,T))
{ return gt(x,y) ? x : y ; }
```

(These examples were discussed in detail in Section 8.9.)