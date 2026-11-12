# Use the program below for problems #15 – #16

```
#include<stdio.h>
#define SIZE 8
int main(void)
{
   int i;
   int index;
   int data[SIZE] = {3, 8, 9, 2, 5, 4, 1, 7};
   for(i = 0; i < SIZE; i++)
   {
      index = data[i];
      data[index % SIZE] += 1;
   }
   return(0);
}
```

15. Which of the following values is found at index 1 of the array after the termination of the loop in the program above?
A) 8
B) 9
C) 10
D) None of the above.

16. How many of the elements in the array above were not changed by the loop in the program above?
A) Three elements.
B) Two elements.
C) Four elements.
D) None of the above.

17. Which of the following statements regarding arrays in the C programming language is TRUE?
A) All arrays sent to a given user-defined function must be of the same defined size.
B) The name of an array is the address of the first element in the array.
C) When passing a whole array to the function the total size of the array is necessary in the definition of the called function.
D) None of the above.

18. Which of the following statements regarding arrays in the C programming language is FALSE?
A) An expression of any data type may be used as an index for an array.
B) When accessing an array element the gcc compiler does not verify that the index is within the defined range of a given array.
C) The index value represents an offset from the beginning of the array to the element being referenced.
D) None of the above.

19. Which of the following statements regarding data type conversions is TRUE?
A) Assignment type conversions occur only when the programmer specifically requests them.
B) Explicit type conversions cannot result in the loss of data.
C) Implicit type conversions occur in a mixed-type expression according to the data types of each operand and the precedence of each operator.
D) None of the above.