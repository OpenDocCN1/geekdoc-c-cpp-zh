+   - In the UML, each class is modeled in a class diagram (p. 68) as a rectangle with three compartments, which (top to bottom) contain the class’s name, attributes and operations, respectively.
+   - The UML models operations as the operation name followed by parentheses. A plus sign (+) preceding the name indicates a public operation (i.e., a public member function in C++).

# ### *Section 3.3 Defining a Member Function with a Parameter*

+   - A member function can require one or more parameters (p. 68) that represent additional data it needs to perform its task. A function call supplies an argument (p. 68) for each function parameter.
+   - A member function is called by following the object name with a dot (.) operator (p. 67), the function name and a set of parentheses containing the function’s arguments.
+   - A variable of C++ Standard Library class string (p. 69) represents a string of characters. This class is defined in header `<string>`, and the name string belongs to namespace `std`.
+   - Function `getline` (from header `<string>`, p. 70) reads characters from its first argument until a newline character is encountered, then places the characters (not including the newline) in the string variable specified as its second argument. The newline character is discarded.
+   - A parameter list (p. 70) may contain any number of parameters, including none at all (represented by empty parentheses) to indicate that a function does not require any parameters.
+   - The number of arguments in a function call must match the number of parameters in the parameter list of the called member function’s header. Also, the argument types in the function call must be consistent with the types of the corresponding parameters in the function header.
+   - The UML models a parameter of an operation by listing the parameter name, followed by a colon and the parameter type between the parentheses following the operation name.
+   - The UML has its own data types. Not all the UML data types have the same names as the corresponding C++ types. The UML type String corresponds to the C++ type string.

# ### *Section 3.4 Data Members, set Functions and get Functions*

+   - Variables declared in a function’s body are local variables (p. 71) and can be used only from the point of their declaration in the function to the immediately following closing right brace (`}`).
+   - A local variable must be declared before it can be used in a function. A local variable cannot be accessed outside the function in which it’s declared.
+   - Data members (p. 71) normally are private (p. 73). Variables or functions declared private are accessible only to member functions of the class in which they’re declared, or to friends of the class.
+   - When a program creates (instantiates) an object, its private data members are encapsulated (hidden, p. 74) in the object and can be accessed only by member functions of the object’s class.
+   - When a function that specifies a return type other than void is called and completes its task, the function returns a result to its calling function.
+   - By default, the initial value of a string is the empty string (p. 75)—i.e., a string that does not contain any characters. Nothing appears on the screen when an empty string is displayed.
+   - A class often provides public member functions to allow a class’s clients to set or get (p. 75) private data members. The names of these member functions normally begin with set or get.
+   - Set and get functions allow clients of a class to indirectly access the hidden data. The client does not know how the object performs these operations.
+   - A class’s set and get functions should be used by other member functions of the class to manipulate the class’s private data. If the class’s data representation is changed, member functions that access the data only via the set and get functions will not require modification.
+   - A public set function should carefully scrutinize any attempt to modify the value of a data member to ensure that the new value is appropriate for that data item.