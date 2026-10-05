
## 1.3. C++ review

The C language has a simple philosophy. Its aim is to offer a uniform view of the computer, especially computer memory, to the programmer. C has been so successful that nearly every object that can be called a computer, ranging from supercomputers to routers to embedded and mobile devices, is equipped with a C compiler or a cross-compiler. C is the best vehicle for highly optimized programs.

Because C seeks to be close to the machine, it is a low-level language. There is often a considerable distance between concepts that are native to a problem domain and their expression as C programs. High-level languages provide constructs and syntax that bring the program much closer to ideas and concepts that are native to the problem domain.

The C++ language is something of a compromise to provide the facilities of high-level languages without sacrificing the speed of C. Despite its name, it is not an incremental extension of C. It is a colossal expansion of C syntax. It does not have the seamless nature of truly high-level languages such as Python. Classes in Python use very little syntax and fit cleanly within the highly modular architecture of Python programs. However, languages such as Python are slower than C++.

Although the C++ language is a compromise, or perhaps because of being a compromise, it has a great range of uses. On the one hand, C++ has all of C inside. On the other hand, it provides many mechanisms for capturing concepts and ideas more precisely. Its downside is its complexity. Although clear and careful thinking are essential to all programming, a failure in this respect has particular acute consequences in C++.

Because our focus is on program, the part of C++ we use is quite small. Narrowly defined and flat (as opposed to hierarchical) classes, references, occasional function name overloading, and the ability to define variables in the middle of programs is almost all of C++ features. The classes we define are no more than C structs endowed with functions. Features such as enum, struct, typedef, and static can be powerful for representing concepts and ideas when used judiciously.

Classes in C++ are a mechanism for representing concepts and ending them with functionality that makes them easy to use. Classes can be general or narrow. The Vector class studied in this section is an example of a general class. It can be even more general. The Vector class assumes that each entry of a vector is a double. Using templates, one may define a class that allows each entry to be a double or a float or an int or even some defined type or class.

The Vector is the only example in this book of a class that attempts to capture a general concept (in this instance, the concept of vectors in linear algebra). Every other class discussed in this book is narrowly defined. We begin our discussion of C++ with the Vector class for two reasons. It a a good vehicle for reviewing some of the features of C++. Indeed, we introduce more features of C++ than we need, but that serves a purpose. C++ is sometimes believed to lead to slow programs. This example helps us explain thoroughly how that may come about. In later chapters, we will illustrate the overhead of the Vector class and the related Matrix class, when used in inner-loops or for disk input/output.

### 1.3.1 The Vector class

The C++ language can be used in many different ways. Using general classes, one may make C++ look easy to use languages like Python or Matlab without incurring the enormous cost of such interpreted languages. Our interest is in fast programs, and even more so, in understanding what makes programs fast or slow. The C++ style we adopt is close to C.

Nevertheless, we begin with a general type of class, the Vector class. This class helps us review a few of the features of C++ and is used to implement the Aiken iteration. In a later chapter, we criticize the use of this class and show it to be slow.

### Header file with class definition

The Vector class is defined in the header file Vector.hh. The C++ class consists of data members and member functions. With respect to compute memory, a class object is a collection of data items. The data items could be of basic types such as double or char, or pointers. The data items may also be other class objects or C structures. The member functions provide various means to manipulate the class object, or equivalently, the package of data items that constitutes the class object. definition of the class.

It is typical for header files to give only part of the class. Many of the member functions are typically defined in a separate source. Here the entire class definition is in the header file Vector.hh, which makes the header file a bit long. We present the contents of the header file in stages, gradually unveiling features of C++.

The skeleton of the header file is listed below.

```cpp
1 #ifndef MYVECTOR
2 #define MYVECTOR
3 #include <cassert>
4 #include <cmath>
5 #include <cstdlib>
6 #include <string>
7 #include <iostream>
8 #include <fstream>
9
10 using namespace std;
11
12 class Vector{
13 private:
14 ..
15 public:
16 ...
17 };
18
19 #endif
```

Lines 1, 2, and 19 ensure that the header file expands to the source code in between if only if the variable MYVECTOR is defined. Here MYVECTOR is not good nomenclature, as it may be inadvertently used by some other header, subverting our attempt to ensure conditional inclusion of header files.

It is typical for C/C++ sources to begin by including a number of header files to interface to other source files or libraries. C programs include the header assert.h to use the assert() macro (see section 1.2.3). C++ programs may include either assert.h or cassert, as on line 3, to emphasize that a C facility is employed.

The Vector class uses other facilities as well. It uses the fabs() function frommath (line 4) in one of its member functions to compute the norm of the vector. C facilities to allocate and release memory are defined in stdlib (line 5). C++ facilities for input/output from terminals and files are in iostream (line 7) and fstream (line 8), respectively. Member functions that input/output vectors tofrom files use these facilities.

To output a variable x to standard output (typically the terminal), we may say

```cpp
cout<<x<<endl;
```

Here cout is the name of standard output declared in iostream. The end of line character endl is also declared in iostream. In C, input/output syntax is sensitive to the type of data items handled. The abstraction features of C++ are used by the iostream library to provide a uniform interface for input/output regardless of the type of the variable. Even class objects may be input/output in this manner if the operators << (for output) and >> (for input) are overloaded suitably.

To output to a file, the syntax looks as follows:

```cpp
ofstream file("tmp.txt");
ofile<<x<<endl;
```

Here of is defined as an ofstream object. At the point of definition, it is tied to the file tmp.txt.

To input x from standard input, we may say

```cpp
cin>>x;
```

To input from a file, we may say

```cpp
ofstream file("tmp.txt");
ofile>>x;
```

This work regardless of whether x is a double or an int or a long or a char. The class names ofstream and ifstream as well as class objects cout and cin are defined in the namespace std. In general, we should say std::cout and std::ofstream because these names do not exist outside the namespace. However, the using namespace declaration on line 10 brings all the names in std into scope. It allows us to say cout instead of std::cout.

It is often not a good idea to bring in the std namespace, especially within header files. The C++ standard library is vast. Bringing in the entire std namespace, as we do on line 10, pollutes the namespace considerably. For example, a programmer may define a function copy() double arrays in a program-specific manner and conflict with the std namespace. There are functions with common names as copy() and sort() in the standard library.
