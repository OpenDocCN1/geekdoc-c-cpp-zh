# 9.1 Introduction

+   9.2 Querying an array of int Values Using LINQ
9.2.1 The from Clause
9.2.2 the where Clause
9.2.3 the select Clause
9.2.4 Iterating Through Results of the LINQ Query
9.2.5 The orderby Clause
9.2.6 Interface IEnumerable<T>
9.3.4 Selecting a Property of an Object
9.3.5 Creating New Types in the select Clause of LINQ Query
9.4 Introduction to Collections
9.4.1 List<T> Collection
9.4.2 Dynamically Resizing a List<T>
9.5 Querying the Generic List Using LINQ
9.5.1 The 1st Clause
9.5.2 Deferred Execution
9.5.3 Extension Methods ToArray and ToList
9.5.4 Collection Initializers
9.6 Wrap-Up
9.7 Detail LINQ Resource Count
9.3 Querying an array of Employee Objects Using LINQ
9.3.1 Accessing the Properties of a LINQ Query's Range Variable
9.3.2 Sorting a LINQ Query's Results by Multiple Properties
9.3.3 First and Count Extension Methods

Outline

Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# 9.1 Introduction

Chapter 8 introduced arrays—simple data structures used to store items of a specific type. Although commonly used, arrays have limited capabilities. For instance, you must specify an array's size when you create it. If, at execution time, you wish to modify that size, you must do so by creating a new array and copying elements into it or by using LINQ's Resize Method, which performs tasks for you.

In this chapter, we introduce the .NET Framework's List collection—class which offers greater capabilities than traditional arrays. A List is similar to an array but provides additional functionality, such as dynamic resizing—a List can increase its size when items are added to it. We use the List to implement several data simulations similar to those in the preceding chapter. List and the .NET Framework's other collections are reusable, reliable, powerful and have carefully tested.

Large amounts of data that need to persist beyond an execution are typically stored in a database—an organized collection of data (A database management system (DBMS) provides mechanisms for storing, organizing, retrieving, and modifying a database). A language called SQL (Structured Query Language)—is the international standard used to query (i.e., to request information that satisfies given criteria) and to manage data in relational databases. These organize data to maintain relationships between pieces of data in stored tables—each table is key to eliminate duplicate. For years, accessing a relational database passed SQL queries to the database management system, then processed the returned results. This chapter introduces C# LINQ (Language Integrated Query) capabilities. LINQ allows you to write query expressions, similar to SQL queries, that retrieve information from a variety of data sources, not just databases. In this chapter, we use LINQ to Objects to manipulate objects in memory, such as arrays and Lists.

![](bbox=[0.146, 0.943, 0.238, 0.963])