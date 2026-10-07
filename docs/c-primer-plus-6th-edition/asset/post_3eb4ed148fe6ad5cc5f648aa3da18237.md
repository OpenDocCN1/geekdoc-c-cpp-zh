
# How This Book Is Organized

defining an explicit assignment operator. Chapter 12 shows you how and discusses the behavior of the member functions generated implicitly if you fail to provide explicit definitions. You'll also expand your experience with classes by using pointers to objects and studying the queue simulation problem.

- **Chapter 13: Class Inheritance—** One of the most powerful features of object-oriented programming is inheritance, by which a derived class inherits the features of a base class, enabling you to reuse the base class code. Chapter 13 discusses inheritance, which models relationships, meaning a derived object is a special case of a base object. For example, a physicist is a special case of a scientist. Some inheritance relationships are polymorphic, meaning you can write code using a mixture of classes for which the same method may invoke behavior that depends on the object type. Implementing this kind of behavior necessitates a new kind of member function called a virtual function. Sometimes abstract classes are the best approach to inheritance relationships. This chapter discusses these matters, pointing out when public inheritance is appropriate and when it is not.

- **Chapter 14: Reusing Code in C++—** inheritance is just one way to reuse code. Chapter 14 looks at other ways. Containment is when one class contains members of another class. It also can be used to model has-relationships, in which one class has components of another class. For example, an automobile has a motor. You also can use private and protected inheritance to model relationships. This chapter shows you and points out the differences between the different approaches. Also, you'll learn about class templates, which let you define a class in terms of some generic type, and use the template to create specific classes in specific types. For example, a stack template enables you to create a stack of integers or a stack of strings. Finally, you'll learn about multiple public inheritance, where a class can derive from more than one class.

- **Chapter 15: Friends, Exceptions, and More—** Chapter 15 extends the definition of friends to include friend classes and member functions. It presents several new developments in C++, with exceptions, which provide a mechanism for dealing with unusual program occurrences, such as an inappropriate function argument or running out of memory. You'll learn about the safer RTTI, a mechanism for identifying object types. Finally, you'll learn about the safer alternatives to unrestricted casting.

- **Chapter 16: The string Class and the Standard Template Library—** Chapter 16 discusses some useful libraries added to the language. The string class is a convenient and powerful alternative to traditional C-style strings. The auto_ptr class helps manage dynamically allocated memory. The STL provides generic containers, including template representations of arrays, queues, lists, and maps. It also provides an efficient library of generic algorithms that can be used with STL containers and also with ordinary arrays. The varray template class provides pointers for numeric arrays.

- **Chapter 17: Input, Output, and Files—** Chapter 17 reviews C++ I/O and discusses how to format output. You'll learn how to use class methods to determine the state of an input or output stream and see, for example, whether there has been a mismatch on input or whether the end-of-file has been detected. C++ uses inheritance to derive classes for managing file input and output, how to append data to a file, how to use binary files, how to open files for input and output, how to get access to a file. Finally, you'll learn how to apply standard I/O methods to read from and write to strings.

- **Chapter 18: Visiting with the New C++ Standard—** Chapter 18 begins by reviewing several C++11 features introduced in earlier chapters, including uniform initialization syntax, automatic type deduction, new smart pointers, and scoped enumerations. The chapter then discusses the new value reference type and how it's used to implement a new feature called semantics. The next chapter covers new features, lambda expressions, and variadic templates. Finally, the chapter outlines many new features not covered in earlier chapters of the book.

- **Appendix A: Number Bases—** Appendix A discusses octal, hexadecimal, and binary numbers.

- **Appendix B: C++ Reserved Words—** Appendix B lists C++ keywords.

- **Appendix C: The ASCII Character Set—** Appendix C lists the ASCII character set, along with decimal, octal, hexadecimal, and binary representations.

- **Appendix D: Operator Precedence—** Appendix D lists the C++ operators in order of decreasing precedence.

- **Appendix E: Other Operators—** Appendix E summarizes the C++ operators, as with the bitwise operators, not covered in the main body of the text.

- **Appendix F: The string Template Class—** Appendix F summarizes string methods and functions.

- **Appendix G: The Standard Template Library Methods and Functions—** Appendix G summarizes the STL container methods and the general STL algorithm functions.

- **Appendix H: Selected Readings and Internet Resources—** Appendix H lists some books that can further your understanding of C++.

- **Appendix I: Converting to ISO Standard C++—** Appendix I provides guidelines for moving from C and older C++ implementations to ANSI/ISO C++.

- **Appendix J: Answers to Chapter Review—** Appendix J contains the answers to the review questions posed at the end of each chapter.

# Note to Instructors

One of the goals of this edition of C++ Primer Plus is to provide a book that can be used as either a teach-yourself book or a textbook. Here are some of the features that support using C++ Primer Plus, Sixth Edition, as a textbook:

- This book describes generic C++, so it is not dependent on a particular implementation.
- The contents track the ISO/ANSI C++ standards committee's work and include discussions of templates, the STL, the string class, exceptions, RTTI, and namespaces.
- It does not assume prior knowledge of C, so it can be used without a C prerequisite. (Some background is desirable, however.)
- Topics are arranged so that early chapters can be covered rapidly.
- The book introduces several topics that are appropriate for computer science courses, including abstract data types (ADTs), stacks, queues, simple lists, generic programming, and recursion to implement a divide-and-conquer strategy.
- Most chapters are short enough to cover in a week or less.
- Chapters include review questions and programming exercises. Appendix J provides the answers to the review questions.
- The book links public inheritance to is-a relationships and composition and private inheritance to has-a relationships, and it discusses when to use virtual functions and when not.

# Conventions Used in This Book

This book uses several conventions to distinguish among various kinds of text:

- Code lines, commands, statements, filenames, and program output appear in a computer typeface:

```
#include <iostream>
int main()
{
    using namespace std;
    cout << "What's up, Doc!\n";
    return 0;
}
```

- Program input that you should type appears **bold computer typeface**:
  Please enter your name:
  **Plato**

- Placeholders in syntax descriptions appear in an *italic computer typeface*. You should replace a placeholder with the actual filename, parameter, or whatever element represents.

- *Italic type* is used for new terms.

**Sidebar**
A sidebar provides a deeper discussion or additional background to help illuminate a topic.

**Tip**
Tips present short, helpful guides to particular programming situations.

**Caution**
A caution alerts you to pitfalls.

**Note**
The notes provide a catch-all category for comments that don't fall into one of the other categories.

# Systems Used to Develop This Book’s Programming Examples

For the record, the C++11 examples in this book were developed using Microsoft Visual C++ 2010 and Cygwin with GNU g++ 4.5.0, both running under 64-bit Windows 7. The remaining examples were tested with these systems, as well as on an iMac g++ 4.2.1 under OS X 10.6.8 and on an Ubuntu Linux system using g++ 4.4.1. Most of the pre-C++11 examples were originally developed using Microsoft Visual C++ 2003 and Metroworks CodeWarrior Development Studio 9 running under Windows XP Professional and checked using the Borland C++ 5.5 command-line compiler and GNU gpp 3.3.3 on the same system, using Comeau 4.3.3 and GNU g++ 3.3.1 under SuSE 9.0 Linux, and using Metroworks Development Studio 9 on a Macintosh G4 over OS 10.3.
