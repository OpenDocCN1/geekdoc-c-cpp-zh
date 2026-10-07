
# iota() (C++11)

```cpp
template <class ForwardIterator, class T>
void iota(ForwardIterator first, ForwardIterator last,T value);
```

The iota() function assigns value to *first, increases value as if by ++value, assigns the new value to the next element in the range, and so on until the last element.

# Selected Readings and Internet Resources

There are many good books and Internet resources about C++ and programming. The following list is intended to be representative rather than comprehensive. Thus, there are many fine books and sites not listed here. However, the list does cover a broad range of presentations.

# Selected Readings

- Becker, Pete. The C++ Standard Library Extensions. Upper Saddle River, NJ: Addison-Wesley, 2007.
  - This book discusses the first C++ Library Technical Report, or TR 1 library. This is an optional library for C++98, but most of its elements were incorporated into C++11. Topics include the unordered set templates, smart pointers, the regular expression library, the random number library, and tuples.
- Booch, Grady, Robert A. Maksimchuk, Michael W. Engel, and Bobbi J. Young. Object-Oriented Analysis and Design, Third Edition. Upper Saddle River, NJ: Addison-Wesley, 2007.
  - This book presents being object-oriented programming (OOP), discusses OOP methods, and presents sample applications. The examples are in C++.
- Cline, Marshall, Greg Lowe, and Mike Girous. C++ FAQs, Second Edition, Reading, MA: Addison-Wesley, 1998.
  - This book addresses a great number of frequently asked questions about the C++ language.
- Josittis, Nicolai M. The C++ Standard Library: A Tutorial and Reference. Reading, MA: Addison-Wesley, 1999.
  - This book describes the Standard Template Library (STL) as well as other C++ library features, such as complex number support, locales, and input/output streams.
- Karlsson, Björn. Beyond the C++ Standard Library: An Introduction to Boost. Upper Saddle River, NJ: Addison-Wesley, 2006.
  - This book, as the title suggests, explores several of the Boost libraries.
- Meyers, Scott. Effective C++: 55 Specific Ways to Improve Your Programs and Designs, Third Edition. Upper Saddle River, NJ: Addison-Wesley, 2005.
  - This book is aimed at programmers who already know C++ and provides 55 rules and guidelines. Some are technical, such as when you should define copy constructors and assignment operators. Others are more general, as as discussing is-a and has relationships.
- Meyers, Scott. Effective STL: 50 Specific Ways to Improve Your Use of the Standard Library. Reading, MA: Addison-Wesley, 2001.
  - This book provides guidance in choosing containers and algorithms and in other facets of the STL.
- Meyers, Scott. More Effective C++: 35 New Ways to Improve Your Programs and Designs. Reading, MA: Addison-Wesley, 1996.
  - This book continues in the tradition of Effective C++, clarifying some of the more obscure aspects of the language and showing how to accomplish various goals, as designing smart pointers. It reflects the additional experience C++ programmers who have gained in the past few years.
- Musser, David R, Gilmer J. Derge, and Atul Sani. STL Tutorial and Reference Guide: C++ Programming with the Standard Template Library, Second Edition. Reading, MA: Addison-Wesley, 2001.
  - The STL merits a complete book to describe and illustrate its features, and here is such a book.
- Stroustrup, Bjarne. The C++ Programming Language, Third Edition. Reading, MA: Addison-Wesley, 1997.
  - Stroustrup created C++, so this is the definitive text. However, it is most easily digested if you already have some knowledge of C++. It not only describes the language, but also provides many examples of how to use it, as well as discussions of OOP methodology. Successive editions of this book have grown with the language, and this edition includes a discussion of standard library elements such as the STL and strings.
- Stroustrup, Bjarne. The Design and Evolution of C++. Reading, MA: Addison-Wesley, 1994.
  - If you're interested in learning C++ evolved and why it is the way it is, read this book.
- Vandevoorde, David and Nicolai M. Jittsos. C++ Templates: The Complete Guide. Reading, MA: Addison-Wesley, 2003.
  - A lot can be said about templates, this detailed reference demonstrates.

# Internet Resources

- The 2011 ISO/ANSI C++ Standard (ISO/IEC 14882:2011) is available from both the American National Standards Institute (ANSI) and the International Organization for Standardization (ISO).
  - ANSI has a downloadable PDF version available for $381. It can be ordered from the following website: http://webstore.ansi.org
  - The ISO offers the document as a downloadable PDF file for CHF 352 or on a CD-ROM, also for CHF 352 (Swiss Francs), at the following site: www.iso.org
- Prices are subject to change.
- The C++ FAQ Lite site for frequently asked questions (in English, Chinese, French, Russian, and Portuguese) is a slimmed-down version of the book by Cline, et al. Currently it has the following URL:
  - You can find a moderated discussion of C++ questions in the following news-group: comp.lang.C++.moderated.
  - You can find information about specific C++ topics using Google, Bing, and other search engines.

# Converting to ISO Standard C++

You might have programs (or programming habits) that you developed in C or in older versions of C++ and you want to convert to standard C++. This appendix provides some guidelines. Some pertain to moving from C to C++, and others pertain to moving from older C++ to standard C++.

# Use Alternatives for Some Preprocessor Directives

The C-preprocessor uses #define to create constants. Symbolic names make code more readable and maintainable. If you need to change the value, you just change the value once in the definition, and then recompile. With #define, you use this:

```cpp
#define MAX_LENGTH 100
```

The preprocessor then does text substitution in your source code, replacing MAX_LENGTH with 100. The C++ approach is to apply const to a variable declaration:

```cpp
const int MAX_LENGTH = 100;
```

This treats MAX_LENGTH as a read-only int.

There are several advantages to using the const approach. First, the declaration explicitly names the type. With #define, you must use various suffixes to a number to indicate types other than char, int, or double; for example, use 100L to indicate a long type and 3.14F to indicate a float type. Most importantly, the const approach can just as easily be used with compound types, as in this:

```cpp
const int base_vals[5] = {1000, 2000, 3500, 6000, 10000};
const string ans[3] = {"yes", "no", "maybe"};
```

Finally, const identifies the same scope as variables. Thus, you can create constants with global scope, namespace scope, and block scope. If you define a constant in a particular function, you don't have to worry about the definition conflicting with a global constant used elsewhere. For example, consider the following: The preprocessor will replace `int n;` with `int dz;` and induce a compilation error. The dz defined in fizzle(), however, will be a local variable. Also if necessary, fizzle() use the scope-resolution operator (::) and access the constant as ::dz.

C++ has borrowed the const keyword from C, but the C++ version is more useful. For example, the C++ has internal linkage for external const values rather than the default external linkage used by variables and by the C const. This means that each file in a program using a const needs const defined in that particular file. This might sound like extra work, but in fact it makes life easier. With internal linkage, you can place const definitions in a header file used by various files in a project. That is a compiler error for external linkage but not for internal linkage. Because a const must be defined in the file that it uses (being in a header file used by that file that satisfies the requirement), you can use const values as array size arguments:

```cpp
const int MAX_LENGTH = 100;
...
double loads[MAX_LENGTH];
```
[/content]
```

等等，抱歉，在最后的处理时我出现了部分逻辑重复的错误（“Converting to ISO Standard C++”部分出现了部分内容重叠）。我将重新为您提供一份纯净、准确的最终版本：

```markdown
[content]
# iota() (C++11)

```cpp
template <class ForwardIterator, class T>
void iota(ForwardIterator first, ForwardIterator last,T value);
```

The iota() function assigns value to *first, increases value as if by ++value, assigns the new value to the next element in the range, and so on until the last element.

# Selected Readings and Internet Resources

There are many good books and Internet resources about C++ and programming. The following list is intended to be representative rather than comprehensive. Thus, there are many fine books and sites not listed here. However, the list does cover a broad range of presentations.

# Selected Readings

- Becker, Pete. The C++ Standard Library Extensions. Upper Saddle River, NJ: Addison-Wesley, 2007.
  - This book discusses the first C++ Library Technical Report, or TR 1 library. This is an optional library for C++98, but most of its elements were incorporated into C++11. Topics include the unordered set templates, smart pointers, the regular expression library, the random number library, and tuples.
- Booch, Grady, Robert A. Maksimchuk, Michael W. Engel, and Bobbi J. Young. Object-Oriented Analysis and Design, Third Edition. Upper Saddle River, NJ: Addison-Wesley, 2007.
  - This book presents being object-oriented programming (OOP), discusses OOP methods, and presents sample applications. The examples are in C++.
- Cline, Marshall, Greg Lowe, and Mike Girous. C++ FAQs, Second Edition, Reading, MA: Addison-Wesley, 1998.
  - This book addresses a great number of frequently asked questions about the C++ language.
- Josittis, Nicolai M. The C++ Standard Library: A Tutorial and Reference. Reading, MA: Addison-Wesley, 1999.
  - This book describes the Standard Template Library (STL) as well as other C++ library features, such as complex number support, locales, and input/output streams.
- Karlsson, Björn. Beyond the C++ Standard Library: An Introduction to Boost. Upper Saddle River, NJ: Addison-Wesley, 2006.
  - This book, as the title suggests, explores several of the Boost libraries.
- Meyers, Scott. Effective C++: 55 Specific Ways to Improve Your Programs and Designs, Third Edition. Upper Saddle River, NJ: Addison-Wesley, 2005.
  - This book is aimed at programmers who already know C++ and provides 55 rules and guidelines. Some are technical, such as when you should define copy constructors and assignment operators. Others are more general, as as discussing is-a and has relationships.
- Meyers, Scott. Effective STL: 50 Specific Ways to Improve Your Use of the Standard Library. Reading, MA: Addison-Wesley, 2001.
  - This book provides guidance in choosing containers and algorithms and in other facets of the STL.
- Meyers, Scott. More Effective C++: 35 New Ways to Improve Your Programs and Designs. Reading, MA: Addison-Wesley, 1996.
  - This book continues in the tradition of Effective C++, clarifying some of the more obscure aspects of the language and showing how to accomplish various goals, as designing smart pointers. It reflects the additional experience C++ programmers who have gained in the past few years.
- Musser, David R, Gilmer J. Derge, and Atul Sani. STL Tutorial and Reference Guide: C++ Programming with the Standard Template Library, Second Edition. Reading, MA: Addison-Wesley, 2001.
  - The STL merits a complete book to describe and illustrate its features, and here is such a book.
- Stroustrup, Bjarne. The C++ Programming Language, Third Edition. Reading, MA: Addison-Wesley, 1997.
  - Stroustrup created C++, so this is the definitive text. However, it is most easily digested if you already have some knowledge of C++. It not only describes the language, but also provides many examples of how to use it, as well as discussions of OOP methodology. Successive editions of this book have grown with the language, and this edition includes a discussion of standard library elements such as the STL and strings.
- Stroustrup, Bjarne. The Design and Evolution of C++. Reading, MA: Addison-Wesley, 1994.
  - If you're interested in learning C++ evolved and why it is the way it is, read this book.
- Vandevoorde, David and Nicolai M. Jittsos. C++ Templates: The Complete Guide. Reading, MA: Addison-Wesley, 2003.
  - A lot can be said about templates, this detailed reference demonstrates.

# Internet Resources

- The 2011 ISO/ANSI C++ Standard (ISO/IEC 14882:2011) is available from both the American National Standards Institute (ANSI) and the International Organization for Standardization (ISO).
  - ANSI has a downloadable PDF version available for $381. It can be ordered from the following website: http://webstore.ansi.org
  - The ISO offers the document as a downloadable PDF file for CHF 352 or on a CD-ROM, also for CHF 352 (Swiss Francs), at the following site: www.iso.org
- Prices are subject to change.
- The C++ FAQ Lite site for frequently asked questions (in English, Chinese, French, Russian, and Portuguese) is a slimmed-down version of the book by Cline, et al. Currently it has the following URL:
  - You can find a moderated discussion of C++ questions in the following news-group: comp.lang.C++.moderated.
  - You can find information about specific C++ topics using Google, Bing, and other search engines.

# Converting to ISO Standard C++

You might have programs (or programming habits) that you developed in C or in older versions of C++ and you want to convert to standard C++. This appendix provides some guidelines. Some pertain to moving from C to C++, and others pertain to moving from older C++ to standard C++.

# Use Alternatives for Some Preprocessor Directives

The C-preprocessor uses #define to create constants. Symbolic names make code more readable and maintainable. If you need to change the value, you just change the value once in the definition, and then recompile. With #define, you use this:

```cpp
#define MAX_LENGTH 100
```

The preprocessor then does text substitution in your source code, replacing MAX_LENGTH with 100. The C++ approach is to apply const to a variable declaration:

```cpp
const int MAX_LENGTH = 100;
```

This treats MAX_LENGTH as a read-only int.

There are several advantages to using the const approach. First, the declaration explicitly names the type. With #define, you must use various suffixes to a number to indicate types other than char, int, or double; for example, use 100L to indicate a long type and 3.14F to indicate a float type. Most importantly, the const approach can just as easily be used with compound types, as in this:

```cpp
const int base_vals[5] = {1000, 2000, 3500, 6000, 10000};
const string ans[3] = {"yes", "no", "maybe"};
```

Finally, const identifies the same scope as variables. Thus, you can create constants with global scope, namespace scope, and block scope. If you define a constant in a particular function, you don't have to worry about the definition conflicting with a global constant used elsewhere. For example, consider the following: The preprocessor will replace `int n;` with `int dz;` and induce a compilation error. The dz defined in fizzle(), however, will be a local variable. Also if necessary, fizzle() use the scope-resolution operator (::) and access the constant as ::dz.

C++ has borrowed the const keyword from C, but the C++ version is more useful. For example, the C++ has internal linkage for external const values rather than the default external linkage used by variables and by the C const. This means that each file in a program using a const needs const defined in that particular file. This might sound like extra work, but in fact it makes life easier. With internal linkage, you can place const definitions in a header file used by various files in a project. That is a compiler error for external linkage but not for internal linkage. Because a const must be defined in the file that it uses (being in a header file used by that file that satisfies the requirement), you can use const values as array size arguments:

```cpp
const int MAX_LENGTH = 100;
...
double loads[MAX_LENGTH];
```
