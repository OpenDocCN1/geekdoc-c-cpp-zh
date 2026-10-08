
# 432 Chapter 9 Introduction to LINQ and the List Collection

- deferred execution
- descending modifier of the orderby clause
- Distinct extension method for IEnumerable<T>
- dynamic resizing
- filtering a collection with LINQ
- First extension method for IEnumerable<T>
- from clause of a LINQ query
- IEnumerable<T> interface
- imperative programming
- implicit typed local variable
- Insert method of class List<T>
- interface
- let clause of a LINQ query
- LINQ (Language Integrated Query)
- LINQ provider

- LINQ to Objects
- List<T> collection class
- orderby clause of a LINQ query
- predicate
- projection
- query expression
- query using LINQ
- range variable
- Remove method of class List<T>
- RemoveAt method of class List<T>
- select clause of a LINQ query
- StartsWith method of class string
- To method of class string
- where clause of a LINQ query

# Self-Review Exercises

+ 9.1 Fill in the blanks of the following statements:
  a) Use the property of List class to find the number of elements in the List.
  b) The LINQ clause is used for filtering.
  c) _ are classes specifically designed to store groups of objects and provide methods that organize, store and retrieve objects.
  d) To add an element to the end of a List, use the _ method.
  e) To get only unique elements from LINQ query, use the _ method.

+ 9.2 State each of the following is true or false. explain why:
  a) The orderby clause in a LINQ query can sort only in ascending order.
  b) LINQ queries can be used on both arrays and collections.
  c) The Remove method of the List class removes an element at a specific index.

# Answers to Self-Review Exercises

+ 9.1 a) Count. where b) Collections. Add. c) Distinct.
9.2 a) False. The descending modifier is used to make orderby sort in descending order. b) True. c) False. Remove removes the first element equal to its argument. RemoveAt the element at a specific index.

# Exercises

+ 9.3 (Querying an Array of Invoice Objects) Use the class provided in the ex09_03-file with this examples to create an array of Invoice objects. Use the sample data shown in Fig. 9.8. Class Invoice includes four properties—PartNumber (type int), a PartDescription (type string), a Quantity of the item purchased (type int) and a Price (type decimal). Perform the following queries on the array of Invoice objects and display the results:
  a) Use LINQ to sort the Invoice objects by PartDescription.
  b) Use LINQ to sort the Invoice objects by Price.
  c) Use LINQ to select the PartDescription and Quantity and sort the results by Quantity.

d) Use LINQ to select from each Invoice PartDescription and the value of the Invoice (i.e., Quantity * Price). Name the calculated column InvoiceTotal. [Hint: Use let to store the result of Quantity * Price in a new range variable total.]

e) Using the results of the LINQ query in part (d), select the InvoiceTotals in the range $200 to $500.

| Part number | Part description | Quantity | Price |
|---|---|---|---|
| 83 | Electric sander | 7 | 57.98 |
| 24 | Power saw | 18 | 99.99 |
| 7 | Sledge hammer | 11 | 21.50 |
| 77 | Hammer | 76 | 11.99 |
| 39 | Lawn mower | 3 | 79.50 |
| 68 | Screwdriver | 106 | 6.99 |
| 56 | Jig saw | 21 | 11.00 |
| 3 | Wrench | 34 | 7.50 |

Fig. 9.8 | Sample data for Exercise 9.3.

# 9.4 (Name Connector) Write a console app that inputs 10 names from the user, converts them to upper case. The app also connects and displays the names in descending order (separated by comma). [Hint: You can use string method Join with two arguments (joining letter and the string to joined) and use string method Reverse with no arguments, in sentence.Reverse() to rearrange the names in ascending order. Use method To before calling Join.

# 9.5 (Sorting Pets by Length) Write a console app that inputs pets' names into a List<string>. Perform the following queries on the List and display your results:

+ a) Use LINQ to sort the List in ascending order on the basis of number of characters in the name.

+ b) Use LINQ to sort the List in descending order on the same basis.

+ c) Display the List count after removing duplicate names from the list.

# Classes and Objects:
A Deeper Look

# Objectives

In this chapter you'll:

- Use composition to allow a class to have references to objects of other classes as members.
- Throw an exception to indicate that an argument is out of range.
- Enable an object to refer to itself with the keyword this.
- Use static variables and methods.
- Use readonly fields.
- Take advantage of C#s memory-management features.
- Use the IDE's Class View and Object Browser windows.
- Use object initializers to create an object and initialize it in the same statement.
- Overload built-in operators to work with objects.
- Define your own types with struct.
- Use extension methods to enhance your class.

# 10.1 Introduction

+ 10.1 Introduction
10.2 Throwing Exceptions
10.2.1 Class Declaration
10.2.2 Using Time1
10.3 Controlling Access
10.4 Referring to itself with this
10.5 Overloaded Constructors
10.5.1 Using Time2
10.5.2 Using Overloaded Constructors
10.6 Parameterless Constructors
10.7 Composition
10.7.1 Class Date
10.7.2 ClassEmployee
10.8 Garbage Collection and Destructors
10.9 static Members
10.10 readonly fields
10.11 Class View
10.11.1 Class View
10.11.2 Object Initializers
10.12 Operator Overloading
10.13 Value Types
10.13.1 Creating your own types
10.13.2 Number
10.14 Extension Methods
10.15 Wrap-Up

# Summary | Self-Review Exercises | Answers to Self-Review Exercises

In this chapter, we take a deeper look at classes and objects. We show how to use static members, readonly fields, and composition. We also discuss constructors, access control, and exceptions. We demonstrate how objects can refer to themselves using the `this` keyword. We cover operator overloading, object initializers, and extension methods. Finally, we discuss how C# handles memory-management through features like garbage collection.
