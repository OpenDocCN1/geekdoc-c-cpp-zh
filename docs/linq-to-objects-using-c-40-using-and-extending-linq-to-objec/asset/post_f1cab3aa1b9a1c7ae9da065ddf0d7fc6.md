
# PREFACE

# iii

the LINQ story unfolded in real-world applications and write the first book of the second-generation—the book that isn't just reference, but has integrity that only real-world application can engrain.

The LINQ story is a lot deeper and has wider impact than most people realize at first glance of TechEd session recording or user-group presentation. The ability to store and pass code as a data structure and to control when and how that code executes provides a powerful platform for working with all matter of data sources. The few LINQ providers shipped by Microsoft are just the start, and many more are built by the community through the extension points. After mastering the LINQ syntax and understanding the operators' use (and how to avoid misuse), any developer can work more effectively and write cleaner code. This is the purpose of this book: assist the reader in beginning the journey, to introduce how to use LINQ for more real-world examples and to dive a little deeper than most books on the subject, to explore the performance benefits of one solution over another, and to deeply look how to create operators for any specific purpose.

I hope you agree after reading this book that it does offer an insight into how to use LINQ to Objects on real projects and the examples give a step further in explaining the patterns that make LINQ an integral part of day-to-day programming from this day forward.

## Who Should Read This Book

The audience for this book is primarily developers who write their applications in C# and want to understand how to employ and extend the features of LINQ to Objects. LINQ to Objects is a wide set of technology pieces that work in tandem with working with in-memory data sources easier and more powerful. This book covers the initial C# 3.0 implementation of LINQ and the updates in C# 4.0. If you are accustomed to the LINQ syntax, this book goes deeper than most LINQ reference publication and delves into areas of performance and how to write custom LINQ operators (either as sequential or using parallel algorithms to improve performance).

If you are a beginning C# developer (or new to C# 3.0 or 4.0), this book introduces the code changes and syntax so that you can quickly master working with objects and collections of objects. I've tried to strike a balance and not jump directly into examples before covering the basics. You should obviously know how to build your own custom operators before you start to write queries that are taller than 8 lines (approximately). But you will get to that in the latter chapters.

## Overview of the Book

LINQ to Objects Using C# 4.0 starts by introducing the intention and benefits LINQ offers developers in the world of writing .NET applications. Chapter 1, “Introducing LINQ,” talks to the motivation and basic concepts. This is the first and only chapter that talks about LINQ to SQL and LINQ to XML and demonstrates how multiple data sources can be used from one query syntax over another.

Chapter 2, “Introducing LINQ to Objects,” begins exploring the underlying language features that are necessary to understand how LINQ language compiles. A fast-paced, brief overview of LINQ wraps this chapter; it just touches on syntax and capabilities that are covered at length in future chapters.

Chapter 3, “Writing Basic Queries,” introduces reading and writing LINQ queries in C# and covers the basics of choosing what data to project, what format to select, and what order data from in-memory collections. For simplicity, most examples write their results out to the Console window. To capture these results in this book, they are listed in the same font and format as code-listings, but identified with an output number. By the end of this chapter, each reader should be able to read the intention behind queries and be able to write simple queries that filter, project, and order data.

Chapter 4, “Grouping and Joining Data,” covers the more advanced features of grouping data in a collection and combining multiple data sources. These relational style queries can be structured in depth and why to use grouping or joining.

Chapter 5, “Standard Query Operators,” lists the many additional standard operators that can be used in a query. LINQ has over 50 operators, and this chapter covers the operators that go beyond those covered in the previous chapters.

Chapter 6, “Working with Set Data,” explores working with set-based operators. There are multiple ways of performing set operations over in-memory collections. 

Chapter 7, “Extending LINQ to Objects,” discusses the art of building custom operators. The examples covered in this chapter demonstrate how to build any of the main types of operators and includes the common coding and error-handling patterns to employ in order to match the built-in operators Microsoft supplies.

Chapter 8, “C# 4.0 Features,” is where the additional C# 4.0 language features are introduced with particular attention to how they extend the LINQ to Objects story. This chapter demonstrates how to use the dynamic language features to make LINQ queries more fluent to read and write and how to combine LINQ with Interop in order to use other applications (for example, Microsoft Excel).

Chapter 9, “Parallel LINQ to Objects,” closely examines the motivation and art of building application code that can support multi-core processor machines. Not all queries will see a performance improvement, and this chapter discusses the expectations and likely most queries will see. This chapter concludes with an example of writing a parallel operator to demonstrate the thinking process that goes into correctly coding parallel extensions in addition to those provided.

## Conventions

There is significant code listed in this book. It is an unavoidable fact for books about programming language features that they must demonstrate those features with code samples. Every chapter has dozens of code listings. To help ease the burden, I followed some common typography conventions to make them more readable. References to classes, variables, and other entities are distinguished in a monospace font. Short code listings to be read inline with the surrounding text are also presented in a monospace font, but on their own lines, and they sometimes contain code comments (lines beginning with // characters) for clarity.

```
// With line-breaks added for clarity
var result = nums
    .Where(n => n < 5)
    .OrderBy(n => n);
```

Longer listings for examples that are too big to be inline with the text or samples I specifically wanted to provide in the sample download project are shown using a similar monospace font, but they are denoted by a listing number and a short description, as in the following example, Listing 3-2.

### Listing 3-2 Simple query using the Query Expression syntax

```csharp
List<Contact> contacts = Contact.SampleData();

var q = from c in contacts
where c.State == "WA"
    orderby c.LastName, c.FirstName
    select c;

foreach (Contact c in q)
    Console.WriteLine("{0} {1}",
        c.FirstName, c.LastName);
```

Each example should be simple and consistent.

# Output 3-1

Stewart Kagel
Chance Lard
Armando Valdes
