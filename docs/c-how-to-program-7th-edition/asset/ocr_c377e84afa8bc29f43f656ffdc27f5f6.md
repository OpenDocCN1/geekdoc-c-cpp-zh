+   - A local variable must be declared before it can be used in a function. A local variable cannot be accessed outside the function in which it's declared.
+   - Data members normally are `private`. Variables or functions declared `private` are accessible only to member functions of the class in which they're declared, or to friends of the class.
+   - When a program creates (instantiates) an object of a class, its `private` data members are encapsulated (hidden) in the object and can be accessed only by member functions of the object's class.
+   - When a function that specifies a return type other than `void` is called and completes its task, the function returns a result to its calling function.
+   - By default, the initial value of a `string` is the empty string—i.e., a string that does not contain any characters. Nothing appears on the screen when an empty string is displayed.
+   - Classes often provide `public` member functions to allow clients of the class to `set` or `get` private data members. The names of these member functions normally begin with `set` or `get`.
+   - `Set` and `get` functions allow clients of the class to indirectly access the hidden data. The client does not know how the object performs these operations.
+   - A class's `set` and `get` functions should be used by other member functions of the class to manipulate the class's `private` data. If the class's data representation is changed, member functions that access the data only via the `set` and `get` functions will not require modification.
+   - A `public` `set` function should carefully scrutinize any attempt to modify the value of a data member to ensure that the new value is appropriate for that data item.
+   - The UML represents data members as attributes by listing the attribute name, followed by a colon and the attribute type. Private attributes are preceded by a minus sign (-) in the UML.
+   - The UML indicates the return type of an operation by placing a colon and the return type after the parentheses following the operation name.
+   - UML class diagrams do not specify return types for operations that do not return values.

# ### Section 3.6 Initializing Objects with Constructors

+   - Each class should provide a constructor to initialize an object of the class when the object is created. A constructor must be defined with the same name as the class.
+   - A difference between constructors and functions is that constructors cannot return values, so they cannot specify a return type (not even `void`). Normally, constructors are declared `public`.
+   - C++ requires a constructor call at the time each object is created, which helps ensure that every object is initialized before it's used in a program.
+   - A constructor with no parameters is a default constructor. If you do not provide a constructor, the compiler provides a default constructor. You can also define a default constructor explicitly. If you define a constructor for a class, C++ will not create a default constructor.
+   - The UML models constructors as operations in a class diagram's third compartment with the word `constructor` between guillemets (`<<` and `>>`) before the constructor's name.

# ### Section 3.7 Placing a Class in a Separate File for Reusability

+   - Class definitions, when packaged properly, can be reused by programmers worldwide.
+   - It's customary to define a class in a header file that has a `.h` filename extension.
+   - If the class's implementation changes, the class's clients should not be required to change.
+   - Interfaces define and standardize the ways in which things such as people and systems interact.
+   - A class's `public` interface describes the `public` member functions that are made available to the class's clients. The interface describes *what* services clients can use and how to *request* those services, but does not specify *how* the class carries out the services.