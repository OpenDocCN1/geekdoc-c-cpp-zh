Employee struct.

Compile the code in Listing 7.5 and launch the executable and you will see the following output:

First name: John
Last name: Smith
Title:      Developer
Employee id: 2000

# A POINTER TO A C STRUCT

This section assumes that you have read the relevant pointer-related sections in [Chapter 5], and please read that material if you have not already done so.

Listing 7.6 displays the contents of PointerStructs.c that illustrates how to create a structure for employee-related data as well as a pointer to such a structure (the new code is shown in bold).

# LISTING 7.6: EmployeeStructs.c

```
#include <stdio.h>
#include <string.h>

typedef struct Employee
{
   char fname [50];
   char lname [50];
   char title [100];
   int emp_id;
} emp;

int main()
{
   struct Employee emp1;

   strcpy( emp1.fname, "John");
```