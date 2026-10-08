# Reviewing Your Console Application 21

The program starts executing right after the statement containing Main and ends at the closed brace {} following Main(). (I explain the meaning of these statements in due course. More than that, I cannot say for now.)

The list of directives can come immediately before or immediately after the phrase namespace Program (. The order doesn't matter. You can apply using to lots of things in .NET. I explain the whole business of namespaces and using the object-oriented programming chapters in Book II.

![](bbox=[0.128, 0.226, 0.203, 0.283])

Book I
Chapter 1

First C# Application
Creating Your

# Comments

The template already has lots of lines, and I have added several other lines, such as the following (boldface):

```
// This is your program starts.
public static void Main(string[] args)
```

![](bbox=[0.135, 0.448, 0.203, 0.513])

C# ignores the first line in this example. This line is known as a comment.

Any line that begins with // // // is free text, and C# ignores it. Consider // and // to be equivalent for now.

Why include if the computer ignores them? Because comments explain C# statements. A program, even in C#, isn't easy to understand. Remember that a programming language is a compromise between computers and what humans understand. These comments are useful when you write the code, and they're especially helpful to the poor say — possibly you — who tries to re-create your logic year later. Comments make the job much easier.

![](bbox=[0.135, 0.628, 0.203, 0.693])

# The meat of the program

The real core of this program is embedded within the block of code marked
with Main(), like this:

```
// Prompt user to enter a name.
Console.WriteLine("Enter your name
```