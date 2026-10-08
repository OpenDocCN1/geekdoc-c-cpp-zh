+   2. Run the application by pressing F5. Enter a skip iterations value, select one of the radio buttons, and click the Generate button.
3. Change the location of the continue statement so that it occurs after the power of two has been calculated.
4. Run the application again by pressing F5. Enter a skip iterations value, select one of the radio buttons, and click the Generate button. Because the continue statement occurs after, it has no effect on the iterations.

# The return Statement

You have already seen the return statement in Hour 3, “Understanding Classes and Objects the C# Way,” when you learned about methods and properties. The return statement causes control to return to the caller of the member containing the return statement. A return statement can be used with an expression, as you saw from the examples in Hour 3, in which case it can be used only in a class member that has a non-void return type. A return statement can also be used without an expression, in which case it can be used only in a class member that has a void return type, including constructors and finalizers.

# Summary

In this hour, you moved away from foundational aspects and learned how to control your application by making decisions, repeating sections of code under certain conditions, and unconditionally jumping to different sections of code.

Knowing how to control the flow of an application is the most central concept in programming. These seemingly simple flow control statements provide the most power and flexibility the C# language has to make an application behave in ways that solve a specific problem.

# Q&A

**Q. What are the types of control flow statements available in C#?**

**A. C# provides three types of control flow statements:**

+   - Selection statements, which enable for the selection of a single statement to be executed based on the value of an expression from a number of possible statements.