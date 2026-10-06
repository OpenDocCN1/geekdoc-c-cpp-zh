elements in the sequence associative container, in order to keep the ordered ar-angement of the data, we should ensure that if the insertion fails, the container elements wont be changed. For the remove operation, we should guarantee the success of the operation. For example, to list a container, all operations besides remove(), remove_if(), merge(), sort(), and unique() should be successful, or we should ensure that the container remains the same.

+   For containers based on array implementation, if the addition of elements fails, we must make a backup of all elements after the insert point before to recover the initial state of the container. This can be time consuming. For functions push() and pop(), since they operate on the tail element of the container, we need not back up any element. Once the exception occurs, these two functions can ensure that the container returns to the original state.

# 12.5 Program Example Improvement to Personal Information Administration Program in a Small Company

As in the previous chapters, we take the personal information management program as an example. When accessing the disk file containing personal information, if the file does not exist, the problem cannot be processed. To handle this error condition, we add the exception handling facility to file access in Example 11.11 in Chapter 11. When accessing a file, if it does not exist, the program will throw an exception and quit. If we use a VC++ development environment, 12_3.cpp and employee.cpp should be connected together after compiling. If we use in the same project.

Example 12.3: Personal Information Management.
Here, the program reads and displays the personal information stored in a disk file. If we access files, we use the exception handling facility to solve the problem.

```
//12_3.cpp
#include <iostream>
#include <fstream>
//include the header file of file stream
#include "employee.h"
using namespace std;

class FileException { //file exception handling class
public:
    FileException()
    : message( "File is not created! ) {} {}
    const char *what() const { return message; }
private:
```