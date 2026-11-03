+   7.1 Introduction
+   7.2 Pointer Variable Definitions and Initialization
+   7.3 Pointer Operators
+   7.4 Passing Arguments to Functions by Reference
+   7.5 Using the const Qualifier with Pointers
+   7.5.1 Converting a String to Uppercase Using a Non-Constant Pointer to Non-Constant Data
+   7.5.2 Printing a String One Character at a Time Using a Non-Constant Pointer to Constant Data
+   7.5.3 Attempting to Modify a Constant Pointer to Non-Constant Data
+   7.5.4 Attempting to Modify a Constant Pointer to Constant Data
+   7.6 Bubble Sort Using Pass-by-Reference
+   7.7 sizeof Operator
+   7.8 Pointer Expressions and Pointer Arithmetic
+   7.8.1 Allowed Operators for Pointer Arithmetic
+   7.8.2 Aiming a Pointer at an Array
+   7.8.3 Adding an Integer to a Pointer
+   7.8.4 Subtracting an Integer from a Pointer
+   7.8.5 Incrementing and Decrementing a Pointer
+   7.8.6 Subtracting One Pointer from Another
+   7.8.7 Assigning Pointers to One Another
+   7.8.8 Pointer to void
+   7.8.9 Comparing Pointers
+   7.9 Relationship between Pointers and Arrays
+   7.9.1 Pointer/Offset Notation
+   7.9.2 Pointer/Index Notation
+   7.9.3 Cannot Modify an Array Name with Pointer Arithmetic
+   7.9.4 Demonstrating Pointer Indexing and Offsets
+   7.9.5 String Copying with Arrays and Pointers
+   7.10 Arrays of Pointers
+   7.11 Case Study: Card Shuffling and Dealing Simulation
+   7.12 Pointers to Functions
+   7.12.1 Sorting in Ascending or Descending Order
+   7.12.2 Using Function Pointers to Create a Menu-Driven System
+   7.13 Secure C Programming
+   Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises
+   Special Section: Building Your Own Computer | Array of Function Pointer Exercises | Making a Difference

# 7.1 Introduction

In this chapter, we discuss one of the most powerful features of the C programming language, the pointer.¹ Pointers are among C's most difficult capabilities to master. Pointers enable programs to accomplish pass-by-reference, to pass functions between functions, and to create and manipulate dynamic data structures—ones that can grow and shrink at execution time, such as linked lists, queues, stacks and trees. This chapter explains basic pointer concepts. In Section 7.13, we discuss various pointer-related security issues. Chapter 10 examines the use of pointers with structures. Chapter 12 introduces dynamic memory management techniques and presents examples of creating and using dynamic data structures.

1. Pointers and pointer-based entities such as arrays and strings, when misused intentionally or accidentally, can lead to errors and security breaches. See our Secure C Programming Resource Center (www.deitel.com/SecureC/) for articles, books, white papers and forums on this important topic.