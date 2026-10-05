# Libraries and Namespaces

C++ comes with a number of standard libraries. These libraries place their definitions in a namespace, which is simply a name given to a collection of definitions. The techniques for including libraries and dealing with namespaces will be discussed in detail later in this book. This section discusses enough to allow you to use the standard C++ libraries.

# Libraries and include Directives

C++ includes a number of standard libraries. In fact, it is almost impossible to write a C++ program without using at one of these libraries. The normal way to make a library available to your program is with an include directive. An include directive for a standard library has the form

```
#include <Library_Name>
```

For example, for the console I/O is iostream. Most of our demonstration programs will begin

```
#include <iostream>
```

Compilers (preprocessors) can be very fussy about spacing in include directives. Thus, it is safest to type an include directive with no extra space: # no space before the #, and no spaces inside the <.

An include directive is a simple instruction to include the text found in a file at the location of the include directive. A library name is simply the name of a file that includes all the definition of items in the library. We will eventually discuss include directives for other than standard libraries, but for now we only need include directives for standard C++ libraries. A list of standard C++ libraries is given in Appendix A.

C++ has a preprocessor that handles some textual manipulation before the text of your program is given to the compiler. Some people will tell you that include directives are not processed by the compiler but by a preprocessor. They're right, but the difference is more of a word than anything that will concern you. On all compilers, the preprocessor is called automatically when you compile your program.

Technically speaking, only part of the library definition is given in the header file. However, at this stage, it is not an important distinction, since the include directive with the header file for a library will (on almost all systems) cause C++ to automatically add the rest of the library definition.

# Namespaces

A namespace is a collection of name definitions. In fact, such as a name, can be different definitions in two namespaces. A program can then use one of these namespaces in one place and the other in another location. We will