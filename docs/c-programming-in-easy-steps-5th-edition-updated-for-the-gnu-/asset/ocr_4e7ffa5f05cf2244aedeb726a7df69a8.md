```
printf("Regular variable contains: %d\n", num );
printf("Pointer variable contains: 0x%p\n", ptr );
printf("Pointer points to value: %d\n\n", *ptr );
```

Now, in the main function block, assign a new value to the regular variable via the pointer variable, then output the contents and dereferenced value once more

```
*ptr = 12 ;
printf("Regular variable contains: %d\n", num );
printf("Pointer variable contains: 0x%p\n", ptr );
printf("Pointer points to value: %d\n\n", *ptr );
```

At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0 ;
```

Save the program file, then compile and execute the program to see variable contents and dereferenced value

![](bbox=[0.27, 0.45, 0.75, 0.65])

![](bbox=[0.1, 0.68, 0.22, 0.78])

Declare variables before making other statements – for instance, at the beginning of main().