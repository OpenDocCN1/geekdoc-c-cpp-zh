rameters (x, y and z) to accomplish its task. Multiple parameters are specified as a comma-separated list. When maximum is called from line 21, the parameters x, y and z are initialized with the values of arguments number1, number2 and number3, respectively. There must be one argument in the method call for each parameter in the method declaration. Also, each argument must be consistent with the type of the corresponding parameter. For example, a parameter of type double can receive values like 7.35, 22 or −0.03456, but not Strings like "hello" nor the boolean values true or false. Section 6.7 discusses the argument types that can be provided in a method call for each parameter of a primitive type.

To determine the maximum value, we begin with the assumption that parameter x contains the largest value, so line 30 declares local variable maximumValue and initializes it with the value of parameter x. Of course, it’s possible that parameter y or z contains the actual largest value, so we must compare each of these values with maximumValue. The if statement at lines 33–34 determines whether y is greater than maximumValue. If so, line 34 assigns y to maximumValue. The if statement at lines 37–38 determines whether z is greater than maximumValue. If so, line 38 assigns z to maximumValue. At this point the largest of the three values resides in maximumValue, so line 40 returns that value to line 21. When program control returns to the point in the program where maximum was called, maximum’s parameters x, y and z no longer exist in memory.

# Software Engineering Observation 6.5

Methods can return at most one value, but the returned value could be a reference to an object that contains many values.

# Software Engineering Observation 6.6

Variables should be declared as fields only if they’re required for use in more than one method of the class or if the program should save their values between calls to the class’s methods.

# Common Programming Error 6.1

Declaring method parameters of the same type as float x, y instead of float x, float y is a syntax error—a type is required for each parameter in the parameter list.

# Implementing Method maximum by Reusing Method Math.max

The entire body of our maximum method could also be implemented with two calls to Math.max, as follows:

```
return Math.max( x, Math.max( y, z ) );
```

The first call to Math.max specifies arguments x and Math.max( y, z ). Before any method can be called, its arguments must be evaluated to determine their values. If an argument is a method call, the method call must be performed to determine its return value. So, in the preceding statement, Math.max( y, z ) is evaluated to determine the maximum of y and z. Then the result is passed as the second argument to the other call to Math.max, which returns the larger of its two arguments. This is a good example of software reuse—we find the largest of three values by reusing Math.max, which finds the larger of two values. Note how concise this code is compared to lines 30–38 of Fig. 6.3.

# Assembling Strings with String Concatenation

Java allows you to assemble String objects into larger strings by using operators + or +=. This is known as string concatenation. When both operands of operator + are String ob-