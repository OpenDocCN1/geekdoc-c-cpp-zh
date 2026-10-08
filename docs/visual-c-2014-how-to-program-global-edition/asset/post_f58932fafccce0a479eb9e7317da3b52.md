
276 Chapter 6 Control Statements: Part 2

## Making-a-Difference Exercises

**6.29 (Global Warming Facts Quiz)** The controversial issue of global warming has been widely publicized by the film *An Inconvenient Truth*, featuring Vice President Al Gore. Mr. Gore and a U.N. network of scientists, the Intergovernmental Panel on Climate Change, shared the 2007 Nobel Prize in recognition of "their efforts to build and disseminate greater knowledge about man-made climate change." Research both sides of the global warming online (you might want to search for phrases like "global warming skeptics"). Create a five-question multiple-choice quiz on global warming, each having four answers (numbered 1–4). Be objective and try to fairly represent both sides of the issue. Next, write an app that administers the quiz. The user calculates the number of correct answers (zero through five) and returns a message to the user. If the user correctly answers five questions, display "Excellent"; if four, display "Very good"; if three or fewer, display "Time to brush up on your knowledge of global warming," and include a list of some of the websites where you found your facts.

**6.30 (Tax Plan Alternatives; "FairTax")** There are many proposals to make taxation fairer. Check out the FairTax initiative in the United States at http://www.fairtax.org

Research how the proposed FairTax works. One suggestion is to eliminate income taxes and most other taxes in favor of a tax on all products and services that you buy. Some FairTax opponents question the 23% figure and say that because of the way the tax is calculated, it would be more accurate to say the rate is 30%—check this carefully. Write a program that prompts the user to enter expenses in various expense categories they have (e.g., housing, food, clothing, transportation, education, health care, vacations), then displays the estimated FairTax that person would pay.

## Chapter 7 Methods: A Deeper Look

### Objectives

In this chapter you'll:

- Learn how static methods and variables are associated with classes rather than objects.
- Use common Math class functions.
- Learn C#'s argument promotion rules for when argument types do not match parameter types exactly.
- Get a high-level overview of various namespaces from the .NET Framework Class Library.
- Use random-number generation to implement game-playing apps.
- Understand how the visibility of identifiers is limited to specific regions of programs.
- Learn how the method call and return mechanism is supported by the method-call stack.
- Create overloaded methods.
- Use optional and named parameters.
- Use recursive methods.
- Understand what value types and reference types are.
- Pass method arguments by value and by reference.

![](img/57baed2319be0bb1b5f98674846f2711_277_0.png)

### 7.1 Introduction

In this chapter, we take a deep look at methods. We'll discuss the difference between static and static methods. You'll see that the Math class in the .NET Framework Library provides many static methods to perform mathematical calculations. We'll also discuss static variables (known as class variables) and why method Main is declared static.

![](img/57baed2319be0bb1b5f98674846f2711_278_0.png)

### 7.2 Packaging Code in C#

You'll declare a method with multiple parameters and learn how to use operator + to perform string concatenations. We'll discuss C#'s argument promotion rules for implicitly converting simple values to other types and when these rules are applied by the compiler. We'll also present several used Framework Class namespaces.

We'll take a brief, and hopefully entailing, diversion into simulation techniques with random-number generation and develop a version of a popular casino dice game that uses most of the programming techniques you've learned so far. You'll declare named constants with the const keyword and with enum types. We'll then present C# scope rules, which determine identifiers can be referenced in an app.

We'll discuss how method-call stack enables C# to keep track of which method is currently executing, and how method knows to return after it completes. You'll overload methods in a class by providing methods with the same name but different numbers/or types of parameters, and learn to use optional and named parameters.

We'll introduce C#'s expression-bodied methods, which provide a concise notation for methods that simply return a value. We'll also use this expression-bodied notation for a read-only property's getter.

We'll discuss how recursive methods call themselves, breaking larger problems into smallerproblems until the original problem is solved. Finally, we will provide more insight into how value-type and reference-type arguments are passed to methods.

So we've used properties, methods and classes to package code. We'll present additional packaging mechanisms in later chapters. C# apps are written by combining your properties, methods and classes with predefined properties, methods and classes available in the .NET Framework Class Library and in other libraries. Related classes are often grouped into namespaces and compiled into class libraries so they can be reused in other apps. You'll learn to create your own namespaces and class libraries in Chapter 15. The Framework Class Library provides many predefined classes methods for performing mathematical calculations, string manipulations, character manipulations, input/output operations, graphical interfaces, graphics, multi-media, printing, file processing, database operations, networking operations, error checking, web-app development, accessibility (for people with disabilities) and more.

> Software Engineering Observation 7.1
Don't try to "reinvent the wheel". When possible, reuse Framework Class libraries and methods (https://msdn.microsoft.com/library/mt42912). This reduces development time and effort, contributes to good performance and enhances security.

#### 7.2.1 Modularizing Programs

Methods called functions and procedures in other languages allow you to modularize an app by separating its tasks into self-contained units. You've declared methods in every app you've written. The actual statements in the method body are written only once, can be reused from several locations in an app and are hidden from other methods.

---
**Table of Contents Reference:**
- 7.1 Introduction
- 7.2 Packaging Code in C#
    - 7.2.1 Modularizing Programs
    - 7.2.2 Calling Methods
- 7.3 static Methods, static Variables and Class Math
    - 7.3.1 Math Class Methods
    - 7.3.2 Math Class Constants PI and E
    - 7.3.3 Why Is Main declared static?
    - 7.3.4 Additional Comments About Main
- 7.4 Methods with Multiple Parameters
    - 7.4.1 Keyword static
    - 7.4.2 Method Maximum
    - 7.4.3 Resembling strings with Concatenation
    - 7.4.4 Passing Large string literals
    - 7.4.5 When to Declare Variables as Fields
    - 7.4.6 Implementing Maximum by Reusing Math, Max
- 7.5 Notes on Using Methods
- 7.6 Argument Promotion and Casting
    - 7.6.1 Promotion Rules
    - 7.6.2 Sometimes Implicit Casts Are Required
- 7.7 .NET Framework Class Library
- 7.8 Case Study: Random-Number Generation
    - 7.8. Creating an Object of Random
    - 7.8.2 Generating a Random Index
    - 7.8.3 Scaling the Random-Number Range
    - 7.8.4 Shifting Random-Number Range
    - 7.8.5 Combiningifting and Scaling
    - 7.8.6 Rolling a Six-Die
    - 7.8.7 Scaling Random Numbers
    - 7.8.8 Repeatability for Testing and Debugging
- 7.9 Case Study: A Game of Chance: Introducing Enumerations
    - 7.9.1 Method Main's Local Variables
    - 7.9.2 RollDice 
    - 7.9.3 enum Type Status
    - 7.9.4 The First Roll
    - 7.9.5 enum DiceNames
- 7.10 Scope of Declarations
- 7.11 Method-Call Stack and Activation
    - 7.11.1 Method-Call Stack
    - 7.11.2 Stack Frames
    - 7.11.3 Local Variables and Stack Frames
    - 7.11.4 Stack Overflow
- 7.12 Method Overloading
    - 7.12.1aring Overloaded Methods
    - 7.12.2 Distinguishing Between Overloaded Methods
    - 7.12.3 Return Type of Overloaded Methods
- 7.13 Optional Parameters
- 7.14 Named Parameters
- 7.15 C# & Expression-Bodied Methods and Properties
- 7.16 Recursion
    - 7.16.1 Base Cases and Recursive Calls
    - 7.16.2 Recursive own Calculations
    - 7.16.3 Implementing Factorial Recursively
- 7.17 Value Types vs. Reference Types
- 7.18 Passing Arguments By Value and By Reference
    - 7.18.1 ref and out Parameters
    - 7.18.2 Demonstrating ref, and out Value Parameters
