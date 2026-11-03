```
integer a,b,sum;
read in a and b;
add a & b and set it to sum;
write sum;
}
```

# # Structure of C program (Source Code) -

```
```c
#include<stdio.h> /* For printf() & scanf() */
#include<conio.h> /* For clrscr() & getch() */
main()
/* Starting point of the program execution*/
{
	int a,b,sum;
	/* Variable Declarations */
	clrscr();
	/* Clear Screen */
	printf("enter two numbers");
	/* Request for Input */
	scanf("%d %d",&a,&b);
	/* Input from user */
	sum=a+b;
	/* Adding two numbers */
	printf("sum=%d",sum);
	/* Output Sum */
	getch();
	/* To hold output screen */
}
/* End of main */
```
```

# # Explanation of C Program -

# # STORY OF HEADER FILES -

Header files contain definitions of functions and variables which can be incorporated into any C program by using the pre-processor #include statement. Standard header files are provided with each compiler, and cover a range of areas, string handling, mathematical, data conversion, printing and reading of variables.

To use any of the standard functions, the appropriate header file should be included. This is done at the beginning of the C source file. For example, to use the function printf() in a program, the line --

#include <stdio.h>