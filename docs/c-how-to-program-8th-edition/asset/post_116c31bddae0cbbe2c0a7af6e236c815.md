
Client) to the file. Line 231 displays a message to inform the user that the record has been deleted. A typical output for Option 4 is

```
Enter account to delete (1 – 100): 29
Account #29 deleted
```

Line 25 opens the `credit.dat` file by creating an `fstream` object for both reading and writing, using modes `ios::in` and `ios::out` “or-ed” together.

## 17.11 Object Serialization

This chapter and Chapter 15 introduced the object-oriented style of input/output. However, our examples concentrated on I/O of fundamental types rather than objects of user-defined types. In Chapter 11, we showed how to input and output objects using operator overloading. We accomplished object input by overloading the stream extraction operator, `>>`, for the appropriate `istream`. We accomplished object output by overloading the stream insertion operator, `<<`, for the appropriate `ostream`. In both cases, only an object’s data members were input or output, and, in each case, they were in a format meaningful only for objects of that particular type. An object’s member functions are *not input or output with the object’s data; rather, one copy of the class’s member functions remains available internally and is shared by all objects of the class.*

When object data members are output to a disk file, we lose the object’s type information. We store only the values of the object’s attributes, not type information, on the disk. If the program that reads this data knows the object type to which the data corresponds, the program can read the data into an object of that type as we did in our random-access file examples.

An interesting problem occurs when we store objects of different types in the same file. How can we distinguish them (or their collections of data members) as we read them into a program? The problem is that objects typically do *not* have type fields (we discussed this issue in Chapter 13).

One approach used by several programming languages is called **object serialization**. A so-called **serialized object** is an object represented as a sequence of bytes that includes the object’s data as well as information about the object’s type and the types of data stored in the object. After a serialized object has been written to a file, it can be read from the file and **deserialized**—that is, the type information and bytes that represent the object and its data can be used to recreate the object in memory. C++ does not provide a built-in serialization mechanism; however, there are third party and open source C++ libraries that support object serialization. The open source Boost C++ Libraries (www.boost.org) provide support for serializing objects in text, binary and extensible markup language (XML) formats (www.boost.org/libs/serialization/doc/index.html). We overview the Boost C++ Libraries in Chapter 23.

## 17.12 Wrap-Up

In this chapter, we presented various file-processing techniques to manipulate persistent data. You were introduced to the differences between character-based and byte-based streams, and to several file-processing class templates in header <fstream>. Then, you learned how to use sequential file processing to manipulate records stored in order, by a record-key field. You also learned how to use random-access files to “instantly” retrieve and manipulate fixed-length records. We presented a substantial transaction-processing program using a random-access file to achieve “instant-access” processing. Finally, we discussed the basic concepts of object serialization. In the next chapter, we discuss typical string-manipulation operations provided by class template basic_string. We also introduce string stream-processing capabilities that allow strings to be input from and output to memory.

## Summary

### Section 17.1 Introduction

- Files are used for data persistence (p. 659)—permanent retention of data.
- Computers store files on secondary storage devices (p. 659), such as hard disks, CDs, DVDs, flash memory and tapes.

### Section 17.2 Files and Streams

- C++ views each file simply as a sequence of bytes.
- Each file ends either with an end-of-file marker (p. 659) or at a specific byte number recorded in a system-maintained, administrative data structure.
- When a file is opened, an object is created, and a stream is associated with the object.
- To perform file processing in C++, headers <iostream> and <fstream> must be included.
- Header <fstream> (p. 659) includes the definitions of the stream classes templates basic_ifstream (for file input), basic_ofstream (for file output) and basic_fstream (for file input and output).
- Each class template has a predefined template specialization that enables char I/O. The <fstream> library provides typedef aliases for these template specializations. The typedef ifstream represents a specialization of basic_ifstream that enables char input from a file. The typedef ofstream represents a specialization of basic_ofstream that enables char output to files. The typedef fstream (p. 659) represents a specialization of basic_fstream that enables char input from and output to files.
- The file-processing templates derive from class templates basic_istream, basic_ostream and basic_iostream, respectively. Thus, all member functions, operators and manipulators that belong to these templates also can be applied to file streams.

### Section 17.3 Creating a Sequential File

- C++ imposes no structure on a file; you must structure files to meet the application’s requirements.
- A file can be opened for output when an ofstream object is created. Two arguments are passed to the object’s constructor—the filename (p. 661) and the file-open mode (p. 661).
- For an ofstream (p. 661) object, the file-open mode can be either ios::out (p. 661) to output data to a file or ios::app (p. 661) to append data to the end of a file. Existing files opened with mode ios::out are truncated (p. 661). If the specified file does not exist, the ofstream object creates the file using that filename.
- By default, ofstream objects are opened for output.
- An ofstream object can be created without opening a specific file—a file can be attached to the object later with member function `open` (p. 662).
- The `ios` member function `operator!` determines whether a stream was opened correctly. This operator can be used in a condition that returns a true value if either the `failbit` or the `badbit` is set for the stream on the open operation.
- The `ios` member function `operator void *` converts a stream to a pointer, so it can be compared to 0. When a pointer value is used as a condition, a null pointer represents false and a non-null pointer represents true. If the `failbit` or `badbit` has been set for a stream, 0 (false) is returned.
- Entering the end-of-file indicator sets the `failbit` for `cin`.
- The `operator void *` function can be used to test an input object for end-of-file instead of calling the `eof` member function explicitly on the input object.
- When a stream object’s destructor is called, the corresponding stream is closed. You also can close the stream object explicitly, using the stream’s `close` member function.

### Section 17.4 Reading Data from a Sequential File

- Files store data so it may be retrieved for processing when needed.
- Creating an `ifstream` object opens a file for input. The `ifstream` constructor can receive the file-name and the file open mode as arguments.
- Open a file for input only if the file’s contents should not be modified.
- Objects of class `ifstream` are opened for input by default.
- An `ifstream` object can be created without opening a specific file; a file can be attached to it later.
- To retrieve data sequentially from a file, programs normally start reading from the beginning of the file and read all the data consecutively until the desired data is found.
- The member functions for repositioning the file-position pointer (p. 665) are `seekg` (“seek get”; p. 665) for `istream` and `seekp` (“seek put”; p. 665) for `ostream`. Each `istream` has a “get pointer,” which indicates the byte number in the file from which the next input is to occur, and each `ostream` has a “put pointer,” which indicates the byte number in the file at which the next output should be placed.
- The argument to `seekg` (p. 665) is a long integer. A second argument can be specified to indicate the seek direction (p. 665), which can be `ios::beg` (the default; p. 665) for positioning relative to the beginning of a stream, `ios::cur` (p. 665) for positioning relative to the current position in a stream, or `ios::end` (p. 666) for positioning relative to the end of a stream.
- The file-position pointer (p. 665) is an integer value that specifies the location in the file as a number of bytes from the file’s starting location (i.e., the offset (p. 666) from the beginning of the file).
- Member functions `tellg` (p. 666) and `tellp` (p. 666) are provided to return the current locations of the “get” and “put” pointers, respectively.

### Section 17.5 Updating Sequential Files

- Data that is formatted and written to a sequential file cannot be modified without the risk of destroying other data in the file. The problem is that records can vary in size.

### Section 17.6 Random-Access Files

- Sequential files are inappropriate for instant-access applications (p. 670), in which a particular record must be located immediately.
- Instant access is made possible with random-access files (p. 670). Individual records of a random-access file can be accessed directly (and quickly) without having to search other records.
