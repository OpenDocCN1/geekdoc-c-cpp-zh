
- b) Keywords typename and class as used with a template type parameter specifically mean “any user-defined class type.”
- c) A function template can be overloaded by another function template with the same function name.
- d) Template parameter names among template definitions must be unique.
- e) Each member-function definition outside a class template must begin with a template header.
- f) A friend function of a class template must be a function-template specialization.
- g) If several class-template specializations are generated from a single class template with a single static data member, each of the class-template specializations shares a single copy of the class template’s static data member.

### 14.2 Fill in the blanks in each of the following:

- a) Templates enable us to specify, with a single code segment, an entire range of related functions called ________, or an entire range of related classes called ________.
- b) All function-template definitions begin with the keyword ________, followed by a list of template parameters to the function template enclosed in ________.
- c) The related functions generated from a function template all have the same name, so the compiler uses ________ resolution to invoke the proper function.
- d) Class templates also are called ________ types.
- e) The ________ operator is used with a class-template name to tie each member-function definition to the class template’s scope.
- f) As with static data members of nontemplate classes, static data members of class-template specializations must also be defined and, if necessary, initialized at ________ scope.

### Answers to Self-Review Exercises

- 14.1 a) True. b) False. Keywords typename and class in this context also allow for a type parameter of a fundamental type. c) True. d) False. Template parameter names among function templates need not be unique. e) True. f) False. It could be a nontemplate function. g) False. Each class-template specialization will have its own copy of the static data member.
- 14.2 a) function-template specializations, class-template specializations. b) template, angle brackets (< and >). c) overloading. d) parameterized. e) binary scope resolution. f) global namespace.

### Exercises

- 14.3 *(Selection Sort Function Template)* Write a function template selectionSort based on Fig. 8.13. Write a driver program that inputs, sorts and outputs an int array and a float array.
- 14.4 *(Print Array Range)* Overload function template printArray of Fig. 14.1 so that it takes two additional integer arguments, namely int lowSubscript and int highSubscript. A call to this function will print only the designated portion of the array. Validate lowSubscript and highSubscript; if either is out of range or if highSubscript is less than or equal to lowSubscript, the overloaded printArray function should return 0; otherwise, printArray should return the number of elements printed. Then modify main to exercise both versions of printArray on arrays a, b and c (lines 22–24 of Fig. 14.1). Be sure to test all capabilities of both versions of printArray.
- 14.5 *(Function Template Overloading)* Overload function template printArray of Fig. 14.1 with a nontemplate version that prints an array of character strings in neat, tabular, column format.
- 14.6 *(Operator Overloads in Templates)* Write a simple function template for predicate function isEqualTo that compares its two arguments of the same type with the equality operator (==) and returns true if they are equal and false otherwise. Use this function template in a program that calls isEqualTo only with a variety of fundamental types. Now write a separate version of the program

## 15 Stream Input/Output

![](img/023f159fdd47d944d48e08843cea732d_681_0.png)

> Consciousness ... does not appear to itself chopped up in bits. A “river” or a “stream” are the metaphors by which it is most naturally described.
>
> —William James

### Objectives

In this chapter you’ll learn:

- To use C++ object-oriented stream input/output.
- To format input and output.
- The stream-I/O class hierarchy.
- To use stream manipulators.
- To control justification and padding.
- To determine the success or failure of input/output operations.
- To tie output streams to input streams.

**Error-Prevention Tip 15.1**

C++ I/O is type safe.

**Software Engineering Observation 15.2**

C++ enables a common treatment of I/O for predefined types and user-defined types. This commonality facilitates software development and reuse.

### 15.2 Streams

C++ I/O occurs in streams, which are sequences of bytes. In input operations, the bytes flow from a device (e.g., a keyboard, a disk drive, a network connection, etc.) to main memory. In output operations, bytes flow from main memory to a device (e.g., a display screen, a printer, a disk drive, a network connection, etc.).

An application associates meaning with bytes. The bytes could represent characters, raw data, graphics images, digital speech, digital video or any other information an application may require.

The system I/O mechanisms should transfer bytes from devices to memory (and vice versa) consistently and reliably. Such transfers often involve some mechanical motion, such as the rotation of a disk or a tape, or the typing of keystrokes at a keyboard. The time these transfers take is typically much greater than the time the processor requires to manipulate data internally. Thus, I/O operations require careful planning and tuning to ensure optimal performance.

C++ provides both “low-level” and “high-level” I/O capabilities. Low-level I/O capabilities (i.e., unformatted I/O) specify that some number of bytes should be transferred device-to-memory or memory-to-device. In such transfers, the individual byte is the item of interest. Such low-level capabilities provide high-speed, high-volume transfers but are not particularly convenient.

Programmers generally prefer a higher-level view of I/O (i.e., formatted I/O), in which bytes are grouped into meaningful units, such as integers, floating-point numbers, characters, strings and user-defined types. These type-oriented capabilities are satisfactory for most I/O other than high-volume file processing.

**Performance Tip 15.1**

Use unformatted I/O for the best performance in high-volume file processing.

**Portability Tip 15.1**

Using unformatted I/O can lead to portability problems, because unformatted data is not portable across all platforms.

#### 15.2.1 Classic Streams vs. Standard Streams

In the past, the C++ standard stream libraries enabled input and output of chars. Because a char normally occupies one byte, it can represent only a limited set of characters (such as those in the ASCII character set). However, many languages use alphabets that contain more characters than a single-byte char can represent. The ASCII character set does not provide these characters; the Unicode® character set does. Unicode is an extensive international character set that represents the majority of the world’s “commercially viable” languages, mathematical symbols and much more. For more information on Unicode, visit www.unicode.org.

C++ includes the standard stream libraries, which enable developers to build systems capable of performing I/O operations with Unicode characters. For this purpose, C++ includes an additional character type called **wchar_t**, which can store 2-byte Unicode characters. The C++ standard also redesigned the classic C++ stream classes, which processed only chars, as class templates with separate specializations for processing characters of types char and wchar_t, respectively. We use the char type of class templates throughout this book.

#### 15.2.2 iostream Library Header Files

The C++ iostream library provides hundreds of I/O capabilities. Several header files contain portions of the library interface.

Most C++ programs include the `<iostream>` header file, which declares basic services required for all stream I/O operations. The `<iostream>` header file defines the cin, cout, cerr and clog objects, which correspond to the standard input stream, the standard output stream, the unbuffered standard error stream and the buffered standard error stream, respectively. (cerr and clog are discussed in Section 15.2.3.) Both unformatted and formatted-I/O services are provided.

The `<iomanip>` header declares services useful for performing formatted I/O with so-called parameterized stream manipulators, such as **setw** and **setprecision**.

The `<fstream>` header declares services for user-controlled file processing. We use this header in the file-processing programs of Chapter 17.

C++ implementations generally contain other I/O-related libraries that provide system-specific capabilities, such as the controlling of special-purpose devices for audio and video I/O.

#### 15.2.3 Stream Input/Output Classes and Objects

The iostream library provides many templates for handling common I/O operations. For example, class template **basic_istream** supports stream-input operations, class template **basic_ostream** supports stream-output operations, and class template **basic_iostream** supports both stream-input and stream-output operations. Each template has a predefined template specialization that enables char I/O. In addition, the iostream library provides a set of typedefs that provide aliases for these template specializations. The **typedef** specifier declares synonyms (aliases) for previously defined data types. Programmers sometimes use **typedef** to create shorter or more readable type names. For example, the statement

```cpp
typedef Card *CardPtr;
```

defines an additional type name, **CardPtr**, as a synonym for type `Card *`. Creating a name using **typedef** does not create a data type; **typedef** creates only a type name that may be used in the program. Section 21.5 discusses **typedef** in detail. The **typedef** **istream** represents a specialization of **basic_istream** that enables char input. Similarly, the **typedef** **ostream** represents a specialization of **basic_ostream** that enables char output. Also, the **typedef** **iostream** represents a specialization of **basic_iostream** that enables both char input and output. We use these typedefs throughout this chapter.
