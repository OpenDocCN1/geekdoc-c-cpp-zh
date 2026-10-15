+   3.1 Introduction
+   3.2 Classes, Objects, Member Functions and Data Members
+   3.3 Overview of the Chapter Examples
+   3.4 Defining a Class with a Member Function
+   3.5 Defining a Member Function with a Parameter
+   3.6 Data Members, set Functions and get Functions
+   3.7 Initializing Objects with Constructors
+   3.8 Placing a Class in a Separate File for Reusability
+   3.9 Separating Interface from Implementation
+   3.10 Validating Data with set Functions
+   3.11 (Optional) Software Engineering Case Study: Identifying the Classes in the ATM Requirements Specification
+   3.12 Wrap-Up

# 3.1 Introduction

In Chapter 2, you created simple programs that displayed messages to the user, obtained information from the user, performed calculations and made decisions. In this chapter, you'll begin writing programs that employ the basic concepts of object-oriented programming that we introduced in Section 1.10. One common feature of every program in Chapter 2 was that all the statements that performed tasks were located in function main. Typically, the programs you develop in this book will consist of function main and one or more classes, each containing data members and member functions. If you become part of a development team in industry, you might work on software systems that contain hundreds, or even thousands, of classes. In this chapter, we develop a simple, well-engineered framework for organizing object-oriented programs in C++.

First, we motivate the notion of classes with a real-world example. Then we present a carefully paced sequence of seven complete working programs to demonstrate creating and using your own classes. These examples begin our integrated case study on developing a grade-book class that instructors can use to maintain student test scores. This case study is enhanced over the next several chapters, culminating with the version presented in Chapter 7, Arrays and Vectors. We also introduce the C++ standard library class string in this chapter.

# 3.2 Classes, Objects, Member Functions and Data Members

Let’s begin with a simple analogy to help you reinforce your understanding from Section 1.10 of classes and their contents. Suppose you want to drive a car and make it go faster by pressing down on its accelerator pedal. What must happen before you can do this? Well, before you can drive a car, someone has to design it and build it. A car typically begins as engineering drawings, similar to the blueprints used to design a house. These drawings include the design for an accelerator pedal that the driver will use to make the car go