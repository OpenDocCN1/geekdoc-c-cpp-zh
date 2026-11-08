# 7.7 Functions and Pointers

# 7.7.1 Pointers as Function Arguments

Functions also take pointer as parameters. This allows the data items of the program inside the calling function to be accessed, altered and then returned to the calling function with the new changes reflected in the data item passed. This use of pointer is referred to as passing arguments by reference (address/location). [recall: passing arguments by value discussed in the earlier chapter on functions].

When an argument is passed by value, the data item is copied in function and any change done to it is not reflected in the calling function. However, when an argument is passed by reference, the address of the data item is passed into the function and any changes/alterations done will be reflected in both the function and the calling function. Thus, the use of a pointer as a function argument permits the corresponding data item to be altered globally from within the function.

When pointers are used as arguments to a function, formal pointer arguments must each be preceded by an asterisk. Function prototypes are written in the same manner. In case the function declaration does not include variable names, the data type of each pointer argument must be followed by an asterisk.

*Example*

```
void show_int(int x, int y);        //function prototype
void show_int1(int *pt_x, int *pt_y);
void main()
{
        int x = 56;
        int y = 75;
        printf("\n Original values: x=%d, y=%d", x, y);
        show_int(x,y);
        printf("\n Values of x and y after calling show_int(): x=%d, y=%d", x, y);
        show_int1(&u, &v);
        printf("\n Values of x and y after calling show_int1(): x=%d, y=%d", x, y);
}
void show_int(int x, int y)
{
        x=y=1;
        printf("\n\n Values of x and y inside show_int1(): x=%d, y=%d", x, y);
}
void show_int1(int *pt_x, int *pt_y)
{
        *pt_x=*pt_y=1;
        printf("\n\n Values of x and y inside show_int1(): *pt_x=%d, *pt_y=%d", *pt_x, *pt_y);
}
```

As seen in the above program, there are two functions show_int() and show_int1() which accept two arguments. The first function show_int() accepts two integer arguments and modifies their values to 1. But these changes are not reflected in the main(); as these arguments are passed by value. The changes done to the arguments are local to the function in which the changes occur.