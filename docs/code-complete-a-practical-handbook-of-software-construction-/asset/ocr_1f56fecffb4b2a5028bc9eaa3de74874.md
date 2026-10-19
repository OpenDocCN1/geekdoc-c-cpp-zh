# Chapter 6

# Working Classes

# Contents

+   - 6.1 Class Foundations: Abstract Data Types (ADTs): page 126
+   - 6.2 Good Class Interfaces: page 133
+   - 6.3 Design and Implementation Issues: page 143
+   - 6.4 Reasons to Create a Class: page 152
+   - 6.5 Language-Specific Issues: page 156
+   - 6.6 Beyond Classes: Packages: page 156

# Related Topics

+   - Design in construction: Chapter 5
+   - Software architecture: Section 3.5
+   - High-quality routines: Chapter 7
+   - The Pseudocode Programming Process: Chapter 9
+   - Refactoring: Chapter 24

In the dawn of computing, programmers thought about programming in terms of statements. Throughout the 1970s and 1980s, programmers began thinking about programs in terms of routines. In the twenty-first century, programmers think about programming in terms of classes.

![](bbox=[0.11, 0.65, 0.21, 0.71])

A class is a collection of data and routines that share a cohesive, well-defined responsibility. A class might also be a collection of routines that provides a cohesive set of services even if no common data is involved. A key to being an effective programmer is maximizing the portion of a program that you can safely ignore while working on any one section of code. Classes are the primary tool for accomplishing that objective.

This chapter contains a distillation of advice in creating high-quality classes. If you’re still warming up to object-oriented concepts, this chapter might be too advanced. Make sure you’ve read Chapter 5, “Design in Construction.” Then start with Section 6.1, “Class Foundations: Abstract Data Types (ADTs),” and ease your way into the remaining sections. If you’re already familiar with class basics, you might skim Section 6.1 and then dive into the discussion of class interfaces in Section 6.2. The “Additional Resources” section at the end of this chapter contains pointers to introductory reading, advanced reading, and programming-language-specific resources.