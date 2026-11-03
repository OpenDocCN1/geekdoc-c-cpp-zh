```
int a=5;
begin:
if(a)
    printf("%d\t",a);
    a--;
    goto begin;
}
```

```
(8) main()
{
    int a=2,x=10;
    if(a==2)
        if(x==8)
            printf("a is equal to 2 and x is equal to 8");
        else
            printf("a is not equal to 2");
}
```

```
(9) main()
{
    int a=6,b=4;
    while(a+b)
    {
        printf("a = %d, b = %d\n",a,b);
        a=a/2;
        b-=3;
    }
}
```

```
(10)main( )
{
    int i=10;
    do
    {
        printf("i=%d\n",i);
        i=i-3;
    }while(i);
}
```

```
(11)main()
{
    int i,j=10;
    for(;i<j;j-=2)
        printf("%d ",j);
}
```

```
(12)main()
{
    int i,j,x=0;
    for(i=0;i<5;i++)
        for(j=i;j>0;j--)
```