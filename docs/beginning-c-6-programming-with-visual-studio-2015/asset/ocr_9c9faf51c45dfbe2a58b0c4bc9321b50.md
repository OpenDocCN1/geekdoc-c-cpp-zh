# Diagnostics Output Versus Tracepoints

Now that you have seen two methods of outputting essentially the same information, consider the pros and cons of each. First, tracepoints have no equivalent to the Trace commands; that is, there is no way to output information in a release build using tracepoints. This is because tracepoints are not included in your application. Tracepoints are handled by Visual Studio and, as such, do not exist in the compiled version of your application. You will see tracepoints doing something only when your application is running in the Visual Studio debugger.

The chief disadvantage of tracepoints is also their major advantage, which is that they are stored in Visual Studio. This makes them quick and easy to add to your applications as you need them, but also makes them all too easy to delete. Deleting a tracepoint is as simple as clicking on the red diamond indicating its position, which can be annoying if you are outputting a complicated string of information.

One bonus of tracepoints, though, is the additional information that can be easily added, such as $FUNCTION which adds the current function name to the output message. Although this information is available to code written using Debug and Trace commands, it is trickier to obtain. In summary, use these two methods of outputting debug information as follows:

+   - **Diagnostics output** — Use when debug output is something you always want to output from an application, particularly when the string you want to output is complex, involving several variables or a lot of information. In addition, Trace commands are often the only option should you want output during execution of an application built in release mode.
+   - **Tracepoints** — Use these when debugging an application to quickly output important information that may help you resolve semantic errors.

# Debugging in Break Mode

The rest of the debugging techniques described in this chapter work in break mode. This mode can be entered in several ways, all of which result in the program pausing in some way.

# Entering Break Mode

The simplest way to enter break mode is to click the Pause button in the IDE while an application is running. This Pause button is found on the Debug toolbar, which you should add to the toolbars that appear by default in Visual Studio. To do this, right-click in the toolbar area and select Debug. Figure 7-6 shows the Debug toolbar that appears.

![](bbox=[0.75, 0.95, 0.95, 0.99])

The first three buttons on the toolbar allow manual control of breaking. In Figure 7-6, these are grayed out because they don't work with a program that isn't currently executing. The following sections describe the rest of the buttons as needed.

![](bbox=[0.75, 0.95, 0.95, 0.99])

When an application is running, the toolbar changes to look like Figure 7-7.