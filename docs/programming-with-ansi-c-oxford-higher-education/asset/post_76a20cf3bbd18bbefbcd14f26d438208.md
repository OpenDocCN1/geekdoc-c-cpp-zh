
## 13.11 OBJECT PERSISTENCE AND SERIALIZING

Serializing is a process of storing and retrieving of objects on and from auxiliary devices. The objects that can be stored and retrieved later are known as persistent objects. Serializing is not available to C++ programmers directly. The objects have to be written in a binary file as was done using the customer file in earlier cases. Writing to and reading from binary files do not make objects serialized. The object states and their dependencies are also to be preserved. Binary files are just the beginning.

It is important to note that when objects are written to a file, it is similar to writing a struct variable to the file. The functions that are provided with the class are stored neither with the objects stored in the main memory (normal objects with which we have dealt so far) nor with the objects stored in a file. Any virtual base class information (such as the information whether a specific function is virtual or not, or which objects are embedded in a class with similar values) cannot be stored. Using the built-in features of C++, it is impossible to store an object with its status values and extract it later after restarting the program.

The problem of object persistence becomes more complicated while dealing with polymorphic objects, because objects do not bear any ‘type’ tag. For example, if a few letters and a few memos are stored as document object (a parent object from which letters and memos are derived), there is no way to differentiate between them once stored. The simplest possible solution is to store documents and memos in the file. Unfortunately, vptr is not stored in the file and that information is lost. The entire inheritance chain information is just lost. Even when there are embedded objects, the trace of vptr of those objects and the related values are lost. When one wants this process by the base class pointer, it becomes more difficult as one needs to store different vptr entries for each inherited class. How can a C++ programmer provide serialization of professional degree is difficult to explain here, but one can visualize the difficulty of the task. Some of the other object-oriented programming languages, most notably Java, provide serialization.

Why would one like to store objects in the auxiliary devices? It is because one would like to preserve the status of the object. For example, if there is a TeachingStaff object derived from an employee object where the designation is changed from Professor to Director and one would like to have that information available the next time onwards. Assume the program is printing salary slips of employees; it can use this information to print the proper salary slips. If an employee pointer is being used to access the different types of employees, the change in the object of a specific person must be noted, which is not possible in C++ directly. There is no method in C++ to identify objects uniquely. All standard extensions provide some form of wrapping, which adds an identifier and a few other important information that one can use to provide serialization.

C++ cannot provide persistent objects; so, programmers must adopt solutions with object identification and a few other tricks in order to get this feature.

The process of serialization relates to storing and retrieving objects and retaining their status during storage and retrieval. Such objects are known as persistent objects. C++ does not provide any facility for serialization.

## 13.12 I/O ERRORS

The OS has to be requested for file handles and disk space for the files. In most of the cases, the OS complies with the requests; however, it might not comply in some specific cases. It is actually the programmer’s responsibility to check whether the operation is successfully completed or not. Let us enumerate a few such cases here.

One must test for errors after different file operations. C++ has no default mechanism to check and correct errors.

Error handling is possible by calling functions such as fail() or is_open() or by testing the return value of most of the I/O functions.

- 1. When one is providing paths in phrases such as Customer.dat, the OS looks at the current directory to find that file. The current directory is different when the program is running elsewhere. If the path is not provided to retrieve the file in different situations, the same program running fine at one place will not be able to work at another place.
- 2. While working with multi-user OS such as Linux or Windows 2000, it is also important to know that files can be created or read only where there is a permission to write or read, respectively. The same program running perfectly on one machine or one account might just not work on another.
- 3. A program copied from one user account to another might not work as expected in the other user account on the same machine because of permission restrictions for different files and folders to different users.

The errors can be checked in the following ways:

- 1. While opening a file:
  - (a) A function is_open() is available to all file objects. It is possible to write
  if(filename.is_open())
  to check whether a file has opened or not after an open() call.

  ```
  if(filename.is_open())
  ```
  - (b) One can open the file using ios::nocreate option when one does not want the file to be accidentally overwritten, if it already exists. This option ensures that a file is created only when there is no such file.
  - (c) One can open the file using ios::noreplace option when one does not want to generate a new file if an old file with the same name exists.
- 2. While reading or writing a file:
  - (a) Both read() and write(), when successful, return the stream, and return zero otherwise. Adding read() and write() inside the if statement’s condition part is also a common practice. It is done as follows:

  ```
  if(MCA_StudFile_In.read((char*) &MCA_Student_In, sizeof(struct student)))
  {
      // Actions to be taken
  }
  else
  {
      // Actions to be taken when error occurs
  }
  ```

  This construct automatically checks for errors and there is no need to write specific code for finding whether an error has occurred or not.
  - (b) After executing a read() or write() statement, one can check whether it has failed by calling the function fail(). It is done as follows:

  ```
  MCA_StudFile_In.read((char*) &MCA_Student_In, sizeof(struct student));
  if(MCA_StudFile_In.fail())
      break;
  ```

  The fail() function is quite generic. One can call fail() after any file-related operation to check whether the operation was successful or not.

## RECAPITULATION

- I/O is a special operation as the program needs to take the help of the OS and other devices to perform.
- For providing I/O, an I/O library is used in C++. The I/O library helps in the portability of the program.
- A file on the auxiliary device has minimum four operations possible; they are open(), read(), write(), and close().
- The files mechanism is provided in C++ by the <fstream> header. It has two different mechanisms to open files, one using constructors and the other using the open() function.
- Text and binary are the two different streams provided.
- Text is more portable than binary, but binary is preferable for commercial programs.
- It is also possible to use get() and put() functions on text stream for reading and writing single characters.
- It is possible to use getline() for reading a single line.
- Binary files require read() and write() functions for reading from and writing in a file.
- seekg() and seekp() are functions for seek in the read and the write modes, respectively.
- tellp() and tellg() are functions for tell in the write and read modes, respectively.
- C++ does not provide object serialization.

## KEYWORDS

Binary files
Files containing integers in binary and other data in ASCII format are known as binary files.

eof()
This denotes the end of a file. In text file, it is indicated by a special character. In binary files, this is determined implicitly using the length of the file.

File pointer
This term has two different meanings in two different contexts. When we are dealing with file handles to access files, a file handle is sometimes referred to as the file pointer. In C, conventionally, the file handle is called the file pointer and is usually written as FILE *fp; where fp is actually a handle but called a pointer. Another meaning of file pointer is a place in the file where the next read or write is to take place.

I/O modes
These are the different modes such as read only, write only, read-write, and append in which we can open files.

Logical file name
This is the name of the file that we refer in our program.

Physical file name
This is the name of the file that is referred by the OS.

seekg() and seekp()
These are similar to the seek pointer in C. 'g' indicates get() or read() and 'p' indicates put() or write(). Thus, seekg() is for seeking while reading, whereas seekp() is for seeking while writing

Seek
This is an operation to move the file pointer (second definition above) to the place we want.

Serialization
This is the process of placing the objects in auxiliary memory for later retrieval and later getting them back as it is.

Text files
Files containing integers and other data in ASCII format are known as text files.

tellg() and tellp()
These are similar to the tell pointer in C. 'g' indicates get() or read() and 'p' indicates put() or write(). Thus tellg() is for indicating the file position while reading, whereas tellp() is for indicating it while writing.

## EXERCISES

## Multiple Choice Questions

1. The logical and the physical file needs to be ________ to enable a programmer to work on that file.
(a) created
(b) executed
(c) associated
(d) de-referenced

2. ________ helps read and write operations to be carried out in bulk.
(a) File handle
(b) File pointer
(c) File buffers
(d) Any of the above
