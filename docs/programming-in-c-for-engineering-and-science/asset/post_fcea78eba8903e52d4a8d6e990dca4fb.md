
# 10.6.3.1 Parameters for Types

Here, the better way is to recognize that the only differences in any of these definitions are the three places where a type is specified. It would be nice if we could define the function and leave these types “blank” as in our earlier pattern and somehow pass the type to the function when we call it. Then we could replace all of these definitions with one.

This is effectively what C++ allows us to do, as shown in Example 10.9.

## Example 10.9 The swap() Template

```
/* This header file provides a template that generates functions
   for interchanging the values of two variables.
   ... remaining opening documentation omitted ...
---------------------------------------------------------------*/

template<typename Item>
inline void swap(Item & first, Item & second)
{
    Item temporary = first;
    first = second;
    second = temporary;
}
```

Rather than specify that the function is to exchange two values of a particular type such as char, int, and so on, this definition uses the identifier Item as a placeholder for the type of the value to be exchanged. More precisely, the line informs the compiler of two things:

- 1. This definition is a template: a pattern from which the compiler can create a function.
- 2. The identifier Item is the name of a type parameter for this definition that will be given a value when the function is called.

The rest of the definition simply specifies the behavior of the function, using the type parameter Item in place of any specific type.

Using this version of the swap library, we can now write

```
#include "swap.h"
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int i1 = 11,
        i2 = 22;
```

5 C++ also allows the keyword class to be used to specify a type parameter.

```
swap(i1, i2);
cout << i1 << ' ' << i2 << endl;

double d1 = 33.3,
d2 = 44.4;
swap(d1, d2);
cout << d1 << ' ' << d2 << endl;

string s1 = "Hi",
s2 = "Ho";
swap(s1, s2);
cout << s1 << ' ' << s2 << endl;
}
```

When the compiler encounters the first call to swap(),

```
swap(i1, i2);
```

in which the two arguments i1 and i2 are of type int, it uses the pattern given by our template to generate a new definition of swap() in which the type parameter Item is replaced by int:

```
inline void swap(int & first, int & second)
{
    int temporary = first;
    first = second;
    second = temporary;
}
```

When it reaches the second call,

```
swap(d1, d2);
```

where the two arguments d1 and d2 are of type double, the compiler will use the same pattern to generate a second definition of swap() in which the type parameter Item is replaced by double:

```
inline void swap(double & first, double & second)
{
    double temporary = first;
    first = second;
    second = temporary;
}
```

When the compiler reaches the final call,

```
swap(s1, s2);
```

in which the two arguments s1 and s2 are of type string, it will use the same pattern to generate a third definition of swap() in which the type parameter Item is replaced by string:

```
inline void swap(string & first, string & second)
{
    string temporary = first;
    first = second;
    second = temporary;
}
```

We are spared from all of the redundant coding of the earlier approach because the compiler is providing multiple versions of the swap operation as they are needed.

## 10.6.3.2 Templates vs. Overloading

If there are several versions of the same operation to be encoded as functions, it may not be clear whether one should write several functions that overload the same name or write one function template. The following guideline helps with making this decision:

If each version of the operation behaves in exactly the same way,

regardless of the type of data being used,

then define a function template to perform the operation.

Otherwise, define a separate function for each operation

and use overloading to give them the same name.

Thus, because each version of swap() uses the three-way swap and behaves in exactly the same manner regardless of the type of values being interchanged, a function template is appropriate.

By contrast, the two summation functions we considered earlier use different formulas, and thus behave differently. These operations are therefore best performed by two separate functions that overload the name sum().

The reasoning behind this guideline should be clear. When the compiler creates a function definition from a template, it blindly replaces each occurrence of the type parameter with the type of the arguments. As a result, each definition created from a template must behave in exactly the same way, except for the type of data being operated upon. Overloading has no such restriction and so can be used for a wider variety of operations.

# CHAPTER SUMMARY

## Key Terms

- alias
- anchor
- argument
- base case
- call by reference
- call by value
- code bloat
- const reference parameter
- hole in the scope
- inductive step
- inline specifier
- namespace
- overload
- parameter
- parameter-passing mechanism
- recursion
- recursive definition of a function
- reference parameter
- scope
- signature
- template
- type parameter
- using directive
- value parameter

## NOTES

- By default, parameters are value parameters; their values are *copies* of the corresponding arguments. Thus, changing the value of a value parameter has no effect on the value of the corresponding argument.
- Reference parameters are aliases for their corresponding arguments; they refer to the same memory locations. Thus, changing the value of a reference parameter also changes the value of the corresponding argument, which must be a variable. To specify that a parameter is a reference parameter, insert an ampersand (&) between its type and its name in the function heading.
- A `const` reference parameter, specified by inserting the keyword `const` before a reference parameter’s type, is a preferred alternative to a value parameter whose type is a class (or that is some other large object) because it does not require copying the value of the corresponding argument.
- Use a `return` statement to send back a single value from a function; use reference parameters to send back multiple values.
- An identifier’s scope is the portion of a program where the object or function that it names can be accessed. Basic scope rules for an identifier are:
  - *Declared in a block*: from declaration to end of block
  - *Parameter*: body of the function
  - *In initialization of for loop*: from declaration to end of loop body
  - *Declared outside all blocks*: from declaration to end of file
- A `using` clause makes names in a namespace available without qualification.
- A recursive function must have an anchor that will eventually be executed and cause a return from the function and an inductive step that specifies the current action of the function in terms of previously defined actions.
- A simple function can be inlined to avoid the overhead of calling that function and thereby reduce execution time. Prepend the keyword `inline` to the function heading to do this.
- The signature of a function is the list of its parameter types. A function may overload another function (i.e., have the same name) provided they have different signatures.
- Preceding the prototype and the definition of a function with a template clause of the form `template<typename T>` converts the function into a function template, which is a type-independent pattern for a function. When the function is called, the compiler will use the type of the arguments to determine what type to substitute for `T` and generate a type-specific function.

## Style and Design Tips

- *Functions should be documented in the same way that programs are. The documentation should include specifications and descriptions of:*
  - The purpose of the function
  - Any items that must be received by the function from its caller
  - Any items that must be input to the function
  - Any items that are returned or passed back by the function to its caller
  - Any items that are output by the function
- *Follow the same stylistic standards for functions that are used for main programs.*
- *Declaring variable objects as close as possible to their first use increases the readability of a program and also aids with debugging.*
- *Value parameters receive copies of the corresponding arguments and are used for simple/small arguments. For arguments such as classes (and arrays studied in the next chapter) that are stored in large amounts of memory, use const reference parameters.*
- *Use a `return` statement to return a single value from a function; use reference parameters when several values are to be returned.*
- *All variables used within a function should be defined within that function, either as parameters or as local variables. This keeps functions self-contained and increases their generality and reusability.*
- *Recursive functions should be clearly marked as such. For clarity and readability, the anchor case and inductive steps of a recursive function should be marked with comments.*
- *Only simple functions should be specified as being inline functions. Substitution of an inline function's body for each of its calls can increase a program's size considerably if the function is nontrivial and/or it is called at several places in the program.*
