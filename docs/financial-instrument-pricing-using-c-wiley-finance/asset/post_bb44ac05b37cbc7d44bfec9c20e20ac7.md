
## CHAPTER 27
## Microsoft .Net, C# and C++11 Interoperability

- 26.10 Generating Random Numbers 845
- 26.10.1 Appendix: Overview of the Eigen Matrix Library 846
- 26.11 Summary and Conclusions 848
- 26.12 Exercises and Projects 849
- 27.1 Introduction and Objectives 853
- 27.2 The Big Picture 854
- 27.3 Types 858
- 27.4 Memory Management 859
- 27.5 An Introduction to Native Classes 861
- 27.6 Interfaces and Abstract Classes 861
- 27.7 Use Case: C++/CLI as ‘Main Language’ 862
- 27.8 Use Case: Creating Proxies, Adapters and Wrappers for Legacy C++ Applications 864
- 27.8.1 Alternative: SWIG (Simplified Wrapper and Interface Generator) 871
- 27.9 ‘Back to the Future’ Use Case: Calling C# Code from C++11 872
- 27.10 Modelling Event-Driven Applications with Delegates 876
- 27.10.1 Next-Generation Strategy (Plug-in) Patterns 877
- 27.10.2 Events and Multicast Delegates 881
- 27.11 Use Case: Interfacing with Legacy Code 886
- 27.11.1 Legacy DLLs 886
- 27.11.2 Runtime Callable Wrapper (RCW) 887
- 27.11.3 COM Callable Wrapper (CCW) 888
- 27.12 Assemblies and Namespaces for C++/CLI 889
- 27.12.1 Assembly Types 889
- 27.12.2 Specifying Assembly Attributes in AssemblyInfo.cs 890
- 27.12.3 An Example: Dynamically Loading Algorithms from an Assembly 891
- 27.13 Summary and Conclusions 895
- 27.14 Exercises and Projects 896

## CHAPTER 28
## C++ Concurrency, Part I Threads

- 28.1 Introduction and Objectives 899
- 28.2 Thread Fundamentals 900
- 28.2.1 A Small Digression into the World of OpenMP 902
- 28.3 Six Ways to Create a Thread 903
- 28.3.1 Detaching a Thread 908
- 28.3.2 Cooperative Tasking with Threads 908
- 28.4 Intermezzo: Parallelising the Binomial Method 909
- 28.5 Atomics 916
- 28.5.1 The C++ Memory Model 918
- 28.5.2 Atomic Flags 920
- 28.5.3 Simple Producer-Consumer Example 922
- 28.6 Smart Pointers and the Thread-Safe Pointer Interface 924

## CHAPTER 29
## C++ Concurrency, Part II Tasks

- 28.7 Thread Synchronisation 926
- 28.8 When Should we use Threads? 929
- 28.9 Summary and Conclusions 929
- 28.10 Exercises and Projects 930
- 29.1 Introduction and Objectives 935
- 29.2 Finding Concurrency: Motivation 936
- 29.2.1 Data and Task Parallelism 936
- 29.3 Tasks and Task Decomposition 937
- 29.3.1 Data Dependency Graph: First Example 937
- 29.3.2 Data Dependency Graph: Generalisations 939
- 29.3.3 Steps to Parallelisation 940
- 29.4 Futures and Promises 941
- 29.4.1 Examples of Futures and Promises in C++ 942
- 29.4.2 Mapping Dependency Graphs to C++ 944
- 29.5 Shared Futures 945
- 29.6 Waiting on Tasks to Complete 948
- 29.7 Continuations and Futures in Boost 950
- 29.8 Pure Functions 952
- 29.9 Tasks versus Threads 953
- 29.10 Parallel Design Patterns 953
- 29.11 Summary and Conclusions 955
- 29.12 Quizzes, Exercises and Projects 955

## CHAPTER 30
## Parallel Patterns Language (PPL)

- 30.1 Introduction and Objectives 961
- 30.2 Parallel Algorithms 962
- 30.2.1 Parallel For 963
- 30.2.2 Parallel for_each 964
- 30.2.3 Parallel Invoke and Task Groups 964
- 30.2.4 Parallel Transform and Parallel Reduction 967
- 30.3 Partitioning Work 967
- 30.3.1 Parallel Sort 970
- 30.4 The Aggregation/Reduction Pattern in PPL 971
- 30.4.1 An Extended Example: Computing Prime Numbers 973
- 30.4.2 An Extended Example: Merging and Filtering Sets 975
- 30.5 Concurrent Containers 977
- 30.6 An Introduction to the Asynchronous Agents Library and Event-Based Systems 978
- 30.6.1 Agents Library Overview 979
- 30.6.2 Initial Examples and Essential Syntax 980
- 30.6.3 Simulating Stock Quotes Work Flow 983
- 30.6.4 Monte Carlo Option Pricing Using Agents 985
- 30.6.5 Conclusions and Epilogue 985

## CHAPTER 31
## Monte Carlo Simulation, Part I

31.1 Introduction and Objectives 993

31.1.1 Software Product and Process Management 994

31.1.2 Who can Benefit from this Chapter? 995

31.2 The Boost Parameters Library for the Impatient 995

## CHAPTER 32
## Monte Carlo Simulation, Part II

32.1 Introduction and Objectives 1023

32.2 Parallel Processing and Monte Carlo Simulation 1023

## Appendix 1: Multiple-Precision Arithmetic 1053

## Appendix 2: Computing Implied Volatility 1075

## References 1109

## Index 1117

## CHAPTER 1
## A Tour of C++ and Environs

> riverrun, past Eve and Adam’s, from swerve of shore to bend of bay, brings us by a commodius vicus of recirculation back to Howth Castle and Environs
> —Joyce (1939)

### 1.1 INTRODUCTION AND OBJECTIVES

This book is the second edition of Financial Instrument Pricing Using C++, also written by the author (Duffy, 2004B). The most important reason for writing this hands-on book is to reflect the many changes and improvements to the C++ language, in particular due to the announcement of the new standard C++11 (and to a lesser extent C++14 and C++17). It feels like a new language compared to C++03 and in a sense it is. First, C++11 improves and extends the syntax of C++03. Second, it has become a programming language that supports the functional programming model in addition to the object-oriented and generic programming models.

We apply modern C++ to design and implement applications in computational finance, in particular option pricing problems using partial differential equation (PDE)/finite difference method (FDM), Monte Carlo and lattice models. We show the benefits of using C++11 compared to similar solutions in C++03. The resulting code tends to be more maintainable and extendible, especially if the software system has been properly designed. We recommend spending some time on designing the software system before jumping into code and to this end we include a defined process to take a problem description, design the problem and then implement it in such a way that it results in a product that satisfies the requirements and that is delivered on time and within budget.

This book is a detailed exposition of the language features in C++, how to use these features and how to design applications in computational finance. We discuss modern numerical methods to price plain and American options and the book is written in a hands-on, step-by-step fashion.

### 1.2 WHAT IS C++?

C++ is a general-purpose systems programming language that was originally designed as an extension to the C programming language. Its original name was ‘C with classes’ and its object-oriented roots can be traced to the programming language *Simula* which was one of the first object-oriented languages. C++ was standardised by the *International Organization for Standardization* (ISO) in 1998 (called the C++03 standard) and C++14 is the standard at the moment of writing. It can be seen as a minor extension to C++11 which is a major update to the language.

C++ was designed primarily for applications in which performance, efficiency and flexibility play a vital role. In this sense it is a systems programming language and early applications in the 1990s were in telecommunications, embedded systems, medical devices and *Computer Aided Design* (CAD) as well as first-generation option pricing risk management systems in computational finance. The rise in popularity continued well into the late 1990s as major vendors such as Microsoft, Sun and IBM began to endorse object-oriented technology in general and C++ in particular. It was also in this period that the Java programming language appeared which in time became a competitor to C++.

C++ remains one of the most important programming languages at the moment of writing. It is evolving to support new hardware such as multicore processors, GPUs (graphics processing units) and heterogeneous computing environments. It also has a number of mathematical libraries that are useful in computational finance applications.

### 1.3 C++ AS A MULTIPARADIGM PROGRAMMING LANGUAGE

We give an overview of the programming paradigms that C++ supports. In general, a *programming paradigm* is a way to classify programming languages according to the style of computer programming. Features of various programming languages determine which programming paradigms they belong to. C++ is a multiparadigm programming language because it supports the following styles:

- *Procedural*: organises code around functions, as typically seen in programs written in C, FORTRAN and COBOL. The style is based on structured programming in which a function or program is decomposed into simpler functions.
- *Object-oriented*: organises code around classes. A *class* is an abstract entity that encapsulates functions and data into a logical unit. We instantiate a class to produce *objects*. Furthermore, classes can be grouped into hierarchies. It is probably safe to say that this style is the most popular one in the C++ community.
- *Generic/template*: templates are a feature of C++ that allow functions and classes to operate with generic types. A function or class can then work on different data types.
- *Functional*: treats computation as the evaluation of mathematical functions. It is a declarative programming paradigm; this means that programming is done with expressions and declarations instead of statements. The output value of a function depends only on its input arguments.

The generic programming style is becoming more important and pronounced in C++, possibly at the expense of the traditional object-oriented model which is based on class hierarchies and subtype (dynamic) polymorphism. Template code tends to perform better at run-time while many errors are caught at compile-time, in contrast to object-oriented code where the errors tend to be caught by the linker or even at run-time.
