# 10.2.3.2 Instance variables in classes

An instance variable of a class comes into existence when a new instance of that class is created, and ceases to exist when there are no references to that instance and the instance’s finalizer (if any) has executed.

The initial value of an instance variable of a class is the default value (§10.3) of the variable’s type.

For the purpose of definite assignment checking, an instance variable of a class is considered initially assigned.

# 10.2.3.3 Instance variables in structs

An instance variable of a struct has exactly the same lifetime as the struct variable to which it belongs. In other words, when a variable of a struct type comes into existence or ceases to exist, so too do the instance variables of the struct.

The initial assignment state of an instance variable of a struct is the same as that of the containing struct variable. In other words, when a struct variable is considered initially assigned, so too are its instance variables, and when a struct variable is considered initially unassigned, its instance variables are likewise unassigned.

# 10.2.4 Array elements

The elements of an array come into existence when an array instance is created, and cease to exist when there are no references to that array instance.

The initial value of each of the elements of an array is the default value (§10.3) of the type of the array elements.

For the purpose of definite assignment checking, an array element is considered initially assigned.

# 10.2.5 Value parameters

A parameter declared without a ref or out modifier is a value parameter.

A value parameter comes into existence upon invocation of the function member (method, instance constructor, accessor, or operator) or anonymous function to which the parameter belongs, and is initialized with the value of the argument given in the invocation. A value parameter normally ceases to exist when execution of the function body completes. However, if the value parameter is captured by an anonymous function (§12.16.6.2), its lifetime extends at least until the delegate or expression tree created from that anonymous function is eligible for garbage collection.

# 10.2.6 Reference parameters

A parameter declared with a ref modifier is a reference parameter.

A reference parameter does not create a new storage location. Instead, a reference parameter represents the same storage location as the variable given as the argument in the function member or anonymous function invocation. Thus, the value of a reference parameter is always the same as the underlying variable.

The following definite assignment rules apply to reference parameters. [Note: The rules for output parameters are different, and are described in §10.2.7. end note]

+   - A variable shall be definitely assigned (§10.4) before it can be passed as a reference parameter in a function member or delegate invocation.
+   - Within a function member or anonymous function, a reference parameter is considered initially assigned.