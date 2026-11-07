
## Summary

### Section 3.2 Defining a Class with a Member Function

- A class definition (p. 68) contains the data members and member functions that define the class’s attributes and behaviors, respectively.
- A class definition begins with the keyword `class` followed immediately by the class name.
- By convention, the name of a user-defined class (p. 69) begins with a capital letter and, for readability, each subsequent word in the class name begins with a capital letter.
- Every class’s body (p. 68) is enclosed in a pair of braces (`{` and `}`) and ends with a semicolon.
- Member functions that appear after access specifier `public` (p. 68) can be called by other functions in a program and by member functions of other classes.
- Access specifiers are always followed by a colon (`:`).
- Keyword `void` (p. 69) is a special return type which indicates that a function will perform a task but will not return any data to its calling function when it completes its task.
- By convention, function names (p. 69) begin with a lowercase first letter and all subsequent words in the name begin with a capital letter.
- An empty set of parentheses after a function name indicates that the function does not require additional data to perform its task.
- A function that does not, and should not, modify the object on which it’s called should be declared `const`.
- Typically, you cannot call a member function until you create an object of its class.
- Each new class you create becomes a new type in C++.
- In the UML, each class is modeled in a class diagram (p. 70) as a rectangle with three compartments, which (top to bottom) contain the class’s name, attributes and operations, respectively.
- The UML models operations as the operation name followed by parentheses. A plus sign (+) preceding the name indicates a public operation (i.e., a public member function in C++).

### Section 3.3 Defining a Member Function with a Parameter

- A member function can require one or more parameters (p. 70) that represent additional data it needs to perform its task. A function call supplies an argument (p. 71) for each function parameter.
- A member function is called by following the object name with a dot (`.`) operator (p. 70), the function name and a set of parentheses containing the function’s arguments.
- A variable of C++ Standard Library class `string` is a string of characters. This class is defined in header `<string>`, and the name string belongs to namespace `std`.
- Function `getline` (from header `<string>`, p. 72) reads characters from its first argument until a newline character is encountered, then places the characters (not including the newline) in the string variable specified as its second argument. The newline character is discarded.
- A parameter list (p. 73) may contain any number of parameters, including none at all (represented by empty parentheses) to indicate that a function does not require any parameters.
- The number of arguments in a function call must match the number of parameters in the parameter list of the called member function’s header. Also, the argument types in the function call must be consistent with the types of the corresponding parameters in the function header.
- The UML models a parameter of an operation by listing the parameter name, followed by a colon and the parameter type between the parentheses following the operation name.
- The UML has its own data types. Not all the UML data types have the same names as the corresponding C++ types. The UML type `String` corresponds to the C++ type `string`.

**3.10** *(Set and Get Functions)* Explain why a class might provide a *set* function and a *get* function for a data member.

**3.11** *(Modifying Class GradeBook)* Modify class GradeBook (Figs. 3.11–3.12) as follows:

- a) Include a second `string` data member that represents the course instructor’s name.
- b) Provide a *set* function to change the instructor’s name and a *get* function to retrieve it.
- c) Modify the constructor to specify course name and instructor name parameters.
- d) Modify function `displayMessage` to output the welcome message and course name, then the string "This course is presented by: " followed by the instructor’s name.

Use your modified class in a test program that demonstrates the class’s new capabilities.

**3.12** *(Account Class)* Create an `Account` class that a bank might use to represent customers’ bank accounts. Include a data member of type `int` to represent the account balance. [Note: In subsequent chapters, we’ll use numbers that contain decimal points (e.g., 2.75)—called floating-point values—to represent dollar amounts.] Provide a constructor that receives an initial balance and uses it to initialize the data member. The constructor should validate the initial balance to ensure that it’s greater than or equal to 0. If not, set the balance to 0 and display an error message indicating that the initial balance was invalid. Provide three member functions. Member function `credit` should add an amount to the current balance. Member function `debit` should withdraw money from the `Account` and ensure that the debit amount does not exceed the `Account`’s balance. If it does, the balance should be left unchanged and the function should print a message indicating "Debit amount exceeded account balance." Member function `getBalance` should return the current balance. Create a program that creates two `Account` objects and tests the member functions of class `Account`.

**3.13** *(Invoice Class)* Create a class called `Invoice` that a hardware store might use to represent an invoice for an item sold at the store. An `Invoice` should include four data members—a part number (type `string`), a part description (type `string`), a quantity of the item being purchased (type `int`) and a price per item (type `int`). [Note: In subsequent chapters, we’ll use numbers that contain decimal points (e.g., 2.75)—called floating-point values—to represent dollar amounts.] Your class should have a constructor that initializes the four data members. A constructor that receives multiple arguments is defined with the form:

```
ClassName( TypeName1 parameterName1, TypeName2 parameterName2, . . . )
```

Provide a *set* and a *get* function for each data member. In addition, provide a member function named `getInvoiceAmount` that calculates the invoice amount (i.e., multiplies the quantity by the price per item), then returns the amount as an `int` value. If the quantity is not positive, it should be set to 0. If the price per item is not positive, it should be set to 0. Write a test program that demonstrates class `Invoice`’s capabilities.

**3.14** *(Employee Class)* Create a class called `Employee` that includes three pieces of information as data members—a first name (type `string`), a last name (type `string`) and a monthly salary (type `int`). [Note: In subsequent chapters, we’ll use numbers that contain decimal points (e.g., 2.75)—called floating-point values—to represent dollar amounts.] Your class should have a constructor that initializes the three data members. Provide a *set* and a *get* function for each data member. If the monthly salary is not positive, set it to 0. Write a test program that demonstrates class `Employee`’s capabilities. Create two `Employee` objects and display each object’s yearly salary. Then give each Employee a 10 percent raise and display each Employee’s yearly salary again.

**3.15** *(Date Class)* Create a class called `Date` that includes three pieces of information as data members—a month (type `int`), a day (type `int`) and a year (type `int`). Your class should have a constructor with three parameters that uses the parameters to initialize the three data members. For the purpose of this exercise, assume that the values provided for the year and day are correct, but ensure that the month value is in the range 1–12; if it isn’t, set the month to 1. Provide a *set* and a *get* function for each data member. Provide a member function `displayDate` that displays the month, day
