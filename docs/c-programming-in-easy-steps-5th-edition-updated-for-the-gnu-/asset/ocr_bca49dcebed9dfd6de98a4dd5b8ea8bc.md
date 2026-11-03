```
static int sum = 100 ;
```

Add a main function that declares it wants to use the global static variable and output its value

```
int main()
{
    extern int sum ;
    printf("Sum is %d \n", sum) ;
}
```

Now, insert a declaration to use a second global variable and output its value

```
extern int num ;
printf("Num is %d \n", num) ;
```

Insert a final statement to return a zero integer value, as required by the function declaration, then save the file

```
return 0 ;
```

In a separate file define the second global variable, then save that file

```
int num = 200 ;
```

![](bbox=[0.1, 0.5, 0.18, 0.6])

global_2.c

Compile both source files into one executable program, by supplying each source code filename in the command, then execute the program to see the global values output

![](bbox=[0.27, 0.7, 0.78, 0.85])