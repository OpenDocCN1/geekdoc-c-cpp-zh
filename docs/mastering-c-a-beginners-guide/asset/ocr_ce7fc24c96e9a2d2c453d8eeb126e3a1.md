Similarly, we may witness multiple data types in the same way while the code is being developed. For example, we have a bunch of strings in a code. In it, we perform certain kinds of operations by using the built-in functionality of the list. Not only that, there is a list of integers in the code, where we have the absolute freedom to run the operations using the built-in list functionality.

So imagine there is a need to implement a user-defined functionality, and it has to be familiar and work with all the primitive and user-defined data types. So there is a need to develop a generic class similar to List (that comes with C# collections), and it should include methods like the ones that are in lists (Add, AddRange, Where, etc.). And the methods have got to work with the same set of data types as the new class.

So, how to create a user-defined class with data types assigned at run time and executes methods that are part of it? C# comes with a feature called Generics provides us an answer to this.

# WHAT ARE GENERICS

Generic is a class that lets the user define classes and methods with the placeholder. Generics were incorporated into version 2.0 of the C# language. The fundamental idea behind using Generic is to let type (Integer, String, ... etc., and user-defined types) be a parameter to classes, methods, and interfaces. A main limitation of collections is the absence of productive type checking. This actually means that you can put any object in a collection as all classes in the C# programming language stick out from the object