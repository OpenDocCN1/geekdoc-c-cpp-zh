Visual Studio allows you to right-click on a block of code within a method and click Quick Actions and Refactorings... (Ctrl+) to extract the block into its own method, automatically inserting code to call the new method from the original location.

# Formal Parameter Declaration

Consider the declarations of the DisplayGreeting(), GetFullName(), and the GetInitials() methods. The text that appears between parentheses of a method declaration is the formal parameter list. (As we will see when we discuss generics, methods may also have a type parameter list. When it is clear from the context which kind of parameters we are discussing, simply refer to them as parameters in a parameter list.) Each parameter in the parameter list includes the type of the parameter along with the parameter name. A comma separates each parameter in the list.

Behaviorally, most parameters are virtually identical to local variables, and the naming convention of parameters follows accordingly. Therefore, parameter names use camelCase. Also, it is not possible to declare a local variable (a variable declared inside a method) with the same name as a parameter of the containing method, because this would create two local variables of the same name.

> Guidelines
DO use camelCasing for parameter names.

# Method Return Type Declaration

In addition to GetUserInput(), GetFullName(), and the GetInitials() each of these methods includes a method return type to be specified, You can tell that a method returns a value because a data type appears immediately before the method name in the method declaration. Each of these method examples specifies a string return type. Unlike parameters, of which there can be any number, only one return type is allowable.