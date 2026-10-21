
## Programming with ANSI C++

3. We have seen one case in the text where virtual functions cannot directly solve our problem. We have provided a RTTI-based solution there. Can you suggest some other cases similar to this?

4. What is the need for a `typeinfo` object? What is the role of the `typeid` operator in RTTI?

5. Give an example of conversion of a program using `dynamic_cast` to one using `typeid`, other than the one provided in the book.

6. Is it possible to convert a problem solved using `dynamic_cast` to one using `typeid`? Give your views on such conversion.

7. Write down the differences between solutions provided using `typeid` and using `dynamic_cast`.

8. What are the problems with the use of `typeid` mechanism for solving problems?

9. Design a few class hierarchies yourself. Identify cases where we can use virtual functions, `typeid`, and `dynamic_cast`.

10. Draw a comparison between different casting operators.

11. When working with templates, do we need to use RTTI?

12. Suggest a few cases where downcasting or cross casting is useful.

### Practical Exercises

1. Read an integer and a float. Try to compare them using `typeid`. Print their type names using the function `name()`. Now, cast the integer into float. Repeat the same thing. Try comparing the types of both the items using the `==` operator.

2. Recall Problem 9 of Chapter 10 related to visiting faculty and regular faculty. Visiting faculty is now divided into visiting faculty from another educational institute and visiting faculty from non-educational institute. All visiting faculty now need facility for transport. Details of such need are stored with their objects and can be retrieved using a function `TransportNeed()`. This function cannot be a part of the faculty base class. Use `typeid` to find whether the faculty is a regular faculty or not, and then read the need for transport.

3. Replace `typeid` with `dynamic_cast` to provide a single statement instead of two different `typeid` statements in Problem 4.

4. Recall Problem 1 of Chapter 10 and define objects of all three (time) classes. Use `dynamic_cast` to ...

Define classes for DailyEmployees, PermanentEmployees, and HumanResource employees. Define a single array for storing all employee objects. Define a function `Salary`, which displays the salary (do not calculate salary; just display any value) of permanent employees alone. Use `dynamic_cast` to solve the problem.

> (Hint: we cannot use virtual functions defined in the Employee class here as DailyEmployees do not have salary functions defined. We have to define salary as a virtual function in the class PermanentEmployees. We have to use Employee pointer to access the objects. Whenever it is valid to cast from Employee to PermanentEmployees, the object belongs to any of the descendants of PermanentEmployees class. `dynamic_cast` helps us to find this.)

13. Define a Student class. Inherit that into MCAStudents and NonMCAStudents classes. MCAStudents inherits into GLSStudents and NonGLSStudents. A function `ShowPracticalHours()` can only be applied to MCAStudents. We have a base class Student pointer to point to a GLSStudents object. Use `dynamic_cast` to check that NonMCAStudents do not call `ShowPracticalHours()`.

## Chapter 12: Streams and Formatted Input/Output

### Learning Objectives

- Concept of input/output (I/O) and streams
- Predefined streams in C++
- Formatted and unformatted I/O
- Formatting using I/O members
- `fmtflags` and displaying the flag information
- Manipulators and their use in formatting
- User-defined manipulators

### 12.1 Introduction

Provision for input/output (I/O) is one of the major tasks of a programming language. Streams are (conceptually) pipe-like constructs used for providing I/O. When a programmer needs to handle input from or output to external entities such as a keyboard, file, or printer, then streams are used.

Different devices have different I/O specifications. For example, printers can be used for output but not for input, keyboard can be used only for input and not for output, and the hard disk is used for both. Conventional monitors of our desktop machines are output devices, but swanky touch screen monitors avoid keyboards by also acting as an input device.

Writing to a disk is a different operation from writing to a printer. In disks, the sector to write is determined, the head is placed on top of it, and the proper representation for input (what magnetic value to write for one and zero) is to be provided. If the sector is full, another empty sector is found to continue writing. It is also to be mentioned somewhere that the new empty sector that has been found is in continuation with the earlier sector. As a result, the content looks contiguous while reading a file. When writing to a disk, it is possible to have multiple disk writes from different users executed (disk being a shared resource).

Writing to a printer is an entirely different case. Here, writing means placing the printer head at the required position (in case of dot matrix) or selecting one from various heads for a given position (in case of line printer); inkjet and laser printers use a totally different technology. Writing to a terminal of a multi-user system involves yet another complexity. Some sort of address manipulation (finding out where the destination machine is) and a communication protocol are to be used.

To conclude, the operation remains the same, that is, writing. One can write to both the printer and the hard disk. However, the execution is different because the devices involved are different.

To make things even more complex, vendors keep upgrading their devices with new features and services. An upgraded product may perform the same tasks in a different way. For example, a new laser printer may have the ability to print more number of colours than its predecessor. Given all these complexities, how does a programmer communicate with different I/O devices?

> Though output and input operations look the same, actual devices need different types of attention to complete them.

Due to competition, vendors keep on adding features to devices. This requires more operations to be managed by the programmers.

The OS provides input and output streams, which programmers use for reading and writing to devices.

The OS provides an interface with which external programs can interact, regardless of the type of the I/O devices and their complexity. All programming languages extend this interface to the programmers so that they can write to or read from the stream. C++, not being an exception, supports stream-based I/O.

The problem is solved partly by the vendors by providing device drivers and partly by the operating system (OS) by providing an interface of the device drivers to the program. The OS can provide a consistent interface for all such devices in a way that when one asks for write operation, the OS would look at the particular device and execute the write operation that suits the device. For example, if one writes to a printer, the OS sends the printer driver a message for writing, and the printer driver sends the commands suited for that brand of printer and gets the job done. Instead, if one writes to a disk, the OS does the same operation, but now communicating to the disk driver. Since the OS provides a consistent interface for writing, there is no need to know where one is writing. For example, when a `printf()` statement is written in C, by default, it writes to the screen. However, if the executable were redirected to some file, the same `printf()` statement would write to that file. If the file were redirected to a printer, it would print on the printer. Thus, the OS provides abstraction by taking all the pressure on its shoulders.

The OS soaks in all the complexity and makes the programmer’s life easy by providing a consistent interface. This interface, in other words, is known as a stream. Streams provide independence from having different operations for different I/O devices. When `printf()` or `cout` is used, one is writing to a stream and not to the device directly. Conceptually, it is easier to consider the stream as a pipe-like structure. When one writes to a stream, one is writing to one end of the pipe. The other end is by default attached to the screen. When the OS provides redirection (using `>` operator with executable files such as `test.exe > OutputFile`), the other end of the pipe is then attached to the redirected device. This does not make any difference to the user’s end; he/she can continue writing in the same way.

### 12.2 I/O Streams of C vs C++

C++ provides two different stream-based I/O systems. Due to the backward compatibility needed with C, C++ provides C stream I/O as it is. One can still include `<stdio.h>` and use `printf()` and `scanf()` in the programs (though it is not recommended). It also provides a new I/O (the one with `cout`, `cin`, and `<<` and `>>` operators overloaded). The new I/O is also stream-based.

Though C I/O is still available and is robust and proven, there are a few distinct advantages of using C++ I/O, which are as follows:

1. C++ I/O is object-oriented. Objects represent streams in C++. `cout` is an object of the output stream class, whereas `cin` is an object of the input stream class. `<<` and `>>` are overloaded operators in those streams. Using objects from `istream` or `ostream` class enables the users to overload operators provided by that stream to use it for user-defined types. We have earlier seen examples to overload `<<` and `>>`

C++ provides C-type I/O as well as a new object-oriented I/O.
