
Rename in the GradeBook object to a shorter name that does not need to be truncated. Then, lines 25–28 output the course names for the GradeBook objects again.

## Additional Notes on Set Functions

A public set function such as setCourseName should carefully scrutinize any attempt to modify the value of a data member (e.g., courseName) to ensure that the new value is appropriate for that data item. For example, an attempt to set the day of the month to 37 should be rejected, an attempt to set a person’s weight to zero or a negative value should be rejected, an attempt to set a grade on an exam to 185 (when the proper range is zero to 100) should be rejected, and so on.

![](img/d0d3b7423c2d9e5650be79209ea1885d_652_0.png)

> **Software Engineering Observation 16.3**
> 
> *Making data members private and controlling access, especially write access, to those data members through public member functions helps ensure data integrity.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_652_1.png)

> **Error-Prevention Tip 16.4**
> 
> *The benefits of data integrity are not automatic simply because data members are made private—you must provide appropriate validity checking and report the errors.*

A set function could return a value indicating that an attempt was made to assign invalid data to an object of the class. A client could then test the return value of the set function to determine whether the attempt to modify the object was successful and to take appropriate action if not. We will do that in later chapters after we introduce a bit more programming technology. In C++, clients of objects also can be notified of problems via the exception-handling mechanism, which we present in-depth in Chapter 17.

## 16.9 Wrap-Up

In this chapter, you created user-defined classes, and created and used objects of those classes. We declared data members of a class to maintain data for each object of the class. We also defined member functions that operate on that data. You learned that member functions that do not modify a class’s data should be declared const. We showed how to call an object’s member functions to request the services the object provides and how to pass data to those member functions as arguments. We discussed the difference between a local variable of a member function and a data member of a class. We also showed how to use a constructor and a member-initializer list to ensure that every object is initialized properly. You learned that a single-parameter constructor should be declared explicit, and that a constructor cannot be declared const because it modifies the object being initialized.

We demonstrated how to separate the interface of a class from its implementation to promote good software engineering. You learned that using directives and using declarations should never be placed in headers. We presented a diagram that shows the files that class-implementation programmers and client-code programmers need to compile the code they write. We demonstrated how set functions can be used to validate an object’s data and ensure that objects are maintained in a consistent state. UML class diagrams were used to model classes and their constructors, member functions and data members. In the next chapter, we begin our deeper treatment of classes.

## Summary

### Section 16.2 Defining a Class with a Member Function

- A class definition (p. 625) contains the data members and member functions that define the class's attributes and behaviors, respectively.
- A class definition begins with the keyword class followed immediately by the class name.
- By convention, the name of a user-defined class (p. 624) begins with a capital letter and, for readability, each subsequent word in the class name begins with a capital letter.
- Every class's body (p. 623) is enclosed in a pair of braces ({ and }) and ends with a semicolon.
- Member functions that appear after access specifier public (p. 624) can be called by other functions in a program and by member functions of other classes.
- Access specifiers are always followed by a colon (:).
- Keyword void (p. 624) is a special return type which indicates that a function will perform a task but will not return any data to its calling function when it completes its task.
- By convention, function names (p. 624) begin with a lowercase first letter and all subsequent words in the name begin with a capital letter.
- An empty set of parentheses after a function name indicates that the function does not require additional data to perform its task.
- A function that does not, and should not, modify the object on which it's called should be declared const.
- Typically, you cannot call a member function until you create an object of its class.
- Each new class you create becomes a new type in C++.
- In the UML, each class is modeled in a class diagram (p. 625) as a rectangle with three compartments, which (top to bottom) contain the class's name, attributes and operations, respectively.
- The UML models operations as the operation name followed by parentheses. A plus sign (+) preceding the name indicates a public operation (i.e., a public member function in C++).

### Section 16.3 Defining a Member Function with a Parameter

- A member function can require one or more parameters (p. 625) that represent additional data it needs to perform its task. A function call supplies an argument (p. 626) for each function parameter.
- A member function is called by following the object name with a dot (.) operator (p. 625), the function name and a set of parentheses containing the function's arguments.
- A variable of C++ Standard Library class string (p. 627) represents a string of characters. This class is defined in header `<string>`, and the name string belongs to namespace std.
- Function getline (from header `<string>`, p. 627) reads characters from its first argument until a newline character is encountered, then places the characters (not including the newline) in the string variable specified as its second argument. The newline character is discarded.
- A parameter list (p. 628) may contain any number of parameters, including none at all (represented by empty parentheses) to indicate that a function does not require any parameters.
- The number of arguments in a function call must match the number of parameters in the parameter list of the called member function's header. Also, the argument types in the function call must be consistent with the types of the corresponding parameters in the function header.
- The UML models a parameter of an operation by listing the parameter name, followed by a colon and the parameter type between the parentheses following the operation name.
- The UML has its own data types. Not all the UML data types have the same names as the corresponding C++ types. The UML type String corresponds to the C++ type string.

### Section 16.4 Data Members, set Member Functions and get Member Functions

- Variables declared in a function’s body are local variables (p. 629) and can be used only from the point of their declaration to the closing right brace (}) of the block in which they are declared.
- A local variable must be declared before it can be used in a function. A local variable cannot be accessed outside the function in which it’s declared.
- Data members (p. 629) normally are private (p. 631). Variables or functions declared private are accessible only to member functions of the class in which they’re declared, or to friends of the class.
- When a program creates (instantiates) an object, its private data members are encapsulated (hidden, p. 631) in the object and can be accessed only by member functions of the object’s class (or by “friends” of the class, as you’ll see in Chapter 17).
- When a function that specifies a return type other than void is called and completes its task, the function returns a result to its calling function.
- By default, the initial value of a string is the empty string (p. 632)—i.e., a string that does not contain any characters. Nothing appears on the screen when an empty string is displayed.
- A class often provides public member functions to allow the class’s clients to set or get (p. 633) private data members. The names of these member functions normally begin with set or get.
- Set and get functions allow clients of a class to indirectly access the hidden data. The client does not know how the object performs these operations.
- A class’s set and get functions should be used by other member functions of the class to manipulate the class’s private data. If the class’s data representation is changed, member functions that access the data only via the set and get functions will not require modification.
- A public set function should carefully scrutinize any attempt to modify the value of a data member to ensure that the new value is appropriate for that data item.
- The UML represents data members as attributes by listing the attribute name, followed by a colon and the attribute type. Private attributes are preceded by a minus sign (-) in the UML.
- The UML indicates the return type of an operation by placing a colon and the return type after the parentheses following the operation name.
- UML class diagrams do not specify return types for operations that do not return values.

### Section 16.5 Initializing Objects with Constructors

- Each class should provide one or more constructors (p. 634) to initialize an object of the class when the object is created. A constructor must be defined with the same name as the class.
- A difference between constructors and functions is that constructors cannot return values, so they cannot specify a return type (not even void). Normally, constructors are declared public.
- C++ automatically calls a constructor for each object that’s created, which helps ensure that objects are initialized properly before they’re used in a program.
- A constructor with no parameters is a default constructor (p. 635). If you do not provide a constructor, the compiler provides a default constructor. You can also define a default constructor explicitly. If you define any constructors for a class, C++ will not create a default constructor.
- A single-parameter constructor should be declared explicit.
- A constructor uses a member initializer list to initialize a class’s data members. Member initializers appear between a constructor’s parameter list and the left brace that begins the constructor’s
