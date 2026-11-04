| Method | Description | Example |
| --- | --- | --- |
| Exp(x) | exponential method e^x | Exp(1.0) is 2.71828<br>Exp(2.0) is 7.38906 |
| Log(x) | natural logarithm of x (base e) | Log(Math.E) is 1.0<br>Log(Math.E * Math.E) is 2.0 |
| Max(x, y) | larger value of x and y | Max(2.3, 12.7) is 12.7<br>Max(2.3, -12.7) is 2.3 |
| Min(x, y) | smaller value of x and y | Min(2.3, 12.7) is 2.3<br>Min(2.3, -12.7) is -12.7 |
| Pow(x, y) | x raised to the power y (i.e., x^y) | Pow(2.0, 7.0) is 128.0<br>Pow(3.0, 0.5) is 3.0 |
| Sqrt(x) | square root of x | Sqrt(900.0) is 30.0 |

**Fig. 7.1** | Math class methods. (Part 2 of 2)

# ### 7.3.2 Math Class Constants PI and E

Each object of a class maintains its own copy of each of the class's *instance variables*. There are also variables for which each object of a class does not need its own separate copy (as you'll see momentarily). Such variables are declared static and are also known as class variables. When objects of a class containing *static variables* are created, all the objects of that class share *one* copy of those variables. Together a class's *static variables* and *instance variables* are known as its fields. You'll learn more about static fields in Section 10.9.

Class Math also declares two double constants for commonly used mathematical values:

+   - Math.PI (3.1415926535897931) is the ratio of a circle's circumference to its diameter, and
+   - Math.E (2.7182818284590451) is the base value for natural logarithms (calculated with static Math method Log).

These constants are declared in class Math with the modifiers `public` and `const`. Making them public allows other programmers to use these variables in their own classes. A constant is declared with the keyword `const`—its value cannot be changed after the constant is declared. Fields declared `const` are implicitly static, so you can access them via the class name Math and the member-access operator (.), as in Math.PI and Math.E.

**Common Programming Error 7.1**
*Constants declared in a class, but not inside a method or property, are implicitly static—it's a syntax error to declare such a constant with keyword static explicitly.*

# ### 7.3.3 Why Is Main Declared static?

Why must Main be declared static? During app startup, when no objects of the class have been created, the Main method must be called to begin program execution. Main is sometimes called the app's entry point. Declaring Main as static allows the execution environment to invoke Main without creating an instance of the class. Method Main is typically declared with the header: