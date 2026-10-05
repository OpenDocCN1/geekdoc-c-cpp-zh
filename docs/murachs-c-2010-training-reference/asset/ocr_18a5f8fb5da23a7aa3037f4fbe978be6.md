# How to handle multiple events with one event handler

In some cases, you'll want to use the same event handler to handle two or more events. For example, it's common to use one event handler for the Changed event of multiple text boxes on a form. To do that, you can use the procedure shown in figure 6-8.

To start, you must generate the event handler as described in figure 6-6. Typically, you will want to give this event handler a name that's not specific to any one control. Suppose, for example, that any time the user changes the value of the future value's currently displayed. Then, when you create the event handler for the first text box, you might give this event handler the name ClearFutureValue.

Once you've created this event handler, it will appear in the drop-down list of the event handlers that are available. In this figure, for example, you can see that the ClearFutureValue event handler is included in the drop-down list for the TextChanged event of the Yearly Interest Rate text box. Then, you can select this event handler to generate a statement that wires the event to the event handler.