you create a new macro or change an existing macro, you'll be prompted to save the macro. In fact, you must save the macro before Access runs it for you. When prompted, click Yes to save it, provide a name (such as "mcrHelloWorld"), and click OK. The macro runs and displays a message box with the arguments you specified (shown in Figure 22.4).

# FIGURE 22.4

Running the Hello World! macro displays a message box.

![](bbox=[0.2, 0.38, 0.45, 0.58])

You can also run the macro from the Navigation pane. Close the macro builder and display the Macros group in the Navigation pane. Double-click the mcrHelloWorld macro to run it. You'll see the same message box that displayed when you ran the macro from the design window.

Notice that the message box always appears near the middle of the screen and blocks you from working with Access until you click OK. These are built-in behaviors of the message box object and are identical in every regard to a message box displayed from VBA code.

When you're satisfied with the Hello World! macro, click the Close button in the upper-right corner of the macro builder to return to the main Access window.

# Assigning a macro to an event

When you're creating macros, you probably don't want end users using the Navigation pane to run them—or worse, running them from the macro builder. Macros are intended for you to automate your application without writing VBA code. In order to make an application easy to use, assign your macros to an object's event.

The most common event to which you might assign a macro is a button's Click event.

Follow these steps to create a simple form with a button that runs mcrHelloWorld:

+   1. Select the Create tab on the Ribbon, and then click the Form Design button in the Forms group.

+   2. On the Form Design Tools Design tab of the Ribbon, deselect the Use Control Wizards option in the Controls group. For this example, you don't want to use a wizard to decide what this button does.

+   3. Click the Button control and draw a button on the form.

+   4. Set the button's Name property to cmdHelloWorld. Press F4 to open the button's Property Sheet if it isn't visible on the screen.