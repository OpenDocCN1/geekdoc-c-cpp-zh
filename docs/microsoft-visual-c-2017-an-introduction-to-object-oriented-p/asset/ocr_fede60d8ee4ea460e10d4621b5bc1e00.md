# Issues Using Methods in GUI Programs

You can call methods from other methods in a GUI application in the same way you can in a console application. Some special considerations when creating GUI applications include the following:

+   - Understanding methods that are automatically generated in the visual environment
- Appreciating scope in a GUI program
- Creating methods to be nonstatic when associated with a Form

# Understanding Methods That Are Generated Automatically in the Visual Environment

When you create GUI applications using the IDE, methods are generated automatically. For example, when you place a Button on a Form in the IDE and double-click it, a method is generated with the following header:

```
private void OkButton_Click(object sender, EventArgs args)
```

The method is private, which means it can be used only within its class, and it is void, meaning it does not return a value. You could change the access specifier to public and the method would still work, but you would usually have no reason to make such a change. If you change the return type (void), the program will not compile.

The format of the name okButton_Click() is conventional for event-handling methods that are created automatically. This includes the control name, an underscore, and the event that causes the method to execute—in this case, a Click event. Because the C# convention is to begin methods with an uppercase letter, you would usually want to change the automatically-generated method names as you saw in the examples in Chapter 3. For example, you might change okButton_Click() to OkButton_Click().

The parameters received by a Click() method arrive automatically when a user clicks the corresponding Button. The parameter sender is the object that generated the event that caused the method to execute, and the parameter e contains information about the type of event. Figure 7-23 shows a Click() method in a GUI application that displays the ToString() values of these two parameters.

```
private void OkButton_Click(object sender, EventArgs args)
{
  label1.Text = "object sender is: " + sender.ToString();
  label2.Text = "EventArgs is: " + e.ToString();
}
```

**Figure 7-23** The OkButton_Click() method in the ClickParameterInfo region