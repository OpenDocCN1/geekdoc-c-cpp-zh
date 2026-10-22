```
(*pf)(mis);    // apply ToUpper to mis (syntax 1)
pf = ToLower;
pf(mis);       // apply ToLower to mis (syntax 2)
```

Each approach sounds sensible. Here is the first approach: Because pf points to the ToUpper function, *pf is the ToUpper function, so the expression (*pf)(mis) is the same as ToUpper(mis). Just look at the declarations of ToUpper and of pf to see that ToUpper and (*pf) are equivalent. Here is the second approach: Because the name of a function is a pointer, you can use a pointer and a function name interchangeably, hence pf(mis) is the same as ToLower(mis). Just look at the assignment statement for pf to see that pf and ToLower are equivalent. Historically, the developers of C and Unix at Bell Labs took the first view and the extenders of Unix at Berkeley took the second view. K&R C did not allow the second form, but to maintain compatibility with existing code, ANSI C accepted both forms ((*pf)(mis) and pf(mis)) as equivalent. Subsequent standards have continued with this lofty ambivalence.

Just as one of the most common uses of a data pointer is an argument to a function, one of the most common uses of a function pointer is an argument to a function. For example, consider this function prototype:

```
void show(void (* fp)(char *), char * str);
```

It looks messy, but it declares two parameters, fp and str. The fp parameter is a function pointer, and the str is a data pointer. More specifically, fp points to a function that takes a char * parameter and has a void return type, and str points to a char. So, given the declarations we had earlier, you can make function calls such as the following:

```
show(ToLower, mis);  /* show() uses ToLower() function: fp = ToLower  */
show(pf, mis);       /* show() uses function pointed to by pf: fp = pf */
```

And how does show() use the function pointer passed to it? It uses either the fp() or the (*fp)() syntax to invoke the function:

```
void show(void (* fp)(char *), char * str)
{
    (*fp)(str); /* apply chosen function to str */
    puts(str);  /* display result               */
}
```

Here, for example, show() first transforms the string str by applying to it the function pointed to by fp, and then it displays the transformed string.

By the way, functions with return values can be used two different ways as arguments to other functions. For example, consider the following:

```
function1(sqrt);      /* passes address of sqrt function     */
function2(sqrt(4.0)); /* passes return value of sqrt function */
```