
## 12.1.2 Pointer Declaration and Initialization

To declare a pointer in C, you need to specify the data type to which the pointer will refer. The syntax for declaring a pointer is as follows:

```
data_type *pointer_name;
```

Here, data_type can be any valid C data type, such as int, float, char, or a user-defined struct.

For example, to declare an integer pointer, you would use:

```c
int *ptr;
```

Once declared, you can initialize the pointer to point to a specific memory location. You can do this by assigning the address of a variable to the pointer using the address-of operator (&):

```c
int num = 5;
int *ptr = &num;
```

In this example, the pointer ptr is initialized to hold the address of the variable num, which has a value of 5. See Fig. 12.1.

![](img/33fb6b7acbb6df48a3c9564e97117da6_191_0.png)

## 12.1.3 Understanding Memory Addresses

Every variable in a C program occupies a unique memory location, identified by its memory address. A pointer is a variable that stores a memory address. We must differentiate between the pointer itself, the memory address that it holds, and the value stored at that address.

When working with pointers, assigning the address of a variable to a pointer is valid, but assigning the variable is not. For example:

```c
ptr = &num; // Valid, assigns the address of num to ptr
ptr = num; // Invalid, trying to assign the variable num to ptr
```

For the curious, you can print the memory address stored in a pointer using the %p specifier in the printf() function. This is useful when you want to verify the memory address stored in a pointer or to understand how pointers work in C.

## 12.1 Introduction to Pointers

181

```c
#include <stdio.h>

int main() {
    int num = 5;
    int *ptr = &num;

    printf("Pointer Value: %p\n", ptr);
    return 0;
}
```

In this example, the %p format specifier is used to print the memory address stored in the ptr pointer. The output of this code will be similar to this:

Pointer Value: 0x7ffce6501fc

Note that the memory address printed may vary from machine to machine, depending on available memory and memory allocation. In the given example, the address has 16 hexadecimal digits, since the code is running on a 64-bit machine. However, for the sake of simplicity, we will use shorter addresses in this chapter as examples.

## 12.1.4 Accessing the Value Stored at a Pointer Address

Dereferencing is the process of accessing the value stored at the memory location pointed to by a pointer. It is done using the dereference (or direction) operator (*). It allows you to indirectly access the value at the pointer's target address. For example:

```c
int num = 5;
int *ptr = &num; // Pointer ptr points to the memory address of
```

```c
printf("Value of num: %d\n", num);    // Output: Value of num: 5
printf("Value of ptr: %d\n", *ptr);   // Output: Value of *ptr: 5
```

Here, ptr holds the memory address of num. The dereference operator allows you to access the value of num using the ptr. We can read "*ptr" as "the value pointed to by ptr".

Another example:

```c
int a = 88;
int *ip, b;
ip = &a;
b = *ip; // Dereferencing ip to access the value of a
```

```c
printf("Value of b: %d\n", b);    // Output: Value of b: 88
```

In this example, a and b are integer variables, and ip is a pointer to an integer. By dereferencing, we assign b with the value stored at the memory address pointed to by ip, which is 88 in this case. See Fig. 12.2 for a clearer picture.

## Chapter 12. Pointers

| int a = 88; | int *ip; | ip = &a; | b = *ip; |
| :--- | :--- | :--- | :--- |
| 88 | *ip | Address of a | 88 |

Figure 12.2: Dereferencing a pointer

a
*ip
ip pointer to Integer
ip now points to a
b
*ip is value pointed by ip

## 12.2 Pointer Arithmetic

Pointer arithmetic is the process of performing arithmetic operations on pointers. The size of the data type being pointed to determines the size of the increment or decrement. The most commonly used pointer arithmetic operations involve the increment (++) and decrement (--) operators. These operators increase or decrease the pointer by the size of the data type it is pointing to. For example, consider a string:

```c
char string[] = "Kucing oben";
char *strptr;
```

```c
// Pointer strptr to the second character: 'u'
strptr = &string[1];
```

```c
// Outputs: Character at strptr: 'u'
printf("Character at strptr: %c\n", *strptr);
```

```c
// Incrementing strptr moves it to the next character
strptr++;
```

```c
// Outputs: Character at strptr after increment: 'c'
printf("Character at strptr after increment: %c\n", *strptr);
```

Here, ptr initially points to the second character in the string. Incrementing ptr moves it to the next element in the array by the increment operator. For instance, consider an integer array:

```c
int arr[] = {10, 20, 30, 40, 50};
// Pointer ptr points to the first element of the array
int *ptr = arr;
```

```c
// Outputs: Value at ptr: 10
printf("Value at ptr: %d\n", *ptr);
```

```c
// Incrementing ptr moves it to the next element in the array
ptr++;
```

## 12.3 Pointers and Arrays

```c
// Outputs: Value at ptr after increment: 20
printf("Value at ptr after increment: %d\n", *ptr);
```

Here, ptr initially points to the first element of the array. Incrementing ptr to the next element in the array, resulting in it pointing to the value 20.
