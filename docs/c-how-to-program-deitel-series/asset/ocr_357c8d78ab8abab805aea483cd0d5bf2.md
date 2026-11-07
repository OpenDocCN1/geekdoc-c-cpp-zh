# ## 23.4 namespaces

A program may include many identifiers defined in different scopes. Sometimes a variable of one scope will “overlap” (i.e., collide) with a variable of the *same name* in a *different* scope, possibly creating a *naming conflict*. Such overlapping can occur at many levels. Identifier overlapping occurs frequently in third-party libraries that happen to use the same names for global identifiers (such as functions). This can cause compilation errors.

C++ solves this problem with **namespaces**. Each namespace defines a scope in which identifiers and variables are placed. To use a **namespace member**, either the member’s name must be qualified with the namespace name and the *scope resolution operator* (`::`), as in

```
MyNameSpace::member
```

or a using directive must appear before the name is used in the program. Typically, such using statements are placed at the beginning of the file in which members of the namespace are used. For example, placing the following using directive at the beginning of a source-code file

```
using namespace MyNameSpace;
```

specifies that members of namespace *MyNameSpace* can be used in the file without preceding each member with *MyNameSpace* and the scope resolution operator (`::`).

A using directive of the form

```
using std::cout;
```

brings *one name* into the scope where the directive appears. A using directive of the form

```
using namespace std;
```

brings *all* the names from the specified namespace (`std`) into the scope where the directive appears.

> **Error-Prevention Tip 23.2**
> 
> *Precede a member with its namespace name and the scope resolution operator (`::`) if the possibility exists of naming conflict.*

*Not all namespaces are guaranteed to be unique.* Two third-party vendors might inadvertently use the same identifiers for their namespace names. Figure 23.3 demonstrates the use of namespaces.

```
1  // Fig. 23.3: fig23_03.cpp
2  // Demonstrating namespaces.
3  #include <iostream>
4  using namespace std;

6  int integer1 = 98; // global variable

8  // create namespace Example
9  namespace Example
   {
```

**Fig. 23.3**  |  Demonstrating the use of namespaces. (Part 1 of 3.)