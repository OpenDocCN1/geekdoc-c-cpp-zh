
The second declaration makes the object that it points at read-only and of course, both the object and what it points at might be constant. Because we have declared the value pointed to by `ptr` to be `const`, the compiler will check for any statements that attempt to modify the value pointed to by `ptr` and flag such statements as error. For example, the following statement will now result in an error message from the compiler:

```c
*ptr = 100; /* ERROR */
```

As the declaration asserted that what `ptr` points to must not be changed. But the following assignment is valid.

```c
n = 50;
```

The value pointed to has changed but here it was not tried to use the pointer to make the change. Of course, the pointer itself is not constant, so it is always possible to change what it points to:

```c
int v = 100;
ptr = &v;  /* OK - changing the address in ptr */
```

This will change the address stored in `ptr` to point to the variable `v`.

It is to be noted that the following declarations are equivalent.

```c
const int *ptr = &n;
int const *ptr = &n;
```

### 13.20.2 Constant Pointers

Constant pointers ensure that the address stored in a pointer cannot be changed. Consider the following statements:

```c
int n = 10;
int *const ptr = &n;  /* Defines a constant */
```

Here is how one could ensure that a pointer always points to the same object; the second statement declares and initializes `ptr` and indicates that the address stored must not be changed.

Any attempt to change what the pointer points to elsewhere in the program will result in an error message when you compile:

```c
int v = 5;
ptr = &v;  /* Error - attempt to change a constant pointer */
```

It is still legitimate to change the value that `ptr` points to using `ptr` though:

```c
*ptr = 100;     /* OK - changes the value of v */
```

This statement alters the value stored in `v` through the pointer and changes its value to 100.

You can create a constant pointer that points to a value that is also constant:

```c
int n = 25;
const int *const ptr = &n;
```

`ptr` is a constant pointer to a constant so everything is fixed. It is not legal to change the address stored in `ptr` as well as `ptr` cannot be used to modify what it points to.

### 13.20.3 Constant Parameters

Recall that arrays are passed to functions by address and it is also known that function implementations can alter the original array’s contents. To prevent an array argument from being altered in a function, use the `const` qualifier as demonstrated in the following programs.

*Version 1*

```c
#include <stdio.h>
void change(char *);
int main(void)
{
    char s[]="Siva";
    change(s);
    printf("\n The string after calling change():\n%s", s);
    return 0;
}
void change(char *t)
{
    *t='V';
}
```

**Output**

The string after calling change():Viva

*Version 2*

```c
#include <stdio.h>
void change(const char *);
int main(void)
{
    char s[]="Oxford University";
    change(s);
    printf("\n The string after calling change():\n%s", s);
    return 0;
}
void change(const char *t)
{
    *t='V';
}
```

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_400_0.png)

**Output**

Compiler error: Assignment of read-only location

The same error will occur when the following program is compiled.

```c
#include <stdio.h>
void change(const int [], int);

int main(void)
{
    int a[]={1,2,3,4,5};
    int n,i;

    n=sizeof(a)/sizeof(a[0]);
    change(a,n);
    printf("\n The array elements after calling\n        change()\n");
    for(i=0;i<n;++i)
        printf("\t%d",a[i]);
    return 0;
}
void change(const int b[],int n)
{
    int i;
    for(i=0;i<n;++i)
        b[i]+=10;
}
```

> The expression `sizeof(a)/sizeof(a[0])` yields 5 as `sizeof(a)` returns 20 and `sizeof(a[0])` returns 4.

In the above program, use of constant parameter protects the elements of the array from being modified within the function `change()`, though arrays passed as arguments are passed by address automatically.

### Check Your Progress

What will be the output of the following program?

- **1.**
```c
int main()
{
    int val = 5;
    int *ptr = &val;
    printf("%d %d", ++val, *ptr);
    return 0;
}
```
**Output:** 6 5

- **2.**
```c
int main()
{
    int val = 5;
    int *ptr = &val;
    printf("%d %d", val, *ptr++);
    return 0;
}
```
**Output:** 5 5

- **3.**
```c
int main()
{
    int val = 5;
    int *ptr = &val;
    printf("%d %d", val, ++*ptr);
    return 0;
}
```
**Output:** 6 6

- **4.**
```c
int main()
{
    int a[] = {1,2,3,4,5,6};
    int *ptr = a + 2;
    printf("%d %d", *++a, --*ptr);
    return 0;
}
```
**Output:** Error: lvalue required

- **5.**
```c
int main()
{
    int a[] = {1,2,3,4,5,6};
    int *ptr = a + 2;
    printf("%d %d", --*ptr+1,1+*--ptr);
    return 0;
}
```
**Output:** 2 3

- **6.**
```c
int main()
{
    char myArray[5], *p = myArray;
    int i;
    for(i = 4; i > 0; i--){
        *p++ = i * i; p++;
    }
    for (i = 4; i >= 0; i--)
        printf("%d", myArray[i]);
    return 0;
}
```
**Output:** 0 1 4 9 16

- **7.**
```c
int main()
{
    int a = 555, *ptr = &a, b = *ptr;
    printf("%d %d %d", ++a, --b, *ptr++);
    return 0;
}
```
**Output:** 556 554 555

- **8.**
```c
int main()
{
    int val = 5;
    int *ptr = &val;
    printf("%d %d", val,(*ptr)++);
    return 0;
}
```
**Output:** 6 5

- **9.**
```c
int main()
{
    int a[100];
    int sum = 0;
    for(k = 0; k < 100; k++)
        *(a+k) = k;
    printf("%d", a[--k]);
    return 0;
}
```
**Output:** 99

- **10.**
```c
int main()
{
    void F(int *a, int n);
    int arr[5] = {5,4,3,2,1};
    F(arr,5);
    return 0;
}
void F(int *a, int n)
{
    int i;
    for(i = 0; i < n; i++)
        printf("%d", *(a+++i));
}
```
**Output:** 55555

- **11.**
```c
int main(void)
{
    int a[10];
    printf("%d", ((a + 9) + (a + 1)));
    return 0;
}
```
**Output:** Error

- **12.**
```c
int main()
{
    char A[] = {'a','b','c','d','e','f','g','h'};
    char *p = A;
    ++p;
    while(*p != 'e')
        printf("%c", *p++);
    return 0;
}
```
**Output:** bcd

- **13.**
```c
int main()
{
    char *p1 = "Name";
    char *p2;
    p2 = (char *) malloc(20);
    while(*p2++ = *p1++);
    printf("%s\n", p2);
    return 0;
}
```
**Output:** An empty string

- **14.**
```c
int main()
{
    int a = 2, b = 3;
    printf("%d", a+++b);
    return 0;
}
```
**Output:** 5

- **15.**
```c
int main()
{
    int a[] = {1,2,3,4,5,6,7};
    char c[] = {'a','x','h','o','e','k'};
    printf("%d %d", (&a[3]-&a[0]),(&c[3]-&c[0]));
    return 0;
}
```
**Output:** 3 0

- **16.**
```c
#include<stdio.h>
int main()
{
    char s1[] = "Manas";
    char s2[] = "Ghosh";
    s1 = s2;
    printf("%s", s1);
    return 0;
}
```
**Output:** Error

- **17.**
```c
int main()
{
    char *ptr = "Mira Sen";
    (*ptr)++;
    printf("%s\n", ptr);
    ptr++;
    printf("%s\n", ptr);
    return 0;
}
```
**Output:**
```
Nira Sen
     ira Sen
```

- **18.**
```c
int main()
{
    char *p = "The Matrix Reloaded";
    int i = 0;
    while(*p)
    {
        if(!isupper(*p++))
            ++i;
    }
    printf("%d", i);
    return 0;
}
```
**Output:** 16

- **19.**
```c
int main()
{
    char str[] = "Test";
    if((printf("%s", str)) == 4)
        printf("Success");
    else
        printf("Failure");
    return 0;
}
```
**Output:** Test Success

- **20.**
```c
int main()
{
    printf("Hi Friends"+3);
    return 0;
}
```
**Output:** Friends

- **21.**
```c
int main()
{
    int a[] = {1,2,3,4,5,6};
    int *ptr = a + 2;
    printf("%d", *--ptr);
    return 0;
}
```
**Output:** 2

- **22.**
```c
int main()
{
    int i = 100, j = 20;
    i++ = j;
    i *= j;
    printf("%d\t %d\n", i,j);
    return 0;
}
```
**Output:** Error lvalue required

- **23.**
```c
int main()
{
    int a[5], *p;
    for(p = a; p < &a[5]; p++)
    {
        *p = p-a;
        printf("%d", *p);
    }
    return 0;
}
```
**Output:** 2

- **24.**
```c
int main()
{
    putchar(5["manas"]);
    return 0;
}
```
**Output:** Nothing will be printed

- **25.**
```c
int main()
{
    int a[] = {1,2,3,4,5};
    int i, s = 0;
    for(i = 0; i < 5; ++i)
        if((a[i]%2) == 0)
            s += a[i];
    printf("%d", s);
    return 0;
}
```
**Output:** 6

- **26.**
```c
int main()
{
    int i;
    char s[] = "Oxford University Press";
    for(i = 0; s[i] != '\0'; ++i)
        if((i%2) == 0)
            printf("%c %c", s[i], s[i]);
    return 0;
}
```
**Output:** O Of fr r n nv vr ri iy yP Pe es s

- **27.**
```c
int main()
{
    int i;
    char s[] = "Oxford University Press";
    for(i = 0; s[i] != '\0'; ++i)
        if((i%2) == 0)
            putchar(s[i]);
    return 0;
}
```
**Output:** Ofr nviryPes

- **28.**
```c
int main()
{
    char s[3][6] = {"ZERO", "ONE", "TWO"};
    printf("%s", s[2]);
    printf("%c", s[2][0]);
    return 0;
}
```
**Output:** TWOT

- **29.**
```c
int main()
{
    int a[][3] = {0,1,2,3,4,5};
    printf("%d", sizeof(a));
    return 0;
}
```
**Output:** 12

- **30.**
```c
int main()
{
    int a[2][3] = {0,1,2,3,4,5};
    printf("%d", sizeof(a[2]));
    return 0;
}
```
**Output:** 6 OR 12

- **31.**
```c
int main()
{
    char *str = "This is my string";
    str[3] = 'B';
    puts(str);
    return 0;
}
```
**Output:** ThiB is my string
