# Loop Examples

```
unsigned int STDCALL MyFunction(unsigned int *array)
{
    register unsigned int b;
    register unsigned int a = 0;
    for(b = 0; b != 100; b++)
    {
        a = a + array[b];
    }
    return a;
}
```

And finally with a do-while loop:

```
unsigned int STDCALL MyFunction(unsigned int *array)
{
    register unsigned int b = 0;
    register unsigned int a = 0;
    do
    {
        a = a + array[b];
        b++;
    }while(b != 100);
    return a;
}
```