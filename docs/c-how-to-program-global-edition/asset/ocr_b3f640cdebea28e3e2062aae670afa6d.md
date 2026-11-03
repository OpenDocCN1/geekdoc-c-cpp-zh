+   - The UML has its own data types. Not all the UML data types have the same names as the corresponding C++ types. The UML type string corresponds to the C++ type string.

# Section 16.4 Data Members, set Member Functions and get Member Functions

+   - Variables declared in a function's body are local variables (p. 629) and can be used only from the point of their declaration to the closing right brace } of the block in which they are declared.
+   - A local variable must be declared before it can be used in a function. A local variable cannot be accessed outside the function in which it's declared.
+   - Data members (p. 629) normally are private (p. 631). Variables or functions declared private are accessible only to member functions of the class in which they're declared, or to friends of the class.
+   - When a program creates (instantiates) an object, its private data members are encapsulated (hidden, p. 631) in the object and can be accessed only by member functions of the object's class (or by "friends" of the class, as you'll see in Chapter 17).
+   - When a function that specifies a return type other than void is called and completes its task, the function returns a result to its calling function.
+   - By default, the initial value of a string is the empty string (p. 632)—i.e., a string that does not contain any characters. Nothing appears on the screen when an empty string is displayed.
+   - A class often provides public member functions to allow the class's clients to set or get (p. 633) private data members. The names of these member functions normally begin with set or get.
+   - Set and get functions allow clients of a class to indirectly access the hidden data. The client does not know how the object performs these operations.
+   - A class's set and get functions should be used by other member functions of the class to manipulate the class's private data. If the class's data representation is changed, member functions that access the data only via the set and get functions will not require modification.
+   - A public set function should carefully scrutinize any attempt to modify the value of a data member to ensure that the new value is appropriate for that data item.
+   - The UML represents data members as attributes by listing the attribute name, followed by a colon and the attribute type. Private attributes are preceded by a minus sign (-) in the UML.
+   - The UML indicates the return type of an operation by placing a colon and the return type after the parentheses following the operation name.
+   - UML class diagrams do not specify return types for operations that do not return values.

# Section 16.5 Initializing Objects with Constructors

+   - Each class should provide one or more constructors (p. 634) to initialize an object of the class when the object is created. A constructor must be defined with the same name as the class.
+   - A difference between constructors and functions is that constructors cannot return values, so they cannot specify a return type (not even void). Normally, constructors are declared public.
+   - C++ automatically calls a constructor for each object that's created, which helps ensure that objects are initialized properly before they're used in a program.
+   - A constructor with no parameters is a default constructor (p. 635). If you do not provide a constructor, the compiler provides a default constructor. You can also define a default constructor explicitly. If you define any constructors for a class, C++ will not create a default constructor.
+   - A single-parameter constructor should be declared explicit.
+   - A constructor uses a member initializer list to initialize a class's data members. Member initializers appear between a constructor's parameter list and the left brace that begins the constructor's