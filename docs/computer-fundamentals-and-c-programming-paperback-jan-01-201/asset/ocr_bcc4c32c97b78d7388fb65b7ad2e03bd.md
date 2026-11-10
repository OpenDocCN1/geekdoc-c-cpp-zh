```
~~~c
int main(void)
{
    fp1 = print_something;
    print(fp1);

    fp2 = add;
    printf("Calling add from fp2 argument in compute, result = %.2f\n",
           compute(fp2, 100, 200));
    printf("Calling add from add argument in compute, "
           "result = %.2f\n", compute(add, 3500, 1000));

    return 0;
}
void print_something(void)
{
    printf("Used here as a callback function.\n");
    return;
}
void print(void (*fp)(void))
{
    printf("Calling a function passed as argument.\n");
    fp();
    return;
}
float add(float x, float y)
{
    return x + y;
}
float compute(float (*fp)(float, float), float x, float y)
{
    return fp(x, y);
}
~~~
```

PROGRAM 17.5: callback_func.c

```
~~~text
Calling a function passed as argument.
Used here as a callback function.
Calling add from fp2 argument in compute, result = 300.00
Calling add from add argument in compute, result = 4500.00
~~~
```

PROGRAM OUTPUT: callback_func.c

# ## 17.12 FUNCTIONS WITH VARIABLE ARGUMENTS

Ever wondered how `printf` and `scanf` work with a variable number of arguments? C obviously supports functions of this type, so you can devise one, say, to sum a variable number of integers. However, C doesn't have the means to determine the number of arguments passed to a function. So, it's the programmer's job to convey that number to the function. This task can be achieved in the following ways: