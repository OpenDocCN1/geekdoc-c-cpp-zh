This chapter presents the basics of the C++ programming language. The top-level programming topics we will learn about are as follows:

+   - Constants, variables, `auto`, and built-in data types
+   - Common containers and algorithms from the Standard Library
+   - Basics of data structures and their initialization
+   - Introduction to classes
+   - Indirect object access with references
+   - Indirect object access with pointers
+   - C++ statements
+   - Functions, passing objects from and to functions, and lambda functions
+   - C++ operators

We will analyze and present detailed implementations of several projects that we hope will be interesting. Our goal is to show some programming techniques and, in particular, C++ features in action.



To perform computations, we need to represent data and define operations on it. Data is stored in the dedicated computer’s memory regions as what we will call _objects_, although we will extend this concept soon. All computer languages have ways to reserve sufficient memory, initialize such objects, and read from and/or write to them. However, all of them require a means of access. This can be

+   - _Direct_, by providing a direct name for an object, or
+   - _Indirect_, by providing a _link_ to an object (a reference or a pointer)

Objects can be further divided into the following two groups:

+   - _Mutable_ – After creation and initialization, the objects can be further changed. These are also all variables
+   - _Immutable_ – Such objects can be created and initialized, but they cannot be changed. These are called constants