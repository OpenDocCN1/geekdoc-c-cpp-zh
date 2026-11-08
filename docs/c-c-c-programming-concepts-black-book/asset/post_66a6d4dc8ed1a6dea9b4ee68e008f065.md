
## Chapter 15

### `underflow_error()`

This class defines the type of objects thrown as exceptions to emphasize the arithmetic underflow errors. It is designed in such a way that apart from the elements of the standard library, any program can throw it as an exception. This class may be defined as follows:

```cpp
class underflow_error : public runtime_error
{
public:
    explicit underflow_error(const string& what_arg);
};
```

### `ios_base::failure`

The standard exception class derives this embedded class, which serves as a base class for the objects thrown as exceptions by the member functions in the iostream hierarchy of classes. This class is defined within the std namespace as:

```cpp
class ios_base::failure : public exception
{
public:
    explicit failure(const string& msg);
    virtual ~failure();
    virtual const char* what() const throw();
};
```

The value of the string received as the `msg` parameter in the constructor `explicit failure(const string& msg)` is internally stored and its C-string equivalent is returned by subsequent calls to `what()`. It effectively calls its parent class's constructor (`exception::exception`). The destructor `virtual ~failure()` has no operation. The declaration `virtual const char* what() const throw()` returns the C-string value equivalent to the `msg` argument used on its construction.

Let’s now summarize the main points discussed in this chapter.

### Summary

In this chapter, we have learnt about I/O streams and exception handling. In I/O streams, we have discussed the advantages of the Stream classes, the Stream class hierarchy, explicit file opening and closing, disk I/O using member functions, random access, and manipulators. In exception handling, we have discussed error handling in C and C++, the throw statement, catching an exception, re-throwing an exception, handling derived class exceptions and the standard library exception hierarchy.

### Quick Revise

### Multiple Choice Questions

- **Q1.** If a catch statement is written to catch the exception objects of a base class type, then it can also catch all the __________ derived from that base class.
  - i. Exceptions for objects
  - ii. Objects of classes
  - iii. Arguments
  - iv. Errors

- **Q2.** Which of the following is the most general exception handler that catches the exception of any type?
  - i. `catch(std::exception)`
  - ii. `catch(std::any_exception)`
  - iii. `catch(...)`
  - iv. `catch()`

- **Q3.** Which of the following is the most preferred way of throwing and handling exceptions?
  - i. Throw by value and catch by reference
  - ii. Throw by reference and catch by reference
  - iii. Throw by value and catch by value
  - iv. Throw the pointer value and provide catch for the pointer type

- **Q4.** When do we throw the `std::bad_alloc` exception?
  - i. When new operator cannot allocate memory
  - ii. When alloc function fails
  - iii. When type requested for new operation is considered bad
  - iv. When delete operator cannot delete the allocated (corrupted) object

- **Q5.** After the program terminates, any values left in the input stream are ______.
  - i. Reused
  - ii. Updated
  - iii. Discarded
  - iv. Copied

- **Q6.** We can use the stream function ______ to restore the input stream to a working state.
  - i. Restore
  - ii. Fix
  - iii. Update
  - iv. Clear

- **Q7.** A ______ is either an input stream variable or an output stream variable.
  - i. Function variable
  - ii. User-defined variable
  - iii. Common output variable
  - iv. Stream variable

- **Q8.** The extraction operator `>>` is binary; and therefore, takes ______ operand(s):
  - i. No
  - ii. One
  - iii. Two
  - iv. Three

- **Q9.** In the `cin.get` statement, `varChar`, which appears in the parentheses following the function name, is called the argument or ______ of the function.
  - i. Variable
  - ii. Parameter
  - iii. Value
  - iv. Content

- **Q10.** When we want to process only partial data, we can use the stream function ______ to discard a portion of the input.
  - i. Put
  - ii. Get
  - iii. cin
  - iv. Ignore

### Subjective Questions

- **Q1.** Write a C++ program to convert the newline-separated entries to comma-separated in a file.
- **Q2.** What problems are faced when calling a C function from a C++ function? How can we avoid it?
- **Q3.** What is the function of `tellg()`?
- **Q4.** Explain the difference between `seekp()` and `seekg()`.
- **Q5.** What is the use of file pointers? What are the two types of file pointers? Explain their use.
- **Q6.** What does the file mode parameter `ios::binary` mean?
- **Q7.** What is the difference between `ios::ate` and `ios::app` mode?
- **Q8.** In which class is the function `eof()` present?
- **Q9.** What are manipulators?
- **Q10.** What are the ways of opening a file?
- **Q11.** What are the parts of a file name?
- **Q12.** What is a stream? Define the types of stream.
- **Q13.** Write a C++ program that uses a loop to sum ten numbers read from the standard input, and then writes the sum to the standard output.
- **Q14.** Write a C++ program that includes two functions:
  - a. The `compare()` function that has three parameters: two input streams and one output stream. The function reads the characters from each of the two inputs. If the sequences of characters are the same, then it writes equal to the output stream; otherwise, it writes not equal.
  - b. The `main()` function that opens the files `Input1` and `Input2` for reading (giving an appropriate error message and quitting if either open fails), then calls the `compare()` function, passing the two input files as well as the standard output.
- **Q15.** Write a program to show that the `getline` and three-argument `get` istream member functions each end the input string with a string-terminating null character. In addition, show that `get` leaves the delimiter character on the input stream while `getline` extracts the delimiter character and discards it. What happens to the unread characters in the stream?

![](img/43c5f409f9b17790a628c4b4df854b61_504_0.png)

## Chapter 16: An Introduction to C# and .NET Architecture

| If you need information on: | See page: |
|---|---|
| Introduction to .NET Architecture | 464 |
| Class Library | 468 |
| Assemblies in C# | 471 |
| Assembly Manifest | 472 |
| Type Metadata | 474 |
| MSIL/CIL Information | 475 |
| Resource File | 475 |
| Global Assembly Cache | 476 |
| Memory Management in C# Programming | 476 |
| Introduction to C# Programming Language | 478 |
| C# Evolution | 480 |

Microsoft first came up with Active Server Pages (ASP) that provides a server-side scripting language using which a developer can create dynamically generated Web pages. This is often called classic ASP. ASP was released on the Internet Information Services 4.0 (IIS 4.0). However, it has the problem with separating the presentation and content of the code. This compelled the developers in Microsoft to come up with a platform that helps in writing a clean code.

In the year 2002, Microsoft introduced the successor of ASP known as ASP.NET. Though it is the successor, ASP.NET represents a Web application framework using which a developer can develop Web pages, Web applications, and Web services. This is built on the Common Language Runtime (CLR) platform that helps the developer to choose the languages supported by CLR to develop their Web applications. It also provides the environment of Object-Oriented Programming (OOP), garbage collection, and other features that were not supported by Microsoft's Component Object Model (COM) platform.

In the year 2000, as a response to Java, Microsoft introduced the new language C Sharp whose name was inspired by the musical note C#. This language was Microsoft’s attempt to provide a modern, general-purpose OOP language. C# embeds a large amount of system programming that helps in developing any software component. The functionalities of C# are similar to that of Java, but it is not intended to compete with C or any assembly-level language.

In this chapter, we learn about the .NET architecture, which includes CLR and class library. After that, we explore the assembly in C# as well as the memory management in C# with the help of garbage collection technique. Towards the end of the chapter, we give an introductory discussion on C# language and present a comparative study on various versions of C#.

Let’s start with the introduction to .NET architecture.

### Introduction to .NET Architecture

The .NET Framework is the main building block of .NET architecture that is introduced to develop and execute highly distributed component-based applications. It enables different programming languages to work together in the same environment. Component-based application refers to the applications that support COM, which provides inter-process communication along with the dynamic object creation in a large range of programming languages.

In the Windows platform, the .NET Framework provides security, program portability, and a common programming model to develop applications. It is widely known for its language interoperability, which can be done by using CLR. Figure 16.1 shows a simplified view of the .NET architecture:

![](img/43c5f409f9b17790a628c4b4df854b61_505_0.png)

**Figure 16.1: Displaying the Simplified View of .NET Architecture**

As shown in Figure 16.1, during the execution of C# code, the code first references a class library, which provides a set of namespaces that are deployed in a shared library known as an assembly. Both the class library and the assembly are Dynamic Link Library (DLL) files. After that, the code encounters the CLR that converts it into the machine-level language. At the end, the code is executed with the help of the operating system. This is the simplified model; however, C# code needs to get through several other components, such as Common
