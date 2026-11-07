![](bbox=[0.0, 0.125, 0.137, 0.302])

+   7.1 Introduction
+   7.2 Arrays
+   7.3 Declaring Arrays
+   7.4 Examples Using Arrays
+     - 7.4.1 Declaring an Array and Using a Loop to Initialize the Array’s Elements
+     - 7.4.2 Initializing an Array in a Declaration with an Initializer List
+     - 7.4.3 Specifying an Array’s Size with a Constant Variable and Setting Array Elements with Calculations
+     - 7.4.4 Summing the Elements of an Array
+     - 7.4.5 Using Bar Charts to Display Data Graphically
+     - 7.4.6 Using the Elements of an Array as Counters
+     - 7.4.7 Using Arrays to Summarize Survey Results
+   7.4.8 Static Local Arrays and Automatic Local Arrays
+   7.5 Passing Arrays to Functions
+   7.6 Case Study: Class GradeBook Using an Array to Store Grades
+   7.7 Searching Arrays with Linear Search
+   7.8 Sorting Arrays with Insertion Sort
+   7.9 Multidimensional Arrays
+   7.10 Case Study: Class GradeBook Using a Two-Dimensional Array
+   7.11 Introduction to C++ Standard Library Class Template vector
+   7.12 Wrap-Up
+   
+   *Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Recursion Exercises | vector Exercises | Making a Difference*

# ### 7.1 Introduction

This chapter introduces the topic of **data structures**—collections of related data items. **Arrays** are data structures consisting of related data items of the same type. You learned about classes in Chapter 3. In Chapter 21 we discuss the notion of **structures**. Structures and classes can each hold related data items of possibly different types. Arrays, structures and classes are “static” entities in that they remain the same size throughout program execution. (They may, of course, be of automatic storage class and hence be created and destroyed each time the blocks in which they’re defined are entered and exited.)

After discussing how arrays are declared, created and initialized, we present a series of practical examples that demonstrate several common array manipulations. We present an example of searching arrays to find particular elements. The chapter also introduce one of the most important computing applications—sorting data (i.e., putting the data in some particular order). Two sections of the chapter enhance the GradeBook class by using arrays to enable the class to maintain a set of grades in memory and analyze student grades from multiple exams in a semester.

The style of arrays we use throughout most of this chapter are C-style pointer-based arrays. (We’ll study pointers in Chapter 8.) In Section 7.11, and in Chapter 22, Standard Template Library (STL), we’ll cover C++’s all-ﬂedged objects called vectors. We’ll discover that these object-based arrays are safer and more versatile than the C-style, pointer-based arrays that we discuss in the early part of this chapter. As part of the vector example, we introduce the exception-handling mechanism and use it to allow a program to continue executing when the program attempts to access a vector element that does not exist.