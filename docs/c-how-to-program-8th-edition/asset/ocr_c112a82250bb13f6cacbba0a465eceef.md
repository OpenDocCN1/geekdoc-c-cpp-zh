![](bbox=[0.063, 0.125, 0.132, 0.301])

+   6.1 Introduction  
+   6.2 Program Components in C++  
+   6.3 Math Library Functions  
+   6.4 Function Definitions with Multiple Parameters  
+   6.5 Function Prototypes and Argument Coercion  
+   6.6 C++ Standard Library Headers  
+   6.7 Case Study: Random Number Generation  
+   6.8 Case Study: Game of Chance: Introducing `enum`  
+   6.9 Storage Classes  
+   6.10 Scope Rules  
+   6.11 Function Call Stack and Activation Records  
+   6.12 Functions with Empty Parameter Lists  
+   6.13 Inline Functions  
+   6.14 References and Reference Parameters  
+   6.15 Default Arguments  
+   6.16 Unary Scope Resolution Operator  
+   6.17 Function Overloading  
+   6.18 Function Templates  
+   6.19 Recursion  
+   6.20 Example Using Recursion: Fibonacci Series  
+   6.21 Recursion vs. Iteration  
+   6.22 Wrap-Up

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Making a Difference

# ## 6.1 Introduction

Most computer programs that solve real-world problems are much larger than the programs presented in the first few chapters of this book. Experience has shown that the best way to develop and maintain a large program is to construct it from small, simple pieces, or components. This technique is called **divide and conquer**.

We’ll overview a portion of the C++ Standard Library’s math functions. Next, you’ll learn how to declare a function with more than one parameter. We’ll also present additional information about function prototypes and how the compiler uses them to convert the type of an argument in a function call to the type specified in a function’s parameter list, if necessary.

Next, we’ll take a brief diversion into simulation techniques with random number generation and develop a version of the casino dice game called craps that uses most of the programming techniques you’ve learned.

We then present C++’s storage classes and scope rules. These determine the period during which an object exists in memory and where its identifier can be referenced in a program. You’ll learn how C++ keeps track of which function is currently executing, how parameters and other local variables of functions are maintained in memory and how a function knows where to return after it completes execution. We discuss topics that help improve program performance—inline functions that can eliminate the overhead of a function call and reference parameters that can be used to pass large data items to functions efficiently.

Many of the applications you develop will have more than one function of the same name. This technique, called function overloading, is used to implement functions that perform similar tasks for arguments of different types or possibly different numbers of arguments. We consider function templates—a mechanism for defining a family of overloaded functions. The chapter concludes with a discussion of functions that call themselves, either directly, or indirectly (through another function)—a topic called recursion.