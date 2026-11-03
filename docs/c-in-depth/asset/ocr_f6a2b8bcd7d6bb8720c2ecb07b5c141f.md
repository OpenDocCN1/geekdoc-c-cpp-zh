```
(*ptr)++;
}
```

```
(24)main()
{
    int arr[10];
    func(arr);
}
func(int a[10])
{
    int b[10];
    int x=5,y=4;
    a=&x;
    b=&y;
}
```

```
(25)main()
{
    int arr[3][4]; /*Assume base address of arr is 5000*/
    printf(\"%u\\t\",arr);
    printf(\"%u\\t\",arr[0]);
    printf(\"%u\\n\",&arr[0][0]);
    printf(\"%d\\t\",sizeof(arr));
    printf(\"%d\\t\",sizeof(arr[0]));
    printf(\"%d\\n\",sizeof(arr[0][0]));
}
```

```
(26)main()
{
    int arr[3][4][5];  /*Assume base address of arr is 2000*/
    printf(\"%u\\t\",arr);
    printf(\"%u\\t\",arr[0]);
    printf(\"%u\\t\",arr[0][0]);
    printf(\"%u\\n\",&arr[0][0][0]);
    printf(\"%d\\t\",sizeof(arr));
    printf(\"%d\\t\",sizeof(arr[0]));
    printf(\"%d\\t\",sizeof(arr[0][0]));
    printf(\"%d\\n\",sizeof(arr[0][0][0]));
}
```

```
(27)main()
{
    int arr[10] = {1,2,3,4,5,6,7,8,9,10};
    func(arr+3);
}
func(int a[])
{
    int i;
    for(i=0;a[i]!=8;i++)
        printf(\"%d \",a[i]);
}
```