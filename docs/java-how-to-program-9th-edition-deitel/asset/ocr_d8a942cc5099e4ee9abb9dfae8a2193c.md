+   - When a method has more than one parameter, the parameters are specified as a comma-separated list. There must be one argument in the method call for each parameter in the method declaration. Also, each argument must be consistent with the type of the corresponding parameter. If a method does not accept arguments, the parameter list is empty.
+   - Strings can be concatenated (p. 204) using operator +, which places the characters of the right operand at the end of those in the left operand.
+   - Every primitive value and object in Java has a String representation. When an object is concatenated with a String, the object is converted to a String, then the two Strings are concatenated.
+   - If a boolean is concatenated with a String, the word "true" or the word "false" is used to represent the boolean value.
+   - All objects in Java have a special method named toString that returns a String representation of the object's contents. When an object is concatenated with a String, the JVM implicitly calls the object's toString method to obtain the string representation of the object.
+   - You can break large String literals into several smaller Strings and place them on multiple lines of code for readability, then reassemble the Strings using concatenation.

# Section 6.5 Notes on Declaring and Using Methods

+   - There are three ways to call a method—using a method name by itself to call another method of the same class; using a variable that contains a reference to an object, followed by a dot (.) and the method name to call a method of the referenced object; and using the class name and a dot (.) to call a static method of a class.
+   - There are three ways to return control to a statement that calls a method. If the method does not return a result, control returns when the program flow reaches the method-ending right brace or when the statement
+   
+     `return;`
+   
+   is executed. If the method returns a result, the statement
+   
+     `return expression;`
+   
+   evaluates the *expression*, then immediately returns the resulting value to the caller.

# Section 6.6 Method-Call Stack and Activation Records

+   - Stacks (p. 206) are known as last-in, first-out (LIFO) data structures—the last item pushed (inserted) on the stack is the first item popped (removed) from the stack.
+   - A called method must know how to return to its caller, so the return address of the calling method is pushed onto the program-execution stack when the method is called. If a series of method calls occurs, the successive return addresses are pushed onto the stack in last-in, first-out order so that the last method to execute will be the first to return to its caller.
+   - The program-execution stack (p. 207) contains the memory for the local variables used in each invocation of a method during a program's execution. This data is known as the method call's activation record or stack frame. When a method call is made, the activation record for that method call is pushed onto the program-execution stack. When the method returns to its caller, its activation record call is popped off the stack and the local variables are no longer known to the program.
+   - If there are more method calls than can have their activation records stored on the program-execution stack, an error known as a stack overflow (p. 207) occurs. The application will compile correctly, but its execution causes a stack overflow.

# Section 6.7 Argument Promotion and Casting

+   - Argument promotion (p. 207) converts an argument's value to the type that the method expects to receive in its corresponding parameter.