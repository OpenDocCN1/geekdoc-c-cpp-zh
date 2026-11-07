```
outFile.write( reinterpret_cast<const char * > (&number ),
    sizeof( number ) );
```

which always writes the binary version of the integer number’s four bytes (on a machine with four-byte integers). Function write treats its first argument as a group of bytes by viewing the object in memory as a const char *, which is a pointer to a byte. Starting from that location, function write outputs the number of bytes specified by its second argument—an integer of type size_t. As we’ll see, stream function read can subsequently be used to read the four bytes back into integer variable number.

# Converting Between Pointer Types with the reinterpret_cast Operator

Unfortunately, most pointers that we pass to function write as the first argument are not of type const char *. To output objects of other types, we must convert the pointers to those objects to type const char *; otherwise, the compiler will not compile calls to function write. C++ provides the reinterpret_cast operator for cases like this in which a pointer of one type must be cast to an unrelated pointer type. Without a reinterpret_cast, the write statement that outputs the integer number will not compile because the compiler does not allow a pointer of type int * (the type returned by the expression &number) to be passed to a function that expects an argument of type const char *—as far as the compiler is concerned, these types are inconsistent.

A reinterpret_cast is performed at compile time and does not change the value of the object to which its operand points. Instead, it requests that the compiler reinterpret the operand as the target type (specified in the angle brackets following the keyword reinterpret_cast). In Fig. 14.11, we use reinterpret_cast to convert a ClientData pointer to a const char *, which reinterprets a ClientData object as bytes to be output to a file. Random-access file-processing programs rarely write a single field to a file. Typically, they write one object of a class at a time, as we show in the following examples.

> **Error-Prevention Tip 14.4**  
> It’s easy to use reinterpret_cast to perform dangerous manipulations that could lead to serious execution-time errors.

![](bbox=[0.134, 0.595, 0.19, 0.63])

> **Portability Tip 14.1**  
> reinterpret_cast is compiler dependent and can cause programs to behave differently on different platforms. Use this operator only if it’s absolutely necessary.

![](bbox=[0.134, 0.666, 0.19, 0.702])

> **Portability Tip 14.2**  
> A program that reads unformatted data (written by write) must be compiled and executed on a system compatible with the program that wrote the data, because different systems may represent internal data differently.

![](bbox=[0.134, 0.735, 0.19, 0.77])

# Credit Processing Program

Consider the following problem statement:

> Create a credit-processing program capable of storing at most 100 fixed-length records for a company that can have up to 100 customers. Each record should consist of an account number that acts as the record key, a last name, a first name and a balance. The program should be able to update an account, insert a new account, delete an account and insert all the account records into a formatted text file for printing.