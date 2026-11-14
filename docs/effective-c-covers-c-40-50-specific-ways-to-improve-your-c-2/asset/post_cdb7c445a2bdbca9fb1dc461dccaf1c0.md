
- Item 27: Prefer Making Your Types Serializable 157
- Item 28: Create Large-Grain Internet Service APIs 166
- Item 29: Support Generic Covariance and Contravariance 171

## Chapter 4 Working with the Framework 179

- Item 30: Prefer Overrides to Event Handlers 179
- Item 31: Implement Ordering Relations with IComparable<T> and IComparer<T> 183
- Item 32: Avoid ICloneable 190
- Item 33: Use the new Modifier Only to React to Base Class Updates 194
- Item 34: Avoid Overloading Methods Defined in Base Classes 198
- Item 35: Learn How PLINQ Implements Parallel Algorithms 203
- Item 36: Understand How to Use PLINQ for I/O Bound Operations 215
- Item 37: Construct Parallel Algorithms with Exceptions in Mind 220

## Chapter 5 Dynamic Programming in C# 227

- Item 38: Understand the Pros and Cons of Dynamic 227
- Item 39: Use Dynamic to Leverage the Runtime Type of Generic Type Parameters 236
- Item 40: Use Dynamic for Parameters That Receive Anonymous Types 239
- Item 41: Use DynamicObject or IDynamicMetaObjectProvider for Data-Driven Dynamic Types 243
- Item 42: Understand How to Make Use of the Expression API 254
- Item 43: Use Expressions to Transform Late Binding into Early Binding 261
- Item 44: Minimize Dynamic Objects in Public APIs 267

## Chapter 6 Miscellaneous 275

- Item 45: Minimize Boxing and Unboxing 275
- Item 46: Create Complete Application-Specific Exception Classes 279
- Item 47: Prefer the Strong Exception Guarantee 284
- Item 48: Prefer Safe Code 294
- Item 49: Prefer CLS-Compliant Assemblies 298
- Item 50: Prefer Smaller, Cohesive Assemblies 303

## Index 309

## Introduction

The C# community is very different in 2010 than it was in 2004 when the first edition of *Effective C#* was published. There are many more developers using C#. A large contingent of the C# community is now seeing C# as their first professional language. They aren't approaching C# with a set of ingrained habits formed using a different language. The community has a much broader range of experience. New graduates all the way to professionals with decades of experience are using C#.

The C# language has also grown in the last five years. The language I covered in the first edition did not have generics, lambda expressions, LINQ, and many of the other features we now take for granted. C# 4.0 adds new features that change our toolset again. And yet, even with all the growth in the C# language, much of the original advice is as relevant now as it was in the C# 1.x days. Viewed in hindsight, the changes to the C# language appear to be natural and obvious extensions to what we had in C# 1.0. New editions give us new ways of solving problems, without invalidating previous idioms.

I organized this second edition of *Effective C#* by taking into account both the changes in the language and the changes in the C# community. *Effective C#* does not take you on a historical journey through the changes in the language. Rather, I provide advice on how to use the current C# language. The items that have been removed from this second edition are those that aren't as relevant in today's C# language. The new items cover the new language and framework features, and those practices the community has learned from building several versions of software products using C#. Overall, these items are a set of recommendations that will help you use C# 4.0 more effectively as a professional developer.

This book covers C# 4.0, but it is not an exhaustive treatment of the new language features. Like all books in the Effective Software Development Series, this book offers practical advice on how to use these features to solve problems you're likely to encounter every day. Many of the items are equally valid in the 3.0 and even earlier versions of the language.

### Who Should Read This Book?

Effective C# was written for professional developers who use C# as part of their daily toolset. It assumes you are familiar with the C# syntax and the language’s features. The second edition assumes you understand the new syntax added in C# 4.0, as well the syntax available in the previous versions of the language. This book does not include tutorial instruction on language features. Instead, this book discusses how you can integrate all the features of the current version of the C# language into your everyday development.

In addition to language features, I assume you have some knowledge of the Common Language Runtime (CLR) and Just-In-Time (JIT) compiler.

### About the Content

There are language constructs you’ll use every day in almost every C# program you write. Chapter 1, “C# Language Idioms,” covers those language idioms you’ll use so often they should feel like well-worn tools in your hands. These are the building blocks of every type you create and every algorithm you implement.

Working in a managed environment doesn’t mean the environment absolves you of all your responsibilities. You still must work with the environment to create correct programs that satisfy the stated performance requirements. It’s not just about performance testing and performance tuning. Chapter 2, “.NET Resource Management,” teaches you the design idioms that enable you to work with the environment to achieve those goals before detailed optimization begins.

In many ways, we write programs to satisfy human readers rather than a compiler. All the compiler cares about is that a program is valid. Our colleagues want to understand our intent as well. Chapter 3, “Expressing Designs in C#,” discusses how the C# language can be applied to express your design intent. There are always several ways to solve a problem. The recommendations in Chapter 3 will help you choose the solution that best expresses your design intent to fellow developers.

C# is a small language, supported by a rich framework library. Chapter 4, “Working with the Framework,” covers the portions of the .NET Base Class Library (BCL) that support your core algorithms. In addition, I cover some of the common idioms that you'll encounter throughout the framework. Multicore processors are a way of life, and the Parallel Task Library provides a step forward in creating multithreaded programs on the .NET platform. I cover the most common practices for the Parallel Task Library in this chapter.

Chapter 5, “Dynamic Programming in C#,” discusses how to use C# as a dynamic language. C# is a strongly typed, statically typed language. However, more and more programs contain both dynamic and static typing. C# provides ways for you to leverage dynamic programming idioms without losing the benefits of static typing throughout your entire program. You’ll learn how to use dynamic features and how to avoid having dynamic types leak through your entire program.

Chapter 6, “Miscellaneous,” covers those items that somehow continue to defy classification. These are the techniques you’ll use often to create robust programs that are easier to maintain and extend.

## Code Conventions

We no longer look at code in monochrome, and we shouldn’t in books either. While it’s impossible to replicate the experience of using a modern IDE on paper, I’ve tried to provide a better experience reading the code in the book. Where the medium supports it, the code samples use the standard Visual Studio IDE colors for all code elements. Where I am pointing to particular changes in samples, those changes are highlighted.

Showing code in a book still requires making some compromises for space and clarity. I’ve tried to distill the samples down to illustrate the particular point of the sample. Often that means eliding other portions of a class or a method. Sometimes that will include eliding error recovery code for space. Public methods should validate their parameters and other inputs, but that code is usually elided for space. Similar space considerations remove validation of method calls, and try/finally clauses that would often be included in complicated algorithms.

I also usually assume most developers can find the appropriate namespace when samples use one of the common namespaces. You can safely assume that every sample implicitly includes the following using statements:

```
using System;
using System.Collections.Generic;
```
