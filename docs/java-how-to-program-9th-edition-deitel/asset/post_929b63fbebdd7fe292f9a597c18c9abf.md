
parameters (x, y and z) to accomplish its task. Multiple parameters are specified as a comma-separated list. When maximum is called from line 21, the parameters x, y and z are initialized with the values of arguments number1, number2 and number3, respectively. There must be one argument in the method call for each parameter in the method declaration. Also, each argument must be consistent with the type of the corresponding parameter. For example, a parameter of type double can receive values like 7.35, 22 or −0.03456, but not Strings like "hello" nor the boolean values true or false. Section 6.7 discusses the argument types that can be provided in a method call for each parameter of a primitive type.

To determine the maximum value, we begin with the assumption that parameter x contains the largest value, so line 30 declares local variable maximumValue and initializes it with the value of parameter x. Of course, it’s possible that parameter y or z contains the actual largest value, so we must compare each of these values with maximumValue. The if statement at lines 33–34 determines whether y is greater than maximumValue. If so, line 34 assigns y to maximumValue. The if statement at lines 37–38 determines whether z is greater than maximumValue. If so, line 38 assigns z to maximumValue. At this point the largest of the three values resides in maximumValue, so line 40 returns that value to line 21. When program control returns to the point in the program where maximum was called, maximum’s parameters x, y and z no longer exist in memory.

### Software Engineering Observation 6.5

Methods can return at most one value, but the returned value could be a reference to an object that contains many values.

### Software Engineering Observation 6.6

Variables should be declared as fields only if they’re required for use in more than one method of the class or if the program should save their values between calls to the class’s methods.

### Common Programming Error 6.1

Declaring method parameters of the same type as float x, y instead of float x, float y is a syntax error—a type is required for each parameter in the parameter list.

### Implementing Method maximum by Reusing Method Math.max

The entire body of our maximum method could also be implemented with two calls to Math.max, as follows:

```
return Math.max( x, Math.max( y, z ) );
```

The first call to Math.max specifies arguments x and Math.max( y, z ). Before any method can be called, its arguments must be evaluated to determine their values. If an argument is a method call, the method call must be performed to determine its return value. So, in the preceding statement, Math.max( y, z ) is evaluated to determine the maximum of y and z. Then the result is passed as the second argument to the other call to Math.max, which returns the larger of its two arguments. This is a good example of software reuse—we find the largest of three values by reusing Math.max, which finds the larger of two values. Note how concise this code is compared to lines 30–38 of Fig. 6.3.

### Assembling Strings with String Concatenation

Java allows you to assemble String objects into larger strings by using operators + or +=. This is known as string concatenation. When both operands of operator + are String objects, operator + creates a new String object in which the characters of the right operand are placed at the end of those in the left operand—e.g., the expression "hello " + "there" creates the String "hello there".

In line 24 of Fig. 6.3, the expression "Maximum is: " + result uses operator + with operands of types String and double. Every primitive value and object in Java has a String representation. When one of the + operator's operands is a String, the other is converted to a String, then the two are concatenated. In line 24, the double value is converted to its String representation and placed at the end of the String "Maximum is: ". If there are any trailing zeros in a double value, these will be discarded when the number is converted to a String—for example 9.3500 would be represented as 9.35.

Primitive values used in String concatenation are converted to Strings. A boolean concatenated with a String is converted to the String "true" or "false". All objects have a toString method that returns a String representation of the object. (We discuss toString in more detail in subsequent chapters.) When an object is concatenated with a String, the object's toString method is implicitly called to obtain the String representation of the object. toString can be called explicitly.

You can break large String literals into several smaller Strings and place them on multiple lines of code for readability. In this case, the Strings can be reassembled using concatenation. We discuss the details of Strings in Chapter 16.

### Common Programming Error 6.2

It's a syntax error to break a String literal across lines. If necessary, you can split a String into several smaller Strings and use concatenation to form the desired String.

### Common Programming Error 6.3

Confusing the + operator used for string concatenation with the + operator used for addition can lead to strange results. Java evaluates the operands of an operator from left to right. For example, if integer variable y has the value 5, the expression "y + 2 = " + y + 2 results in the string "y + 2 = 52", not "y + 2 = 7", because first the value of y (5) is concatenated to the string "y + 2 =", then the value 2 is concatenated to the new larger string "y + 2 = 5". The expression "y + 2 = " + (y + 2) produces the desired result "y + 2 = 7".

## 6.5 Notes on Declaring and Using Methods

There are three ways to call a method:

- 1. Using a method name by itself to call another method of the same class—such as maximum(number1, number2, number3) in line 21 of Fig. 6.3.
- 2. Using a variable that contains a reference to an object, followed by a dot (.) and the method name to call a non-static method of the referenced object—such as the method call in line 13 of Fig. 5.10, myGradeBook.displayMessage(), which calls a method of class GradeBook from the main method of GradeBookTest.
- 3. Using the class name and a dot (.) to call a static method of a class—such as Math.sqrt(900.0) in Section 6.3.

A static method can call only other static methods of the same class directly (i.e., using the method name by itself) and can manipulate only static variables in the same class directly. To access the class's non-static members, a static method must use a reference to an object of the class. Recall that `static` methods relate to a class as a whole, whereas non-static methods are associated with a specific instance (object) of the class and may manipulate the instance variables of that object. Many objects of a class, each with its own copies of the instance variables, may exist at the same time. Suppose a static method were to invoke a non-static method directly. How would the method know which object’s instance variables to manipulate? What would happen if no objects of the class existed at the time the non-static method was invoked? Thus, Java does not allow a static method to access non-static members of the same class directly.

There are three ways to return control to the statement that calls a method. If the method does not return a result, control returns when the program flow reaches the method-ending right brace or when the statement

```
return;
```

is executed. If the method returns a result, the statement

```
return expression;
```

evaluates the *expression*, then returns the result to the caller.

### Common Programming Error 6.4

Declaring a method outside the body of a class declaration or inside the body of another method is a syntax error.

### Common Programming Error 6.5

Placing a semicolon after the right parenthesis enclosing the parameter list of a method declaration is a syntax error.

### Common Programming Error 6.6

Redeclaring a parameter as a local variable in the method’s body is a compilation error.

### Common Programming Error 6.7

Forgetting to return a value from a method that should return a value is a compilation error. If a return type other than void is specified, the method must contain a return statement that returns a value consistent with the method’s return type. Returning a value from a method whose return type has been declared void is a compilation error.

## 6.6 Method-Call Stack and Activation Records

To understand how Java performs method calls, we first need to consider a data structure (i.e., collection of related data items) known as a stack. You can think of a stack as analogous to a pile of dishes. When a dish is placed on the pile, it’s normally placed at the top (referred to as pushing the dish onto the stack). Similarly, when a dish is removed from the pile, it’s always removed from the top (referred to as popping the dish off the stack). Stacks are known as last-in, first-out (LIFO) data structures—the last item pushed (inserted) on the stack is the first item popped (removed) from the stack.
