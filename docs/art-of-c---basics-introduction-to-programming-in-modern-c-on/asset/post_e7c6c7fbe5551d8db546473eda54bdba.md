
## 3.3. Code Reading - Hello World 3 Redux

When the program runs in this case, the runtime sets the implicit `args` variable to a three element array, "Joe", "and", and "Jill", as explained above. The program then combines these three elements into a single string using `string.Join()`, which results in "Joe and Jill". The output is therefore Hello Joe and Jill!.

What will happen if we run the program as follows: `bin/Debug/net5.0/hello-world   Joe   and   Jill`? (Note the multiple spaces between the command and the arguments as well as between the arguments.) We will leave it to the readers.

![](img/25af69ec45b3c0b589a8dccd0c2a88be_67_0.png)

The hello-world program of this section accepts arguments. The `dotnet` CLI command also accepts optional special arguments known as the "options" or "flags". In some cases, the command line tool like `dotnet` may not be able to tell which are their own arguments and which are the arguments that need to be passed to the target program.

The Unix command line tool convention uses a separator string "--" (two dashes) to delineate the two. For example, we could have invoked our program with `dotnet run---Joe` instead of `dotnet run Joe`.

### 3.3.1. Explanation

The following code, without using the top level statements, is equivalent to the previous program "hello-world-3",

```csharp
// hello-universe-3/Program.cs
class Program {
   static void Main(string[] args) {
       var name = "you";
       if (args.Length > 0) {
           name = string.Join(" ", args);
       }
       Console.WriteLine($"Hello {name}!");
   }
}
```

The behavior is exactly the same as before. If you run the program without any command line arguments, `dotnet run`, then it produces the following output:

```text
Hello you!
```

If you supply the command line arguments, for example, `dotnet run` — *Joe* and *Jill*, then it produces the following output:

```text
Hello Joe and Jill!
```

### 3.3.2. Grammar

The *top-level* *statements* are simply a "syntactic sugar". All top-level statements are effectively a part of an (implicit) `Main()` method in an (implicitly defined) `class`.

These two programs have no difference. As far as the compiler is concerned they are identical. They will (most likely) generate exactly the same IL code, to be run on the .NET runtime. They will (most likely) generate exactly the same executable for a given machine architecture.

The difference is, for us programmers, the code using top-level statements is just a bit easier to write, and easier to read. The only reason why we needed to use the placeholder Program class and the static Main() method was because that was required by the (pre-9.0) C# grammar.

> Note that the use of *class* in this particular example has little to do with the "object oriented programming". We simply could not write a C# program without using a *class* or something comparable. The top-level statements is the new addition to C#, which can help remove certain boilerplate code like this. As stated, C# 10.0 now includes a few more improvements in that direction.

Now that we can use this syntactic shortcut (since C# 9.0), this way of writing the main program is generally preferred. Most of the time, we do not even care if it is a mere syntactic sugar. We will just use them as if the top level statements are truly allowed in C# just like all the other programming languages like C/C++, Rust, Javascript, Python, Go, or Ruby. (Or, you name it. ☺)

(The only exception is really Java, among the commonly used programming languages, on which C# was originally based.)

We can also define and use any top-level static methods as if they are part of the implicitly defined class which includes the *Main()* method. As stated, however, we can use the top level statements in only one source code file in a program (that is, in a project). Furthermore, the top-level statements, including the top-level static methods, are limited to the beginning part of that source file (as of C# 9.0 and 10.0). Once you define a class or struct, etc. in a source file, we cannot use the top-level statements any more beyond that point.

Despite these limitations, the top-level statements are rather useful, as indicated before. And they are here to stay. We will use the top-level statements throughout this book.

The only time that we will need to think about the fact that these are not "true" top-level statements is when we need to deal with the command line arguments, etc. For instance, in the earlier example of hello-world-3, we used a "magic variable" `args`, which was nowhere explicitly declared in the program. The variable `args` is in fact an argument to the implicitly defined `Main()` method, as we can see from the hello-universe-3 example.

## Summary

When we run a C# console program, we can optionally pass in one or more arguments to the starting program. We learned, in this lesson, how to read those "command line arguments" in a program.

When the .NET runtime, or the operating system, starts a C# program, it calls the `Main` method of the program as an entry point. If any command line arguments are provided, then the `args` argument of the `Main` method is set to these values, as the `string[]` type. When the top-level statements are used as an entry point to a C# program, the command line arguments are available in the implicitly defined `args` variable.

When the program is called with no arguments, this `args` argument/variable is an empty string array.

The array is a builtin type in C#, and in many other programming languages, which stores an (ordered) collection of variables. The variables, or the elements, of an array are stored in the consecutive memory space. The array type is generally the most efficient collection data structure (although it may not be the most flexible one).

One of the most powerful aspects of programming is that a single program can behave differently at run time, e.g., based on the user input or other conditions. The `if` statement is used to execute different pieces of the code depending on the runtime conditions. We will learn the `if` statement in more detail later in the book.

## 3.4. Exercises

- Write a program that takes the user’s name as a command line argument and prints out a text "!Hola (user’s name)!". For example, given a user name "Juan", it needs to print out "!Hola Juan!". You can refer to the sample code of "hello-world-3" if you don’t remember how to process the command line arguments, but do not copy and paste.

## Author's Note

## Who is This Book Not for?

Learning new things, or new skills, requires patience, and perseverance. And, most of all, some level of "intellectual curiosity".

If you are only interested in getting some quick knowledge on the C# programming language, then this book may not be for you.

Learning programming can be fun. Programming can be fun. And, useful. Not just as a career choice. But as a pastime, as a hobby. Just as an endeavor to satisfy your intellectual curiosities. And, to express your "creativity". Yes, *programming is a creative process.*

As you might have noticed after a couple of lessons, this book takes a rather unique approach than the vast majority of other programming language books. *The Art of C# - Basics* is a book for reading. It is designed to be read just like novels, or short stories, are to be read. Or, more particularally, the book is written based on the "listen and repeat" paradigm commonly found in foreign language guide books.

This book is written to be *read*. It may not be such an outrageous concept that a book is for reading. But most technical books are written as "study materials". Most programming language books, in particular, follow more or less the same patterns. Grammars. Variables, for loops, if statements, and so on and on. These are not the books for "reading". You do not "read" dictionaries or legal code books.

On the other hand, ***The Art of C# - Basics: Introduction to Programming in Modern C# - Beginner to Intermediate*** is like the "short stories" books for learning foreign languages. The code samples are to be read. In fact, the entire book is written in such a way that you can just "read". You learn by reading, just like you read a story.
