The buf argument points to the memory in which the read data will be stored. The count argument specifies how many bytes will be read from the file.

> Because two systems differ (e.g., in the size of types), there is no guarantee that a file written with the write() function will be read correctly with the read() function in another system.

In the following example, a double number is read and stored in d:

```
double d;
ifstream fin("test.dat", ios_base::in ios_base::binary);
fin.read((char*)&d, sizeof(d));
```

In the next example, 1000 integers are read and stored in arr:

```
int arr[1000];
fin.read((char*)arr, sizeof(arr));
```

> It is safer to use write() and read() with binary rather than text files, because potential translations of the new line character can cause unexpected results.

For example, suppose we use write() to write a string of 50 characters in a text file and the value of count is set to 50. If the program runs in Windows and the string contains line character(s), the replacement(s) with the \r\n pair would make its size more than 50; therefore, write() won't write the entire string.

As we will see in the following examples, write() and read() are often used with objects that occupy the same amount of memory. As we said, when we store an object in the file only the data members are stored and not its functions. However, be careful with classes that use virtual functions. As we know, with virtual functions, there is a hidden pointer that points to the array which contains the pointers to the virtual functions. This hidden pointer will be stored in the file. The next time we run this program this array may be stored in a different memory location, if we read the file, the value of the hidden pointer will change to the one stored in the file. Thus, the pointer will get an invalid value, which may cause the program to crash.

# EXERCISES

C.24.8 Write a program that declares an array of 5 integers with values 10, 20, 30, 40, and 50 and writes them in a binary file. Then, the program should read an integer and replace the third integer with the input number. The program should read and display the file's content before it ends.

```
#include <iostream>
#include <fstream>
#include <cstdlib>
using namespace std;
```