```
int f=1,i;
if((n==0) || (n==1)) // check the condition for n value
return(1);
else
for(i=1;i<=n;i++) // perform the looping operation for calculating the factorial
f=f*i;
return(f);
}
void main()
{
int n;
clrscr();
printf("enter the number :");
scanf("%d",&n);
printf("factoria of number%d",fact(n));
getch();
}
```

# (b) Write a short note on scope of a variable.

Ans: Scope of a variable means whether the variable declared is a global or local variable. Local variable means it is valid only to the block in which it is declared. Global variable means it is valid throughout the program and its value is not changed throughout the program. The scope of a variable for different storage classes in C language is different. The scope of variable for register storage class is local to the block in which the variable is defined. The scope of variable for automatic storage class is local to the block. The scope of variable for static storage class is local to the block in which the variable is defined. The scope of variable for external storage class is global. If the variable is declared in the main function or within any function, that variable is called local variable and if the variable is declared before main, then it is called as global variable. By the scope of variable, we can know about the functioning of the variable in a program.

# Example:

```
#include<stdio.h>
int a; /* global variable*/
Void main ()
{
Int n,m; /* local variable*/
Printf("none");
}
```

# 3. (a) Write a short note on pointers.

Ans: Pointers: Pointer is a variable used to point the address of the another variable. When you declare a variable, storage is allocated to it and the value assigned to it is stored in that storage location.

# Example: int y=5

When this statement is encountered, memory is allocated to variable y; the value 5 is stored at this address