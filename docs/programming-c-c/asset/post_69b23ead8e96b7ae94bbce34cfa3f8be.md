
# Program - Asterisks and Address of Operators in Pointer Variable

```c
#include <stdio.h>
#include <string.h>

int main() {
{
    int i = 5;
    int *ptr;
    ptr = &i;

    printf("Address of i = %u\n", i);
    printf("Address of ptr = %u\n", &ptr);
    printf("Address of i = %u\n", *ptr);
    return 0;
}
```

Output:
Address of i = 65522
Address of ptr = 65526
Address of i = 65522

> Note: In the above program, third printf make sense. Simply, asterisks (*) and address (&) of operators cancelled each other.

# NULL POINTER

It is always a good practice to assign a NULL value to a pointer variable in case you do not have an exact address to be assigned. This is done at the time of variable declaration. A pointer that is assigned NULL is called a null pointer.

The NULL pointer is a constant with a value of zero defined in several standard libraries. Consider the following program.

# Pointers, Structures and Unions

```c
#include<stdio.h>
int main(){
int*ptr = NULL;
printf("The value of the ptr is : %x\n", ptr );
return 0;
}
```

When the above code is compiled and executed, it produces the following result:

The value of ptr is 0

# Common Mistakes While Working with Pointer in C

Here are some of the common mistakes programmers generally tend to working with pointers:

# 1. The incorrect data type for pointers

It is important to note that in order to avoid the loss of data, it is very important to assign the correct data type to the pointer.

For instance, if the data type of the pointer is of integer type, the C compiler considers the variable address the pointer would point to will store integer values and hence the compiler reserves 4 bytes of space for it when talking about a 64-bit compiler.

Let us consider this fragment of code:

```c
/* Here, both the variables number1 and number2 are of long data type which
occupies 8 bytes */ / long number1, number2; int *p;
scanf("%d",&number1); // To input value of number1 as long data type
p = &number1; // To store the address of number1 into the pointer p
number2 = // To store the value being pointed to by p into number2
```

# 2. Incorrect initialization

We tend to confuse the value of the variable and its memory address. Let's say we have one variable 'a' of int type and a pointer *p again of int type, then the following initializations are incorrect:

```c
a = p;
*p = &a;
```

It is important to understand that it is incorrect as 'a' is a variable whereas p is its memory address.

# ARITHMETIC OPERATIONS WITH POINTERS (POINTER ARITHMETIC IN C)

C allows programmers just like you to do arithmetic operations using pointers. So, programmers can perform any arithmetic operations using pointer variables. Performing arithmetic operations using pointer variables is said to be arithmetic pointer operations.

We can perform arithmetic operations on the pointers like addition, subtraction, However, as we know that pointer contains the address, the result of an arithmetic operation performed on the pointer will also be a pointer if the other operand is of type integer. In pointer-from-pointer subtraction, the result will be an integer value.

Following arithmetic operations are possible on the pointer in C language:

- * Increment
- Decrement
- Addition
- Subtraction
- Comparison

# Increment Pointer Variable

If we increment a pointer by 1, the pointer will start pointing to the immediate next location. This is somewhat different from the general arithmetic since which the pointer will get increased by the size of the data type to which the pointer is pointing.

We can traverse an array using the increment operation on a pointer which will keep pointing to every element of the array, perform some operation on that, and update it in a loop.

The rule to increment the pointer is given below:

```c
new_address = current_address + i * size_of(data_type)
```

where i is the number by which the pointer get increased.

# 32-bit

For 32-bit int variable, it will be incremented by 2 bytes.

# 64-bit

For 64-bit int variable, it will be incremented by 4 bytes.

Let's see the example of incrementing pointer variable on 64-bit architecture.

```c
#include<stdio.h>
int main(){
 int number=50;
 int *p;//pointer to int
p=&number;//stores the address of number variable
printf("Address of p variable is %u \n",p);
p=p+1;

printf("After increment: Address of p variable is %u \n",p); // in our case,
 p will get incremented by 4 bytes.
 return 0;
}
```

Output:
Address of p variable is 3214864300
After increment: Address of p variable is 3214864304

# Traversing an array by using pointer

```c
#include<stdio.h>
void main ()
{
 int arr[5] = {1, 2, 3, 4, 5};
 int *p = arr;
 int i;

printf("printing array elements...\n");
for(i = 0; i < 5; i++)
{
 printf("%d ",*(p+i));
}
}
```

Output:

printing array elements...
1 2 3 4 5

# DECREMENTING POINTER IN C

Like increment, we can decrement a pointer variable. If we decrement a pointer, it will start pointing to the previous location. The formula of decrementing the pointer is given below:

```c
new_address= current_address - i * size_of(data type)
```

32-bit
For 32-bit int variable, it will be decremented by 2 bytes.

64-bit
For 64-bit int variable, it will be decremented by 4 bytes.
Let's see the example of decrementing pointer variable on 64-bit OS.

```c
#include <stdio.h>
void main(){
int number=50;
int *p;//pointer to int
p=&number;//stores the address of number variable
printf("Address of p variable is %u \n",p);
p=p-1;

printf("After decrement: Address of p variable is %u \n",p); // P will now
point to the immediate previous location.

}
```

Output:

Address of p variable is 3214864300

After decrement: Address of p variable is 3214864296

# C POINTER ADDITION

We can add a value to the pointer variable. The formula of adding value to pointer is given below:

```c
new_address= current_address + (number * size_of(data type))
```

32-bit
For 32-bit int variable, it will add 2 * number.

64-bit
For 64-bit int variable, it will add 4 * number.
Let's see the example of adding value to pointer variable on 64-bit architecture.

```c
#include <stdio.h>
int main(){
int number=50;
int *p;//pointer to int
p=&number;//stores the address of number variable
printf("Address of p variable is %u \n",p);
p=p+3; //adding 3 to pointer variable
printf("After adding 3: Address of p variable is %u \n",p);
return 0;
}
```

Output:
Address of p variable is 3214864300
After adding 3: Address of p variable is 3214864312

# C POINTER SUBTRACTION

Like pointer addition, we can subtract a value from the pointer variable. Subtracting any number from a pointer will give an address. The formula of subtracting value from the pointer variable is given below:

```c
new_address= current_address - (number * size_of(data type))
```

32-bit
For 32-bit int variable, it will subtract 2 * number.

64-bit
For 64-bit int, it will subtract 4 * number.
Let's see the example of subtracting value from pointer variable on 64-architecture.

```c
#include<stdio.h>
int main(){
int number=50;
int *p;//pointer to int
p=&number;//stores the address of number variable
printf("Address of p variable is %u \n",p);
p=p-3; //subtracting 3 from pointer variable
printf("After subtracting 3: Address of p variable is %u \n",p);
return 0;
}
```

Output:
Address of p variable is 3214864300
After subtracting 3: Address of p variable is 3214864288
