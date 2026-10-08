
## 324 Chapter 7 Methods: A Deeper Look

## Section 7.5 Notes on Declaring and Using Methods

- You've seen three ways to call a method—using a method name by itself to call another method of the same class; using a variable that contains a reference to an object, by the member access operator (.) and the method name to call a non-static method of the referenced object; and using the class and the member-access operator (.) to a static method of a class.
- A static method can call only static methods of the same class and can manipulate only static variables in the same class.
- You've seen three ways to return to the statement that calls a method—when the method-ending right brace in a method return type void is reached, when the following statement executes in a method return void:

```csharp
return;
```

and when a method returns a result with a statement of the following form in which the expression is evaluated and its result (and control) are returned to the caller:

```csharp
return expression;
```

## Section 7.6 Argument Promotion and Casting

- Another important feature of method calls is argument promotion—implicitly converting an argument's value to the type that the method expects to receive in its corresponding parameter.

## Section 7.6.1 Promotion Rules

- The argument-promotion rules apply to containing values of two or more types and to simple-type values passed as arguments to methods.

## Section 7.6.2 Explicit Casts Are Required

- In cases where information may be lost due to conversion between simple types, the compiler requires you to use a cast operator to explicitly force the conversion.

## Section 7.7 The .NET Framework Class Library

- Many defined classes are grouped into categories of related class namespaces. Together, these are referred to as the .NET Framework Class Library.

## Section 7.8.2 Generating a Random Integer

- Random Next() generates a random int value in the range 0 to +2,147,483,646, inclusive.
- The methods of class Random actually generate pseudorandom numbers based on mathematical calculations. The calculation that produces the pseudorandom numbers uses the time of day as a seed value to control the sequence's starting point.

## Section 7.8.3 Scaling the Random-Number Range

- Class Random provides other versions of Next. One receives an int and returns a value from 0 to up, but not including the argument. The other receives two ints and returns a value from the first argument's value up to, but not including, the second argument's value.

## Section 7.8.8 Repeatability for Testing and Debugging

- If the same seed is used every time, the Random object produces the same sequence of random numbers. Class Random's constructor can receive the seed value as an argument.

## Section 7.9.3 enum Type Status

- An enumeration is introduced by the keyword enum and a type name. Braces limit the body of an enum declaration. Inside the braces is a comma-separated list of enumeration constants.
- Variables of enum type should be assigned only constants of that enum type.

Summary 325

## Section 7.9.5 enum Type DiceNames

- When an enum is declared, each enum declaration is a constant value of type int. If you do not assign a value to an identifier in the enum declaration, the compiler will do so. If the first enum constant is unassigned, the compiler gives it 0. If any other enum constant is unassigned, the compiler gives it a value equal to one more than the value of the preceding enum constant. The enum names must be unique, but their underlying values need not be.

## Section 7.9.6 Underlying Type of an enum

- If you need to compare a simple integer value to the underlying value of an enumeration constant, you must use a cast operator to make the two types match.

## Section 7.10.10 Scope of Declarations

- The scope of a declaration is the portion of that that can refer to the declared entity by its unqualified name.
- The scope of a parameter declaration is the body of the method in which the declaration appears.
- A local variable's scope is from the point at which the declaration appears to the end of that block.
- The scope of a local-variable declaration that appears in the initialization section of a state method's header is the body of the statement and the other expressions in the header.
- The scope of a method, property or field is the entire body of the class.
- Any block may contain variable declarations. If a local variable or parameter in a method has the same name as a field, it is hidden until the block terminates execution.

## Section 7.11.1 Method-Call Stack and Activation Records

- Stacks are known as last-in, first-out (FIFO) data structures—the last item pushed (on) to the stack is the first item popped (off) from the stack.

## Section 7.11.1 Method-Call Stack

- The method-call stack (sometimes referred to as the program-execution stack) is a data structure that supports the method call/return mechanism. It also supports the creation, maintenance and destruction of each method's local variables.

## Section 7.11.2 Stack Frames

- Each method must return control to the method that called it. The method-call stack is the perfect data structure for handling this information.
- Each time a method calls another, an entry (called a stack frame or an activation record) is pushed onto the stack. This entry contains the return address that the method needs in order to return to the calling method.
- If a call returns instead of calling another method before returning, the stack frame for the method is popped, and control returns to the return address in the popped stack frame.
- The same techniques apply when a method accesses a property or when a property calls a method.

## Section 7.11.3 Local Variables and Stack Frames

- Stack frames also contain the memory for parameters and any local variables a method declares.
- When a method returns—and no longer needs its local variables—its stack frame is popped from the stack, and those local variables no longer exist.

## Section 7.11.4 Stack Overflow

- If more method calls occur than can their activation records stored on the stack, a fatal error known as stack overflow occurs.

326

## Section 7.12.1 Declaring Overloaded Methods

- Methods of the same name can be declared in the same class, as long as they have different sets of parameters. This is called overloading. When an overloaded method is called, the C# compiler selects the appropriate method by examining the name, types and order of arguments.

## Section 7.12.2 Distinguishing Between Overloaded Methods

- The compiler distinguishes overloaded methods by their signature—a combination of the name and order of parameters. The signature also includes the way parameters are passed, which can be modified by ref and keywords.

## Section 7.12.3 Return Types of Overloaded Methods

- The compiler will generate an error when two methods have the same signature but different return types. Overloaded methods can have the same or different return types if the methods have different parameter lists.

## Section 7.13 Optional Parameters

- Methods can have optional parameters, allowing the calling method to vary the number of arguments to pass. An optional parameter specifies a default value that's assigned to the parameter if the argument is omitted.
- Methods can have one or more optional parameters. All optional parameters must be placed to the right of the method's non-optional parameters.
- When a parameter has a default value, the caller has the option of passing that particular argument.

## Section 7.14 Named Parameters

- Normally, when calling a method, the argument values—in order—are assigned to the parameters from left to right in the parameter list.
- C provides a feature called named parameters, which enable you to call methods that receive optional parameters by providing only the optional arguments you wish to specify. To do so, you explicitly specify the parameter's name and value—separated by a colon (:)—in the argument list of the method.

## Section 7.15 C# Expression-Bodied Methods and Properties

- C# introduces a new expression-bodied method syntax for methods that contain only a statement that returns a value or a single-statement body, and a new expression-bodied property for read-only properties in which the getter only returns a return statement.
- In a property, the symbol => follows the method's parameter list and introduces the body—no braces or return statement are required.
- A read-only property can be implemented as an expression-bodied property with the syntax `returnType PropertyName => expression;`

## Section 7.16 Recursion

- A recursive method calls itself, either directly or indirectly through another method.

## Section 7.16.1 Base Cases and Recursive Calls

- When a recursive method is called to solve a problem, the method actually is capable of solving only the simplest case(s), or base case(s). If the method is called with a base case, the method returns a result.
