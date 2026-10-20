
## Perspective

In this chapter, you learned how to use five new controls for building Windows applications. These controls are the ones you’ll use most often. If you need to use any of the controls that weren’t presented here, though, you should be able to figure out how to do that on your own. In most cases, it’s just a matter of becoming familiar with the properties, methods, and events that are available, and you can usually do that by reviewing the documentation for the class the control is based on.

In addition, you learned how to work with a project that contains two or more forms. Specifically, you learned how to work with projects that use dialog boxes. For many projects, the skills presented in this chapter are the only ones you’ll need when you’re working with the forms of an application. In chapter 12, though, you’ll learn another technique for passing data between forms.

### Terms

- combo box
- list box
- radio button
- group box
- check box
- tab order
- modal form
- modeless form

### Exercise 10-1    Create the Payment application

This exercise will guide you through the process of creating the Payment application that’s described in this chapter. To make that easier for you, you’ll start from an application that contains the Customer form.

#### Open the project and prepare the two forms

1. Open the application that’s in the `C:\C#\Chapter 10\Payment` directory. This application contains a single form named Form1.
2. Rename Form1 to frmCustomer. Make sure to change both the file name and the name that’s used in the code. If necessary, modify the `Main()` method so it displays this form when the application starts.
3. Add a second form named frmPayment to the project.

#### Design the Payment form

4. Add the controls to the Payment form and set the properties for this form and its controls as described in figures 10-15 and 10-16.
5. Use Tab Order view to set the tab order for the controls on the Payment form if necessary.

#### Add the code for the Customer form

6. Generate the event handlers for the Load event of the Customer form, for the Closing event of the form, and for the Click event of all three buttons. Then, add the global `isDataSaved` variable, and add the code for these events as shown in figure 10-17.

7. Generate event handlers for the SelectedIndexChanged event of the Customer Name combo box and the TextChanged event of the Payment Method label. Then, add the code for these event handlers so they set the `isDataSaved` variable to false. The event handler for the SelectedIndexChanged event should also clear the Payment Method label.

8. Add the `SaveData()` and `IsValidData()` methods.

9. Test the Customer form to make sure that it works properly. At this point, you should be able to display the Payment form, but it won’t work correctly since you haven’t added any code to it.

#### Add the code for the Payment form

10. Generate the event handlers for the Load event of the Payment form and for the Click event of the OK button. Then, add the code for these events as shown in figure 10-18.

11. Generate an event handler named `Billing_CheckChanged()` for the CheckChanged event of the Credit Card radio button. Then, wire this event handler to the CheckChanged event of the Bill Customer radio button, and add the code for this event handler. (If you need to refresh your memory on how to wire an event to an existing event handler, see figure 6-11 in chapter 6.)

12. Add the `EnableControls()`, `DisableControls()`, `IsValidData()`, and `SaveData()` methods.

13. Test the program to be sure that it works as described in figure 10-15. When you’re sure it does, close the project.

### Exercise 10-2 Enhance the Future Value application

This exercise will guide you through the process of adding a combo box and a list box to the Future Value application.

#### Open the Future Value application and add two controls

1. Open the application that’s in the `C:\C#\Chapter 10\FutureValue` directory.
2. Delete the Number of Years text box and replace it with a Number of Years combo box. Then, delete the Future Value text box and replace it with a Future Values list box.

#### Add the code that works with the controls

3. Generate the event handler for the Load event of the form. Then, add code that loads the numbers 1 through 20 in the Number of Years combo box, and add code that selects 3 as the default number of years.

4. Delete the code in the `IsValidData()` method that refers to the Number of Years text box since it isn’t needed anymore.

5. Modify the event handler for the Click event of the Calculate button so it gets the number of years from the combo box and adds the future value for each year to the Future Values list box. For example, if you calculate the future value for three years, the Future Value form should return a result like this:

![](img/844f608d10a44654833ea5efc8a2e7a7_363_0.png)

6. To get this to work correctly, you’ll need to use the `Clear()` method of the list box to clear the list box each time the Calculate button is clicked. In addition, you can use the modulus operator (%) to add the future value after every twelve months of the calculation. For example:

```
if (month % 12 == 0) // add the future value to the list box
```

7. Test this application to make sure it works correctly.

## 11 How to debug an application

In chapters 3 and 5, you learned how to work in break mode when a runtime error occurs, how to use the Exception Helper to get information about the error, how to use data tips to find out what value a variable or property contains, how to use a breakpoint to enter break mode before a specific statement is executed, and how to step through the statements in an application from a breakpoint. These are the basic skills that you need for debugging simple applications.

As your applications get more complicated, though, debugging gets more complicated. In fact, if you’ve done much programming, you know that debugging is often the most difficult and time-consuming phase of programming. The good news is that Visual Studio offers many other tools for testing and debugging. In this chapter, you’ll learn how to use the most useful ones, and you’ll review the tools you’ve already been introduced to.

| Section | Page |
| --- | --- |
| Basic debugging techniques | 342 |
| How to set the debugging options | 342 |
| How to work in break mode | 344 |
| How to use the Edit and Continue feature | 344 |
| How to work with data tips | 346 |
| How to use breakpoints | 348 |
| How to control the execution of an application | 350 |
| How to use the debugging windows | 352 |
| How to use the Locals window to monitor variables | 352 |
| How to use the Autos window to monitor variables | 352 |
| How to use Watch windows to monitor expressions | 354 |
| How to use the Immediate window to execute commands | 356 |
| How to use the Call Stack window to monitor called methods | 358 |
| How to use the Call Hierarchy window to navigate through your code | 360 |
| How to use the Output window to view project information | 362 |
| How to write data to the Output window | 364 |
| How to use the Visualizer dialog boxes to view strings | 366 |
| Perspective | 368 |

### Basic debugging techniques

Before you begin debugging, you can set the options that control how Visual Studio handles exceptions. Then, you can use the basic debugging skills that you learned in previous chapters to find and fix most types of exceptions.

#### How to set the debugging options

Figure 11-1 presents the dialog box and window you can use to set the options for debugging. Although you may never need to change any of these options, you should at least take the time to review them so you know what they do.

The Options dialog box lets you set General options like whether the Exception Helper is displayed when an exception occurs as shown in the next figure. It also lets you enable or disable the Edit and Continue feature, which you’ll learn more about in a moment.

The Exception Settings window lets you determine how exceptions are handled. These exceptions are grouped by categories, and you can set the options for a category or a specific exception within a category.

By default, an application will continue when most exceptions are thrown. That’s why the Break When Thrown option isn’t selected for any of the Common Language Runtime exceptions that you can see in the window in this figure. This gives any exception-handling code that you have written a chance to be executed, which is usually what you want. However, if you check the Break When Thrown option, you can enter break mode when the exception is thrown and use the debugging features described in this chapter before any exception-handling code is executed.

When you use the Exception Settings window, the option that you set for a category cascades down to all exceptions in that category. As a result, the setting for the Common Language Runtime Exceptions applies to all of the exceptions below that entry. However, you can override this setting for any of the exceptions below a category by changing the option for each exception. For example, if you want to break any time an ArgumentOutOfRangeException is thrown (even if the exception is handled), you can check the Break When Thrown option for that exception.
