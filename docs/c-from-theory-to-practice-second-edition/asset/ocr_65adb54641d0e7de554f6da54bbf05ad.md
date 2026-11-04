Because the i variable declared inside the if block is unrelated to the first i, the program displays 20. A reason to declare a variable inside a compound statement instead of the beginning of a function is that memory will be allocated only if needed. This might be useful when writing applications in systems with limited memory. A compound statement is not needed to join a conditional or loop statement. For example, the following program outputs 50 and 20.

```
~~~c
#include <stdio.h>
int main(void)
{
    int i = 20;

    {
        int i = 50;
        printf("%d\n", i);
    }
    printf("%d\n", i);
    return 0;
}
~~~
```

Since the memory of a local variable is released, a function should not return its address. For example:

```
~~~c
#include <stdio.h>

int *test(void);

int main(void)
{
    int *ptr, j;

    ptr = test();
    printf("%d\n", *ptr);

    j = *ptr;
    printf("%d\n", j);
    return 0;
}

int *test(void)
{
    int i = 10;
    return &i;
}
~~~
```

When test() is called, the compiler allocates memory for the local variable i. Then, it returns the address of i. Since this memory is released, it may be used for other purposes, so the value 10 might be overwritten. Therefore, the program might output 10 and a random value, or two random values, instead of 10 and 10. The behavior of the program is unpredictable. Most probably, the compiler will warn you with a message such as “returning address of local variable.”