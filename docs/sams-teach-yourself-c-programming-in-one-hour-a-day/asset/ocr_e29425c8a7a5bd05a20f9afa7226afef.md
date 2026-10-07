4. When using a void pointer, what is meant by a typecast, and when must you use it?

5. Can you write a function that takes a variable argument list only, with no fixed arguments?

6. What macros should be used when you write functions with variable argument lists?

7. What value is added to a void pointer when it's incremented?

8. Can a function return a pointer?

9. What macro is used to retrieve values from a variable list of arguments passed to a function?

10. What are the elements that need to be used when using variable argument lists?

# Exercises

+   1. Write the prototype for a function that returns an integer. It should take a pointer to a character array as its argument.

+   2. Write a prototype for a function called numbers that takes three integer arguments. The integers should be passed by reference.

+   3. Show how you would call the numbers function in exercise 2 with the three integers int1, int2, and int3.

+   4. BUG BURSTER: Is anything wrong with the following?

```
void squared(void *nbr)
{
  *nbr *= *nbr;
}
```

+   5. BUG BURSTER: Is anything wrong with the following?

```
float total(int num, ...)
{
  int count, total = 0;
  for (int count = 0; count < num; count++)
  total += va_arg(arg_ptr, int);
  return ( total );
}
```

Because of the many possible solutions, answers are not provided for the following exercises.