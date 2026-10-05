
# Chapter 6 How to code methods and event handlers 173

## The Events list for a text box control

![](img/3148667e42d4db35b3d08576aaa1fa01_192_0.png)

### Description

- To generate the event handler for the default event of a form or control, you can double-click the form or control in the Form Designer.
- To view a list of all events for a form or control, you can select the form or control and click the Events button in the Properties window to display the Events list. Then, you can double-click on any event to generate an event handler for that event.
- By default, an event handler is given a name that consists of the form or control name, an underline, and the event name. To generate an event handler with a custom name, you can type the name of the event handler to the right of the event in the Events list and press Enter to generate the event handler.
- When you generate an event handler for a control, Visual Studio generates the method declaration for the event handler and it connects, or *wires*, the event as shown in the next figure.

Figure 6-6 How to generate an event handler for any event

### How event wiring works

6-7 shows the declarations for two event handlers, along with the statements that wire the appropriate events to these handlers. As you can see, the first event handler was generated with a default name. In contrast, a custom name was given to the second event handler.

As you recall from chapter 3, the code that wires events to event handlers is stored in the Designer.cs file for a form. Most of the time, you won't need to work with this code. However, you may occasionally need to delete or modify a statement.

If you delete an event handler, for example, if you don't, you'll get an error when you try to run the application. This error will be displayed in an Error List window, and it will indicate that the event handler is missing. One way to correct this is to double-click on the error message in the Error List window. This will open the Designer.cs file for the form and jump to the statement that contains the wiring for the missing event handler. Then, you can delete this statement.

Similarly, if you modify the name of an event handler, you'll need to modify the name in the event wiring statements too. The easiest way to do that is to use refactoring as described in chapter 3 when you rename the event handler. This automatically updates the name of the event handler in the corresponding event wiring statements. However, if you prefer to use refactoring when you rename the event handler, you can use the technique presented in this figure to wire the corresponding events to the newly renamed event handler.

To wire an event handler, Visual Studio uses a *delegate*, which is an object that represents a method. In this figure, the code uses the EventHandler delegate that is provided by the .NET Framework. This delegate defines the type and parameter list for a method that can handle an event. Then, the code uses the new keyword to create an EventHandler delegate. When this delegate is created, the name of the method is passed to the delegate. Finally, to wire the TextChanged event of a text box to the method specified by the delegate, Visual Studio uses the += operator.

Although you can use the C# language to define your own delegates, rarely do you need to do. For now, you can focus on working with the delegates that are provided by the .NET Framework. Most of the time, that means using the System.EventHandler delegate as shown in this figure.

For C to recognize a method as an event handler, the method must include the two parameters defined by the EventHandler delegate as shown in the examples. The first parameter is an object named sender. When event handler is executed, this parameter receives the object that the event occurred on. The second parameter identifies an EventArgs object named e that contains information about the event. The exact content of this depends on the event that occurred.

### The default event handler for a text box

The method declaration for the event handler

```csharp
private void txtMonthlyInvestment_TextChanged(object sender,
    System.EventArgs e)
{}
```

The generated statement that wires the event to the event handler

```csharp
this.txtMonthlyInvestment.TextChanged +=
new System.EventHandler(this.txtMonthlyInvestment_TextChanged);
```

### A custom event handler for a text box

The method declaration for the event handler

```csharp
private void ClearFutureValue(object sender, System.EventArgs e)
{}
```

The generated statement that wires the event to the event handler

```csharp
this.txtMonthlyInvestment.TextChanged +=
new System.EventHandler(this.ClearFutureValue);
```

### Description

- When you use the Form Designer to generate an event handler, a statement is also generated in the Designer.cs file for the form. This statement uses a delegate to wire the event to a method.
- A delegate is an object that represents a method. C# uses the EventHandler delegate that's defined by the .NET Framework to wire events to methods.
- The EventHandler specifies the return type and the parameters that are for a method that can handle an event. These objects are passed to the event handler when the event occurs. The first parameter (sender) identifies the object that the event occurred on, and the second parameter identifies an EventArgs object that contains additional information about the event.
- The new keyword is used to create an instance of a delegate, and the argument must be the name of the method. This method must have the return type and parameters specified by the delegate.
- After the delegate is created, the += operator is used to wire the method specified by the delegate.

![](img/3148667e42d4db35b3d08576aaa1fa01_194_0.png)

### How to handle multiple events with one handler

In some cases, you'll want to use the same event handler to handle two more events. For example, it's common to use one event handler for multiple text boxes. To do that, you can use the procedure shown in figure.

To start, you must generate the event handler as described in figure-6. Typically, you'll want to give this event handler the name ClearValue. Once you've created this event handler, it will appear in the drop-down list. In this figure, for example, you can see that the EventHandler is for the Changed event of text box. Then, you can select the event handler for the event to generate a statement that wires the event to the event handler.

![](img/3148667e42d4db35b3d08576aaa1fa01_195_0.png)

### How to select an event handler for an event

![](img/3148667e42d4db35b3d08576aaa1fa01_196_0.png)

### How to wire an event to an event handler

1. Select the Form Designer.
2. If necessary, click the Events button in the Properties window to display a list of the events.
3. Click to the right of the event you want to handle and display the drop-down list.
4. Select the event handler you want to use.

### Description

- The drop-down list that's available for each event includes all of the event handlers.
- When you select an event handler from the drop-down list, Visual Studio generates a statement that wires the event to the event handler.

### Another version of the Future Value application

### Another version of the Future Value application

Now that you know how to code methods and work with event handlers, you are ready to see an enhanced version of the Future Value application. This version uses a private method to calculate the future value, and it uses a single event handler to clear the Future Value text box whenever the user changes the text boxes in any of the other text boxes on the form.

### The event handlers and the CalculateFutureValue method

Figure 6-9 shows the code for the event handlers and CalculateFutureValue method of the Future Value application. This includes the event handlers for the Click events of the Calculate and Exit buttons, and it includes a custom event handler named ClearFutureValue that handles the Changed event of the first three text boxes on the form.

The CalculateFutureValue method contains the code that calculates the future value. It is called by the shaded code in the event handler for the Click event of the Calculate button. This separates the calculation from the other code for the event. In a lengthy event handler, using methods like this can make it easier to code, test, and debug an application. You will see more of this in the next chapter.

The ClearFutureValue event handler contains a single statement that sets the Text property of the Future Value text box to an empty string. In other words, it clears the future value that is displayed on the form. Since this event handler is wired to the Changed event of the first three text boxes on this form, it clears the Future Value text box every time the user changes a value in any of the other text boxes. As a result, the future value isn't displayed until the user clicks the Calculate button again.
