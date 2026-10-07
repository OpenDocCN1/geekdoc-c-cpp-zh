# CHAPTER 14: Introducing the Xcode Debug

![](bbox=[0.135, 0.055, 0.864, 0.403])

Figure 14–8. The Debugger view with execution stopped on 25 lines

The debugger views some additional windows. Let's go over the different parts of the debugger shown in Figure 14–8.

+   1. **Debugger controls:** (circled in red) The debugger controls can pause, continue, step over, step into, and step out of statements in the program. The stepping controls are used most often. The first button on the left is used to show or hide the Debug area. In Figure 14–8 the the area is is.
2.. **:** The variables window displays the variables in scope. Clicking on the little triangle to the left of a variable will expand it.
3. **Output Window:** The output window will show very useful information in the event of a crash or exception. Also, NSLog output goes here.
4. **Stack Trace:** The stack shows the object stack as well as the threads currently active in the program. The stack is a hierarchical view of what methods are being called. For example, main calls UIApplication and UIApplication calls the AppDelegate delegate. These method call "stack" until they finally return, hence the name.

# Working with the Debugger Controls

As mentioned previously, once the debugger starts, the view changes. What appears are the debugging controls (item B in Figure 14–8). The controls are straightforward and are explained in Table 14–1.