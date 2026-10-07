# Working with Pointers to Functions

function that returns a pointer to type int. (Functions that return pointers are covered in Lesson 19, "Getting More from Functions.") When you declare a pointer to a function, always remember to include a set of parentheses around the pointer name and indirection operator, or you can get into trouble.

# Initializing and Using a Pointer to a Function

A pointer to a function must not only be declared, but also initialized to point to something. That "something" is, of course, a function. There's nothing special about a function that gets pointed to. The only requirement is that its return type and parameter list match the return type and parameter list of the pointer declaration. For example, the following code declares and defines a function and a pointer to that:

```
float square(float x);      // The function prototype.
float (*ptr)(float x);     // The pointer declaration.
float square(float x)      // The function definition.
{
    return x * x;
}
```

Because the function square() and the pointer ptr have the same parameter and return types, you can initialize ptr to point to square as follows:

ptr = square;

You can call the function using the pointer as follows:

answer = ptr(x);

It's simple. For a real example, compile and run Listing 16.1, which declares and initializes a pointer to a function and then calls the function twice, using the function name the first time and the pointer the second time. Both produce the same result.

# Input
LISTING 16.1 ptrfunc.c: Using a Pointer to a Function to Call the Function

```
1: // ptrfunc.c--Demonstration of declaring and using a pointer to a function.
2:
3: #include <stdio.h>
4:
5: // The function prototype.
6:
7: double square(double x);
8:
9: // The pointer declaration.
10:
11: double (*ptr) (double x);
```