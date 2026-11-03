```
```c
void disp(int a, int b)
{
    printf("%d\n", a, b);
}
```
```

```
```c
void func(void);
main()
{
    int i=5;
    for(i=i+1;i<8;i++)
        func();
}
void func(void)
{
    int j;
    for(j=1;j<3;j++)
        printf("%d\t",++j);
}
```
```

```
```c
main()
{
    int i=10,k;
    for ( ; ; )
    {
        k=mult(i);
        if(-i<5)
            break;
    }
    printf("k=%d\n",k);
}
mult(int j)
{
    j*=j;
    return(j);
}
```
```

```
```c
main()
{
    int i=2,j=3;
    printf("%d\n",func(i,j));
}
func(int a,int b)
{
    a=a-5;
    b++;
    return(!a+-b);
}
```
```

```
```c
main()
{
    int x;
```
```