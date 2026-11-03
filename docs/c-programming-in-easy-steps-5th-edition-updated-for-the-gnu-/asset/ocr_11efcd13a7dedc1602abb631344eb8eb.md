```
int num ;
int (*fptr)(int) = bounce ;
}
```

After the main function block, define the first custom function to output a received value and return an integer

```
int bounce( int a )
{
printf( "InReceived Value: %d\n", a );
return ( ( 3 * a ) + 3 );
}
```

Next, define the second custom function to call a regular function from a received function pointer, and pass it a received integer value

```
int caller( int (*function)(int), int b )
{
(*function)(b);
}
```

Back in the main function block, assign a value to the integer variable by calling the regular function via the function pointer, and output the value it returns

```
num = (*fptr)(10);
printf( "Returned Value: %d\n" , num );
```

Now, assign a new value to the integer variable by passing the function pointer and an integer to another function, which in turn calls the regular function, then output the value it returns

```
num = caller( fptr, 5 );
printf( "Returned Value: %d\n", num );
```

At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0 ;
```

Save the program file, then compile and execute the program to see the values output via function pointers