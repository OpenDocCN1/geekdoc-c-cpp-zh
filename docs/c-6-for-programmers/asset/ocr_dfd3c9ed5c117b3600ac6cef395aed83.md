# Outline

+   - **19.1** Introduction
+   - **19.2** Collections Overview
+   - **19.3** Class Array and Enumerators
+     - 19.3.1 C# 6 using static Directive
+     - 19.3.2 Class UsingArray's static Fields
+     - 19.3.3 Array Method Sort
+     - 19.3.4 Array Method Copy
+     - 19.3.5 Array Method BinarySearch
+     - 19.3.6 Array Method GetEnumerator and Interface IEnumerator
+     - 19.3.7 Iterating Over a Collection with foreach
+     - 19.3.8 Array Methods Clear, IndexOf, LastIndexOf and Reverse
+   - **19.4** Dictionary Collections
+     - 19.4.1 Dictionary Fundamentals
+     - 19.4.2 Using the SortedDictionary Collection
+   - **19.5** Generic LinkedList Collection
+   - **19.6** C# 6 Null Conditional Operator [?]
+   - **19.7** C# 6 Dictionary Initializers and Collection Initializers
+   - **19.8** Delegates
+     - 19.8.1 Declaring a Delegate Type
+     - 19.8.2 Declaring a Delegate Variable
+     - 19.8.3 Delegate Parameters
+     - 19.8.4 Passing a Method Name Directly to a Delegate Parameter
+   - **19.9** Lambda Expressions
+     - 19.9.1 Expression Lambdas
+     - 19.9.2 Assigning Lambdas to Delegate Variables
+     - 19.9.3 Explicitly Typed Lambda Parameters
+     - 19.9.4 Statement Lambdas
+   - **19.10** Introduction to Functional Programming
+     - 19.10.1 Functional Programming with LINQ Method-Call Syntax and Lambdas
+   - **19.11** LINQ Extension Methods Min, Max, Sum and Average
+     - 19.11.2 Aggregate Extension Method for Reduction Operations
+     - 19.11.3 The Where Extension Method for Filtering Operations
+     - 19.11.4 Select Extension Method for Mapping Operations
+   - **19.12** PLINQ: Improving LINQ to Objects Performance with Multicore
+   - **19.13** (Optional) Covariance and Contravariance for Generic Types
+   - **19.14** Wrap-Up

# 19.1 **Introduction**

For the vast majority of apps, there’s no need to build custom data structures. Instead, you can use the *prepackaged* data-structure classes provided by the .NET Framework. These are known as collection classes—they store collections of data. Each instance of one of these classes is a collection of items. Some examples of collections are the cards you hold in a card game, the songs stored in your computer, the real-estate records in your local registry of deeds (which map book numbers and page numbers to property owners), and the players on your favorite sports team.

# *Use the Existing Collection Classes Rather Than Building Your Own*

Collection classes enable you to store sets of items by using existing data structures, without concern for how they’re implemented. This is a nice example of code reuse. You can code faster and expect excellent performance, maximizing execution speed and minimizing memory consumption. In this chapter, we discuss

+   - the collection interfaces that declare each collection type’s capabilities
+   - the implementation classes
+   - the enumerators that iterate through collections (these are like iterators in languages like C++ and Java).