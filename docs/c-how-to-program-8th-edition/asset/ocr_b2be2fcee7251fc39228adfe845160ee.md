```
In printValues:
integer1 = 8
PI = 3.14159
E = 2.71828
doubleInUnnamed = 88.22
(global) integer1 = 98
FISCAL3 = 1992
```

**Fig. 24.3** | Demonstrating the use of namespaces. (Part 3 of 3.)

# *Defining Namespaces*

Lines 9--24 use the keyword namespace to define namespace Example1. The body of a namespace is delimited by braces ({}). Namespace Example1’s members consist of two constants (PI and E in lines 12--13), an int (integer1 in line 14), a function (printValues in line 16) and a nested namespace (Inner in lines 19--23). Notice that member integer1 has the same name as global variable integer1 (line 6). *Variables that have the same name must have different scopes*—otherwise compilation errors occur. A namespace can contain constants, data, classes, nested namespaces, functions, etc. Definitions of namespaces must occupy the global scope or be nested within other namespaces. Unlike classes, different namespace members can be defined in separate namespace blocks—each standard library header has a namespace block placing its contents in namespace std.

Lines 27--30 create an *unnamed namespace* containing the member doubleInUnnamed. Variables, classes and functions in an unnamed namespace are accessible only in the current *translation unit* (a .cpp file and the files it includes). However, unlike variables, classes or functions with static linkage, those in the unnamed namespace may be used as template arguments. The unnamed namespace has an implicit using directive, so its members appear to occupy the *global namespace*, are accessible directly and do not have to be qualified with a namespace name. Global variables are also part of the global namespace and can be accessed in all scopes following the declaration in the file.

> **Software Engineering Observation 24.2**
> 
> *Each separate compilation unit has its own unique unnamed namespace; i.e., the unnamed namespace replaces the static linkage specifier.*

# *Accessing Namespace Members with Qualified Names*

Line 35 outputs the value of variable doubleInUnnamed, which is directly accessible as part of the unnamed namespace. Line 38 outputs the value of global variable integer1. For both of these variables, the compiler first attempts to locate a local declaration of the variables in main. Since there are no local declarations, the compiler assumes those variables are in the global namespace.

Lines 41--43 output the values of PI, E, integer1 and FISCAL3 from namespace Example1. Notice that each must be qualified with Example1:: because the program does not provide any using directive or declarations indicating that it will use members of namespace Example1. In addition, member integer1 must be qualified, because a global variable has the same name. Otherwise, the global variable’s value is output. FISCAL3 is a member of nested namespace Inner, so it must be qualified with Example1::Inner::.