# Chapter 9

+   - A function in a base class may be declared as `virtual`. This allows other definitions of the function appearing in derived classes to be selected at execution time, depending on the type of object for which the function call is made.
+   - You should declare the destructor in a native C++ class base class that contains a virtual function as `virtual`. This ensures correct selection of a destructor for dynamically-created derived class objects.
+   - A native C++ class may be designated as a `friend` of another class. In this case, all the function members of the friend class may access all the members of the other class. If class A is a friend of B, class B is not a friend of A unless it has been declared as such.
+   - A virtual function in a native C++ base class can be specified as pure by placing `= 0` at the end of the function declaration. The class then is an abstract class for which no objects can be created. In any derived class, all the pure virtual functions must be defined; if not, it, too, becomes an abstract class.
+   - A C++/CLI reference class can be derived from another reference classes. Value classes cannot be derived classes.
+   - An interface class declares a set of public functions that represent a specific capability that can be implemented by a reference class. An interface class can contain public functions, events, and properties. An interface can also define static data members, functions, events and properties and these are inherited in a class that implements the interface.
+   - An interface class can be derived from another interface class and the derived interface contains the members of both interfaces.
+   - A delegate is an object that encapsulates one or more pointers to functions that have the same return type and parameter list. Invoking a delegate calls all the functions pointed to by the delegate.
+   - An event member of a class can signal when the event occurs by calling one or more handler functions that have been registered with the event.
+   - A generic class is a parameterized type that is instantiated at run-time. The arguments you supply for type parameters when you instantiate a generic type can be value class types or reference class types.
+   - The `System::collections::Generic` namespace contains generic collection classes that define typesafe collections of objects of any C++/CLI type.
+   - You can create a C++/CLI class library in a separate assembly and the class library resides in a `.dll` file.

You have now gone through all of the important language features of ANSI/ISO C++ and C++/CLI. It’s important that you feel comfortable with the mechanisms for defining and deriving classes and the process of inheritance in both language versions. Windows programming with Visual C++ 2005 involves extensive use of all these concepts.

# Exercises

You can download the source code for the examples in the book and the solutions to the following exercises from http://www.wrox.com.