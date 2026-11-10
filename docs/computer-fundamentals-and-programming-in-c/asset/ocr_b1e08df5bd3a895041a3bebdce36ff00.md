and arrays. This discussion is also applicable to strings as strings are arrays of characters. Consider the following program that uses a pointer to shift to the next character of the string.

```
14. #include <stdio.h>
int main()
{
    char a[15] = "test string";
    char *pa;
    pa = a;
    while(*pa)
    {
        putchar(*pa);
        pa++;
    }
    printf("\n");
    return 0;
}
```

# Output

test string

The while loop is equivalent to `while(*pa!='\\0')`. More aspects of pointers and strings are illustrated here by studying versions of some useful functions adapted from the standard library `string.h`. The first function is `strcpy(t,s)`, which copies the string `s` to the string `t`. It would be nice just to write `s = t` but this copies the pointer, not the characters. To copy the characters, a loop is needed. The array version is as follows.

```
15. #include <stdio.h>
int main()
{
    char a[50], b[50];
    void scopy(char *, char *);
    printf("\n Enter the string: ");
    gets(a);
    scopy(b,a);
    printf("\n %s",b);
    return 0;
}
```

```
/* scopy: copy s to t; array subscript version */
void scopy(char *t, char *s)
{
    int i;
    i = 0;
    while(s[i] != '\\0')
    {
        t[i] = s[i];
        i++;
    }
    t[i] = '\\0';
}
```

An equivalent version of `scopy()` is given as follows.

```
void scopy(char *t, char *s)
{
    int i;
    i = 0;
    while((t[i] = s[i]) != '\\0')
        i++;
}
```

For contrast, here is a version of `scopy()` with pointers.

```
/* scopy: copy s to t; pointer version */
void scopy(char *t, char *s)
{
    int i;
    i = 0;
    while((*t = *s) != '\\0')
    {
        s++;
        t++;
    }
}
```

Because arguments are passed by value, `scopy` can use the parameters `b` and `a`. Here they are conveniently initialized pointers, marching along the arrays one character at a time, until the `\\0` that terminates `s` has been copied into `t`. Experienced C programmers would prefer the following version.

```
/* scopy: copy s to t; pointer version 2 */
void scopy(char *s, char *t)
{
    while((*t++ = *s++) != '\\0')
        ;
}
```

This moves the increment of `s` and `t` into the test part of the loop. The value of `*s++` is the character that `s` pointed to before it was incremented; the postfix `++` does not change `s` until after this character has been fetched. In the same way, the character is stored into the old `t` position before `t` is incremented. This character is also the value that is compared against `\\0` to control the loop. The net effect is that characters are copied from `s` to `t`, up to and including the terminating `\\0`.

The C99 standards state that the `strcpy()` function must return a copy of its destination parameter. In both cases, we return a copy of the destination parameter—that is, we return a pointer as the function’s value. Thus, the `strcpy()` in the standard library (`<string.h>`) returns the target string as its function value. It might look like

```
char *strcpy(char *destination, char *source)
{
    char *p = destination;
    while(*source != '\\0')
    {
        *p++ = *source++;
    }
    *p = '\\0';
    return destination;
}
```

The following is the array subscript version of the `strlen` library function.

```
int strlen(char s[])
{
```