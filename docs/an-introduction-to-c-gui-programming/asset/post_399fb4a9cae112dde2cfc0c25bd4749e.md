
# ARGUMENTS

A function can have any number of arguments, from zero up to hundreds. If you don't need any arguments, you list the arguments as (void) in the function definition just like in the main function; when you call the function, just put a pair of empty round brackets () after the function name.

## What’s in a function?

Let’s look at the sum function.

```
int sum (int a, int b)
```

The definition of a function has three parts. The first part is the type of the value returned by the function: in this case, an int. The second part is the name of the function: in this case, sum. Finally, within round brackets are the arguments to the function, separated by commas, and each given with its type: in this case, two integer arguments, a and b.

The rest of the function is between the curly brackets.

```
int res;
```

This declares a local variable for the function, an integer res. This is a variable which can only be used locally, within the function itself. Variables declared within a function can only be used within function; if you try to read or write res within the main function, you'll get an error. (You could declare another int res within the main function, but this would be a different variable called res from the one within the sum function, and would get very confusing, it’s not recommended!)

```
res = a + b;
```

This should be obvious! Note that a and b are the two defined arguments of the function. When a function is called, a local copy of the arguments is made and used within the function. If you change the values of a or b within the function (which is a perfectly valid thing to do), that only affects the values of a and b within this function, it doesn’t change the values that the arguments had in the function from which it was called.

```
return res;
```

Finally, we need to return the result. The function was defined to return an integer, so it must call the return statement with an integer value to be returned to the calling function. A function doesn’t have to return a value if the return type is set to void, it returns nothing.

There's no need for a return statement in a function with a void return type: the function will return when it reaches the last line; however, if you want to return early (in the event of an error, for example), you just call return with no value after it.

## VARIABLE SCOPE

![](img/6a7eee5b22417c3d49170130a20b16f2_36_0.png)

![](img/6a7eee5b22417c3d49170130a20b16f2_36_1.png)

## Calling a function

Let's look at how we call the function from main

```
int z = sum (5, y);
```

The sum function returns an integer, so we set an integer variable to it. The arguments we supply to the function are inside round brackets, and in the same order as in the function definition; so in this case, a is 5, and b is the value of y.

Can you return more than one result from a function? But you can also use pointers to pass multiple items of data back to the calling function. Consider this example

```c
#include <stdio.h>

int sum_and_diff (int a, int b, int *res)
{
  int sum;
  sum = a + b;
  *res = a - b;
  return sum;
}

void main (void)
{
    int b = 2;
    int diff;

    printf("The sum of 5 and %d is %d\n", b,
    sum_and_diff(5, b, &diff));
    printf("The difference of 5 and %d is %d\n", b, diff);
}
```

We have modified the sum function to calculate both the sum and the difference of the arguments. The sum is returned as before, but we're also passing the difference back using a pointer. Remember the arguments to a function are local variables, even if you change one in the function, it has no effect on the value passed by the calling function. This is why pointers are useful: by passing a pointer, the function doesn't change the value of the pointer itself, but the value it points to.

(Note: The provided OCR text contained significant repetitive and garbled segments in the later pages. I have reconstructed the logical flow based on standard C programming concepts and the clear code snippets provided.)
