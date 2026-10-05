
# Object-Oriented Programming with C++

## Summary

Streams are nothing but a flow of data from program variables. Input stream is the flow of data from a file on the permanent storage medium to program variables. The keyboard is also treated as source of input stream. Output stream is the flow of data to a file on the permanent storage medium from program variables. The monitor is also treated as target for output streams.

C++ provides us with a hierarchy of classes to implement various aspects of stream handling. The class ios is the base class in this hierarchy.

The class ostream is derived from the class ios and handles the general output. The operator (<<) is derived and overloaded in the class stream to handle output streams from program variables to output.

The class ostream_with_base is derived from the class ostream. cout is an object of the class ostream which stands for console output. As mentioned earlier, C++ treats all peripheral devices as streams. It treats nothing but a file (for input) streams. The object cout monitors the screen.

The class istream is derived from the class ios and handles the general input streams. The extraction operator (>>) is defined and overloaded in the class stream to handle input streams from files to program variables.

The class istream_with_base is derived from the class cin. cin is an object of the class istream_with_base. cin stands for console input. C++ treats all peripheral devices as streams. It treats the keyboard also as a file (for input). The object cin represents the keyboard.

The class iostream is derived by multiple inheritance from the classes istream and ostream. It has the functionality to handle both input and output streams. The class ofstream is derived from the class stream. It has the functionality to handle output streams to disks. The class fstream is derived from the class istream. It has the functionality to handle both input and output streams from files to disks.

In text mode, numeric data that exists in base 2 format in the memory variables, is first converted to base 10 before being output. In binary mode, no such conversion exists.

In text mode input, numeric data that is being input into a memory variable is reckoned to be in base 10 format. Therefore, it is first converted into base 2 format and then stored in the target variable.

The insertion operator is used to output in text mode. The put() function is used to output a single character at a time. The get() function is used to use in data to input a single character at a time.

The write() function is used to output in binary mode. The read() function is used to input data in binary.

Apart from the constructors of the library classes, the open() function can also be used to open files. The first parameter of the constructor and the open() function is the name of the file. The second parameter specifies the mode. Destructors of stream classes close the files associated with any stream. The close() function can be used to explicitly close files.

Files can be moved by the seekp() and seekg() functions. Their current positions are determined by the tellp() and tellg(). An intermediate record can be directly accessed by the seeking() or seek() function to make the file pointer jump to a specific byte in the file. It is necessary for member functions for outputting and inputting data of complex cases.

Every object of the istream, or of a class that is derived from either of these classes, contains three flags that indicate the state of the next file. These flags are:

- eof becomes true if the file is end of input (the eof flag).
- fail becomes true if the read/write operation fails. The fail() function returns the state of the failbit flag.
- bad becomes true if the file is being corrupt during recovery (the bad() function returns the state of the badbit flag).

The clear() function is used to clear the bits described. C++ provides several pre-defined manipulators. The programmer can create his own application-specific manipulators.

![](img/5bfa77b13fdaa376725789bb8c00ee79_221_0.png)

# Stream and File Handling

Command line arguments are values that are passed to executables when they are run from the command line. They enable programs to capture input values from the user and other systems.

The first argument gives us the number of arguments present on the command line, including the name of the executable. It is known as the argument counter. The second argument is an array of character pointers. Each pointer to a separate command line argument. It is known as the argument vector.

The main() function can be programmed to read command line arguments. We need to define the header of the main() function as follows:

```
void main(int argc, char * argv[])
```

# Key Terms

- streams: standard stream handling classes of C++
- ios:
  - ostream
  - ostream_with_base
  - istream
  - istream_with_base
  - iostream
  - ofstream
  - ifstream
- text mode input/output
- out: insertion operator
- put() function
- cin: extraction operator
- get() function
- write() function
- read() function
- open() function
- close() function
- seekp() function
- seek-g() function
- tellp() function
- tell-g() function
- eof() and the eof flag
- fail() and the failbit flag
- bad() and the badbit flag
- clear() function
- manipulators

# Exercises

1. Briefly describe the class hierarchy provided by C++ for stream handling.
2. State true or false.
   (a) a cout is an object of the class ostream_with_base.
   (b) The insertion operator (<<) is defined and overloaded in the class stream.
   (c) The insertion operator outputs in binary mode.
   (d) The header file istream.h is included in the stream.
3. What are text and binary input/output? What are their strengths and weaknesses?
4. What is the difference between a text file and a binary file?
5. Why are command line arguments important?
6. How are values of various types output to disk using the insertion operator?
7. Can a file be opened for reading and writing?
8. What is the difference between the constructor of the stream and the open() function?
9. Explain the prototype.
10. Describe how the contents of a disk file can be randomly accessed in C++.
11. Describe the circumstances under which each of the flags--eofbit, failbit, and badbit--becomes true.
12. Describe use of the following manipulators:
    - setw()
    - precision()
    - setfill()
    - setiosflags()
    - resetiosflags()
13. How can a programmer define his/own manipulators?
14. What are command line arguments?
15. How can the main() function be programmed to read command line arguments?
16. Write a program to obtain as many integers from user as she wants and write them into a disk file. After the user has finished the integers, read them from the file and display them on the monitor.
17. Create a class objects would hold linked lists of integers. the objects would also have the necessary functionality to download their data into a specified disk file and upload their data from specified disk files. The application will be menu-driven. the user will have the option to save the linked list and to 'save as' the linked list.
18. Write a manipulator that fixes a currency symbol to the output value. For this, the manipulator should read the symbol from a disk file.
19. Write a program that gives an error message if the number of arguments passed to the executable is not equal to 1 (hint: 'arg' != 2), and then terminates itself. The error message should advise the user that exactly one argument should be passed to the executable, and it should be the name of a file.
20. Otherwise, if the user has passed exactly argument to the executable, the program should open the file whose name matches the value of argument (hint: argv[1]). It should then append the name of the executable (hint: argv[0]) to a new line in the file. For example, if name of the executable is test, then the following line should get appended to the file:

Hint:
Create two classes as follows:

```
class intNode
{
  int data;
  intNode * Next;
public:
  //functions to set and get the data
  members
};

```

class intList
{
intNode * head;
public:
  //functions to add, delete, modify,
  save and load
};
