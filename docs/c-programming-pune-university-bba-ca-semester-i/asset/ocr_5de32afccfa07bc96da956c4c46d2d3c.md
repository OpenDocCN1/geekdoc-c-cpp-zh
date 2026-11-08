# Address in C

If you have a variable **var** in your program, **&var** will give you its address in the memory, where **&** is commonly called the reference operator or address of operator.

You must have seen this notation while using scanf() function. It was used in the function to store the user inputted value in the address of **var**.

```
scanf("%d", &var);
/* Example to demonstrate use of reference operator in C programming. */
#include <stdio.h>
int main()
{
        int var = 5;
        printf("Value: %d\\n", var);
        printf("Address: %u", &var);  //Notice, the ampersand(&) before var.
        return 0;
}
```

**Output:**

Value: 5

Address: 2686778

> **Note:** You may obtain different value of address while using this program.

In above source code, value 5 is stored in the memory location 2686778. var is just the name given to that location.

# Address of OR Reference Operator (&) and Indirection OR Dereference Operator (*)

**&** is called address of OR reference operator. It gives you the address of a variable.

Likewise, there is another operator that gets you the value from the address, it is called a indirection OR dereference operator (*).

> **Note:** The * sign when declaring a pointer is not a dereference operator. It is just a similar notation that creates a pointer.

# *Example To Demonstrate Working of Pointers*

```
/* Source code to demonstrate, handling of pointers in C program */
#include <stdio.h>
int main()
{
        int* pc;
        int c;
        c=22;
        printf("Address of c:%u\\n", &c);
        printf("Value of c:%d\\n",c);
        pc=&c;
        printf("Address of pointer pc:%u\\n",pc);
```