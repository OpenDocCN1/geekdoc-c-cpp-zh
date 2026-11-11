![](bbox=[0.181, 0.11, 0.687, 0.419])

**Figure 15.17:** Syntax to use read and write functions

It is important to note that each of the functions require the programmer to cast the address of the variable read/written to be casted into a character pointer. This is because, although we are reading and writing the data in the binary form, the file pointer will still continue to progress byte by byte. Hence, the address of the variable whose value is to be transferred must be casted into a char pointer as char is 1 byte in size. Further, the function will also need to know, how many bytes are to be transferred between the file and the program. Therefore, the second argument should give the size of the variable in bytes to be written or read to/from the file. We will generally use a function sizeof () to determine the size of variable to be transferred as shown in the Figure 15.17.

As an example, the program given below writes the values of two variables a and b to the file named Values.dat, using the write function. The program again opens the same file in the read mode, using ifstream and reads back the values, which were written before into variables c and d. As an evidence, we have read back the values correctly, the program prints the values of c and d on the computer screen using cout. You can see that the first value read from the file goes in the variable c and the second value read from the file goes in the variable d. This is because the value of the variable a was written before the value of the variable b. Hence, you can see in the output that the variable c contains the same value as that of variable a, and the variable d contains the same value as that of the variable b.

```
```cpp
#include<iostream.h>
#include<fstream.h>
void main()
{
```
```