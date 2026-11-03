It is especially important to use the sizeof operator to accurately discover the amount of memory allocated for user-defined structures that have members of different data types, as “padding” is often automatically added. This means that total memory allocation may exceed the sum allocated to each member. It might seem reasonable to expect that a structure comprising member variables int score and char grade will be allocated total memory of 5 bytes (4+1), but the total allocation will typically be 8 bytes. This is because computer systems like to read and write data in “word”-sized chunks of 4 bytes each. So, padding gets added to make the memory allocation a multiple of four each.

> Always enclose an operand supplied to the sizeof operator within parentheses for code consistency.

![](bbox=[0.05, 0.28, 0.25, 0.38])

+   1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
+   #include <stdio.h>

```
int main()
{
 int num = 1234567890 ;
}
```

+   2. Add a main function that declares and initializes a single integer variable

```
printf("Size of int data type is %d bytes\n", sizeof(int));
printf("Size of int variable is %d bytes\n", sizeof(num ));
```

+   3. Next, in the main function block, insert statements to reveal the memory allocated to the int data type (in this implementation) by type name and object name