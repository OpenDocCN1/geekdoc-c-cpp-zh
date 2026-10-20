+   - At the time a method is called, its arguments are assigned to its parameters. Then the method body uses the parameter variables to access the argument values.
+   - A method specifies multiple parameters in a comma-separated list.
+   - The number of arguments in the method call must match the number of parameters in the method declaration’s parameter list. Also, the argument types in the method call must be consistent with the types of the corresponding parameters in the method’s declaration.
+   - Class String is in package java.lang, which is imported implicitly into all source-code files.
+   - By default, classes compiled into the same directory are in the same package. Classes in the same package are implicitly imported into the source-code files of other classes in the same package.
+   - import declarations are not required if you always use fully qualified class names (p. 79).
+   - The UML models a parameter of an operation by listing the parameter name, followed by a colon and the parameter type between the parentheses following the operation name.
+   - The UML has its own data types similar to those of Java. Not all the UML data types have the same names as the corresponding Java types.
+   - The UML type String corresponds to the Java type String.

# Section 3.4 Instance Variables, set Methods and get Methods

+   - Variables declared in a method’s body are local variables and can be used only in that method.
+   - A class normally consists of one or more methods that manipulate the attributes (data) that belong to a particular object of the class. Such variables are called fields and are declared inside a class declaration but outside the bodies of the class’s method declarations.
+   - When each object of a class maintains its own copy of an attribute, the corresponding field is known as an instance variable.
+   - Variables or methods declared with access modifier private are accessible only to methods of the class in which they’re declared.
+   - Declaring instance variables with access modifier private (p. 80) is known as data hiding.
+   - A benefit of fields is that all the methods of the class can use the fields. Another distinction between a field and a local variable is that a field has a default initial value (p. 82) provided by Java when you do not specify the field’s initial value, but a local variable does not.
+   - The default value for a field of type String (or any other reference type) is null.
+   - When a method that specifies a return type (p. 73) is called and completes its task, the method returns a result to its calling method (p. 73).
+   - Classes often provide public methods to allow the class’s clients to set or get private instance variables (p. 83). The names of these methods need not begin with set or get, but this naming convention is recommended and is required for special Java software components called JavaBeans.
+   - The UML represents instance variables as an attribute name, followed by a colon and the type.
+   - Private attributes are preceded by a minus sign (–) in the UML.
+   - The UML indicates an operation’s return type by placing a colon and the return type after the parentheses following the operation name.
+   - UML class diagrams (p. 75) do not specify return types for operations that do not return values.

# Section 3.5 Primitive Types vs. Reference Types

+   - Types in Java are divided into two categories—primitive types and reference types. The primitive types are boolean, byte, char, short, int, long, float and double. All other types are reference types, so classes, which specify the types of objects, are reference types.