
## 2.3.1. Explanation

If you run the program with `dotnet run`, then we get the same output as before.

```
Hello Joe!!!
```

## 2.3.2. Grammar

These two programs, "hello-world-2" and "hello-universe-2", have some differences, but they are insignificant in this case. In fact, the hello-world-2 program and the following code would have been compiled to more or less the same IL code:

```csharp
class Program {
    static void Main() {
        const string name = "Joe";
        var greeting = $"Hello {name}!!!";
        Console.WriteLine(greeting);
    }
}
```

Besides the fact that this version is using a temporary local variable `greeting`, the main difference is the location of the `const` definition `name`. In this version, the "scope" of the name `name` is limited to the body of the `Main()` method.

On the other hand, in the example code of this lesson `hello-universe-2`, the name's scope is the entire class. If we had another method, say, after `Main()`, then we could have used the `const name` within that method as well. We will discuss the scopes in more detail throughout this book.

### Summary

In this lesson, we learned the important concepts of variables and constants in C#. A variable holds a value in a C# program, which can change during the execution of the program. The value of a constant, on the other hand, does not change.

Variables, and constants, are associated with types. The type of a variable/constant is determined at build time, and it remains the same while the program is running. C# is a statically typed programming language.

### 2.4. Exercises

- 1. Write a program which keeps your name as a constant variable, stores a greeting in your native language (e.g., corresponding to "hello" in English) as another variable, and prints out a text that combines the greeting with your name as a single string. You can refer to the sample code of "hello-world-2", but do not copy and paste.

## Author's Note

## Who is This Book for?

Learning programming is hard. Learning a new language is hard. It can be frustrating. It can be discouraging. ...

This book is written primarily for the beginners who have dabbled with other programming languages like Python or Javascript, or even the languages like Java or C++, but could not make a real progress in programming.

C# is a much more interesting language. Much more fun to learn and use. The language designs of other modern languages like Swift and Kotlin are largely influenced by the modern C# (although they may not admit it). As stated, C# is probably one of the most fun languages to learn programming with, and to use, as your primary programming language.

This book is also written with more experienced programmers in mind who want to learn the *modern C# programming language*, and its new programming styles.

There are a lot of resources, but none really explains what the modern C# really is. Its root from C, C++, and Java is mostly irrelevant at this point. If you want to really use C#, then you really have to learn it as a *new language*. Learning just the C# syntax will not do. You'll need deeper understanding.

Hope you can find some interesting ideas in this book that will help you become a better C# programmer, and a better programmer in general.

We mentioned the IDEs a few times in this lesson. As stated, however, we do not use the IDEs in any of the examples in this book. In fact, the author does NOT recommend the use of *any* IDEs for the beginning programmers.

It may sound counterintuitive. But, the times are changing. It used to be the case that an IDE was a must when you started learning programming, or new programming languages.

The modern “trend” is that the simplicity is preferred. If you are just starting, or if you are a “hobby programmer”, then you do not need the “full power” of the IDEs like Visual Studio or Rider.

As a matter of fact, you will benefit more, learn better, by using the simple command line tools like `dotnet` instead of the IDEs, which can obscure certain essential aspects of programming (in the name of the “convenience”).

You will still need to use a good “programmer’s editor”. Notepad will not do. 😏 There are many choices like Sublime Text, Atom, etc. The author primarily uses `VSCode` [https://code.visualstudio.com/].

## Tip - How to Use This Book

*The Art of C# - Basics: Introduction to Programming in Modern C#* is written for a broad audience, from the absolute beginners to the more seasoned developers with experience in other programming languages who want to get a quick taste of C#.

This first part, *First Steps*, in particular, is primarily for the beginners who are new to programming, or at least new to programming in C#. Depending on your experience, you may find some of the lessons too easy or trivial. Or, too slow or boring. You can skip, or skim through, certain portions of the book.

Each lesson starts with a sample code, in the "code reading" or "code review" sections. Some lessons include multiple such sections. Learning a new programming language is not much different from learning a foreign language. We primarily emphasize the "reading comprehension" skills in this book.

Through gradual exposure to many sample programs, from simple to more complex, you will become familiar with the C# language, and its idiomatic styles, without even touching a keyboard.

Here’s a good way to use this book.

*For each lesson, read the sample program(s) first.* If you understand what the overall program does, and know what each part of the program means syntactically, then you can skip the lesson. Go to the next lesson.

If you are new to programming, however, some parts of the book might be rather difficult, or even more or less incomprehensible. That is perfectly all right. Read the book through. (Or, at least the parts I and II.)

Then, come back to the beginning, and read the book again. This time, test your knowledge by reading the sample code first. Do you understand what the program does? If so, then you can skip this particular lesson and go to the next one. If not, that’s all right. Read the lesson again.

You do not have to understand *everything* in the lesson. As indicated, the book covers a lot of "advanced concepts", which may be considered TMI (too much information) for the beginning programmers. *Your goal should be understanding the sample code. Everything else is a bonus.*

Eventually, you will end up feeling like you understand all the sample code in this book (regardless of where you started in the first place). Then you will have learned everything you need to learn from this book.

A time to learn a new programming language. (Just kidding. 💪)

## Lesson 3. Hello World 3

### 3.1. Agenda - Arrays, Command Line Arguments, `if` Statements

We will learn how to read the "command line arguments" in a C# program in this lesson, while continuing with the "hello world" theme.

![image](img/25af69ec45b3c0b589a8dccd0c2a88be_59_0.png)

### 3.2. Code Reading - Hello World 3

Here's another variation of the Hello World program.

```
hello-world-3/Program.cs
```

```csharp
var name = "you";
if (args.Length > 0) {
    name = string.Join(" ", args);
}

Console.WriteLine($"Hello {name}!");
```

### 3.2.1. Explanation

This third Hello-World program takes an (optional) argument (although it is not obvious from reading the program). If you run the program in the usual way,

```
dotnet run
```

It produces the following output:

```
Hello you!
```

If you run the program as follows, with an extra text "Joe" in the command line,

```
dotnet run Joe
```

It produces a different output:

```
Hello Joe!
```

### 3.2.2. Grammar

This example program introduces a few new constructs of the C# programming language.

The keywords `if` and `else` are used for conditional statements. `if` is followed by a Boolean expression (i.e., an expression that evaluates to a `bool` value, `true` or `false`) and a "block" (from the opening bracket `{` to the closing bracket `}`).

If the Boolean or logical expression (`args.Length > 0` in this case) evaluates to `true`, then the statements in this `if` block are executed, if any. An optional `else` can be used. The statements in the `else` block are executed if the value of the Boolean
