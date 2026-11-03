# 2.

```
main()
{
    static int c = 5;
    printf('\n c = %d',c--);
    if(c !=0)
        main();
}
```

Output:- 5 4 3 2 1

Because c = 5 and first printed and then decrease by 1 and then call main() but because here c is defined as static so the control doesn't go to the initialization and this condition will be true for five times and each time c gets printed and then decrease so c will be 5 4 3 2 1.

```
main()
{
    int x = 20;
    {
        int x = 30;
        printf('%d ',x);
    }
    printf('\n %d',x);
}
```

Output:- 30 20

Because when control executes the innermost printf it will print 30 because the local variable gets priority and when control comes out from this block the scope will ends and here x =20 and gets printed.

# 3.

```
main()
{
    int i,j;
    for(i = 1; i<5; i++)
    {
        j = g(i);
        printf('\n%d',j);
    }
}
Int g(int x)
{
    static int v = 1;
    int b = 3;
    v+=x;
    return(v+x+b);
}
```

Output:- 6 9 13 18

# 7.

```
main()
{
    extern int i;
    i=20;
    printf('%d',sizeof(i));
}
```

Output:- Error extern int i is a declaration and not definition

# 8.

```
main()
{
    extern int a;
    printf('%d',a);
}
int a=20;
```

Output:- 20