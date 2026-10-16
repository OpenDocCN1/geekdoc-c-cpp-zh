![](bbox=[0.106, 0.064, 0.895, 0.196])

**Figure 17.37**

# # Debugging Your Code

At this point, you are ready to run and debug the application. In C#, as in pre-.NET languages, the main technique involved in debugging is simply setting breakpoints and using them to examine what is going on in your code at a certain point in its execution.

# ## Setting Breakpoints

You can set breakpoints from Visual Studio on any line of your code that is actually executed. The simplest way is to click the line in the code editor, within the shaded area near the far left of the document window (or press the F9 key when the appropriate line is selected). This sets up a breakpoint on that particular line, which pauses execution and transfers control to the debugger as soon as that line is reached in the execution process. As in previous versions of Visual Studio, a breakpoint is indicated by a red circle to the left of the line in the code editor. Visual Studio also highlights the line by displaying the text and background in a different color. Clicking the circle again removes the breakpoint.

If breaking every time at a particular line is not adequate for your particular problem, you can also set conditional breakpoints. To do this, select Debug ➔ Windows ➔ Breakpoints. This brings up a dialog that requests details about the breakpoint you want to set. Among the options available, you can do the following:

+   - Specify that execution should break only after the breakpoint has been passed a certain number of times.
+   - Specify that the breakpoint should be activated only after the line has been reached a defined number of times—for example, every twentieth time a line is executed. (This is useful when debugging large loops.)
+   - Set the breakpoints relative to a variable, rather than an instruction. In this case, the value of the variable is monitored and the breakpoints are triggered whenever the value of this variable changes. You might find, however, that using this option slows down your code considerably. Checking whether the value of a variable has changed after every instruction adds a lot of processor time.