```
void mat_arith(int a[][col], int b[][col])
{
    int c[row][col],i,j,choice;
    printf("\n For addition enter: 1 \n");
    printf("For subtraction enter: 2\n");
    printf("\nEnter your choice:");
    scanf("%d",&choice);
    for(i=0; i<row; i++)
    for(j=0; j<col; j++)
    {
        if(choice==1)
            c[i][j]= a[i][j] + b[i][j];
        else if(choice==2)
            c[i][j]= a[i][j] - b[i][j];
        else
        {
            printf("\n Invalid choice. Task not done.?");
            return;
        }
    }
    printf("\n The resulting matrix is:\n");
    for(i=0; i<row; i++)
    {
        for(j=0; j<col; j++)
            printf("%d", c[i][j]);
        printf("\n\n");
    }
    return;
}
```

+   **Output**
+   
+   Enter elements of the second matrix.
+   
+   1 3 5 7 9 11
+   
+   For addition enter: 1
+   
+   For subtraction enter: 2
+   
+   Enter your choice: 1
+   
+   The resulting matrix is:
+   
+   3 7 11
+   
+   14 17 21

Till now, the function definition was always placed after the main program. In fact, C allows the function definition to be placed ahead of the main program. In such a case, the function prototype is not required.

# 12.7 SCOPE AND EXTENT

The region of the program over which the declaration of an identifier is visible is called the scope of the identifier. The scope relates to the accessibility, the period of existence, and the boundary of usage of variables declared in a statement block or a function. These features in turn define whether a variable is local or global in nature.

# 12.7.1 Concept of Global and Local Variables

There are two common terms related to the visibility or accessibility of a variable. They are global and local variables. Global and local are the terms related with lifetime. *Lifetime* is the period during execution of a program in which a variable or function exists. It will be discussed in detail later in this section.

Variables declared within the function body are called *local variables*. They have local scope. Local variables are automatically created at the point of their declaration within the function body and are usable inside the function body. These variables exist only inside the specific function that creates them. They are unknown to other functions and to the main program. The existence of the local variables ends when the function completes its specific task and returns to the calling point. They are recreated each time a function is executed or called.

Variables declared outside of all the functions of a program and accessible by any of these functions are called *global variables*. The existence and region of usage of these variables are not confined to any specific function body. They are implemented by associating memory locations with variable names. Global variables are created at the beginning of program execution and remain in existence all through the period of execution of the program. These variables are known to all functions in the program and can be used by these functions as many times as may be required. They do not get recreated if the function is recalled. Global variables do not cease to exist when control is transferred from a function. Their value is retained and is available to any other function that accesses them.

All global variables are declared outside of all the functions. There is no general rule for where outside the functions these should be declared, but declaring them on top of the code is normally recommended for reasons of scope, as explained through the given examples. If a variable of the same name is declared both within a function and outside of it, the function will use the variable that is declared within it and ignore the global one. If not initialized, a global variable is initialized to zero by default. As a matter of style, it is best to avoid variable names that conceal names in an outer scope; the potential for confusion and error is too great. Moreover, the use of global variables should be as few as possible. Consider the following example.

# EXAMPLE

+   16. Write a program that uses a function to swap values stored in two integer variables to understand the concept of local and global variables.

```
#include <stdio.h>
void exchange(int, int);
```