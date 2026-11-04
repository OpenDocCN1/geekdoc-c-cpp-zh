
| Method | Description | Example |
| --- | --- | --- |
| Exp(x) | exponential method e^x | Exp(1.0) is 2.71828<br>Exp(2.0) is 7.38906 |
| Log(x) | natural logarithm of x (base e) | Log(Math.E) is 1.0<br>Log(Math.E * Math.E) is 2.0 |
| Max(x, y) | larger value of x and y | Max(2.3, 12.7) is 12.7<br>Max(2.3, -12.7) is 2.3 |
| Min(x, y) | smaller value of x and y | Min(2.3, 12.7) is 2.3<br>Min(2.3, -12.7) is -12.7 |
| Pow(x, y) | x raised to the power y (i.e., x^y) | Pow(2.0, 7.0) is 128.0<br>Pow(3.0, 0.5) is 3.0 |
| Sqrt(x) | square root of x | Sqrt(900.0) is 30.0 |

**Fig. 7.1** | Math class methods. (Part 2 of 2)

### 7.3.2 Math Class Constants PI and E

Each object of a class maintains its own copy of each of the class's *instance variables*. There are also variables for which each object of a class does not need its own separate copy (as you'll see momentarily). Such variables are declared static and are also known as class variables. When objects of a class containing *static variables* are created, all the objects of that class share *one* copy of those variables. Together a class's *static variables* and *instance variables* are known as its fields. You'll learn more about static fields in Section 10.9.

Class Math also declares two double constants for commonly used mathematical values:

- Math.PI (3.1415926535897931) is the ratio of a circle's circumference to its diameter, and
- Math.E (2.7182818284590451) is the base value for natural logarithms (calculated with static Math method Log).

These constants are declared in class Math with the modifiers `public` and `const`. Making them public allows other programmers to use these variables in their own classes. A constant is declared with the keyword `const`—its value cannot be changed after the constant is declared. Fields declared `const` are implicitly static, so you can access them via the class name Math and the member-access operator (.), as in Math.PI and Math.E.

**Common Programming Error 7.1**
*Constants declared in a class, but not inside a method or property, are implicitly static—it's a syntax error to declare such a constant with keyword static explicitly.*

### 7.3.3 Why Is Main Declared static?

Why must Main be declared static? During app startup, when no objects of the class have been created, the Main method must be called to begin program execution. Main is sometimes called the app's entry point. Declaring Main as static allows the execution environment to invoke Main without creating an instance of the class. Method Main is typically declared with the header:

```
static void Main()
```

but also can be declared with the header:

```
static void Main(string[] args)
```

which we'll discuss and demonstrate in Section 8.12, Shuffling and Dealing Cards. In addition, you can declare Main with return type int (instead of void)-----this can be useful if an app is executed by another app and needs to return an indication of success or failure to that other app.

### 7.3.4 Additional Comments About Main

Most earlier examples have one class that contained only Main, and some examples had a second class that was used by Main to create and manipulate objects. Actually, any class can contain a Main method. In fact, each of our two-class examples could have been implemented as one class. For example, in the app in Figs. 4.11–4.12, method Main (lines 7–43 of Fig. 4.12) could have been moved into class Account (Fig. 4.11). The app results would have been identical to those of the two-class version. You can place a Main method in every class you declare. Some programmers take advantage of this to build a small test app into each class they declare. However, if you declare more than one Main method among the classes of your project, you'll need to indicate to the IDE which one you would like to be the app's entry point. To do so:

- 1. With the project open in Visual Studio, select Project > [ProjectName] Properties... (where [ProjectName] is the name of your project).
- 2. Select the class containing the Main method that should be the entry point from the Startup object list box.

## 7.4 Methods with Multiple Parameters

We now consider how to write a method with multiple parameters. Figure 7.2 defines the Maximum method that determines and returns the largest of three double values. When the app begins execution, the Main method (lines 8–23) executes. Line 19 calls method Maximum (declared in lines 26–43) to determine and return the largest of its three double arguments. In Section 7.4.3, we'll discuss the use of the + operator in line 22. The sample outputs show that Maximum determines the largest value regardless of whether that value is the first, second or third argument.

```csharp
1 // Fig. 7.2: MaximumFinder.cs
2 // Method Maximum with three parameters.
3 using System;
4
5 class MaximumFinder
6 {
7   // obtain three floating-point values and determine maximum value
8   static void Main()
9   {
10    // prompt for and input three floating-point values
11    Console.Write("Enter first floating-point value: ");
12    double number1 = double.Parse(Console.ReadLine());
13    Console.Write("Enter second floating-point value: ");
14    double number2 = double.Parse(Console.ReadLine());
15    Console.Write("Enter third floating-point value: ");
16    double number3 = double.Parse(Console.ReadLine());
17
18    // determine the maximum of three values
19    double result = Maximum(number1, number2, number3);
20
21    // display maximum value
22    Console.WriteLine("Maximum is: " + result);
23  }
24
25  // returns the maximum of its three double parameters
26  static double Maximum(double x, double y, double z)
27  {
28      double maximumValue = x; // assume x is the largest to start
29
30      // determine whether y is greater than maximumValue
31      if (y > maximumValue)
32      {
33          maximumValue = y;
34      }
35
36      // determine whether z is greater than maximumValue
37      if (z > maximumValue)
38      {
39          maximumValue = z;
40      }
41
42      return maximumValue;
43  }
44 }
```

Enter first floating-point values: 3.33
Enter second floating-point values: 1.11
Enter third floating-point values: 2.22
Maximum is: 3.33

Enter first floating-point values: 2.22
Enter second floating-point values: 3.33
Enter third floating-point values: 1.11
Maximum is: 3.33

Enter first floating-point values: 2.22
Enter second floating-point values: 1.11
Enter third floating-point values: 3.33
Maximum is: 3.33

Fig. 7.2 | Method Maximum with three parameters. (Part 2 of 2.)

### 7.4.1 Keyword static

Method Maximum's declaration begins with keyword static, which enables the Main method (another static method) to call Maximum as shown in line 19 without creating an object of class MaximumFinder and without qualifying the method name with the class name MaximumFinder—static methods in the same class can call each other directly.

### 7.4.2 Method Maximum

Consider the declaration of method Maximum (lines 26–43). Line 26 indicates that the method returns a double value, that the method's name is Maximum and that the method requires three double parameters (x, y and z) to accomplish its task. When a method has more than one parameter, the parameters are specified as a comma-separated list. When Maximum is called in line 19, the parameter x is initialized with the value of the argument number1, the parameter y is initialized with the value of the argument number2 and the parameter z is initialized with the value of the argument number3. There must be one argument in the method call for each required parameter in the method declaration. Also, each argument must be consistent with the type of the corresponding parameter. For example, a parameter of type double can receive values like 7.35 (a double), 22 (an int) or -0.03456 (a double), but not strings like "hello". Section 7.6 discusses the argument types that can be provided in a method call for each parameter of a simple type. Note the use of type double's Parse method in lines 12, 14 and 16 to convert into double values the strings typed by the user.

> **Common Programming Error 7.2**
> 
> Declaring method parameters of the same type as double x, y instead of double x, double y is a syntax error—a type is required for each parameter in the parameter list.

**Logic of Determining the Maximum Value**
To determine the maximum value, we begin with the assumption that parameter x contains the largest value, so line 28 declares local variable maximumValue and initializes it with the value of parameter x. Of course, it's possible that parameter y or z contains the largest value, so we must compare each of these values with maximumValue. The if statement at lines 31–34 determines whether y is greater than maximumValue. If so, line 33 assigns y to maximumValue. The if statement at lines 37–40 determines whether z is greater than maximumValue. If so, line 39 assigns z to maximumValue. At this point, the largest of the three values resides in maximumValue, so line 42 returns that value to line 19 where it's assigned to the variable result. When program control returns to the point in the app where Maximum was called, Maximum's parameters x, y and z are no longer accessible. Methods can return at most one value; the returned value can be a value type that contains one or more values (implemented as a struct; Section 10.13) or a reference to an object that contains one or more values.

### 7.4.3 Assembling strings with Concatenation

C# allows string objects to be created by assembling smaller strings using operator + (or the compound assignment operator +=). This is known as string concatenation. When both operands of operator + are string objects, the + operator creates a new string object containing copies of the characters in its left operand followed by copies
