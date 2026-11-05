*Note: As stated in §11.7.6, outside an instance constructor or static constructor for a struct or class that defines a readonly field, that field is considered a value, not a variable. As such, its address cannot be taken. Similarly, the address of a constant cannot be taken.*

The & operator does not require its argument to be definitely assigned, but following an & operation, the variable to which the operator is applied is considered definitely assigned in the execution path in which the operation occurs. It is the responsibility of the programmer to ensure that correct initialization of the variable actually does take place in this situation.

*Example:* In the following code

```
```
using System;

class Test
{
    static void Main()
    {
        int i;
        unsafe
        {
            int* p = &i;
            *p = 123;
        }
        Console.WriteLine(i);
    }
}
```
```

i is considered definitely assigned following the &i operation used to initialize p. The assignment to *p in effect initializes i, but the inclusion of this initialization is the responsibility of the programmer, and no compile-time error would occur if the assignment was removed.

*end example*

*Note: The rules of definite assignment for the & operator exist such that redundant initialization of local variables can be avoided. For example, many external APIs take a pointer to a structure which is filled in by the API. Calls to such APIs typically pass the address of a local struct variable, and without the rule, redundant initialization of the struct variable would be required. end note*

*Note: When a local variable, value parameter, or parameter array is captured by an anonymous function (§11.7.21), that local variable, parameter, or parameter array is no longer considered to be a fixed variable (§22.7), but is instead considered to be a movable variable. Thus it is an error for any unsafe code to take the address of a local variable, value parameter, or parameter array that has been captured by an anonymous function. end note*

# ### 22.6.6 Pointer increment and decrement

In an unsafe context, the ++ and -- operators (§11.7.14 and §11.8.6) can be applied to pointer variables of all types except void*. Thus, for every pointer type T*, the following operators are implicitly defined:

```
```
T* operator ++(T* x);
T* operator --(T* x);
```
```

The operators produce the same results as x+1 and x-1, respectively (§22.6.7). In other words, for a pointer variable of type T*, the ++ operator adds sizeof(T) to the address contained in the variable, and the -- operator subtracts sizeof(T) from the address contained in the variable.