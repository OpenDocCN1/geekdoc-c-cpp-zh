+   1. A function template is a mechanism for generating a new function.
+   2. A class template is a mechanism for generating a new class.
+   3. A template parameter can be either a type or a value.
+   4. All of the template parameters in a function template definition must be used in the function interface. The template parameters can also be used in the function body.
+   5. The proposed C++ standard describes a standard template library that in part includes template versions of common computing tasks such as searching and sorting.
+   6. All of the template parameters in a class template must be used in the definition of the class interface.
+   7. Through the use of class templates, we can develop a container class that represents lists in an array like manner. A major reason that such a container class is preferred to standard arrays is that the container class does not suffer array use limitations (e.g., a container class can be the return type of a function or be a value parameter).
+   8. The standard template library defines a collection of common container classes for list representation. The representations differ in how the elements of the list can be accessed. Various container classes support random access of the elements, sequential access of the elements, and associative access of the elements.
+   9. Often a container class will have an iterator class associated with it. The iterator class provides the means for iteratively accessing the various elements of the list.
+   10. Exception handling is designed for dealing with synchronous errors.
+   11. Exceptions are thrown in try block in a function or in a function called directly or indirectly form the try block.