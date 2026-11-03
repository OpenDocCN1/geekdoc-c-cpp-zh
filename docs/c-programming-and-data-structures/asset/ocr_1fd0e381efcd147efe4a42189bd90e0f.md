```
(a) if (x && y)
    x = 10;
else
    y = 10;
(b) if (x || y || z)
    y = 10;
else
    z = 0;
(c) if (x)
    if (y)
        z = 10;
    else
        z = 0;
(d) if (x = 0 || x && y)
    if (!y)
        z = 0;
    else
        y = 1;
```

# 2.10 Assuming that x = 2, y = 1 and z = 0 initially, what will be their values after executing the following code segments?

```
(a) switch (x)
{
    case 2:
        x = 1;
        y = x + 1;
    case 1:
        x = 0;
        break;
    default:
        x = 1;
        y = 0;
}
```

```
(b) switch (y)
{
    case 0:
        x = 0;
        y = 0;
    case 2:
        x = 2;
        z = 2;
    default:
        x = 1;
        y = 2;
}
```

# 2.11 Find the error, if any, in the following statements:

```
(d) if (x <= 10)
    printf ("Welcome");
```

# 2.12 What is the output of the following program?

```
main ()
{
    int m = 5;
    if (m < 3) printf("%d", m+1);
    else if(m < 5) printf("%d", m+2);
    else if(m < 7) printf("%d", m+3);
    else printf("%d", m+4);
}
```

# 2.13 What is the output of the following program?

```
main ()
{
    int m = 1;
    if ( m==1)
    {
        printf ( " Delhi " );
        if (m == 2)
            printf("Chennai ");
        else
            printf("Bangalore");
    }
    else;
        printf(" END");
}
```

# 2.14 What is the output of the following program?

```
main ()
{
    int m ;
    for (m = 1; m<=5; m++)
        printf("%d\n", (m%2) ? m : m*2);
}
```

# 2.15 What is the output of the following program?

```
main ()
{
    int m, n, p ;
    for ( m = 0; m < 3; m++ )
        for ( n = 0; n<=3; n++ )
            for ( p = 0; p < 3; p++ )
                if ( m + n + p >= 2 )
                    goto print;
    print:
        printf("%d, %d, %d", m, n, p);
}
```

# 2.16 What will be the value of x when the following segment is executed?

```
int x = 10, y = 15;
x = (x>y) ? (y+x) : (y-x);
```