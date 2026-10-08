# 324 Chapter 7 Methods: A Deeper Look

# Section 7.5 Notes on Declaring and Using Methods

+   - You've seen three ways to call a method—using a method name by itself to call another method of the same class; using a variable that contains a reference to an object, by the member access operator (.) and the method name to call a non-static method of the referenced object; and using the class and the member-access operator (.) to a static method of a class.
- A static method can call only static methods of the same class and can manipulate only static variables in the same class.
- You've seen three ways to return to the statement that calls a method—when the method-ending right brace in a method return type void is reached, when the following statement executes in a method return void:

```
return;
```

and when a method returns a result with a statement of the following form in which the expression is evaluated and its result (and control) are returned to the caller:

```
return expression;
```

# Section 7.6 Argument Promotion and Casting

+   - Another important feature of method calls is argument promotion—implicitly converting an argument's value to the type that the method expects to receive in its corresponding parameter.

# Section 7.6.1 Promotion Rules

+   - The argument-promotion rules apply to containing values of two or more types and to simple-type values passed as arguments to methods.

# Section 7.6.2 Explicit Casts Are Required

+   - In cases where information may be lost due to conversion between simple types, the compiler requires you to use a cast operator to explicitly force the conversion.

# Section 7.7 The .NET Framework Class Library

+   - Many defined classes are grouped into categories of related class namespaces. Together, these are referred to as the .NET Framework Class Library.

# Section 7.8.2 Generating a Random Integer

+   - Random Next() generates a random int value in the range 0 to +2,147,483,646, inclusive.
- The methods of class Random actually generate pseudorandom numbers based on mathematical calculations. The calculation that produces the pseudorandom numbers uses the time of day as a seed value to control the sequence's starting point.

# Section 7.8.3 Scaling the Random-Number Range

+   - Class Random provides other versions of Next. One receives an int and returns a value from 0 to up, but not including the argument. The other receives two ints and returns a value from the first argument's value up to, but not including, the second argument's value.

# Section 7.8.8 Repeatability for Testing and Debugging

+   - If the same seed is used every time, the Random object produces the same sequence of random numbers. Class Random's constructor can receive the seed value as an argument.

# Section 7.9.3 enum Type Status

+   - An enumeration is introduced by the keyword enum and a type name. Braces limit the body of an enum declaration. Inside the braces is a comma-separated list of enumeration constants.
- Variables of enum type should be assigned only constants of that enum type.