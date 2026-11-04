```
```c
double step, x, area;

do {
    printf("Enter number of intervals: ");
    scanf("%d", &n);
} while(n <= 0);

do {
    printf("Enter low and up limit (a < b): ");
    scanf("%d%d", &a, &b);
} while(a >= b);

step = (double)(b-a)/n;
x = a;
area = 0;
for(i = 0; i < n; i++)
{
    area += 0.5*step*(f(x)+f(x+step));
    x += step;
}
printf("Calculus = %f\n", area);
return 0;
}

double f(double x) /* The reason we're using a function is that if we've to calculate another integral it is easy to change the code in the function. */
{
    return x*x;
}
```
```

# Storage Classes and Variables Scope

Every variable is characterized by three properties: storage class, scope, and linkage. The default properties of a variable depend on the point of its declaration.

The storage class of a variable determines when memory is allocated for the variable and when that memory is released. There are two storage classes: automatic and static. The storage class is specified by using one of the keywords: auto, register, extern or static. The scope of a variable is the part of the program in which the variable can be accessed, or else it is visible; it depends on the point of its declaration. The linkage of a variable concerns the linker and determines whether it can be shared by different parts of the program. A variable with external linkage may be shared by several files in a program, while a variable with internal linkage is restricted to the file that it is declared; however, it may be shared by the functions in that file. A variable with no linkage belongs to a function and cannot be shared.