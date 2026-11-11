is not a constant pointer, and use it as an array. For example, we can create a pointer p as shown below.

```
```cpp
int *p;  /*create a non-constant pointer*/
if (condition)
{
p=(int [5]){10,20,30,40,50};
}
else
{
p=(int [5]){100,200,300,400,500};
}
```
```

The statement,

```
```cpp
p=(int [5]){10,20,30,40,50};
```
```

stores starting address of an array of size 5 in a pointer p as shown in the Figure 8.28.

![](bbox=[0.25, 0.44, 0.65, 0.49])

Figure 8.28: Pointer pointing to an array of size 5

Note that, we have to apply type casting in this initialization because the initializer {} works only to initialize arrays and not pointers. The type cast (int [5]) informs the compiler that the initializer type is an array of 5 integers. And we know that, when an array is initialized to the pointer, the pointer always stores the starting address of the array. Hence the whole statement works as if an array of size 5 is initialized to a pointer p.

As p points to the first element of the array, we can access any i<sup>th</sup> element of the array as p[i] or *(p+i) as shown below:

```
```cpp
for(i=0;i<=n-1;i++)
{
printf("%d\n",*(p+i)); /*print a[i] using pointer p*/
}
```
```

Similarly, the statement

```
```cpp
p=(int [5]){100,200,300,400,500};
```
```

makes the pointer p point to a different data set.

> > **NOTES**
> >
> > A string constant can be initialized to a character pointer without casting it to array type. This is because compiler anyway creates an array of characters to store a string. For example, the statement,
> > `char *p="ducks";`
> > makes pointer p point to a character array as shown in Figure 8.29.