Now, add a loop to output the error message associated with each defined numerical errno error code

```
for( i = 0 ; i < 44 ; i++ )
{
    printf( "Error %d : %s\n" , i , strerror(i) ) ;
}
```

At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0 ;
```

Save the program file, then compile and execute the program to see the error messages

![](bbox=[0.26, 0.38, 0.76, 0.92])