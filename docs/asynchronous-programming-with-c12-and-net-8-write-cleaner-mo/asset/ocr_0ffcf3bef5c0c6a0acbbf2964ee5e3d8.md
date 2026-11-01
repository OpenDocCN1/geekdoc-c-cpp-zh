# Chapter 2

# Utilizing top-level statements for cleaner and more concise asynchronous code

Utilizing top-level statements in C# 9 and above allows developers to write cleaner and more concise code, especially in asynchronous scenarios. Top-level statements eliminate boilerplate code, making asynchronous programming more straightforward and easier to read. Let's explore how top-level statements can be used effectively in asynchronous code using C# 12 and .NET 8, along with code examples.

# 1. Top-Level Statements Overview:

Top-level statements were introduced in C# 9 as a way to simplify entry points and reduce ceremony in code files. They allow developers to write code without explicit namespaces, class declarations, or Main method signatures, making code files more focused on the actual logic rather than setup.

# 2. Using Top-Level Statements in Asynchronous Code:

Let's dive into an example where we'll create an asynchronous program using top-level statements to fetch data from an API and process it asynchronously.

# Example: Fetching and Processing Data Asynchronously

```
```csharp
using System;

using System.Net.Http;
```
```