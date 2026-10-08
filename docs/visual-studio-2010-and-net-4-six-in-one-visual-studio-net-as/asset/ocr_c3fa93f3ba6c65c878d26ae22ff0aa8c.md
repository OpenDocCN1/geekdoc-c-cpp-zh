> Note that you can substitute OutputItem with your own custom method to process project items.

# Dealing with User Input

The Interaction object type in the Microsoft.VisualBasic namespace contains a method named InputBox that can be easily used to collect user input, as the following sample macro shows:

```
Sub SaveView()
  Dim name As String

  name = InputBox("Enter the name you want to save:", "Save window layout")
  If (name =") Then
    MsgBox("Empty string, enter a valid name.")
  Else
    DTE.WindowConfigurations.Add(name)
  End If
End Sub
```

As its name suggests, InputBox pops up a modal dialog where you can enter an input string. You can specify a label for the input and a caption for the dialog. The SaveView macro uses this information to create a new window configuration with the specified name and saves it to the configuration settings.

By using the System.Windows.Forms namespace, you can create forms dynamically at run-time, and then show them. It may worth it to create simple modal dialogs, but if you need a more complex UI, you'll be off working with Visual Studio add-ins.

# CREATING VISUAL STUDIO ADD-INS

As described earlier, Visual Studio is an extensibility point to integrate add-ins into the IDE. Add-ins are tools to gain enhanced functionality. This section examines what add-ins are, and how you can use them. You will also build a small add-in to help you understand internal details through source code.

# Add-In Architecture

Add-ins are COM components that implement the following COM interfaces:

+   - The IDTextensibility2 interface is responsible for handling the life cycle of the add-in so that it can initialize and clean up appropriately in the context of the IDE and the other add-ins.
- The IDCommandTarget interface provides a way in which the add-in can handle commands the IDE routes to it.

COM components must be registered on the machine so that the add-in can work with them. Fortunately, the manual mechanism needed before Visual Studio 2008 has been changed to enable you to easily deploy your add-ins, without any explicit registration.