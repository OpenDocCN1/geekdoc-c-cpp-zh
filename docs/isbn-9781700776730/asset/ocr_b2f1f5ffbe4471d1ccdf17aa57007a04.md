# Encapsulation

While it is possible to hide implementation details in almost any programming language, C++ explicitly supports it by providing mechanisms to prevent clients from accessing data and operations that are supposed to be hidden.

The provider of a C++ ADT can specify private data and private operations, so if a client program attempts to use them, the C++ compiler issues an error message. This enforcement of the separation between specification and implementation is called *encapsulation*.

Encapsulation is an extremely important feature because without it we must rely on clients to cooperate by observing the separation between the specification and the implementation. Experience tells us that this is not practical, particularly on large software projects involving more than a few programmers. Somebody inevitably forgets the rules or succumbs to the temptation to use an implementation-dependent optimization, and the guarantee of being able to change an implementation without causing client problems to malfunction is gone.

# Overview of C++ Support for Data Abstraction

C++ provides the class declaration for defining ADTs. A C++ class is similar to a C struct, but it allows you to associate both variables and functions with the name of a data type.

The variables and functions that belong to a class are *members*. You can make a member either public or private. Any program can use the public members of a class. But only member functions of the same class can use its private members.

You can practice encapsulation in C++ by declaring classes with all member variables, private, so that the clients can access or modify them only as permitted by the class's public member functions.

# Function Name Overloading

Unlike C, C++ requires you to specify the number any type of all of functions arguments. You can then use the same function name for more than one function as long as the number and/or type of the function arguments are distinctive. This is called *function name overloading*. Function name overloading eliminates the need to use different function names when you wish to perform the same operation on different data types.