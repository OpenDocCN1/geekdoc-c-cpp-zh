```
(2) #define MSSG printf("If you lapse, don't collapse\n");
main()
{
    MSSG
}
```

```
(3) #define PROD (x,y) ((x)*(y))
main()
{
    int a=3,b=4;
    printf("Product of a and b = %d",PROD(a,b));
}
```

```
(4) #define A 50
#define B A+100
main()
{
    int i,j;
    i=B/20;
    j=500-B;
    printf("i = %d, j = %d\n",i,j);
}
```

```
(5) #define NEW_LINE printf("\n");
#define BLANK_LINES(n) {int i; for(i=0;i<n;i++) printf("\n");}
main()
{
    printf("When you have a chance");
    NEW_LINE
    printf("to embrace an opportunity");
    BLANK_LINES(3)
    printf("Give it a big hug");
    NEW_LINE
}
```

```
(6) #define INFINITE while(1)
#define CHECK(a) if(a==0) break
main()
{
    int x=5;
    INFINITE
    {
        printf("%d ",x--);
        CHECK(x);
    }
}
```

```
(7) #define ABS(x) ((x)<0 ?-(x):(x))
main()
{
    int array[4]={1,-2,3,-4};
```