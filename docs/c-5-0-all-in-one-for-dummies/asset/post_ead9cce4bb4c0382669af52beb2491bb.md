
![](img/80ff26f06fc9ab951e1cd4257b867366_559_0.png)

Figure 2-12: Teeny little outline marks.

## Exploring the auxiliary windows

A number of windows affect text input and output in order to solve certain problems. As a group, they don't really have a name, so I call them auxiliary windows. I cover four of them here.

### The Output window

I use the Output window regularly for two things:
- *Build logging:* Every time you build, the Output window tracks all of the linking and compiling that goes on under the hood and shows any errors that might come up.

By default, the Output window shows when you build. You can set it to not show, after choosing General→Projects and Solutions in the Visual Studio Options dialog box.

Errors listed in the Output window can be used to navigate the code. The buttons in the Output box assist with getting around the code based on the messages in the window.

![](img/80ff26f06fc9ab951e1cd4257b867366_559_1.png)

- *Debug statements:* The second use of the Output window is Standard Out (for all you C++ people). If you use a `Debug.Write` statement in your code, the Output window is where it will go. Additionally, if you use `Console.Write`, but are running a Windows Forms application, for instance, the text will go to the Output window.

### The Immediate window

This window does exactly what one would expect it to do — it does something immediately. In debug mode, you can use the Immediate window to send commands to the program as it is running, to change the state, or evaluate operations. Try this to see what I mean:

![](img/80ff26f06fc9ab951e1cd4257b867366_560_0.png)

1. **Open a Windows Forms project.**
   The one in the sample code for this chapter on this book's companion website is fine — you just need a default project template.

2. **Put a breakpoint on `InitializeComponent()` by clicking in the grey bar running down the side of Code View.**
   A red dot appears.

3. **Debug the program.**
   The program should stop on the `load` method.

4. **Open the Immediate window.**
   You should be able to do this in the Debug window or by pressing Ctrl+D, I.

5. **Type ?this.**
   See the IntelliSense menu?

6. **After the dot, type WindowPosition.**
   The question mark in Step 5 means Print. This command prints the window position to the screen.
   The response should be `windowDefaultLocation`.

That's what the Immediate window is for. You can do more than print values, too. You can change variable values and modify the execution of your program. It is a powerful part of your debugging toolbox.

### The Breakpoints window

Wait! Don't change anything in Visual Studio after trying the last example. Press Ctrl+D, B. The Breakpoints window appears, and the breakpoint you just added will be in it (see Figure 2-13).

![](img/80ff26f06fc9ab951e1cd4257b867366_561_0.png)

Figure 2-13:
The Breakpoints window, which isn't called the Bookmark window.

What's cool here is that you can right-click any breakpoint and completely alter the properties of that breakpoint. Try it — the important options are described in this list:

- *Location*: Specifies the location of the line of code that should host the breakpoint. This is convenient if you have filters set and you find you need to shift a line back.
- *Condition*: You can teach the breakpoint to stop at this line only if a certain variable is a specific value.
- *Hit Count*: Stop here only after the xth time it is hit.
- *Filter*: It's similar to Condition, except that you can use system values such as `MachineName`, `ProcessName`, `ProcessId`, `ThreadName`, and `ThreadId`. It's useful for multiprocessor development, among other things.
- *WhenHit*: You can do more than just stop on a breakpoint — instead, you can do something like print a value to the Output window, or even run a test script.

### The Task List window

While coding, have you ever wanted to tell the developer working after you that something still needs to be done? Maybe you make a comment, maybe you call it `// TODO:`.

Well, if you do that, it appears in a task in the Task List. Isn’t that just cool? Clicking the task in the Task List takes you to the line where the task was set, so you don’t have to search for it.

## Using the Tools of the Trade

There are always a few things in any overview chapter that just don’t fit in any category. In this one, there are a double handful of tools that I want to at least mention.

### The Tools menu

I am sure you are shocked to find that the Tools menu is a great place to find tools that don’t fit anywhere else, including the following:

- **Attach to Process:** For debugging, this tool enables you to connect to another running program on a machine and debug your code in that service.
- **Connect to Database:** See the “Server Explorer” section, earlier in this chapter.
- **Connect to Server:** Discussed in the “Server Explorer” section.
- **Code Snippets Manager:** I chat about snippets in Chapter 3 of this minibook.
- **Choose Toolbox Items:** This tool helps you manage the items in the Toolbox. You can add or remove a variety of components including .NET, WPF, COM, and Silverlight.
- **Add-in Manager:** Manages Visual Studio Add-ins. Add, remove, enable, and disable.
- **Macros:** You can group these commands or instructions as a single command to accomplish a task automatically. They’re generally used to automate repetitive actions. Macros are covered in Chapter 4.
- **Create GUID:** Funny that this is here. This tool literally creates a Globally Unique ID (GUID), one of those 25 character codes that are supposed to be unique over the next 2,500 years or something. Make a new one and sell it on eBay.
- **Dotfuscator Community Edition:** This is a free code obfuscator for .NET.
- **WCF Service Configuration Manager:** Graphic interface for the WCF config files. Services are covered in Book VII.
- **External Tools:** This tool enables you to add separate .EXE files to the Tools menu, such as Notepad, NUnit, or other tools, that add functionality to Visual Studio.

before it is performed and lets you select or deselect any of the items that would be renamed.

- **Extract Method:** Perhaps you've written a block of code and then thought "oh boy, I am going to need this over there." If so, Extract Method is for you. It will take a highlighted block of code, move it to a method, extract all the variables, make them parameters, and then you'll be ready for code reuse.
- **Encapsulate Field:** In a similar vein as extracting a method, Encapsulate Field takes a private variable and makes it a public field. For instance, take a line of code like private string _theValue; highlight it in code designer and select Encapsulate Field from the Refactor menu.
- **Extract Interface:** Extract Interface takes a set of method signatures and makes an interface for you. Interfaces are vital to contract driven development.
- **Remove Parameters:** This is the safe way to get excess parameters out of methods. In all honesty, I use this refactoring tool the least.
- **Reorder Parameters:** Being able to change the order of parameters is significantly handier. Sometimes, you just need to switch the order of two parameters. If you do this, all the places where you call that method must have the parameter order changed, or they will send in the wrong stuff.

Visual Studio asks you to name the new property and create a new property based on your selections:

```
public string TheValue
{
    get { return _theValue; }
    set { _theValue = value; }
}
```

If you are working on a project that suddenly has more than one programmer (as in, they got you help!), extracting interfaces to common classes in your project decreases barriers to the new folks' entry pattern and lets you make your code easier to change in the future.

This simple tool enables you to change the parameter order and then finds all places that call the method in question and switches the parameter order sent in.
