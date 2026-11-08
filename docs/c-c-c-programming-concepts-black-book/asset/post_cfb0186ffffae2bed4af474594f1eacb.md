
## Chapter 3

Output of the preceding program is as follows:

```text
Enter String 1 -> TANUMAN

Enter String 2 -> JACK

The result of the operation is -> TANUMANJACK
```

Let’s now summarize the main points discussed in the chapter.

### Summary

In this chapter, we have covered the basics of string manipulation in C. First, we have learned how to display strings using pointers and the printf() function. Next, we have learned about the strcat(), strcmp(), strlen(), strcpy(), strncpy(), strncat(), strchr(), and strspn() functions.

### Quick Revise

### Multiple Choice Questions

- Q1. Which of the following function is used to concatenate a string with another string?
  - i. `strcat()`
  - ii. `strcpy()`
  - iii. `strncpy()`
  - iv. `strncat()`
- Q2. Which of the following function is used to compare two strings?
  - i. `strchr()`
  - ii. `strspn()`
  - iii. `strcmp()`
  - iv. `strlen()`
- Q3. Which of the following function is used to copy the content of a string into another?
  - i. `strncpy()`
  - ii. `strcmp()`
  - iii. `strlen()`
  - iv. None of the above

### Subjective Questions

- Q1. Write a program that implements the strlen() function.
- Q2. Write a program that implements the strcat() function.
- Q3. Write a program that searches a substring within a string and returns the number of occurrences of that substring.
- Q4. Write a program that replaces a pattern within a string, without using any standard library function.

![](img/43c5f409f9b17790a628c4b4df854b61_136_0.png)

## Chapter 4: Pointers and Function Pointers in C

| *If you need an Information on:* | *See page:* |
|---|---|
| Pointers | 96 |
| Single Dimensional Arrays using Pointers | 98 |
| Two-Dimensional Arrays using Pointers | 100 |
| Three-Dimensional Arrays using Pointers | 106 |
| Array of Pointers | 114 |
| Function Pointers | 116 |
| Callbacks | 120 |
| Functors | 123 |
| Complex Examples of Pointers and Function Pointers | 125 |

The C language provides an option of manipulating a variable and its content using its memory address. All the memory related operations take place in C using pointers. C allows the programmers to access any part of the code using memory addresses. However, while using a memory address, extra care should be taken so that other portions of code are not hampered. Therefore, content overwriting using memory addresses should be strictly checked before using them.

In this chapter, we learn about the functionalities of pointers. Next, we learn how to handle single and multi-dimensional arrays using pointers. The chapter also discusses array of pointers, function pointers, callbacks, and functors. Finally, we learn about the criticality in the implementation of pointers and function pointers through some examples.

### Pointers

A pointer is defined as a variable that contains the address of another variable. The term address refers to the memory location where the actual value of the variable is stored.

To better understand the pointers, consider the following statement:

```c
int k = 3;
```

By applying the unary operator & on the k variable, we can retrieve its address, as follows:

```c
ptr = &k;
```

The preceding statement assigns the address of the k variable to the ptr variable. This implies that ptr now points to the k variable.

Another unary operator *, which is also called indirection or dereferencing operator, is used to access the object that the pointer is currently pointing at. Listing 4.1 demonstrates how to retrieve the value and address of a variable using a pointer:

**Listing 4.1:** Showing the Usage of Pointers

```c
#include<stdio.h>
int main()
{
    int var_A = 10;

    printf("\n Value of A is -> %d ",var_A);
    printf("\n Address of A is -> %u",&var_A);
    printf("\n Value of A is -> %d ",*(&var_A));
    return 0;
}
```

In Listing 4.1, the & unary operator is used to return the address of the var_A variable. Similarly, the dereferencing operator * is used to display the value at the specified memory location.

> **NOTE**
>
> The & unary operator is also called an address-of operator.

We can also assign the address of a variable to another pointer variable. For example, `int *ptr` declares ptr as a pointer to an integer, which implies that ptr can contain the address of any integer variable. Note that the compiler will allocate a memory location for ptr as well because ptr is itself a variable.

We should keep in mind that declaring a pointer does not mean that it will contain a value of a similar data type. For example, `float *ptr` does not imply that the content of ptr is a floating-point value. However, it implies that ptr will contain the address of a location whose content is a floating-point value.

Let’s now learn about multiple indirection and pointer handling.

### Multiple Indirection in Pointers

As discussed, a pointer is a variable that contains the address of another variable. However, address of a pointer can also be stored in another pointer. This concept is known as multiple indirection of pointers, which creates several layers of pointers. This implies that multiple indirection in pointers introduces the concept of pointer to another pointer. Syntactically, a pointer to a pointer has one more asterisk in front of it that describes the depth in the pointer. Listing 4.2 demonstrates the multiple indirection in pointers:

**Listing 4.2: Showing the Usage of Multiple Indirection in Pointers**

```c
#include<stdio.h>
int main()
{
    int var_A = 10;
    int *ptr;
    int **ptr2ptr;

    ptr = &var_A;
    ptr2ptr = &ptr;

    printf("\n Address of var_A %u",ptr);
    printf("\n Address of var_A %u",*ptr2ptr);

    printf("\n Value of var_A %d ",*ptr);
    printf("\n Value of var_A %d ",**ptr2ptr);
    return 0;
}
```

In Listing 4.2, we have declared ptr as a pointer and ptr2ptr as a pointer to a pointer.

Figure 4.1 shows the memory map of ptr2ptr:

![](img/43c5f409f9b17790a628c4b4df854b61_138_0.png)

The ptr pointer points to a variable, which has a memory location of 7485. As ptr2ptr is a double pointer, it will contain the address of a pointer. In our case, ptr2ptr contains the address of ptr, that is, 6495. For displaying the content of var_A, we must use `**` before ptr2ptr, as it is a double pointer.

### Pointer Handling

While dealing with pointers, pointer assignment should be done correctly. As we know, an integer variable takes four bytes of data in the memory. Now, if we display the address of an integer variable with the %u format, then we only get the address of the first byte in the memory. To solve this problem, we should use the `*ptr` convention, which allows us to access the information stored in all the four bytes of memory.

Let's understand the concept with the code given in Listing 4.3:

**Listing 4.3: Handling Different Types of Pointers**

```c
#include<stdio.h>
int main()
{
    int var_A = 10;
    float var_B = 5.65;
    char *ptr_A, *ptr_B;

    ptr_A = (char*)&var_A;
    ptr_B = (char*)&var_B;

    printf("\n Address in ptr_A %u",ptr_A);
    printf("\n Address of ptr_B %u",ptr_B);

    printf("\n Value at ptr_A %d ",*ptr_A);
    printf("\n Value at ptr_B %d ",*ptr_B);
    return 0;
}
```

The preceding code will compile successfully as we have type cast the addresses of integer and float variables to a character pointer. However, we might face problems while displaying the value stored at the given memory location with the help of the `*` operator, as we have used a char pointer while assigning the address of an integer. In this case, only the information stored in the first byte of memory location is fetched. For the var_A variable, we will get a valid output, as the value stored is 10 and the binary representation of 10 requires only one byte of storage. However, if we change the value to a larger one, which needs more bits for storage in the memory, then we will get a truncated or garbage result. Therefore, if we want to access an integer, then we should store the address in an integer pointer. The same concept applies for the float variable as well.

Next, let's learn how to deal with single dimensional arrays using pointers.

### Single Dimensional Arrays using Pointers

An array can be considered as a collection of similar types of elements that are stored in contiguous memory locations. Similar types of elements imply that the variables getting stored could be all int, char, or any other storage class specifier. Following is the syntax for declaring a single dimensional array (also called one-dimensional array):

```c
int a[10];
```

The preceding syntax declares an array of size 10, where each cell in the array is of type int. The size 10 can also be defined as the dimension of array, and the `[ ]` brackets tell the compiler that the array is being used. As per the C convention, the first element in an array is numbered as 0; therefore, the last element in the array can be found at a location one less than the size of the array. Consider the following example where we have declared and initialized two arrays at the same time:

```c
int arr[4] = {1,2,3,4};
int arr[] = {6,7,8,9};
```

As shown in the second array, when we declare and define an array at the same time, mentioning the dimension of array becomes optional.

Extra care should be taken while dealing with arrays, as error checks are not done in C to determine whether the subscript used to access the array elements exceeds the size of the array. If the subscript exceeds the size of an array, then the subscript might overwrite its own information on top of some other, which might lead to fatal memory corruption.

Let's now learn how to pass array elements to a function.

Array elements can be passed to a function in two ways: call by value and call by reference. Call by value implies passing the values of array elements to a function; whereas, call by reference implies passing the addresses of array elements to a function. Listing 4.4 shows how to pass the values of array elements to a function:

**Listing 4.4: Passing Values of Array Elements to a Function**

```c
#include<stdio.h>
void show_value(int value);
int main()
{
```
