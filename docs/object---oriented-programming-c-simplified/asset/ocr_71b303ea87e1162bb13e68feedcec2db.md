# 138 Object-Oriented Programming C++ Simplified

Enter ptr[2] element : 8
Enter ptr[2] element : 92

Matix is
1 2 3
4 5 6
7 8 92

Max of each row is as follows
Row1->3
Row2->6
Row3->92

EXPLANATION : To create a 2-D array dynamically we will have to take a double pointer. Initially the pointer ptr points to memory allocated for 3 rows. The statement ptr= new int *[row]; creates an array of pointer of size row. As each of the row will consists of a 1-D array of 3 elements so using for loop for the number of row (3 in output) we allocated memory for columns (Here 3 in output) using 
for(i=0; i< row; i++)
ptr[i] = new int [col];

We are having three rows here so ptr[0] points to first 1-D array, ptr[1] points to the second 1-D array and ptr[2] points to the third 1-D array. Now, the pointer ptr can be treated as a 2-D array (combination of three 1-D array). To access any of the element we can write say ptr[i] [j] or *(*(ptr+i) +j).

For finding maximum of each row we have created a dynamic array max of size row. Initially first element of each row is considered as maximum. Then running a for loop for each row we find maximum of element of the row.

To delete the 2-D array we write delete [] ptr. This statement first de-allocates memory each row and later deletes pointer itself.

```
/*PROG 4.20 DYNAMIC ARRAY OF STRINGS */
#include <iostream.h>
#include <conio.h>
void main( )
{
 int n,i;
 clrscr();
 cout << "Enter how many strings \n ";
 cin > n;
 char **ptr = new char*[n];
 int *len=new int [n];
```