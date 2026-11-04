+   - 7.1 Introduction
+   - 7.2 Packaging Code in C#
+   - 7.3 static Methods, static Variables and Class Math
+   - 7.3.1 Math Class Methods
+   - 7.3.2 Math Class Constants PI and E
+   - 7.3.3 Why Is Main Declared static?
+   - 7.3.4 Additional Comments About Main
+   - 7.4 Methods with Multiple Parameters
+   - 7.4.1 Keyword static
+   - 7.4.2 Method Maximum
+   - 7.4.3 Assembling strings with Concatenation
+   - 7.4.4 Breaking Apart Large string Literals
+   - 7.4.5 When to Declare Variables as Fields
+   - 7.4.6 Implementing Method Maximum by Re-using Method Math.Max
+   - 7.5 Notes on Using Methods
+   - 7.6 Argument Promotion and Casting
+   - 7.6.1 Promotion Rules
+   - 7.6.2 Sometimes Explicit Casts Are Required
+   - 7.7 The .NET Framework Class Library
+   - 7.8 Case Study: Random-Number Generation
+   - 7.8.1 Creating an Object of Type Random
+   - 7.8.2 Generating a Random Integer
+   - 7.8.3 Scaling the Random-Number Range
+   - 7.8.4 Shifting Random-Number Range
+   - 7.8.5 Combining Shifting and Scaling
+   - 7.8.6 Rolling a Six-Sided Die
+   - 7.8.7 Scaling and Shifting Random Numbers
+   - 7.8.8 Repeatability for Testing and Debugging
+   - 7.9 Case Study: A Game of Chance; Introducing Enumerations
+   - 7.9.1 Method Roll1Dice
+   - 7.9.2 Method Main's Local Variables
+   - 7.9.3 enum Type Status
+   - 7.9.4 The First Roll
+   - 7.9.5 enum Type DiceNames
+   - 7.9.6 Underlying Type of an enum
+   - 7.9.7 Comparing Integers and enum Constants
+   - 7.10 Scope of Declarations
+   - 7.11 Method-Call Stack and Activation Records
+   - 7.11.1 Method-Call Stack
+   - 7.11.2 Stack Frames
+   - 7.11.3 Local Variables and Stack Frames
+   - 7.11.4 Stack Overflow
+   - 7.11.5 Method-Call Stack in Action
+   - 7.12 Method Overloading
+   - 7.12.1 Declaring Overloaded Methods
+   - 7.12.2 Distinguishing Between Overloaded Methods
+   - 7.12.3 Return Types of Overloaded Methods
+   - 7.13 Optional Parameters
+   - 7.14 Named Parameters
+   - 7.15 C# 6 Expression-Bodied Methods and Properties
+   - 7.16 Recursion
+   - 7.16.1 Base Cases and Recursive Calls
+   - 7.16.2 Recursive Factorial Calculations
+   - 7.16.3 Implementing Factorial Recursively
+   - 7.17 Value Types vs. Reference Types
+   - 7.18 Passing Arguments By Value and By Reference
+   - 7.18.1 ref and out Parameters
+   - 7.18.2 Demonstrating ref, out and Value Parameters
+   - 7.19 Wrap-Up

# 7.1 Introduction

In this chapter, we take a deeper look at methods. We'll discuss the difference between non-static and static methods. You'll see that the Math class in the .NET Framework Class Library provides many static methods to perform mathematical calculations. We'll also discuss static variables (known as class variables) and why method Main is declared static.

You'll declare a method with multiple parameters and use operator + to perform string concatenations. We'll discuss C#'s argument promotion rules for implicitly con-