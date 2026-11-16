```
54.#ifdef something
#if something == 0
int some = 0;
#endif
void main()
{
 int thing = 0;
 printf("%d %d",some,thing);
}
```

```
55.void main()
{
 int arr[2][2];
 printf("%d%d",(arr==*arr)
 ****(arr==arr[0])) );
}
```

```
56.void main()
{
 int i = 5;
 printf("%d",++i++);
}
```

```
57.void main()
{
 int i = 5;
 printf("%d",i+++i=6);
}
```

```
58.void main()
{
 char text1[] = "%d\n";
 text[1] = 'c';
 printf(text, 65);
}
```

```
59.void main()
{
 int i=5, j=10;
 i = i &= j & 10;
 printf("%d %d",i,j);
}
```

```
60.void main()
{
 int i=5, j=10;
 i = j = i || 10;
 printf("%d %d",i,j);
}
```

```
61.void main()
{
 int i=5, j=10;
 j = i = j = 10;
 printf("%d %d",i,j);
}
```

```
62.void main()
{
 int i=5, j=10;
 j = i = j > i;
 printf("%d %d",i,j);
}
```

```
63.void main()
{
 int i = 4, j = 7;
 j||i++&&printf("YOU CAN WIN");
 printf("%d %d",i,j);
}
```

```
64.void main()
{
 register int a = 2;
 printf("Address of a = %d",&a);
 printf("Value of a = %d",a);
}
```

```
65.void main()
{
 extern i;
 printf("%d\n",i);
 {
 int i = 20;
 printf("%d",i);
 }
}
```

```
66.#define DIM(array, type)
 sizeof(array)/sizeof(type)
 void main()
 {
 int arr[10];
 printf("The dimension of the
 array is %d",DIM(arr,int));
 }
```

```
67.void main()
{
 printf("sizeof(void *) = %d\n",
 sizeof(void *));
 printf("sizeof(int*) = %d\n",
 sizeof(int *));
 printf("sizeof(double *) = %d\n",
 sizeof(double *));
 printf("sizeof(struct unknown*) = %d",
 sizeof(struct unknown*));
}
```

```
68.void main()
{
 char a[4] = "HELLO";
 printf("%s",a);
}
```

```
69.void main()
{
 char a[4] = "HELLO";
 printf("%s",a);
}
```

```
70.void main()
{
 extern int i;
 {
 int i = 20;
 {
 const volatile unsigned i=30;
 printf("%d", i);
 }
 printf("%d", i);
 }
 printf("%d", i);
}
```