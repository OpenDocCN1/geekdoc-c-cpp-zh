# CONTENTS OF APPENDED FILE

| Name | Code | Cost |
|---|---:|---:|
| AA | 11 | 100 |
| BB | 22 | 200 |
| CC | 33 | 300 |
| DD | 44 | 400 |
| XX | 99 | 900 |
| YY | 10 | 101 |

Number of objects = 6
Total bytes in the files = 96
Enter object number to be updated
6
Enter new values of the object
Enter name: ZZ
Enter code: 20
Enter cost: 201

# CONTENTS OF UPDATED FILE

| Name | Code | Cost |
|---|---:|---:|
| AA | 11 | 100 |
| BB | 22 | 200 |
| CC | 33 | 300 |
| DD | 44 | 400 |
| XX | 99 | 900 |
| ZZ | 20 | 201 |

We are using the **fstream** class to declare the file streams. The **fstream** class inherits two buffers, one for input and another for output, and synchronizes the movement of the file pointers on these buffers. That is, whenever we read from or write to the file, both the pointers move in tandem. Therefore, at any point of time, both the pointers point to the same byte.

Since we have to add new objects to the file as well as modify some of the existing objects, we open the file using **ios::ate** option for input and output operations. Remember, the option **ios::app** allows us to add data to the end of the file only. The **ios::ate** mode sets the file pointers at the end of the file when opening it. We must therefore