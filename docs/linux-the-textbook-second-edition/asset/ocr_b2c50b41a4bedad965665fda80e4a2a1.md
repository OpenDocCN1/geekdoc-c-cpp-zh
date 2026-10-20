When you use the touch command with one or more existing files as its arguments, it sets their last update time to the current time. When used with a nonexistent file as an argument, it creates a zero-length (i.e., empty) file with that name.

In the following in-chapter exercise, you will use the make command to create an executable for a single source file.

# Exercise 14.5

Create the executable code for the C program in the power.c file and place it in a file called XpowerY. Use the make utility to perform this task by using the makefile given previously. Run XpowerY to confirm that the program works properly.

To show a next-level use of the make utility, we partition the C program in the power.c file into two files: power.c and compute.c. The following session shows the contents of these files. The compute.c file contains the compute function, which is called from the main function in power.c. To generate the executable in the power file, we need to compile the two source files independently and then link them, as shown in the two cc command lines at the end of the session.

```
$ cat power.c
#include <stdio.h>
double compute(double x, double y);
int main()
{
	float x,y;
	printf ("The program takes x and y from stdin and displays x*y.\n");
	scanf ("%f", &x);
	printf ("Enter integer x: ");
	scanf ("%f", &x);
	printf ("Enter integer y: ");
	scanf ("%f", &y);
	printf ("x*y is: %6.3f\n", compute(x,y));
}
```

```
$ cat compute.c
#include <math.h>
double compute (double x, double y)
{
	return (pow ((double) x, (double) y));
}
```

```
$ gcc -c compute.c power.c
$ ls
compute.c compute.o power.c power.o
$ gcc compute.o power.o -o power -lm
```

The dependency relationship of the two source files is quite simple in this case. To create the executable file power, we need two object modules: power.o and compute.o. If either of the two files power.c or compute.c is updated, the executable needs to be recreated. Figure 14.4 shows this first cut on the dependency relationship.

![](bbox=[0.05, 0.95, 0.95, 1.0])