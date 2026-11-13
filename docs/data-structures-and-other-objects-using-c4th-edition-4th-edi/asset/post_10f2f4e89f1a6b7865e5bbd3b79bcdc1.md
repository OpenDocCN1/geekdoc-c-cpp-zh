
## CHAPTER 12 SEARCHING

### 12.1 Serial Search and Binary Search 584

- Serial Search 584
- Serial Search—Analysis 584
- Binary Search 586
- Binary Search—Design 587
- Pitfall: Common Indexing Errors in Binary Search Implementations 589
- Binary Search—Analysis 590
- Standard Library Search Functions 594
- Functions for Sorted Ranges 594
- Functions for Unsorted Ranges 596
- The STL lower_bound Function 596
- Self-Test Exercises for Section 12.1 598

### 12.2 Open-Address Hashing 598

- Introduction to Hashing 598
- The Table Class—Specification 601
- The Table Class—Design 603
- Programming Tip: Using size_t Can Indicate a Value's Purpose 606
- The Table ADT—Implementation File 606
- C++ Feature: Inline Functions in the Implementation File 612
- Choosing a Hash Function to Reduce Collisions 612
- Double Hashing to Reduce Clustering 613
- Self-Test Exercises for Section 12.2 614

### 12.3 Chained Hashing 615

- Self-Test Exercises for Section 12.3 617

### 12.4 Time Analysis of Hashing 617

- The Load Factor of a Hash Table 617
- Self-Test Exercises for Section 12.4 620

### 12.5 Programming Project: A Table Class with STL Vectors 620

- A New Table Class 620
- Using Vectors in the New Table 621
- Template Parameters That Are Constants 621
- Template Parameters That Are Functions 621
- Implementing the New Table Class 622
- Self-Test Exercises for Section 12.5 623

### 12.6 Hash Tables in the TR1 Library Extensions 624

### Chapter Summary 624

### Solutions to Self-Test Exercises 625

### Programming Projects 628

## CHAPTER 13 SORTING

### 13.1 Quadratic Sorting Algorithms 630

- Selectionsort—Specification 630
- Selectionsort—Design 630
- Selectionsort—Implementation 632
- Selectionsort—Analysis 634
- Programming Tip: Rough Estimates Suffice for Big-O 636
- Insertionsort 636
- Insertionsort—Analysis 640
- Self-Test Exercises for Section 13.1 642

### 13.2 Recursive Sorting Algorithms 642

- Divide-and-Conquer Using Recursion 642
- Creating and Specifying a Subarray with Pointer Arithmetic 643
- Mergesort 645
- The merge Function 646
- The Dynamic Memory Usage in Mergesort 651
- Mergesort—Analysis 651
- Mergesort for Files 653
- Quicksort 653
- The partition Function 655
- Quicksort—Choosing a Good Pivot Element 661
- Self-Test Exercises for Section 13.2 661

### 13.3 An O(n log n) Algorithm using a Heap 662

- Heapsort 662
- Making the Heap 667
- Reheapification Downward 670
- Heapsort—Analysis 671
- Self-Test Exercises for Section 13.3 672

### 13.4 Sorting and Binary Search in the STL 672

- The Original C qsort Function 672
- The STL sort Function 673
- Heapsort in the STL 674
- Binary Search Functions in the STL 674
- The Comparison Parameter for STL Sorting Functions 675
- Writing Your Own sort Function That Uses Iterators 676

### Chapter Summary 677

### Solutions to Self-Test Exercises 678

### Programming Projects 679

## CHAPTER 14 DERIVED CLASSES AND INHERITANCE

### 14.1 Derived Classes 684

- How to Declare a Derived Class 686
- The Automatic Constructors of a Derived Class 687
- Using a Derived Class 688
- The Automatic Assignment Operator for a Derived Class 690
- The Automatic Destructor of a Derived Class 690
- Overriding Inherited Member Functions 691
- Programming Tip: Make the Overriding Function Call the Original 692
- Self-Test Exercises for Section 14.1 692

### 14.2 Simulation of an Ecosystem 692

- Implementing Part of the Organism Object Hierarchy 693
- The organism Class 693
- The animal Class: A Derived Class with New Private Member Variables 696
- How to Provide a New Constructor for a Derived Class 696
- The Other Animal Member Functions 698
- Self-Test Exercises for Middle of Section 14.2 702
- The herbivore Class 703
- The Pond Life Simulation Program 705
- Pond Life—Implementation Details 710
- Using the Pond Model 710
- Dynamic Memory Usage 711
- Self-Test Exercises for Section 14.2 712

### 14.3 Virtual Member Functions and Abstract Classes 712

- Introduction to the Game Class 712
- Protected Members 716
- Introduction Members 716
- Virtual Member Functions 716
- Virtual Destructors 718
- The Protected Virtual Member Functions of the Game Class 718
- A Derived Class to Play Connect Four 719
- The Private Member Variables of the Connect Four Class 719
- The Connect Four Constructor and Restart Function 721
- Three Connect Four Functions That Deal with the Game's Status 721
- The Member Functions for Functions That Deal with Moves 722
- The clone Function 723
- Writing Your Own Derived Games from the Game Class 724
- The Game Class's Play Algorithm with Minimax 724
- Self-Test Exercises for Section 14.3 726

### Chapter Summary 728

### Further Reading 728

### Solutions to Self-Test Exercises 728

### Programming Projects 730

## CHAPTER 15 GRAPHS

### 15.1 Graph Definitions 733

- Undirected Graphs 733
- Programming Example: Undirected State Graphs 734
- Directed Graphs 737
- More Graph Terminology 738
- Airline Routes Example 739
- Self-Test Exercises for Section 15.1 739

### 15.2 Graph Implementations 740

- Representing Graphs with an Adjacency Matrix 740
- Using a Two-Dimensional Array to Store an Adjacency Matrix 741
- Representing Graphs with Edge Lists 741
- Representing Graphs with Edge Sets 742
- Which Representation Is Best? 743
- Programming Example: Labeled Graph Class 743
- Member Functions to Add Vertices and Edges 744
- Labeled Graph Class—Overloading the Subscript Operator 745
- A Const Version of the Subscript Operator 746
- Labeled Graph Class—Neighbors Function 747
- Labeled Graph Class—Implementation 747
- Self-Test Exercises for Section 15.2 748

### 15.3 Graph Traversals 753

- Depth-First Search 754
- Breadth-First Search 757
- Depth-First Search—Implementation 759
- Breadth-First Search—Implementation 761
- Self-Test Exercises for Section 15.3 761

### 15.4 Path Algorithms 763

- Determining Whether a Path Exists 763
- Graphs with Weighted Edges 764
- Shortest-Distance Algorithm 765
- Shortest-Path Algorithm 775
- Self-Test Exercises for Section 15.4 776

### Chapter Summary 777

### Solutions to Self-Test Exercises 777

### Programming Projects 778

## APPENDICES

### A. ASCII CHARACTER SET 781

### B. FURTHER BIG-O NOTATION 782

### C. PRECEDENCE OF OPERATORS 784

### D. COMMAND LINE COMPILING AND LINKING 785

### E. DEALING WITH OLDER COMPILERS 785

### F. INPUT AND OUTPUT IN C++ 785

### G. SELECTED LIBRARY FUNCTIONS 793

### H. BRIEF REFERENCE FOR THE STANDARD TEMPLATE CLASSES 795

### I. A TOOLKIT OF USEFUL FUNCTIONS 803

### J. FUNDAMENTAL STYLE GUIDE 806

### K. DOWNLOADING THE GNU COMPILER AND SOFTWARE 807

### L. EXCEPTION HANDLING 807

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_28_0.png)

## The Phases of Software Development

> Chapter the first which explains how, why, when, and where there was ever any problem in the first place
> NOEL LANGLEY
> The Land of Green Ginger

### LEARNING OBJECTIVES

When you complete Chapter 1, you will be able to...

- write precondition/postcondition contracts for small functions, and use the C++ assert facility to test preconditions.
- recognize quadratic, linear, and logarithmic running time behavior in simple algorithms, and write big-O expressions to describe this behavior.
- create and recognize test data that is appropriate for simple problems, including testing boundary conditions and fully exercising code.

### CHAPTER CONTENTS

- 1.1 Specification, Design, Implementation
- 1.2 Running Time Analysis
- 1.3 Testing and Debugging
- Chapter Summary
- Solutions to Self-Test Exercises

This chapter illustrates the phases of software development. These phases occur in all software, including the small programs that you'll see in this first chapter. In subsequent chapters, you'll go beyond these small programs, applying the phases of software development to organized collections of data. These organized collections of data are called **data structures**, and the main topics of this book revolve around proven techniques for representing and manipulating such data structures.

Years from now you may be a software engineer writing large systems in a specialized area, perhaps computer graphics or artificial intelligence. Such futuristic applications will be exciting and stimulating, and within your work you will still see the phases of software development and fundamental data structures that you learn and practice now.

Here is a list of the phases of software development:

### The Phases of Software Development

- Specification of the task
- Design of a solution
- Implementation (coding) of the solution
- Analysis of the solution
- Testing and debugging
- Maintenance and evolution of the system
- Obsolescence

Do not memorize this list: Throughout the book, your practice of these phases will achieve far better familiarity than mere memorization. Also, memorizing an "official list" is misleading because it suggests that there is a single sequence of discrete steps that always occur one after another. In practice, the phases blur into each other; for instance, the analysis of a solution's efficiency may occur hand in hand with the design, before any coding. Or low-level design decisions may be postponed until the implementation phase. Also, the phases might not occur one after another. Typically there is back-and-forth travel between the phases.

Most of the work in software development does not depend on any particular programming language. Specification, design, and analysis can all be carried out with few or no ties to a particular programming language. Nevertheless, when we get down to implementation details, we do need to decide on one particular programming language. The language we use in this book is C++.

the phases blur into each other
