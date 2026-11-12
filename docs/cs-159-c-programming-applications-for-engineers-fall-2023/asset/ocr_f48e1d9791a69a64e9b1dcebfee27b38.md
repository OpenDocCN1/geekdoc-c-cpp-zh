# User-defined function for input of starting value:

```
int getStart(void)
{
    int num;
    do
    {
        printf("Enter starting value -> ");
        scanf("%d", &num);
        if(num < 0)
        {
            printf("\nError! Non-negative values only!\\n\n");
        }
    }while(num < 0);
    return(num);
}
```

# User-defined function for input of ending value:

```
int getEnd(int start)
{
    int num;
    do
    {
        printf("Enter ending value -> ");
        scanf("%d", &num);
        if(num < start)
        {
            printf("\nError! Ending value must be at least %d\n\n", start);
        }
    }while(num < start);
    return(num);
}
```