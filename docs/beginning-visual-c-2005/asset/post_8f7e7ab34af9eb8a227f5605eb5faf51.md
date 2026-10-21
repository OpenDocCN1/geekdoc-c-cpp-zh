
You could also have a using directive for std as well, so you wouldn’t need to qualify standard library names either, but this is defeating the whole point of namespaces. Generally, if you use namespaces in your program, you should not add using directives all over your program; otherwise, you might as well not bother with namespaces in the first place. Having said that, we will add a using directive for std in all our examples to keep the code less cluttered and easier for you to read. When you are starting out with a new programming language, you can do without clutter, no matter how useful it is in practice.

## Multiple Namespaces

A real-world program is likely to involve multiple namespaces. You can have multiple declarations of a namespace with a given name and the contents of all namespace blocks with a given name are within the same namespace. For example, you might have a program file with two namespaces:

```
namespace sortStuff
{
    // Everything in here is within sortStuff namespace
}
```

```
namespace calculateStuff
{
    // Everything in here is within calculateStuff namespace
    // To refer to names from sortStuff they must be qualified
}
```

```
namespace sortStuff
{
    // This is a continuation of the namespace sortStuff
    // so from here you can refer to names in the first sortStuff namespace
    // without qualifying the names
}
```

A second declaration of a namespace with a given name is just a continuation of the first, so you can reference names in the first namespace block from the second without having to qualify them. They are all in the same namespace. Of course, you would not usually organize a source file in this way deliberately, but in can arise quite naturally with header files that you include into a program. For example, you might have something like this:

```
#include <iostream>      // Contents are in namespace std
#include "myheader.h"      // Contents are in namespace myStuff
#include <string>           // Contents are in namespace std

// and so on...
```

Here, <iostream> and string are ISO/ANSI C++ standard library headers, and myheader.h represents a header file that contains our program code. You have a situation with the namespaces that is an exact parallel of the previous illustration.

This has given you a basic idea of how namespaces work. There is a lot more to namespaces than I have discussed here, but if you grasp this bit you should be able to find out more about it without difficulty, if the need arises.

Note that the two forms of #include directive in the previous code fragment cause the compiler to search for the file in different ways. When you specify the file to be included between angled brackets, you are indicating to the compiler that it should search for the file along the path specified by the /I compiler option, and failing that along the path specified by the INCLUDE environment variable. These paths locate the C++ library files, which is why this form is reserved for library headers. The INCLUDE environment variable points to the folder holding the library header and the /I option allows an additional directory containing library headers to be specified. When the file name is between double quotes, the compiler will search the folder that contains the file in which the #include directive appears. If the file is not found, it will search in any directories that #include the current file. If that fails to find the file, it will search the library directories.

## C++/CLI Programming

C++/CLI provides a number of extensions and additional capabilities to what I have discussed in this chapter up to now. I'll first summarize these additional capabilities before going into details. The additional C++/CLI capabilities are:

- All of the ISO/ANSI fundamental data types can be used as I have described in a C++/CLI program, but they have some extra properties in certain contexts that I'll come to.
- C++/CLI provides its own mechanism for keyboard input and output to the command line in a console program.
- C++/CLI introduces the safe_cast operator that ensures that a cast operation results in verifiable code being generated.
- C++/CLI provides an alternative enumeration capability that is class-based and offers more flexibility than the ISO/ANSI C++ enum declaration you have seen.

You'll learn more about CLR reference class types beginning in Chapter 4, but because I have introduced global variables for native C++, I'll mention now that variables of CLR reference class types cannot be global variables.

I want to begin by looking at fundamental data types in C++/CLI.

## C++/CLI Specific: Fundamental Data Types

You can and should use the ISO/ANSI C++ fundamental data type names in your C++/CLI programs, and with arithmetic operations they work exactly as you have seen in native C++. In addition C++/CLI defines two additional integer types:

| Type | Bytes | Range of Values |
|---|---|---|
| long long | 8 | From 9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| unsigned long long | 8 | From 0 to 18,446,744,073,709,551,615 |

## Chapter 2

To specify literals of type long long you append LL or lowercase ll to the integer value. For example:

```
long long big = 123456789LL;
```

A literal of type unsigned long long you append ULL or ull to the integer value:

```
unsigned long long huge = 999999999999999ULL;
```

Although all the operations with fundamental types you have seen work in the same way in C++/CLI, the fundamental type names in a C++/CLI program have a different meaning and introduces additional capabilities in certain situations. A fundamental type in a C++/CLI program is a value class type and can behave as an ordinary value or as an object if the circumstances require it.

Within the C++/CLI language, each ISO/ANSI fundamental type name maps to a value class type that is defined in the System namespace. Thus, in a C++/CLI program, the ISO/ANSI fundamental type names are shorthand for the associated value class type. This enables value of a fundamental type to be treated simply as a value or automatically converted to an object of its associated value class type when necessary. The fundamental types, the memory they occupy, and the corresponding value class types are shown in the following table:

| Fundamental Type | Size(bytes) | CLI Value Class |
| --- | --- | --- |
| bool | 1 | System::Boolean |
| char | 1 | System::SByte |
| signed char | 1 | System::SByte |
| unsigned char | 1 | System::Byte |
| short | 2 | System::Int16 |
| unsigned short | 2 | System::UInt16 |
| int | 4 | System::Int32 |
| unsigned int | 4 | System::UInt32 |
| long | 4 | System::Int32 |
| unsigned long | 4 | System::UInt32 |
| long long | 8 | System::Int64 |
| unsigned long long | 8 | System::UInt64 |
| float | 4 | System::Single |
| double | 8 | System::Double |
| long double | 8 | System::Double |
| wchar_t | 2 | System::Char |

By default, type char is equivalent to signed char so the associated value class type is System::SByte. Note that you can change the default for char to unsigned char by setting the compiler option /J, in which case the associated value class type will be System::Byte. System is the root namespace name in which the C++/CLI value class types are defined. There are many other types defined within the System namespace, such as the type String for representing strings that you'll meet in Chapter 4. C++/CLI also defines the System::Decimal value class type within the System namespace and variables of type Decimal store exact decimal values with 28 decimal digits precision.

As I said, the value class type associated with each fundamental type name adds important additional capabilities for such variables in C++/CLI. When necessary, the compiler will arrange for automatic conversions from the original value to the associated class type and vice versa; these processes are referred to as boxing and unboxing, respectively. This allows a variable of any of these types to behave as a simple value or as an object, depending on the circumstances. You'll learn more about how and when this happens in Chapter 6.

Because the ISO/ANSI C++ fundamental type names are aliases for the value class type names in a C++/CLI program, in principle you can use either in your C++/CLI code. For example, you already know you can write statements creating integer and floating-point variables like this:

```
int count = 10;
double value = 2.5;
```

You could use the value class names that correspond with the fundamental type names and have the program compile without any problem, like this:

```
System::Int32 count = 10;
System::Double value = 2.5;
```

While this is perfectly legal, you should use the fundamental type names such as int and double in your code, rather than the value class names System::Int32 and System::Double. The reason is that the mapping between fundamental type names and value class types I have described applies to the Visual C++ 2005 compiler; other compilers are not obliged to implement the same mapping. The fundamental type names are fixed by the C++/CLI language standard, but the mapping to value class types is implementation-dependent for most types. Type long in Visual C++ 2005 maps to type Int32, but it is quite possible that it could map to type Int64 on some other implementation.

Having data of the fundamental types represented by objects of a value class type is an important feature of C++/CLI. In ISO/ANSI C++ fundamental types and class types are quite different, whereas in C++/CLR all data is stored as objects of a class type, either as a value class type or as a reference class type. You'll learn about reference class types in Chapter 7.

Next, you'll try a CLR console program.

## Try It Out  A Fruity CLR Console Program

Create a new project and select the project type as CLR and the template as CLR Console Application. You can then enter the project name as Ex2_12, as shown in Figure 2-13.
