Now, insert a statement to reveal that an array allocates the same memory for each one of its elements

```
printf("Size of an int array is %d bytes\n", sizeof(int[3]));
```

Define a structure comprising one char variable and one int variable then reveal its total memory allocation – including any padding

```
struct { int score ; char grade ; } result ;
printf("Size of a structure is %d bytes\n", sizeof(result));
```

At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0;
```

Save the program file, then compile and execute the program to see output from the sizeof operations

![](bbox=[0.2, 0.42, 0.8, 0.62])

![](bbox=[0.11, 0.62, 0.22, 0.72])

This example includes code for a struct object, which is a list of different variables. Structures are demonstrated in Chapter 9 but a struct is included here to demonstrate how the sizeof operator can measure its memory size.