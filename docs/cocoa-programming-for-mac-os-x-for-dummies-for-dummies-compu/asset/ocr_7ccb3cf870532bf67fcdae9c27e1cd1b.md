This time you're intentionally leaving the trailing semicolon (a common mistake that even pros make). Choose Build:Build and Go to see what happens. The result is that the application doesn't run as expected, and an error overlay appears beneath the code in question, as shown in Figure 3-12. A circle with a white X also appears in the gutter to the left of the code where the error occurred.

The error shows exactly where the problem is. In this case, the error is syntax error before } token. Just before } token is where the semi-colon should be. Fix the code and save it.

The point behind this demonstration is to show that you may encounter different kinds of errors when programming with Xcode. Some errors, like this one, occur during build and debug process, and Xcode shows where you occur. Other bugs are trickier to track down, such as the earlier example, because the application is otherwise functional. For those, it never hurts to use the built-in debugger to solve the problem.

![](bbox=[0.235, 0.458, 0.843, 0.775])

# Removing breakpoints

Now that you're finished debugging your project, you may want to remove the breakpoints that you added. In Xcode, check the Fusebox.m file and look for the breakpoints on the left side of the code editor. Control+click a