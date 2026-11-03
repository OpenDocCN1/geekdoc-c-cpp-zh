dereferenced by that pointer

```
int *ptr = nums ;
printf( "\nAt Address: %p is Value: %d\n", ptr , *ptr ) ;
```

Now, in the main function block, increment the pointer to move along the array elements one by one

```
ptr++ ;
printf( "At Address: %p is Value: %d\n", ptr , *ptr ) ;
ptr++ ;
printf( "At Address: %p is Value: %d\n", ptr , *ptr ) ;
```

![](bbox=[0.12, 0.38, 0.25, 0.52])

The *= and /= operators cannot be used to move a pointer.

Now, jump back two memory places to the address of the first array element

```
ptr -= 2 ;
printf( "At Address: %p is Value: %d\n\n", ptr , *ptr ) ;
```

Next, add a loop to output each array element index number and the value it contains

```
for( i = 0 ; i < 10 ; i++ )
{
    printf( "Element %d Contains Value: %d\n", i , *ptr ) ;
    ptr++ ;
}
```

At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0 ;
```

Save the program file, then compile and execute the program to see values output as the pointer moves between array elements