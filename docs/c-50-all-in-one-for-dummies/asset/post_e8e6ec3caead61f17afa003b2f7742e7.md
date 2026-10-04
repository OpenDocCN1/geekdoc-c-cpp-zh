
shows Hello, followed by the name entered, and displays Press Enter to terminate . . . . Pressing Enter closes the window.

You can also execute the program from the DOS command line. To do so, open a Command Prompt window and enter the following:

```
CD \C#Programs\Program1\bin\Debug
```

Now enter Program1 to execute the program. The output should be identical to what you saw earlier. You can also navigate to the \C#Programs\Program1\bin\Debug folder in Windows Explorer and then double-click the Program1.exe file.

To open a Command Prompt window, try choosing Tools→Command Prompt. If that command isn’t available on your Visual Studio Tools menu, choose Start→All Programs→Microsoft Visual Studio 2008→Visual Studio Tools→Visual Studio 2008 Command Prompt.

## Reviewing Your Console Application

In the following sections, you take this first C# console app apart one section at a time to understand how it works.

## The program framework

The basic framework for all console applications starts as the following:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Program1
{
    public class Program
    {
        // This is where your program starts.
        public static void Main(string[] args)
        {
            // Your code goes here.
        }
    }
}
```

The program starts executing right after the statement containing Main() and ends at the closed curly brace (}) following Main(). (I explain the meaning of these statements in due course. More than that, I cannot say for now.)

The list of using directives can come immediately before or immediately after the phrase namespace Program1 {. The order doesn’t matter. You can apply using to lots of things in .NET. I explain the whole business of namespaces and using in the object-oriented programming chapters in Book II.

## Comments

The template already has lots of lines, and I've added several other lines, such as the following (in boldface):

```
// This is where your program starts.
public static void Main(string[] args)
```

C# ignores the first line in this example. This line is known as a comment.

Any line that begins with // or /// is free text, and C# ignores it. Consider // and /// to be equivalent for now.

Why include lines if the computer ignores them? Because comments explain your C# statements. A program, even in C#, isn't easy to understand. Remember that a programming language is a compromise between what computers understand and what humans understand. These comments are useful while you write the code, and they're especially helpful to the poor sap — possibly you — who tries to re-create your logic a year later. Comments make the job much easier.

Comment early and often.

## The meat of the program

The real core of this program is embedded within the block of code marked with Main(), like this:

```
// Prompt user to enter a name.
Console.WriteLine("Enter your name, please:");

// Now read the name entered.
string name = Console.ReadLine();

// Greet the user with the name that was entered.
Console.WriteLine("Hello, " + name);
```

Save a ton of routine typing with the C# Code Snippets feature. Snippets are great for common statements like Console.WriteLine. Press Ctrl+K,X to see a pop-up menu of snippets. (You may need to press Tab once or twice to open the Visual C# folder or other folders on that menu.) Scroll down the menu to cw and press Enter. Visual Studio inserts the body of a Console.WriteLine() statement with the insertion point between the parentheses, ready to go. When you have a few of the shortcuts, such as cw, for, and if, memorized, use the even quicker technique: Type cw and press Tab twice. (Also try selecting some lines of code, pressing Ctrl+K, and then pressing

![](img/6df7bb88e9302e98442acc219cfbd7fc_46_0.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_46_1.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_46_2.png)

Ctrl+S. Choose something like if. An if statement surrounds the selected code lines.)

The program begins executing with the first C# statement: Console.WriteLine. This command writes the character string Enter your name, please: to the console.

The next statement reads in the user’s answer and stores it in a variable (a kind of workbox) named name. (See Chapter 2 of this minibook for more on these storage locations.) The last line combines the string Hello, with the user’s name and outputs the result to the console.

The final three lines cause the computer to wait for the user to press Enter before proceeding. These lines ensure that the user has time to read the output before the program continues:

```
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
```

This step can be important, depending on how you execute the program and depending on the environment. In particular, running your console app inside Visual Studio, or from Windows Explorer, makes the preceding lines necessary — otherwise, the console window closes so fast you can’t read the output. If you open a console window and run the program from there, the window stays open regardless.

## Introducing the Toolbox Trick

The key part of the program you create in the preceding section consists of the final two lines of code:

```
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
```

The easiest way to re-create those key lines in each future console application you write is described in the following sections.

## Saving code in the Toolbox

The first step is to save those lines in a handy location for future use: the Toolbox window. With your Program1 console application open in Visual Studio, follow these steps:

- 1. In the Main() method of class Program, select the lines you want to save — in this case, the three lines mentioned previously.
- 2. Make sure the Toolbox window is open on the left. (If it isn’t, open it by choosing View→Toolbox.)
- 3. Drag the selected lines into the General tab of the Toolbox window and drop them. (Or copy the lines and paste them into the Toolbox.)

The Toolbox stores the lines there for you in perpetuity. Figure 1-4 shows the lines placed in the Toolbox.

![](img/6df7bb88e9302e98442acc219cfbd7fc_48_0.png)

Figure 1-4: Setting up
the Toolbox
with handy
text for
future use.

## Reusing code from the Toolbox

Now that you have saved text in the Toolbox, you can reuse it in all console applications you write. Here’s how to use it:

- 1. In Visual Studio, create a new console application as described in the “Creating the source program,” earlier in this chapter.
- 2. Click in the editor at the spot where you’d like to insert some
text. (Wait, the OCR text continues below)

The most fundamental of all concepts in programming is that of the variable. A C# variable is like a small box in which you can store things, particularly numbers, for later use. (The term variable is borrowed from the world of mathematics.)

Unfortunately for programmers, C# places several limitations on variables — limitations that mathematicians don't have to consider. This chapter takes you through the steps for declaring, initializing, and using variables. It also introduces several of the most basic data types in C#.

## Chapter 2: Living with Variability — Declaring Value-Type Variables

## In This Chapter

- Visiting the train station — the C# variable as storage locker
- Using integers — you can count on it
- Handling fractional values — what's half a duck?
- Declaring other types of variables — dates, characters, strings
- Handling numeric constants — Π in the sky
- Changing types — cast doesn't mean toss
- Letting the compiler figure out the type — var

## Declaring a Variable

When the mathematician says, “n is equal to 1,” that means the term n is equivalent to 1 in some ethereal way. The mathematician is free to introduce variables in a willy-nilly fashion. For example, the mathematician may say this:

```
x = y^2 + 2y + y
if k = y + 1 then
x = k^2
```

Programmers must define variables in a particular way that's more demanding than the mathematician's looser style. For example, a C# programmer may write the following bit of code:

```
int n;
n = 1;
```
