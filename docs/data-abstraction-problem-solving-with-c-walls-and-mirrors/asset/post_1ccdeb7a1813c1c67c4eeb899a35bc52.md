
## 2.5 Organizing Data

### 2.5.1 The Towers of Hanoi

## 2.6 More Examples

### 2.6.1 The Fibonacci Sequence (Multiplying Rabbits)
### 2.6.2 Organizing a Parade

### 2.6.3 Choosing k Out of n Things

## 2.7 Recursion and Efficiency

## Chapter 3 Array-Based Implementations

## 3.1 The Approach

### 3.1.1 Core Methods
### 3.1.2 Using Fixed-Size Arrays

## 3.2 An Array-Based Implementation of the ADT Bag

### 3.2.1 The Header File
### 3.2.2 Defining the Core Methods
### 3.2.3 Testing More Methods
### 3.2.4 Implementing More Methods
### 3.2.5 Methods That Remove Entries
### 3.2.6 Testing

## 3.3 Using Recursion in the Implementation

### 3.3.1 The Method getIndexOf
### 3.3.2 The Method getFrequencyOf

## C++ Interlude 2 Pointers, Polymorphism, and Memory Allocation

### C2.1 Memory Allocation for Variables and Early Binding of Methods
### C2.2 A Problem to Solve

## C2.3 Pointers and the Program's Free Store

### C2.3.1 Deallocating Memory
### C2.3.2 Avoiding Memory Leaks
### C2.3.3 Avoiding Dangling Pointers

## C2.4 Virtual Methods and Polymorphism

## C2.5 Dynamic Allocation of Arrays

### C2.5.1 A Resizable Array-Based Bag

## Chapter 4 Link-Based Implementations

## 4.1 Preliminaries

### 4.1.1 The Class Node

## 4.2 A Link-Based Implementation of the ADT Bag

### 4.2.1 The Header File
### 4.2.2 Defining the Core Methods
### 4.2.3 Implementing More Methods

## 4.3 Using Recursion in Link-Based Implementations

### 4.3.1 Recursive Definitions of Methods in LinkedBag

## 4.4 Testing Multiple Implementations

## 4.5 Comparing Array-Based and Link-Based Implementations

## Chapter 5 Recursion as a Problem-Solving Technique

## 5.1 Defining Languages

### 5.1.1 The Basics of Grammars
### 5.1.2 Two Simple Languages

## 5.2 Algebraic Expressions

### 5.2.1 K of Algebraic Expressions

## Table of Contents

- 5.2.2 Prefix Expressions 166
- 5.2.3 Postfix Expressions 170
- 5.2.4 Fully Parenthesized Expressions 171
- 5.3 Backtracking
- 5.3.1 Searching for an Airline Route 172
- 5.3.2 The Eight Queens Problem 177
- 5.4 The Relationship Between Recursion and Mathematical Induction 183
- 5.4.1 The Correctness of the Recursive Functional Function 183
- 5.4.2 The Cost of Towers of Hanoi 184

## Chapter 6 Stacks 193
### 6.1 Abstract Data Type Stack 194
### 6.1.1 Developing an ADT During the Design of a Solution 194
### 6.1.2 Specifications for the ADT Stack 196
### 6.2 Simple Uses of a Stack 201
### 6.2.1 Checking for Balanced Braces 201
### 6.2.2 Recognizing Strings in a Language 203
### 6.3 Using Stacks with Algebraic Expressions 205
### 6.3.1 Evaluating Postfix Expressions 205
### 6.3.2 Converting Expressions to Equivalent Expressions 206
### 6.4 Using a Stack to Search a Flight Map 210
### 6.5 The Relationship Between Stacks and Recursion 216

## C++ Interlude 3 Exceptions 227
### C.1 Background 228
### C.1.1 A Problem to Solve 228
### C.2 Assertions 229
### C.3 Throwing Exceptions 230
### C.4 Handling Exceptions 233
### C.4.1 Multiple catch Blocks 235
### C.4.2 Uncaught Exceptions 236
### C.5 Programmer-Defined Exception Classes 239

## Chapter 7 Stack Implementations 241
### 7.1 An Array-Based Implementation 242
### 7.2 A Link-Based implementation 245
### 7.3 Implementations That Use Exceptions 249

## Chapter 8 Lists 253
### 8.1 Specifying the ADT List 254
### 8.2 Using the List Operations 259
### 8.3 Interface Template for the ADT List 261

## Chapter 9 List Implementations 265
### 9.1 An Array-Based Implementation of the ADT List 266
### 9.1.1 The Header File 266
### 9.1.2 The Implementation File 268
### 9.2 A Link-Based Implementation of the ADT List 272
### 9.2.1 The Header File 272
### 9.2.2 The Implementation File 274
### 9.2.3 Using Recursion in LinkedList Methods 281
### 9.3 Comparing Implementations 285

## Chapter 10 Algorithm Efficiency

### 10.1 What Is a Good Solution?
### 10.2 Measuring the Efficiency of Algorithms
### 10.2.1 The Execution Time of Algorithms
### 10.2.2 Algorithm Growth Rates
### 10.2.3 Analysis and Big O Notation
### 10.4 Keeping Your Perspective
### 10.2.5 The Efficiency of Searching Algorithms

## Chapter 11 Sorting Algorithms and Their Efficiency

### 11.1 Basic Sorting Algorithms
### 11.1.1 The Selection Sort
### 11.1.2 The Bubble Sort
### 11.1.3 The Insertion Sort
### 11.2 Faster Sorting Algorithms
### 11.2.1 The Merge Sort
### 11.2.2 The Quick Sort
### 11.2.3 The Radix Sort
### 11.3 A Comparison of Sorting Algorithms

## C++ Interlude 4 Class Relationships and Reuse

### 4.1 Inheritance Revisited
### 4.1.1 Public, Private, and Protected Sections of a Class
### 4.1.2 Public, Private, and Protected Inheritance
### 4.1.3 Is-a and As-a
### 4.2 Composition: Has-a Relationships
### 4.3 Abstract Classes Revisited

## Chapter 12 Sorted Lists and Their Implementations

### 12.1 Specifying the ADT Sorted List
### 12.1.1 An Interface Template for the ADT Sorted List
### 12.1.2 Using the Sorted List Operations
### 12.2 A Link-Based Implementation
### 12.2.1 The Header File
### 12.2.2 The Implementation File
### 12.2.3 The Efficiency of the Link-Based Implementation
### 12.3 Implementations That Use the ADT List
### 12.3.1 Containment
### 12.3.2 Public Inheritance
### 12.3.3 Private Inheritance

## Chapter 13 Queues and Priority Queues

### 13.1 The ADT Queue
### 13.2 Simple Applications of the ADT Queue
### 13.2.1 Reading a String of Characters
### 13.2.2 Recognizing Palindromes
### 13.3 The ADT Priority Queue
### 13.3.1 Tracking Your Assignments
### 13.4 Application: Simulation
### 13.5 Position-Oriented and Value-Oriented ADTs

![](img/d0cb86b2f18b2db569968ad7c743510e_20.png)

## Chapter 14 Queue Implementations

### 14.1 The ADT Queue
### 14.2 An Array-Based Implementation
### 14.2.1 Algorithms for the Array-Based Heap
### 14.2 The Implementation
### 14.3 A Link-Based Implementation of the ADT Queue
### 14.3.1 The Header File
### 14.3.2 The Implementation
### 14.4 A Link-Based Implementation of the ADT Priority Queue
### 14.4.1 Algorithms for the ADT Priority Queue
### 14.4.2 Searching a Binary Tree
### 14.5 Comparing Implementations

## C++ Interlude 5 Overloaded Operators and Access

### C5.1 Overloaded Operators
### C5.1.1 For Assignment
### C5.1.2 For Concatenation
### C5.2 Friend Access

## Chapter 15 Trees

### 15.1 Terminology
### 15.1.1 Kinds of Trees
### 15.1.2 Height of Trees
### 15.1.3 Full, Complete, and Balanced Trees
### 15.1.4 Maximum and Minimum Heights
### 15.2 The ADT Binary Tree
### 15.2.1 Traversals of a Binary Tree
### 15.2 Binary Tree Operations
### 15.3 The ADT Binary Search Tree
### 15.3.1 Algorithms for Binary Search Tree
### 15.3.2 Searching a Binary Search Tree
### 15.3.3 Creating a Binary Search Tree
### 15.3.4 The Efficiency of Binary Search Tree

## Chapter 16 Tree Implementations

### 16.1 Representation
### 16.1.1 Array-Based Representation
### 16.1.2 Link-Based Representation
### 16.2 The ADT Binary Tree
### 16.2.1 The Header File
### 16.2.2 The Implementation
### 16.3 A Link-Based Implementation of the ADT Binary Tree
### 16.3.1 Algorithms for the ADT Binary Tree
### 16.3.2 The Implementation
### 16.4 A Link-Based Implementation of the ADT Binary Search Tree
### 16.4.1 Algorithms for the ADT Binary Search Tree
### 16.4.2 The Implementation
### 16.5 Saving a Binary Search Tree
### 16.6 Tree Sort

## C++ Interlude 6 Iterators

### C6.1 Iterators
### C6.1.1 Common Iterator Operations
### C6.1.2 Using an Iterator
### C6.1.3 Implementing an Iterator
### C6.2 Advanced Iterator Functionality

## Chapter 17 Heaps

### 17.1 The ADT Heap
### 17.2 An Array-Based Implementation of a Heap
### 17.2.1 Algorithms for the Array-Based Heap
### 17.2.2 The Implementation
### 17.3 A Heap Implementation of the ADT Priority Queue
### 17.4 Heap Sort

## Chapter 18 Dictionaries and Their Implementations

### 18.1 The ADT Dictionary
### 18.1.1 An Interface for the ADT Dictionary
### 18.2 Possible Implementations
### 18.2.1 A Sorted Array-Based Implementation of the ADT Dictionary
### 18.2.2 A Binary Tree Implementation of the ADT Dictionary
### 18.3 Selecting an Implementation
### 18.3.1 Scenarios
### 18.4 Hashing
### 18.4.1 Hash Functions
### 18.4.2 Resolving Collisions
### 18.4.3 The Efficiency of Hashing
### 18.4.4 What Constitutes a Good Hash Function?
### 18.4.5 Dictionary Traversal: An Inefficient Operation Under Hashing
### 18.4.6 Using Hashing and Separating to Implement the ADT Dictionary

## Chapter 19 Balanced Search Trees

### 19.1 Balanced Search Trees
### 19.2 2-3 Trees
### 19.2.1 Traversing a 2-3 Tree
### 19.2.2 Searching a 2-3 Tree
### 19.2.3 Inserting Data into a 2-3 Tree
### 19.2.4 Removing Data from a 2-3 Tree
### 19.3 2-3-4 Trees
### 19.3.1 Searching and Traversing a 2-3-4 Tree
### 19.3.2 Inserting Data into a 2-3-4 Tree
### 19.3.3 Removing Data from a 2-3-4 Tree
### 19.4 Red-Black Trees
### 19.4.1 Searching and Traversing a Red-Black Tree
### 19.4.2 Inserting into and Removing from a Red-Black Tree

## Chapter 20 Graphs

### 20.1 Terminology
### 20.2 Graphs as ADTs
### 20.2.1 Implementing Graphs
### 20.3 Graph Traversals
### 20.3.1 Depth-First Search
### 20.3.2 Breadth-First Search
### 20.4 Applications of Graphs
### 20.4.1 Topological Sorting
