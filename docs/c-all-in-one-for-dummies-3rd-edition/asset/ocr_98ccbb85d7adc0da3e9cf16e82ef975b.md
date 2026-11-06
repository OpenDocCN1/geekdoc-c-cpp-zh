# # Chapter 3: Stopping and Inspecting Your Code

+   **In This Chapter**
+   - Setting, enabling, and disabling breakpoints
+   - Temporarily setting or disabling a breakpoint
+   - Inspecting a variable
+   - Watching all the local variables
+   - Watching any variable

Sometimes, things break. But what we're talking about here is the code. Now this is one of those instances when a word or phrase has lots of different meanings. Programmers talk about _breaking the code._ This phrase usually means one of two things. It may mean that the programmer made a mistake and the code no longer _works._ But in this chapter, we're using a different definition for the term. When you're debugging an application, you can have the application run until it gets to a certain line in the code. The debugger then stops at that line, and you can look at the values of variables, inspect the code, or even change the variables. When the application stops, that's called _breaking._ The reason it stops on that particular line is because you put a _breakpoint_ on that line.

In this chapter, we talk about setting and manipulating breakpoints in your code (if nothing else in your code is broken) and inspecting and modifying various aspects of your code, such as variables, after your code stops at a breakpoint.

![](bbox=[0.12, 0.67, 0.18, 0.73])

In the examples in this chapter, we use the debugger supplied with the Code::Blocks IDE. If you use a different product, the debugger will probably work about the same but not precisely the same. For example, everything we show you how to do here you can do in Microsoft Visual C++. The keystrokes and mouse clicks may be different, but the features are present. Make sure you check the vendor documentation for precise details on using your debugger.

![](bbox=[0.12, 0.79, 0.18, 0.85])

To work through the examples in this chapter, make sure that you compile with debug information turned on. (In Code::Blocks, you can compile with debug information by choosing Debug in the Build Target field of the Compiler toolbar. If you can't see the Compiler toolbar, choose View; Toolbars; Compiler to place a check mark next to the Compiler entry.)