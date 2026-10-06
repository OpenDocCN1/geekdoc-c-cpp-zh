```
*res = a - b;
return sum;
}
```

```
void main (void)
{
    int b = 2;
    int diff;

```

```
printf("The sum of 5 and %d is %d\n", b,
sum_and_diff(5, b, &diff));
printf("The difference of 5 and %d is %d\n", b, diff);

```

We have modified the sum function to calculate both the sum and the difference of the arguments. The sum is returned as before, but we're also passing the difference back using a pointer. Remember the arguments to a function are local variables, even if you change one in the function, it has no effect on the value passed by the calling function. This is why pointers are useful: by passing a pointer, the function doesn't change the value of the pointer itself, but it can change the value in the variable to which it's pointing.

So we call the function with the two arguments as before, but we add a third one. a pointer to the variable where we want to write the difference calculated by the function. In the function, we have this line:

```
*res = a - b;
```

The difference is written to the variable to which res is a pointer.
In the main function, we call the sum_and_diff function like:

```
sum_and_diff(5, b, &diff)
```

We provide the address of the integer diff as the pointer argument to the sum_and_diff function; when the difference is calculated, it's written into the variable diff in the main function.

# RETURNING VALUES

A function can return a single value, or no value at all. If you define the function as returning void, there's no need to use a return statement in it, but you'll get an error if you don't include a return of the correct type in a non void function.