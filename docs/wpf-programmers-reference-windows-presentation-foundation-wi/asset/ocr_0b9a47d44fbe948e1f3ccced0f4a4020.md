Unfortunately, if you simply add the event handler declaration to the XAML code, the program won't run. If you try to execute it in Expression Blend or Visual Studio, you'll receive an error that says your program doesn't contain a definition for the event handler routine.

# INCOGNITO CONTROLS

You don't really need to give a control a name to give it an event handler. For example, the Button in the previous code doesn't need to be called btnApply or anything at all. The Click attribute tells the program what event handler to execute. If you're never going to refer to the Button in code (e.g., to enable or disable it), then you can omit the name.
Some development projects have standards for naming controls, however, and some may insist that any control with an event handler has a name.

# SEPARATE NO MORE

The fact that the program won't run without the event handler highlights a pretty serious breakdown in the separation between UI construction and the code-behind. It means the UI designer cannot test the interface until the event handlers exist, but the event handlers are not part of the interface so they should be none of the interface designer's business. You could argue that the programmer should make the event name attribute in the XAML code after writing the event handlers, but the programmer doesn't need to touch the interface.
In practice, this is probably not a huge problem — it just means that the interface designer and programmer need to speak to each other.
The techniques for attaching code-behind later in this chapter — adding event handlers at run time and using the Handles clause (in Visual Basic) — avoid this problem.

The following C# code handles the event declared in the previous XAML code:

```
private void btnApply_Click(object sender, RoutedEventArgs e)
{
this.Background = borSample.Background;
}
```

This code catches the btnApply Button's Click event and sets the window's Background property by the value used by the borSample's Background property (more details on this).
Your code doesn't need to do anything to wire up the event handler to catch the event — Expression Blend and Visual Studio take care of that for you.