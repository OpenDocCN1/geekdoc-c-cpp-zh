# Perspective

Now that you have finished this chapter, you should be able to code and call methods. You should also be able to code event handlers for any event of a form or control. With those skills, you are well on your way toward developing programs at a professional level.

# Terms

|  |  |
|---|---|---|
| method | pass arguments by name |
| access modifier | expression-bodied method |
| return statement | pass arguments by value |
| parameter | pass arguments by reference |
| parameter list | discard |
| signature of a method | tuple |
| overload a method | member |
| call a method | unnamed tuple |
| argument | named tuple |
| argument list | deconstructing a tuple |
| pass arguments by position | event wiring |
| optional parameter | delegate |

# Exercise 6-1   Enhance the Future Value application

In this exercise, you’ll enhance the Future Value application that you created in chapter 5 so it works like the one in figure 6-12.

**Use refactoring to create the CalculateFutureValue() method**

+   1. Open the application that’s in the C:\C#\Chapter 06\Future Value directory.
+   2. Use refactoring as shown in figure 6-5 to refactor the calculation in the event handler and create a new method named CalculateFutureValue().
+   3. Test the application to make sure the new method works correctly.

**Add the CalculateFutureValue() method without using refactoring**

+   4. Press Ctrl+Z twice to return the code to the way it was before you refactored it.
+   5. Add a method named CalculateFutureValue() that works like the one in figure 6-12. To do that, type the start of the new method including its opening brace, and its closing brace will be added automatically. Then, move the related code from the btnCalculate_Click() method to the block within the new method and modify it where necessary.
+   6. Modify the code in the btnCalculate_Click() method so it calls the CalculateFutureValue() method. As you enter the call to the method, note how the IntelliSense feature helps you enter the arguments.
+   7. Test the application to make sure this new method works correctly.