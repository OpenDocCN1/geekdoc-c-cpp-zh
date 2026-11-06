When you run this application by clicking Run, you should see an output value of 2100.

# Watching the variables

To watch the variables in your application, follow these steps:

+   1. Compile this application using a debug build (Build > Select Target > Debug) rather than a release build.
+   2. Set a breakpoint at the `int i = 10;` line in `main()`.
+   3. Click Debug/Continue.
+   4. When the debugger stops at the breakpoint, choose Debug > Debugging Windows > Watches.

You see the Watches window, as shown in Figure 3-6. Notice that the Watches window automatically includes i and mirror. If you click the + next to mirror, you can drill down to see NumberOfPieces.

**FIGURE 3-6:** The Watches window shows the value of variables and objects.

![](bbox=[0.259, 0.459, 0.576, 0.608])

Notice that the values in i and NumberOfPieces are random because the code hasn’t assigned values to them yet. The values you see will differ from those shown in Figure 3-6. This is the reason you never want to use a variable until after you assign a value to it. In this case, the variables are shown in red because C++ has just created them.

![](bbox=[0.174, 0.743, 0.239, 0.811])

**REMEMBER**

Objects such as mirror contain not only variables but also other objects. When an object contains a child object, the child object will also have a plus sign next to it. To see the contents of this child object, simply click the plus sign next to it. You can keep drilling down until you reach the end of the object list.