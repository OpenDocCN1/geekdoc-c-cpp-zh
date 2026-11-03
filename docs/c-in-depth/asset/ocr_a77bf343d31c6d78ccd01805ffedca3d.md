```
(10)main()
{
    int arr[10]={25,30,35,40,55,60,65,70,85,90},*p;
    for(p=&arr[0];p<arr+10;p++)
        printf("%d ",*p);
}
```

```
(11)main()
{
    int arr[10]={25,30,35,40,55,60,65,70,85,90},*p;
    for(p=arr+2;p<arr+8;p+=2)
        printf("%d ",*p);
}
```

```
(12)main()
{
    int i,arr[10]={25,30,35,40,55,60,65,70,85,90};
    int *p=arr+9;
    for(i=0;i<10;i++)
        printf("%d ",*p--);
}
```

```
(13)main()
{
    int arr[10]={25,30,35,40,55,60,65,70,85,90},*p;
    for(p=arr+9;p>=arr;p--)
        printf("%d ",*p );
}
```

```
(14)main()
{
    int arr[4]={10,20,30,40};/*Assume base address of arr is 5000*/
    int x=100,*ptr=arr;
    printf("%u%d  %d\n",ptr,*ptr,x);
    x=*ptr++;
    printf("%u%d  %d\n",ptr,*ptr,x);
    x=++*ptr;
    printf("%u%d  %d\n",ptr,*ptr,x);
    x=++*ptr;
    printf("%u%d  %d\n",ptr,*ptr,x);
    x=(*ptr)++;
    printf("%u%d  %d\n",ptr,*ptr,x);
}
```

```
(15)main()
{
    int x, arr[8]={11, 22, 33, 44, 55, 66, 77, 88};
    x = (arr+2)[3];
    printf("%d\n", x);
}
```