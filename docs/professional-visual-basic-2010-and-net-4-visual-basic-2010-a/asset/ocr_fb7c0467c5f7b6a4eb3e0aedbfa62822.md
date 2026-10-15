The next button is the Prev button, which has been placed and bound to the left-hand side and bottom of the display. Its name has been changed to “ButtonPrev,” and its display text has been changed to read “Prev.” As noted earlier, the arrow symbols are not in the button name; and, as you can test in your own code, attempting to add them here causes an error.

Finally, there is the ButtonLoad button, which is centered in the display area. It has been bound to both sides of the display to maintain its position in the center. The label for this button is “View Images,” which is, of course, the goal of this application. However, in order for that to happen, you need an event handler for this button; in fact, you need several event handlers in order to get the basic behavior of the application in place.

# Event Handlers

In previous versions of Visual Studio you could click on a control and Visual Studio would automatically generate the default event handler for that control in your code. Fortunately, WPF also provides this behavior, so generate the following event handlers:

+   - Double-click on the title bar of the form to generate the MainWindow_Loaded event handler.
+   - Double-click on the Images button to create the ButtonBrowse_Click handler.
+   - Double-click on the Load button to create the ButtonLoad_Click handler.
+   - Double-click on the Prev button to create the ButtonPrev_Click handler.
+   - Double-click on the Next button to create the ButtonNext_Click handler.

To create each of these handlers, you need to return to the Design view and click on the associated control, but after they are created you can stay in Code view for most of this section. Take a look at the ButtonBrowse_Click event handler’s method stub:

```
Private Sub ButtonBrowse_Click(ByVal sender As System.Object, _
    ByVal e As System.Windows.RoutedEventArgs) _
    Handles ButtonBrowse.Click
End Sub
```

The preceding code was reformatted with line extension characters to improve readability, but this is essentially what each of your event handlers looks like. As a Visual Basic developer, you should find this syntax very familiar. Note that the method name has been generated based on the control name and the event being handled. The parameter list is generated with the “sender” and e parameter values, although the e value now references a different object in the System.Windows namespace. Finally, defined here is the VB-specific Handles syntax that indicates this method is an event handler, and which specific event or events it handles.

While this is a very familiar, powerful, and even recommended way of defining event handlers with VB and WPF, it isn’t the only way. WPF allows you to define event handlers within your XAML code. To be honest, if this were a book on C#, we would probably spend a fair amount of time covering the advantages of that type of event handler declaration. After all, C# doesn’t support the direct association of the event handler declaration with the method handling the event; as a result, C# developers prefer to declare their event handlers in XAML.

> Visual Basic provides a default implementation of WPF that encourages less coupling of the UI to the application code than C# does.

However, one of the goals of XAML is the separation of the application logic from the UI, and placing the names of event handlers in the UI actually couples the UI to the application logic. It shouldn’t matter to the UI whether the Click event or the DoubleClick or any other event is being handled by custom logic. Therefore, although this section introduces the way to define events directly in XAML, the recommendation is to define event handlers with the code that implements the handler.