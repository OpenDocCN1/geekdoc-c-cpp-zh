# 7.4 Methods with Multiple Parameters

# 7.4.1 Keyword static

Method Maximum's declaration begins with keyword static, which enables the Main method (or static method) to call Maximum as shown in line 19 without creating an object of class MaximumFinder and qualifying the method name with the class name MaximumFinder—static methods in the same class can call each other directly.

# 7.4.2 Method Maximum

Consider the declaration of Method Maximum (lines 26–43). Line 26 indicates that the method returns a double value, and that the method requires three double parameters (x, y and z) to accomplish this task. When a method has more than one parameter, the parameters are specified as a comma-separated list. Maximum is called in line 19, the parameter x is initialized with the value of the argument number1, the parameter y is initialized with the value of the argument number2 and the parameter z is initialized with the value of the argument number3. There must be one argument in the method for each call required in the method declaration. Each argument must be consistent with the type of the corresponding parameter. For example, a parameter of type double can receive values like 7.35 (double), 22 (int) or -0.0346 (double), but not strings like "hello". Section 7.6 discusses the argument types that can be provided in a method call for each parameter of simple type. Note the use of double's Parse in methods 12, 14 and 16 to convert into double values the strings used by the user.

# Common Programming Error 7.2

Declaring parameters of the same type as double x, instead of double y is a syntax error—type is required for each parameter in the parameter list.

![](bbox=[0.142, 0.503, 0.206, 0.563])

# Logic of Determining the Maximum Value

To determine the maximum, we begin with the assumption that parameter x contains the largest value, so line 28 declares local variable maximum and initializes it with the value of parameter x. It's possible that y or z contains the largest value, so we compare each of these values with maximumValue. The if statement in lines 31–34 determines whether y is greater than maximum. If so, line 33 assigns y to maximumValue. If the statement in lines 37–40 determines whether z is greater than maximum. At this point, the largest of the three values resides in maximumValue, so line 42 returns to value 19 where it's assigned to the variable result. When program control returns to the app where Maximum was called, Maximum's parameters x, y and z are no longer accessible. Methods can return at most one value; the returned value can be a type that contains one or more values (implemented as a struct; Section 10.13) or a reference to an object that contains one or more values.

# 7.4.3 Assembling strings with Concatenation

C allows strings to be created by assembling smaller strings into larger strings using operator + (or the compound assignment operator +=). This is known as string concatenation. When operands of operator + are string objects, the + operator creates a new string object containing copies of the characters in its left operand followed by cop