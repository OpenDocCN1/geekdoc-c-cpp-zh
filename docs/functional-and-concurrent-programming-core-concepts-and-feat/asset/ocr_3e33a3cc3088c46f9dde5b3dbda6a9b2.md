# 1.3  From Functions to Functional Programming Concepts

Many of the programming concepts and features presented in the first part of this book follow quite naturally from the decision to organize code in terms of functions. First, the idea of functions that do not modify anything can be generalized to the broader notion of *immutable data*, which cannot be modified at all. Functional programming often involves applying functions to compute immutable values from other immutable values, such as when you apply √ to (immutable) number 4 to produce (immutable) number 2. Function `firstString2` given earlier can modify its input list because Java lists are (often) mutable. By contrast, Scala lists are immutable:

```
```scala
def firstString(strings: List[String]): String = ...
```
```

It does not matter how the function is implemented: You can know for sure that it does not modify the given list of strings, because the list simply cannot be modified. (Immutability is discussed in Chapters 3 and 4.)

What about performance? Won’t immutable lists force the costly creation of new lists as the state of a system evolves? Not necessarily. New immutable lists can often share data with existing lists and be created with minimal copying and memory allocation. Other data structures also have this property. They are typically defined in terms of *algebraic data types*, and functional programming languages often implement a notion of *pattern matching* to better support programming with such types. (Algebraic data types and pattern matching are the topic of Chapter 5.)

Another important observation about immutability is that code that produces an immutable value from another immutable value gains nothing from being repeated multiple times. This is critical, because it means that, in a purely functional approach to programming, loops are useless. Indeed, if the body of a loop does not change the state of a system in any way, executing it ten times instead of one (or even zero times) makes no difference. If you are used to imperative programming, you may find the idea of programming without loops quite mystifying. It is actually a frequent mistake, when first learning functional programming, to try to use a functional computation as the body of a loop. Instead, functional programming makes heavy use of *recursion*, not only as a replacement for loops, but also as a natural way to process algebraic data types that are recursive in nature, like trees. (Recursion is discussed at length in Chapters 6 to 8, and used throughout the book.)

From the centrality of functions in functional programming emerges another idea, that of functions as values. In functional programming languages, functions are regular values, which can be stored in collections, or used as arguments and return values of other functions. This gives rise to the concepts of *higher-order functions* and of *function literals*, often expressed in terms of *lambda expressions*. (Higher-order functions, function literals, and lambda expressions are the topics of Chapters 9 and 10.)

Since, in functional programming, functions can be used as values, you can sometimes replace an explicit argument with a function that can compute this argument, thus