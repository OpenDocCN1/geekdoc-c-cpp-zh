
## Exercise 5-2 Develop the Future Value application

In this exercise, you'll develop and test the Future Value application that was presented in this chapter. You'll also step through its loop.

## Develop the form, write the code, and test the application

- 1. Open the New Project dialog box by selecting the File→Project command. Then, enter “FutureValue” for the name of the project, enter “C:\Project2010Chapter05” for the location, and click the OK button.
- 2. Add the controls to the form and set the properties of the form and its controls as shown in figure 5-10. Then, generate the event handlers for the Click event of the two buttons, and add the code for these handlers. If necessary, you can refer to the code in figure 5-11, but try to write the code without doing.
- 3. Test the application by entering valid data in each of the three text boxes. To start, enter simple values like 100 for the monthly investment, 12 for the yearly interest rate (which is 1% per month), and 1 for the number of years. The result should be $120.93.
- 4. After you're sure that the application works for valid data, test it with nonnumeric entries and with large values like 100 for the interest rate and 1000 for the number of years. In either case, the application will end with a runtime error, which you'll learn how to prevent in chapter 7. Then, stop the debugging.

## Set breakpoints and step through the loop

- 5. In the Code Editor, set a breakpoint at the statement by clicking in the Margin Indicator Bar to the left of the statement as shown in figure 5-9. A red dot will indicate that you have set the breakpoint.
- 6. Run the application, and enter 100 as the monthly investment, 12 as the yearly interest rate, and 1 as the number of years. Then, click the Calculate button. This will cause the program to enter break mode. If the Locals window isn't displayed, use the Debug menu to display it.
- 7. Press F11 repeatedly to step through the loop. As you do, the Locals window will display the values for i, futureValue, monthlyInvestment, and InterestRate. Then, you'll be able to see exactly how these values change as the loop is executed.
- 8. Press F11 to continue stepping through the application or press F5 to run the application until another breakpoint is reached.
- 9. Remove the old breakpoint and set a new breakpoint on the statement within the loop. Then, run the application and note that the new breakpoint causes the application to enter break mode for each iteration of the loop. As a result, you can press F5 to move from one iteration to the next.
- 10. When you're through experimenting, remove the breakpoint and close the project.

## How to code methods and event handlers

So far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

- **How to code and call methods ................................................ 162**
- How to code methods ....................................................................... 162
- How to call methods ........................................................................ 164
- How to use optional parameters ........................................................ 166
- How to use named arguments ................................................................ 166
- How to use refactoring to create a new method and its calling statement - 168
- When and how to pass arguments by reference and by value ................. 170
- **How to work with events and delegates ........................................ 172**
- How to generate an event handler for any event ................................ 172
- How event wiring works ....................................................................... 174
- How to handle multiple events with one event handler ...................... 176
- **Another version of the Future Value application ........................ 178**
- The event handlers and the CalculateFutureValue method ............... 178
- Some of the generated code ................................................................. 180
- **Perspective ..................................................................................... 182**

## How to code and call methods

So far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

### How to code methods

In so far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

### How to call methods

In so far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

### How to use optional parameters

In so far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

### How to use named arguments

In so far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

### How to use refactoring to create a new method and its calling statement

In so far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

### When and how to pass arguments by reference and by value

In so far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

### How to work with events and delegates

In so far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

### Another version of the Future Value application

In so far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

### Perspective

In so far, you've been writing methods called event handlers for the Click events of button controls. Now, in this chapter, you'll learn how to code methods that can be called from other methods. That will help you logically divide the code for an application into manageable parts. You'll learn how to code event handlers for events other than the Click event.

(Note: The OCR text for pages 181-182 appears to be a repetitive or corrupted fragment of the previous section. I have processed the clear structural elements provided.)
