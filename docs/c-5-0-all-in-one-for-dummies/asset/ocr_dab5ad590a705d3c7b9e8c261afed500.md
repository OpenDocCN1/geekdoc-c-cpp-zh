can apply using to lots of things in .NET. I explain the whole business of namespaces and using in the object-oriented programming chapters in Book II.

# Comments

The template already has lots of lines, and I've added several other lines, such as the following (in boldface):

```
```
// This is where your program starts.
public static void Main(string[] args)
```
```

![](bbox=[0.12, 0.43, 0.24, 0.56])

C# ignores the first line in this example. This line is known as a comment.

Any line that begins with // or /// is free text, and C# ignores it. Consider // and /// to be equivalent for now.

Why include lines if the computer ignores them? Because comments explain your C# statements. A program, even in C#, isn't easy to understand.

Remember that a programming language is a compromise between what computers understand and what humans understand. These comments are useful while you write the code, and they're especially helpful to the poor sap — possibly you — who tries to re-create your logic a year later.

Comments make the job much easier.

Comment early and often.

![](bbox=[0.12, 0.7, 0.24, 0.84])

# The meat of the program

The real core of this program is embedded within the block of code marked with Main(), like this:

```
```
// Prompt user to enter a name.
Console.WriteLine("Enter your name, please:");

// Now read the name entered.
string name = Console.ReadLine();

// Greet the user with the name that was entered.
Console.WriteLine("Hello, " + name);
```
```

![](bbox=[0.12, 0.9, 0.24, 1.0])

Save a ton of routine typing with the C# Code Snippets feature. Snippets are great for common statements like Console.WriteLine. Press Ctrl+K,X to see a pop-up menu of snippets. (You may need to press Tab once or twice to open the Visual C# folder or other folders on that menu.) Scroll down the menu to cw and press Enter. Visual Studio inserts the body of a Console.WriteLine() statement with the insertion point between the parentheses, ready to go. When you have a few of the shortcuts, such as cw, for, and if, memorized, use the even quicker technique: Type cw and press Tab twice. (Also try selecting some lines of code, pressing Ctrl+K, and then pressing