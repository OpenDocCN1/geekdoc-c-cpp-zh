
- **Loaded Libraries:** Contains a list of all of the libraries loaded to run your application. It’s important to know which libraries your application uses when you deploy (load) it on other machines. In many cases, you may not even know that C++ requires certain libraries to run your application, so this window is exceptionally useful.
- **Targets and Files:** Provides a detailed view of how the loaded libraries are used in your application. You won’t normally need to view this information unless you’re performing low-level programming tasks.
- **FPU Status:** Displays the register information for the Floating-Point Unit (FPU) in your processor. At one time, the FPU was a separate chip, but now it appears as part of your main processor. The FPU is exceptionally adept at performing real number (versus integer) math. You won’t normally need to view this information unless you’re performing low-level programming tasks.
- **Signal Handling:** Shows how Code::Blocks handles signals between the hardware and your application, such as an arithmetic exception or a segmentation fault. You won’t normally need to view this information unless you’re performing low-level programming tasks.

## Debugging with Different Tools

You can use several tools for debugging your code. However, which compiler you use also dictates which debugging tools you can use. For example, Microsoft Visual C++ has a really good debugger. But getting it to debug an application compiled with Dev-C++, for example, is difficult because different compilers use different forms of debugging and symbol information. The type used by the various breeds of gcc compilers is different from the type used by Microsoft Visual C++.

### Standard debuggers

Here’s a quick rundown of some of the debuggers that are available:

- **Visual C++:** This debugger works similarly to the Code::Blocks debugger. It’s primarily for debugging applications that were built by using Visual C++. However, if you are brave and need to debug something for which you have no code or symbol information, its support for assembly-code debugging is good.
- **gdb:** This is the standard debugger that ships with MinGW and Cygwin. It’s a command-line tool, but we don’t recommend using it as such. Instead, we suggest using the Insight debugger with it so that you can use a graphical *front end*. This makes life a lot easier. But if you insist on using the command-line version, you can learn about it by typing **gdb** at the command prompt and then typing **help**.
- **Dev-C++ 5:** Starting with Version 5, Dev-C++ has an integrated debugger that works similarly to the Insight debugger. You may want to give this a try. (If you're using a version of Dev-C++ prior to 5.0, you have to use the Insight debugger.)

## Debugging a Code::Blocks Application with Command Line Arguments

A command line argument is something you type along with the command for an application at the command prompt. For example, when you type the Dir (directory listing command) at the command prompt, you can include additional information such as *.DOC, which will list all files with a .DOC extension. (If you use Dir *.DOC instead, you also see any files with a .DOCX extension.) The full command Dir *.DOC consists of a command (Dir) and a command line argument (*.DOC). The addition of command line arguments allows you to extend the functionality of an application and make it do more. In order to test such an application, you need to be able to specify command line arguments as part of the debugger environment.

Code::Blocks, like most other capable IDEs, provides the means for specifying command line arguments. The “Setting the command line parameters in Code::Blocks” sidebar in Book I, Chapter 5 provides you with the basics of setting command line arguments. However, a number of readers of previous editions of this book wanted more information. With this in mind, I wrote a more detailed description of how command line arguments work as part of the post “Debugging a Code::Blocks Application with Command Line Arguments” for this book on my blog at http://blog.johnmuellerbooks.com/2011/11/01/debugging-a-codeblocks-application-with-command-line-arguments.aspx. Please be sure to check out this blog post if you want additional information about precisely what is going on.

## Chapter 3: Stopping and Inspecting Your Code

**In This Chapter**
- Setting, enabling, and disabling breakpoints
- Temporarily setting or disabling a breakpoint
- Inspecting a variable
- Watching all the local variables
- Watching any variable

Sometimes, things break. But what we're talking about here is the code. Now this is one of those instances when a word or phrase has lots of different meanings. Programmers talk about _breaking the code._ This phrase usually means one of two things. It may mean that the programmer made a mistake and the code no longer _works._ But in this chapter, we're using a different definition for the term. When you're debugging an application, you can have the application run until it gets to a certain line in the code. The debugger then stops at that line, and you can look at the values of variables, inspect the code, or even change the variables. When the application stops, that's called _breaking._ The reason it stops on that particular line is because you put a _breakpoint_ on that line.

In this chapter, we talk about setting and manipulating breakpoints in your code (if nothing else in your code is broken) and inspecting and modifying various aspects of your code, such as variables, after your code stops at a breakpoint.

![](img/6ba99460b0feb3585671a4612ff5fabb_416_0.png)

In the examples in this chapter, we use the debugger supplied with the Code::Blocks IDE. If you use a different product, the debugger will probably work about the same but not precisely the same. For example, everything we show you how to do here you can do in Microsoft Visual C++. The keystrokes and mouse clicks may be different, but the features are present. Make sure you check the vendor documentation for precise details on using your debugger.

![](img/6ba99460b0feb3585671a4612ff5fabb_416_1.png)

To work through the examples in this chapter, make sure that you compile with debug information turned on. (In Code::Blocks, you can compile with debug information by choosing Debug in the Build Target field of the Compiler toolbar. If you can't see the Compiler toolbar, choose View; Toolbars; Compiler to place a check mark next to the Compiler entry.)

When you are developing software, you should always have debug information on. That way, you’re always ready to debug your code and fix things. Only when you’re ready to release the product formally should you recompile it without debug information. (We do recommend doing a full test of the software again without debug information, just to make sure that it still functions correctly.)

### Setting and Disabling Breakpoints

*A breakpoint is a place in your code where you tell the debugger to stop.*

In the sections that follow, we talk about breakpoints. Please use the `Breakpoints` sample code, shown in Listing 3-1, for these sections. Remember what you’re supposed to do? Make sure that you compile it with debug information on.

**Listing 3-1: Using an Application for Breakpoints and Inspections**

```cpp
#include <iostream>

using namespace std;

class BrokenMirror
{
private:
    int NumberOfPieces;

public:
    int GetNumberOfPieces();
    void SetNumberOfPieces(int newamount);
    BrokenMirror() : NumberOfPieces(100) {}
};

int BrokenMirror::GetNumberOfPieces()
{
    return NumberOfPieces;
}

void BrokenMirror::SetNumberOfPieces(int newamount)
{
    newamount = newamount * 20;
    NumberOfPieces = newamount;
}

int main()
{
    BrokenMirror mirror;
    mirror.SetNumberOfPieces(10);
    cout << mirror.GetNumberOfPieces() << endl;

    return 0;
}
```
