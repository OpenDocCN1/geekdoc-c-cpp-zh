
might want to search for phrases like “global warming skeptics”). Create a five-question multiple-choice quiz on global warming, each question having four possible answers (numbered 1–4). Be objective and try to fairly represent both sides of the issue. Next, write an application that administers the quiz, calculates the number of correct answers (zero through five) and returns a message to the user. If the user correctly answers five questions, print “Excellent”; if four, print “Very good”; if three or fewer, print “Time to brush up on your knowledge of global warming,” and include a list of some of the websites where you found your facts.

## 5.31 (Tax Plan Alternatives; The “FairTax”) There are many proposals to make taxation fairer. Check out the FairTax initiative in the United States at

www.fairtax.org/site/PageServer?pagename=calculator

Research how the proposed FairTax works. One suggestion is to eliminate income taxes and most other taxes in favor of a 23% consumption tax on all products and services that you buy. Some FairTax opponents question the 23% figure and say that because of the way the tax is calculated, it would be more accurate to say the rate is 30%—check this carefully. Write a program that prompts the user to enter expenses in various expense categories they have (e.g., housing, food, clothing, transportation, education, health care, vacations), then prints the estimated FairTax that person would pay.

## 5.32 (Facebook User Base Growth) According to CNNMoney.com, Facebook hit 500 million users in July of 2010 and its user base has been growing at a rate of 5% per month.

Using the compound-growth technique you learned in Fig. 5.6 and assuming this growth rate continues, how many months will it take for Facebook to grow its user base to one billion users? How many months will it take for Facebook to grow its user base to two billion users (which, at the time of this writing, was the total number of people on the Internet)?

## 6.1 Introduction

Experience has shown that the best way to develop and maintain a large program is to construct it from small, simple pieces, or modules. This technique is called divide and conquer. Methods, which we introduced in Chapter 3, help you modularize programs. In this chapter, we study methods in more depth. We emphasize how to declare and use methods to facilitate the design, implementation, operation and maintenance of large programs.

You’ll see that it’s possible to call certain methods, called static methods, without the need for an object of the class to exist. You’ll learn how to declare a method with more than one parameter. You’ll also learn how Java is able to keep track of which method is currently executing, how local variables of methods are maintained in memory and how a method knows where to return after it completes execution.

We’ll take a brief diversion into simulation techniques with random-number generation and develop a version of the casino dice game called craps that uses most of the programming techniques you’ve used to this point in the book. In addition, you’ll learn how to declare values that cannot change (i.e., constants) in your programs.

Many of the classes you’ll use or create while developing applications will have more than one method of the same name. This technique, called overloading, is used to implement methods that perform similar tasks for arguments of different types or for different numbers of arguments.

We continue our discussion of methods in Chapter 18, Recursion. Recursion provides an intriguing way of thinking about methods and algorithms.

## 6.2 Program Modules in Java

You write Java programs by combining new methods and classes with predefined ones available in the Java Application Programming Interface (also referred to as the Java API or Java class library) and in various other class libraries. Related classes are typically grouped into packages so that they can be imported into programs and reused. You’ll learn

- 6.1 Introduction
- 6.2 Program Modules in Java
- 6.3 static Methods, static Fields and Class Math
- 6.4 Declaring Methods with Multiple Parameters
- 6.5 Notes on Declaring and Using Methods
- 6.6 Method-Call Stack and Activation Records
- 6.7 Argument Promotion and Casting
- 6.8 Java API Packages
- 6.9 Case Study: Random-Number Generation
- 6.9.1 Generalized Scaling and Shifting of Random Numbers
- 6.9.2 Random-Number Repeatability for Testing and Debugging
- 6.10 Case Study: A Game of Chance; Introducing Enumerations
- 6.11 Scope of Declarations
- 6.12 Method Overloading
- 6.13 (Optional) GUI and Graphics Case Study: Colors and Filled Shapes
- 6.14 Wrap-Up

how to group your own classes into packages in Chapter 8. The Java API provides a rich collection of predefined classes that contain methods for performing common mathematical calculations, string manipulations, character manipulations, input/output operations, database operations, networking operations, file processing, error checking and many other useful tasks.

### Software Engineering Observation 6.1

Familiarize yourself with the rich collection of classes and methods provided by the Java API (download.oracle.com/javase/6/docs/api/). Section 6.8 presents an overview of several common packages. Appendix E explains how to navigate the API documentation. Don’t reinvent the wheel. When possible, reuse Java API classes and methods. This reduces program development time and avoids introducing programming errors.

Methods (called functions or procedures in some languages) help you modularize a program by separating its tasks into self-contained units. You’ve declared methods in every program you’ve written. The statements in the method bodies are written only once, are hidden from other methods and can be reused from several locations in a program.

One motivation for modularizing a program into methods is the divide-and-conquer approach, which makes program development more manageable by constructing programs from small, simple pieces. Another is software reusability—using existing methods as building blocks to create new programs. Often, you can create programs mostly from standardized methods rather than by building customized code. For example, in earlier programs, we did not define how to read data from the keyboard—Java provides these capabilities in the methods of class Scanner. A third motivation is to avoid repeating code. Dividing a program into meaningful methods makes the program easier to debug and maintain.

### Software Engineering Observation 6.2

To promote software reusability, every method should be limited to performing a single, well-defined task, and the name of the method should express that task effectively.

### Error-Prevention Tip 6.1

A method that performs one task is easier to test and debug than one that performs many tasks.

### Software Engineering Observation 6.3

If you cannot choose a concise name that expresses a method’s task, your method might be attempting to perform too many tasks. Break such a method into several smaller ones.

As you know, a method is invoked by a method call, and when the called method completes its task, it returns either a result or simply control to the caller. An analogy to this program structure is the hierarchical form of management (Fig. 6.1). A boss (the caller) asks a worker (the called method) to perform a task and report back (return) the results after completing the task. The boss method does not know how the worker method performs its designated tasks. The worker may also call other worker methods, unbeknown to the boss. This “hiding” of implementation details promotes good software engineering. Figure 6.1 shows the boss method communicating with several worker methods in a hierarchical manner. The boss method divides its responsibilities among the various worker methods. Here, worker1 acts as a “boss method” to worker4 and worker5.
