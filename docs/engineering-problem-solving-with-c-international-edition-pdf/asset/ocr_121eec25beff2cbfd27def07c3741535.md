# ADVANCED TOPICS

# CHAPTER OUTLINE

+   - Objectives
+   - 10.1 Generic Programming
+   - 10.2 Data Abstraction
+   - 10.3 Problem Solving Applied: Color Image Processing
+   - 10.4 Recursion
+   - 10.5 Class Templates
+   - 10.6 Inheritance
+   - 10.7 virtual Methods
+   - 10.8 Problem Solving Applied: Iterated Prisoner's Dilemma
+   - Summary, Key Terms, C++ Statement Summary, Style Notes, Debugging Notes, and Problems

# OBJECTIVES

In this chapter, we develop problem solutions containing:

+   - function templates
+   - overloaded operators
+   - image processing examples
+   - recursive member functions
+   - class templates
+   - class hierarchies
+   - an implementation of the iterated prisoner's dilemma game

# 10.1 Generic Programming

Generic programming is a form of programming that supports the implementation of an algorithm, or a type, using a set of parameters rather than a specific type. The C++ programming language supports generic programming through the use of templates. A template is a formal definition of a generic algorithm, or generic type, and can be implemented, or instantiated, by the compiler when referenced with a specific type. The ability to define a concept once, and have the concept implemented automatically for many different types, saves time in the development and testing of problem solutions.

In previous chapters we developed problem solutions that used pre-defined templates from the C++ Standard Library, including vector <type> and random_shuffle(). In this chapter we will illustrate the use of programmer defined templates by writing a set of function templates to perform statistical measures on various sets of data, and a class template to implement the concept of a binary tree.