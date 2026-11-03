This tells the compiler that the formal argument that receives the array is a pointer, not array variable. Pointer parameters are commonly employed in string functions. Consider the function copy which copies one string to another.

```
copy(char *s1, char *s2)
{
    while( (*s1++ = *s2++) != '\0' )
        ;
}
```

This copies the contents of s2 into the string s1. Parameters s1 and s2 are the pointers to character strings, whose initial values are passed from the calling function. For example, the calling statement

```
copy(name1, name2);
```

will assign the address of the first element of name1 to s1 and the address of the first element of name2 to s2.

Note that the value of *s2++ is the character that s2 pointed to before s2 was incremented. Due to the postfix ++, s2 is incremented only after the current value has been fetched. Similarly, s1 is incremented only after the assignment has been completed.

Each character, after it has been copied, is compared with '\0' and therefore copying is terminated as soon as the '\0' is copied.

# 6.14 FUNCTIONS RETURNING POINTERS

We have seen so far that a function can return a single value by its name or return multiple values through pointer parameters. Since pointers are a data type in C, we can also force a function to return a pointer to the calling function. Consider the following code:

```
int *larger (int *, int *);  /* prototype */
main ()
{
    int a = 10;
    int b = 20;
    int *p;
    p = larger(&a, &b);  /*function call */
    printf ("%d", *p);
}
int *larger (int *x, int *y)
{
    if (*x>*y)
        return (x);  /* address of a */
    else
        return (y);  /* address of b */
}
```

The function larger receives the addresses of the variables a and b, decides which one is larger using the pointers x and y and then returns the address of its location. The returned value is then assigned to the pointer variable p in the calling function. In this case, the address of b is returned and assigned to p and therefore the output will be the value of b, namely, 20. Note that the address returned must be the address of a variable in the calling function. It is an error to return a pointer to a local variable in the called function.