# EXERCISES 13.4

+   1. **(Modify)** Modify Program 13.9 to prompt the user for a name. Have the program search the existing list for the entered name. If the name is in the list, display the corresponding telephone number; otherwise, display this message: The name is not in the current phone directory.

+   2. **(Practice)** A C++ program containing a linked list of 10 integers. Have the program display the numbers in the list.

+   3. **(Data Processing)** Using the linked list of structures in Figure 13.10, write the sequence of steps for deleting the record for Edith Dolan from the list.

+   4. **(Modify)** Generalize the description in Exercise 3 to describe the sequence of steps for removing the nth structure from a list of linked structures. The nth structure is preceded by the (n−1)st structure and followed by the (n +1)st structure. Make sure to store all pointers correctly.

+   5. **(Data Processing)** a. In a doubly linked list, each structure contains a pointer to the following and previous structures in the list. Define an appropriate type for a doubly linked list of names and phone numbers.

+   b. Using the type defined in Exercise 5a, modify Program 13.9 to list the names and phone numbers in reverse order.

# 13.5 Dynamic Data Structure Allocation

You have already learned about allocating and deallocating memory space with the new and delete operators (see Section 12.2). For, Table 13.1 repeats the description of these operators.

Table 13.1 Operators for Dynamic Allocation and Deallocation

| Operator Name | Description |
| --- | --- |
| new | Reserves the amount of bytes requested by the requested data type. Returns the address of the first reserved location or NULL if not enough memory is available. |
| delete | Releases a block of bytes previously reserved. The address of the first reserved location is passed as an argument to the operator. |

Dynamic allocation of memory is especially useful when dealing with a list of structures because it permits expanding the list as new records are added and contracting the list as records are deleted. In requesting additional storage space, the user must provide the new operator with an indication of the amount of storage needed for a particular data type. For example, the expression new(int) or new int (the two forms can be used interchangeably) requests