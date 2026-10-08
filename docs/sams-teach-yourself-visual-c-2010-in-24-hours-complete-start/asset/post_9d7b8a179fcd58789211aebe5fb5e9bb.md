
A statement lambda cannot contain a goto, break, or continue statement whose target is outside the scope of the lambda itself. Similarly, normal scoping rules prevent a branch into a nested lambda from an outer lambda.

## Predefined Delegates

Although lambdas are an integral component of LINQ, they can be used anywhere you can use a delegate. As a result, the .NET Framework provides many predefined delegates that can be used to represent a method that can be passed as a parameter without requiring you to first declare an explicit delegate type.

Because delegates that return a Boolean value are common, the .NET Framework defines a Predicate<T> delegate, which is used by many of the methods in the Array and List<> classes.

Although Predicate<T> defines a delegate that always returns a Boolean value, the Func family of delegates encapsulate a method that has the specified return value and 0 to 16 input parameters.

Because Predicate<T> and the Func delegates all have a return type, the family of Action delegates represent a method that has a void return type. Just like the Func delegates, the Action delegates also accept from 0 to 16 input parameters.

## Deferred Execution

Unlike many traditional data query techniques, a LINQ query is not evaluated until you actually iterate over it. One advantage of this approach, called **lazy evaluation**, is that it enables the data in the original collection to change between when the query is executed and the data identified by the query is retrieved. Ultimately, this means you will always have the most up-to-date data.

Even though LINQ prefers to use lazy evaluation, any queries that use any of the aggregation functions must first iterate over all the elements. These functions, such as Count, Max, Average, and First, return a single value and execute without using an explicit foreach statement.

## Deferred Execution and Chained Queries

Another advantage of deferred execution is that it enables queries to be efficiently chained together. Because query objects represent queries, not the results of those queries, they can easily be chained together or reused without causing potentially expensive data fetching operations.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_303_0.png)

You can also force immediate evaluation, sometimes called **greedy evaluation**, by placing the foreach statement immediately after the query expression or by calling the ToList or ToArray methods. You can also use either ToList or ToArray to cache the data in a single collection object.

## Summary

LINQ takes the best ideas from functional languages such as Haskell and other research languages and brings them together to introduce a way to query data in a consistent manner, no matter what the original data source might be, using a simple declarative or method-based syntax. By enabling queries to be written in a source-agnostic fashion, LINQ enables access to a wide variety of data sources, including databases, XML files, and in-memory collections.

Using syntax similar to that used by SQL queries, the declarative syntax of LINQ enables a query to be a first-class language construct, just like arithmetic operations and control flow statements. LINQ is actually implemented as a set of extension methods on the IEnumerable<T> interface, which accept lambdas as a parameter. Lambdas, in the form of expression or statement lambdas, are a compact way to write anonymous delegates.

When you first start with LINQ, you don't need to use lambdas extensively, but as you become more familiar with them, you will find that they are extremely powerful.

## Q&A

- **Q. What is LINQ?**
  - **A.** LINQ is a set of technologies that integrates query capabilities directly into the C# language and eliminates the language mismatch commonly found between working with data and working with objects by providing the same query language for each supported data source.
- **Q. What is a lambda expression?**
  - **A.** A lambda expression represents a compact and concise way to write an anonymous delegate and can be used anywhere a traditional delegate can be used.

## Workshop

### Quiz

- 1. Is there a difference between the declarative and method syntax for LINQ?
- 2. When is a LINQ query executed?
- 3. What is the underlying delegate type for lambda expressions?

### Answers

- 1. The choice of using the declarative syntax or the method syntax is entirely personal and depends on which one you find easier to read. No matter which one you choose, the result of executing the query will be the same.
- 2. By default, LINQ utilizes deferred execution of queries. This means that the query is not actually executed until the result is iterated over using a foreach statement.
- 3. Lambda expressions are inherently typeless, so they have no underlying type; however, they can be implicitly converted to any compatible delegate type.

### Exercises

- 1. Modify the Search_Click method of the MainWindow class of the AddressBook project so that it sets this.DataContext to the result of a query over the contacts collection. This query should select any elements of the collection where the FirstName or LastName property contains the value in this.searchCriterias.Text.
- 2. Modify the Search_Click method so that it will also query using the selected category if the searchCategory check box is checked.

# PART III

# Working with Data

- HOUR 13: Using Files and Streams 289
- HOUR 14: Working with XML 311
- HOUR 15: Working with Databases 329

## HOUR 13

# Using Files and Streams

**What You'll Learn in This Hour:**

- Files and Directories
- Reading and Writing Data
- Binary Files
- Buffered Streams
- Text Files

In Hour 9, “Working with Arrays and Collections,” and Hour 12, “Understanding Query Expressions,” you learned how applications could work with data stored in collections and how to query and manipulate that data. Although these are common activities, many applications need to store or retrieve data from files on a disk.

The .NET Framework treats files as a stream of data. A **stream** is a sequential flow of packets of data, represented as bytes. Data streams have an underlying storage medium, typically called a **backing store**, which provides a source for the stream. Fortunately, the .NET Framework makes working with files and directories easier by the File, Directory, and Path classes provided by the .NET Framework.

The System.IO namespace contains all the classes you need to work with both buffered and unbuffered streams. Buffered streams enable the operating system to create its own internal buffer that it uses to read and write data in whatever increments are most efficient.

In this hour, you learn how to work with files, using the File, Directory, and Path classes to explore and manage the file system and for reading and writing files. You also learn how you can use the Stream class, or any of its derived classes, to perform more complex read and write operations.

## Files and Directories

You can think of a file as a sequence of bytes having a well-defined name and a persistent backing store. Files are manipulated through directory paths, disk storage, and file and directory names. The .NET Framework provides several classes in the System.IO namespace that make working with files easy.

## Working with Paths

A path is a string that provides the location of a file or directory, and can contain either absolute or relative location information. An **absolute path** fully specifies a location, whereas a **relative path** specifies a partial location. When using relative paths, the current location is the starting point when locating the file specified.

> **Current Location**
>
> Every process has a process-wide "current location," which is usually, but not always, the location where the process executable was loaded.

The Path class provides static methods that perform operations on path strings in a cross-platform manner. Although most Path class members don't interact with the file system, they do validate that the specified path string contains valid characters. Table 13.1 shows the commonly used methods.

**TABLE 13.1** Commonly Used Methods of the Path Class

| Method | Description |
| :--- | :--- |
| ChangeExtension | Changes the extension |
| Combine | Combines strings into a path |
| GetDirectoryName | Gets the directory name of the specified path |
| GetExtension | Gets the extension of the specified path |
| GetFileName | Gets the filename and extension of the specified path |
| GetFileNameWithoutExtension | Gets the filename without the extension of the specified path |
| GetPathRoot | Gets the root directory of the specified path |
| GetRandomFileName | Gets a random name |
