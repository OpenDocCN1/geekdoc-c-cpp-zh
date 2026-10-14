
- Using inheritance
- The System.Object class revisited
- Calling base-class constructors
- Assigning classes
- Declaring new methods
- Declaring virtual methods
- Declaring override methods
- Understanding protected access
- Understanding extension methods
- Summary
- Quick reference
- Chapter 13 Creating interfaces and defining abstract classes
- Understanding interfaces
- Defining an interface
- Implementing an interface
- Referencing a class through its interface
- Working with multiple interfaces
- Explicitly implementing an interface
- Interface restrictions
- Defining and using interfaces
- Abstract classes
- Abstract methods
- Sealed classes
- Sealed methods
- Implementing and using an abstract class
- Summary
- Quick reference
- Chapter 14 Using garbage collection and resource management
- The life and times of an object
- Writing destructors
- Why use the garbage collector?
- How does the garbage collector work?
- Recommendations

## Resource management

## Disposal methods

## Exception-safe disposal

## The using statement and the IDisposable interface

## Calling the Dispose method from a destructor

## Implementing exception-safe disposal

## Summary

## Quick reference

## PART III DEFINING EXTENSIBLE TYPES WITH C#

## Chapter 15 Implementing properties to access fields

## Implementing encapsulation by using methods

## What are properties?

## Using properties

## Read-only properties

## Write-only properties

## Property accessibility

## Understanding the property restrictions

## Declaring interface properties

## Replacing methods with properties

## Generating automatic properties

## Initializing objects by using properties

## Summary

## Quick reference

## Chapter 16 Using indexers

## What is an indexer?

## An example that doesn’t use indexers

## The same example using indexers

## Understanding indexer accessors

## Comparing indexers and arrays

## Indexers in interfaces

## Using indexers in a Windows application

## Summary

## Quick reference

## Chapter 17 Introducing generics

## The problem with the *object* type

## The generics solution

## Generics vs. generalized classes

## Generics and constraints

## Creating a generic class

## The theory of binary trees

## Building a binary tree class by using generics

## Creating a generic method

## Defining a generic method to build a binary tree

## Variance and generic interfaces

## Covariant interfaces

## Contravariant interfaces

## Summary

## Quick reference

## Chapter 18 Using collections

## What are collection classes?

## The *List<T>* collection class

## The *LinkedList<T>* collection class

## The *Queue<T>* collection class

## The *Stack<T>* collection class

## The *Dictionary<TKey, TValue>* collection class

## The *SortedList<TKey, TValue>* collection class

## The *HashSet<T>* collection class

## Using collection initializers

## The *Find* methods, predicates, and lambda expressions

## The forms of lambda expressions

## Comparing arrays and collections

## Using collection classes to play cards

## Summary

## Quick reference

## Chapter 19 Enumerating collections

## Enumerating the elements in a collection

## Manually implementing an enumerator

## Implementing the IEnumerable interface

## Implementing an enumerator by using an iterator

## A simple iterator

## Defining an enumerator for the Tree<TItem> class by using an iterator

## Summary

## Quick reference

## Chapter 20 Decoupling application logic and handling events

## Understanding delegates

## Examples of delegates in the .NET Framework class library

## The automated factory scenario

## Implementing the factory control system without using delegates

## Implementing the factory by using a delegate

## Declaring and using delegates

## Lambda expressions and delegates

## Creating a method adapter

## Enabling notifications by using events

## Declaring an event

## Subscribing to an event

## Unsubscribing from an event

## Raising an event

## Understanding user interface events

## Using events

## Summary

## Quick reference

## Chapter 21 Querying in-memory data by using query expressions

## What is LINQ?

## Using LINQ in a C# application

## Selecting data

## Filtering data

## Ordering, grouping, and aggregating data

## Joining data

## Using query operators

## Querying data in Tree<TItem> objects

## LINQ and deferred evaluation

## Summary

## Quick reference

## Chapter 22 Operator overloading

## Understanding operators

## Operator constraints

## Overloaded operators

## Creating symmetric operators

## Understanding compound assignment evaluation

## Declaring increment and decrement operators

## Comparing operators in structures and classes

## Defining operator pairs

## Implementing operators

## Understanding conversion operators

## Providing built-in conversions

## Implementing user-defined conversion operators

## Creating symmetric operators, revisited

## Writing conversion operators

## Summary

## Quick reference

## PART IV BUILDING UNIVERSAL WINDOWS PLATFORM APPLICATIONS WITH C#

## Chapter 23 Improving throughput by using tasks

## Why perform multitasking by using parallel processing?

## The rise of the multicore processor

## Implementing multitasking by using the Microsoft .NET Framework

## Tasks, threads, and the ThreadPool

## Creating, running, and controlling tasks

## Using the Task class to implement parallelism

## Abstracting tasks by using the Parallel class

## When not to use the Parallel class

## Canceling tasks and handling exceptions

## The mechanics of cooperative cancellation

## Using continuations with canceled and faulted tasks

## Summary

## Quick reference

## Chapter 24 Improving response time by performing asynchronous operations

## Implementing asynchronous methods

## Defining asynchronous methods: The problem

## Defining asynchronous methods: The solution

## Defining asynchronous methods that return values

## Asynchronous method gotchas

## Asynchronous methods and the Windows Runtime APIs

## Using PLINQ to parallelize declarative data access

## Using PLINQ to improve performance while iterating through a collection

## Canceling a PLINQ query

## Synchronizing concurrent access to data

## Locking data

## Synchronization primitives for coordinating tasks

## Canceling synchronization

## The concurrent collection classes

## Using a concurrent collection and a lock to implement thread-safe data access

## Summary

## Quick reference

## Chapter 25 Implementing the user interface for a Universal Windows Platform app

## Features of a Universal Windows Platform app

## Using the Blank App template to build a Universal Windows Platform app

## Implementing a scalable user interface

## Applying styles to a UI

## Summary

## Quick reference

## Chapter 26 Displaying and searching for data in a Universal Windows Platform app

## Implementing the Model-View-ViewModel pattern

## Displaying data by using data binding

## Modifying data by using data binding

## Using data binding with a ComboBox control

## Creating a ViewModel

## Adding commands to a ViewModel

## Searching for data using Cortana

## Providing a vocal response to voice commands

## Summary

## Quick reference

## Chapter 27 Accessing a remote database from a Universal Windows Platform app

## Retrieving data from a database

## Creating an entity model

## Creating and using a REST web service

## Inserting, updating, and deleting data through a REST web service

## Reporting errors and updating the UI

## Summary

## Quick reference

## Index

## Introduction

Microsoft Visual C# is a powerful but simple language aimed primarily at developers who create applications built on the Microsoft .NET Framework. Visual C# inherits many of the best features of C++ and Microsoft Visual Basic, but few of the inconsistencies and anachronisms, which results in a cleaner and more logical language. C# 1.0 made its public debut in 2001. With the advent of C# 2.0 with Visual Studio 2005, several important new features were added to the language, including generics, iterators, and anonymous methods. C# 3.0, which was released with Visual Studio 2008, added extension methods, lambda expressions, and most famously of all, the Language-Integrated Query facility, or LINQ. C# 4.0, was released in 2010 and provided further enhancements that improved its interoperability with other languages and technologies. These features included support for named and optional arguments and the *dynamic* type, which indicates that the language runtime should implement late binding for an object. An important addition to the .NET Framework, and released concurrently with C# 4.0, were the classes and types that constitute the Task Parallel Library (TPL). Using the TPL, you can build highly scalable applications that can take full advantage of multicore processors. C# 5.0 added native support for asynchronous task-based processing through the *async* method modifier and the *await* operator. C# 6.0 is an incremental upgrade with features that are intended to make life simpler for developers. These features include items such as string interpolation (you need never use *String.Format* again!), enhancements to the ways in which properties are implemented, expression-bodied methods, and others. They are all described in this book.

Another important event for Microsoft is the launch of Windows 10. This new version of Windows combines the best (and most loved) aspects of previous versions of the operating system and supports highly interactive applications that can share data and collaborate as well as connect to services running in the cloud. The key notion in Windows 10 is Universal Windows Platform (UWP) apps—applications designed to run on any Windows 10 device, whether a fully fledged desktop system, a laptop, a tablet, a smartphone, or even an IoT (Internet of Things) device with limited resources. Once you have mastered the core features of C#, gaining the skills to build applications that can run on all these platforms is important.

Voice activation is another feature that has come to the fore, and Windows 10 includes Cortana, your personal voice-activated digital assistant. You can integrate your own apps with Cortana to allow them to participate in data searches and other operations. Despite the complexity normally associated with natural-language speech analysis, it is surprisingly easy to enable your apps to respond to Cortana’s requests, and I cover this in Chapter 26. Additionally, the
