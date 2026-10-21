operators for user-defined objects for providing I/O operations. On the contrary, objects are not available in C I/O stream and it has no mechanism to provide such natural I/O to user-defined objects.

+   2. C++ I/O stream contains richer formatting options than C. It is possible to have the programmer's own format operators known as user-defined manipulators in C++. We will be learning about manipulators in Section 12.11.
+   
+   3. Though not apparent at first glance, C++ I/O is much easier to use. We have seen the use of cin without the '&' operator unlike scanf(). We have also used overloaded << and >> operators for I/O. For file manipulation, C++ provides constructor functions, which makes it very easy to use files. Writing to and reading from text files can be performed using >> and << operators. We will be looking at those operations in Chapter 13.

> Note C++ I/O streams are object-oriented, contains richer formatting options, and are more user-friendly than C-type I/O.

# 12.3 OLD C++ I/O VS ANSI C++ I/O

ANSI C++ I/O has the following two important differences as compared to the original C++ I/O.

+   Richer set of operations
+   
+   ANSI C++ I/O has more number of operations than the old I/O. The old I/O was supported by iostream.h file, whereas the new I/O is supported by iostream file. There are some new data types and new features in the newer version of the I/O library. The ios class contains the fundamental operations that are possible to be performed on the stream. These operations are provided as member functions. The ios class also contains a number of variables that can be manipulated to achieve the desired effect on the stream that is being dealt with. I/O has been enhanced to a large extent in the newer version.

> Separate namespace and no global sharing
> 
> The old library used to work in the global namespace, but the new library works in the std namespace. The difference will be clearer when we study namespaces in Chapter 16. At the moment, consider namespaces as a type of wrapper. If C++ standard library contains one function, one cannot create another function with the same name in the same namespace.

> There are two important differences between old and new C++ IOs; it is richer in operations and uses a separate namespace.

> Two functions with the same name can be differentiated if they are a part of two different namespaces.

> Third-party library developers can name functions in their own way without worrying about colliding with names used by standard library or some other library developer.

Suppose there are two abs() functions, one for absolute values (provided by the standard library) and another for displaying the absent students in an educational organization, with the same set of arguments. In such cases, the compiler is bound to get confused and hence the program will not be compiled. As per the programmer’s wish, because the library functions are not available in the global namespace. If the function abs() is now defined for absent percentage, one can differentiate between both the functions, abs()(programmer’s function) and std::abs()(the standard library function). Note that here it is assumed that one has not written using namespace std as usual.

This facility makes life easier for the programmers of the third-party libraries while naming their global variables and functions. They can name them as they like. If there is a need to develop a library for a client, it is possible to define functions without having to bother about possible conflicts. Without namespaces,