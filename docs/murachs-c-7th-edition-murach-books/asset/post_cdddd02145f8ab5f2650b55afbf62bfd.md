
## Perspective

Now that you have finished this chapter, you should be able to code and call methods. You should also be able to code event handlers for any event of a form or control. With those skills, you are well on your way toward developing programs at a professional level.

## Terms

|  |  |
|---|---|
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

## Exercise 6-1 Enhance the Future Value application

In this exercise, you’ll enhance the Future Value application that you created in chapter 5 so it works like the one in figure 6-12.

### Use refactoring to create the CalculateFutureValue() method
- 1. Open the application that’s in the C:\C#\Chapter 06\Future Value directory.
- 2. Use refactoring as shown in figure 6-5 to refactor the calculation in the event handler and create a new method named CalculateFutureValue().
- 3. Test the application to make sure the new method works correctly.

### Add the CalculateFutureValue() method without using refactoring
- 4. Press Ctrl+Z twice to return the code to the way it was before you refactored it.
- 5. Add a method named CalculateFutureValue() that works like the one in figure 6-12. To do that, type the start of the new method including its opening brace, and its closing brace will be added automatically. Then, move the related code from the btnCalculate_Click() method to the block within the new method and modify it where necessary.
- 6. Modify the code in the btnCalculate_Click() method so it calls the CalculateFutureValue() method. As you enter the call to the method, note how the IntelliSense feature helps you enter the arguments.
- 7. Test the application to make sure this new method works correctly.

## Add an event handler for the TextChanged events
- 8. In the Form Designer, select the first text box. Then, click the Events button in the Properties window to display the Events list for that text box. Review the events that are available.
- 9. Enter “ClearFutureValue” to the right of the TextChanged event and press Enter. When you do, the Code Editor will open and an event handler named ClearFutureValue will be created. Enter a statement that clears the Future Value text box as shown in figure 6-12.
- 10. Open the frmFutureValue.Designer.cs file for the form, expand the Windows Form Designer generated code region if necessary, and locate the statements that set the properties of the Monthly Investment text box. At the end of those statements, you’ll find a statement that wires the TextChanged event of this control to the ClearFutureValue() event handler.
- 11. Return to the Form Designer and select the Yearly Interest Rate text box. Drop down the list for the TextChanged event of this control, and notice that the ClearFutureValue event handler is included in this list. Select this event handler to wire the event to it. Repeat this process for the Number of Years text box.
- 12. Run the application and perform a calculation. Then, change the value that’s displayed in one of the text boxes. When you do that, the value that’s displayed for the Future Value text box should be cleared.
- 13. When you’re sure the enhancements are working correctly, close the application.

## Exercise 6-2 Experiment with events

This exercise will give you a chance to experiment with events and the event wiring for the Future Value application.

### Generate and delete an event handler
- 1. Open the Future Value application that you enhanced in exercise 6-1.
- 2. In the Form Designer, double-click on the form to generate the handler for the default event of a form, which is the Load event. Then, delete this event handler in the Code Editor, and try to build and run the application. This should lead to one build error.
- 3. Double-click on the error message, which will lead you to the event wiring for the event handler. Then, delete that wiring, and try to build and run the application again. This time, it should work.

### Use a form event and two more control events
- 4. In the Form Designer, select the form, click the Events button in the Properties window, and double-click on the DoubleClick event to generate its event handler. Next, write the code for this handler so it sets the Text property for all four text boxes to an empty string. Then, test the application to make sure this works. (Be sure to double-click on the form, not on a control or the form’s title bar.)
- 5. In the Form Designer, select the Monthly Investment text box. Next, select the MouseHover event, read its description, drop down its list, and select the ClearFutureValue() event handler so it will be executed whenever the user lets the mouse hover over this text box. Then, test the application to make sure this works.
- 6. In the Form Designer, select the Yearly Interest Rate text box, and double-click on the DoubleClick event to generate its event handler. Next, write the code for this handler so it sets the value in the Yearly Interest Rate text box to 12. Then, test this enhancement.
- 7. Use your own imagination to work with other events. When you’re through experimenting with events, close the application.

## Exercise 6-3 Enhance the Invoice Total application

In this exercise, you’ll enhance the Invoice Total application from chapter 5 so it uses a method with a tuple.

### Add a GetInvoiceAmounts() method
- 1. Open the application that’s in the C:\C#\Chapter 06\InvoiceTotal directory.
- 2. Add a method named GetInvoiceAmounts() that accepts the customer type and subtotal and returns the discount percent. You can do that manually or using refactoring.
- 3. Test the application to make sure the new method works correctly.

### Add a tuple
- 4. Modify the declaration for the GetInvoiceAmounts() method so it returns a tuple that includes the discount percent and the discount amount. Then, modify the code for this method so it works with the tuple.
- 5. Modify the calling code so it deconstructs the tuple that’s returned by the GetInvoiceAmounts() method. When you do that, you can delete the statements that declare and calculate the discount amount and invoice total.
- 6. Test the application to make sure the changes work.

## How to handle exceptions and validate data

In the last two chapters, you learned how to code a Future Value application that calculates the future value of a series of monthly payments. However, if the user enters data that can’t be handled by this application, an exception will occur and the application will crash. In this chapter, you’ll learn how to prevent that from happening by handling any exceptions that occur and by validating data to prevent exceptions.

- An introduction to exceptions ............................................ 196
- How exceptions work........................................................... 196
- How to display a dialog box ................................................... 198
- How to use structured exception handling........................... 200
- How to catch an exception..................................................... 200
- How to use the properties and methods of an exception................... 202
- How to catch specific types of exceptions................................... 204
- How to throw an exception..................................................... 206
- The Future Value application with exception handling ................... 208
- How to validate data........................................................... 210
- How to validate a single entry ............................................... 210
- How to code generic methods for data validation........................... 212
- How to validate multiple entries.............................................. 214
- The Future Value application with data validation........... 216
- The dialog boxes............................................................... 216
- The code......................................................................... 216
- Perspective ................................................................... 220
