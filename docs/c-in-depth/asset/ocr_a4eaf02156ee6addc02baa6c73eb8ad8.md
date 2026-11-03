```
```c
x=i+j+1;
    printf("x = %d\n",x);
}
```
```

```
```c
(13)main()
{
    int i,index=0;
    for(i=0;i<10;i++)
    {
        int i=0;
        while(i++<5)
            index++;
    }
    printf("index = %d\n",index);
}
```
```

```
```c
(14)main()
{
    int i;
    for(i=1;i<10;i++)
    {
        if(i==3)
            continue;
        printf("%d ",i);
    }
}
```
```

```
```c
(15)main()
{
    int i=1;
    while(i<10)
    {
        if(i==3)
            continue;
        printf("%d ",i);
        i++;
    }
}
```
```

```
```c
(16)main()
{
    int i,sum;
    for(i=0;i<10;i+=3)
        sum +=i*i;
    printf("%d",sum);
}
```
```

```
```c
(17)main()
{
    int c=50;
    for( ;c ; )
```
```