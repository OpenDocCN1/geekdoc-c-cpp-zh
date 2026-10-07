
The program's New, Open, Save, Save As, and Close commands work more or less as you would expect. For example, if you open a document and draw a rectangle on it, then the Save and Save As commands are enabled, so you can save your changes.

The drawing shown in Figure 19-4 was a new one that had not been saved. Because it did not have a filename, the Save command is disabled and the Save As command is enabled.

One feature of this program that is not common among document editors is that if you do not use the New or Open commands there are unused changes to the current document. Many other programs let you invoke New or Open and then when the current document has unsaved changes the Document DocumentCommands program makes you to save or close the document before New or Open (I did this to make the commands more interesting.)

The following XML code shows how the program binds the New, Open, Save, and Save commands to code-bind. The code-bind creates the binding for the Close command to show how it's done in code.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_390_0.png)

FIGURE 19-4

```xml
<Window.Bindings>
  <CommandBinding Command="New"
    CanExecute="DocumentNewAllowed" Execute="DocumentNew"/>
  <CommandBinding Command="Open"
    CanExecute="DocumentOpenAllowed" Execute="DocumentOpen"/>
  <CommandBinding Command="Save"
    CanExecute="DocumentSaveAllowed" Execute="DocumentSave"/>
  <CommandBinding Command="SaveAs"
    CanExecute="DocumentSaveAsAllowed" Execute="DocumentSaveAs"/>
  <!-- The binding is defined in code
       just to show how it's done. -->
  <CommandBinding Command="Close"
    CanExecute="DocumentCloseAllowed" Execute="DocumentClose"/>
</Window.Bindings>
```

### DocumentCommands

The Window.Bindings section contains the bindings. Note that you can put bindings in a more restricted scope, for example, in a Grid or StackPanel, but usually it makes the most sense to handle commands at a global level. It can be confusing if some are only available from certain parts of the user interface.

Each CommandBinding defines the command that it is binding. The CanExecute attribute gives the name of the function that decides which command should be enabled. The Executed attribute gives the name of the routine to run when the command executes.

The following code shows the code-bind for the New command:

```csharp
// Return True if we can perform the New action.
private void DocumentNewAllowed(Object sender, CanExecuteEventArgs e)
{
    e.CanExecute = (!m_IsDirty);
}

// Perform the New action.
private void DocumentNew(Object sender, ExecutedRoutedArgs e)
{
    // Remove any existing controls on the Canvas.
    Drawing.Children.Clear();

    // Display the canvas.
    Drawing.Visibility = Visibility.Visible;
    m_FileName = null;
}
```

## DocumentCommands

The DocumentAllowed routine sets e.CanExecute True if the program allows the New command. When this function sets e.CanExecute False, the command object denies the item and toolbar button for this command. The function simply returns True if the m_IsDirty flag is False.

> **DOWN AND DIRTY**
> Without going into too much detail how the program works, m_IsDirty is set to True whenever there are unsaved changes to the drawing. When the user clicks-drags to make a new rectangle, the variable is set to True. When the user opens an existing file, creates a new file, or saves changes, the program sets m_IsDirty to False.

The DocumentNew routine removes any rectangle children on the drawing canvas Drawing. It ensures that the Border containing the canvas is visible and sets m_FileName to null to indicate that the new drawing doesn't have a filename yet.

> **SAFETY FIRST**
> Note that this code doesn't need any logic to determine whether it is safe to create a new document. For example, it doesn't check whether there is an existing document with unsaved changes. The DocumentAllowed routine only enables the New command when it is safe to make a new document, so the DocumentNew routine only executes when it is safe.

This is one of the benefits of using WPF commanding. Moving the “allowed” logic to a separate routine simplifies the code that performs the action.

## CUSTOM COMMANDS

WPF provides around 150 predefined commands, so in many cases, you can find an existing command object to suit your needs. There are classes for copy, cut, paste, zoom in, zoom out, print, help, and many other features that are common to many programs. Appendix K summarizes defined command classes.

Occasionally, you may want to define a command that isn't common in other programs and for which WPF does not define a command class. In that case, you can define your own command objects. You can take two basic approaches to defining new command objects.

First, you can build a class that implements the ICommand interface. This is not hard, but it's harder than the other approach so it isn't discussed here.

Second, you can make an instance of the RoutedCommand or RoutedUI class. These classes are mostly the same except the RoutedUI class has a Text property that the RoutedCommand class lacks. That makes RoutedUI a better choice if you want to display your command's text where as in buttons and menu items.

The basic steps for building a custom RoutedCommand object aren't too complicated, but understanding what's going on it can be tricky.

The command that you define must be shared (shared between windows) as all instances of the window share the same instance. Because all instances of the window share the same command, you might wonder if it enables and disables all commands for every window. That would mean different windows could not be in different states.

Fortunately that is not the case. The CanExecute and Executed routines are not. WPF queries each window decide whether it allow its command.

The ImageColors example in Figure 19-5 demonstrates custom commands. Note that the top window's commands are enabled, the bottom window's commands are disabled. Click on the New button to make a new window.

So what do you need to do to make a command object? First, declare the object as static. WPF won't need to set the value of the object, if you like declare it read-only. The following code shows how the ImageColors declares its Invert command:

```csharp
public readonly static RoutedUICommand Invert;
```

# 356 | CHAPTER 19 COMMANDING

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_393_0.png)

FIGURE 19-5

Next, write code to initialize the object. Because it is declared static, the program can only initialize its object in a static constructor. The following code shows how the ImageColors program initializes its Invert command:

```csharp
static Window() {
    Invert = new RoutedUICommand("_Invert",
        "Invert Command", typeof(Window));
    Invert.InputGestures.Add(
        new KeyGesture(Key.I, ModifierKeys.Alt));
}
```

Code for other commands omitted

ImageColors

When the code creates the RoutedUICommand, it adds an underscore before the command-acceler. If you look closely at Figure 19-5, you will see that the I is underlined in the Invert button and menu item.

This code also adds [Alt+I] gesture to gesture the command. The menu item shown in Figure 19-5 automatically displays the gesture to the right.

> **LOTS OF STATIC**
> If you try to initialize the command object in a non-static constructor, Visual Studio complains at design time. If you try to initialize the command object in the window's Loaded event handler, the program fails at run time.
