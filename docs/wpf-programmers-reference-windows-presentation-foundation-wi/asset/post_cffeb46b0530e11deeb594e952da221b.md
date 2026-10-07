
# EXAMPLE CODE

This chapter's source code, which is available for download on the book's web site at www.wrox.com, includes several example applications that all do the same thing but use different techniques for attaching code-behind to the user interface.

Figure 11-1 shows one of the programs in action. You can drag the scrollbars or enter blue values in the textboxes to set the red, green, and blue components of the color displayed on the right. If you click on the Apply button, the program sets the window's background color to match the current sample.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_218_0.png)

The ImageColors example program, which is shown in Figure 11-2, demonstrates all of the different techniques for attaching code-behind in a single program. The program's different buttons are attached to event handlers in different ways. Download the C# or Visual Basic version of this program from the book's web site to see the details.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_218_1.png)

# EVENT NAME ATTRIBUTES

The first way to attach code-behind to a control's events uses an attribute in the XAML code. The attribute's name is the same as the event that you want to catch. Its value is the name of the event handler in the code-behind.

For example, the following XAML code defines a Button named btnApply. The Click attribute indicates that the routine btnApply_Click catches the control's Click event handler.

```
<Button Content="Apply" IsDefault="True"
Name="btnApply" Click="btnApply_Click"/>
```

Unfortunately, if you simply add the event handler declaration to the XAML code, the program won't run. If you try to execute it in Expression Blend or Visual Studio, you'll receive an error that says your program doesn't contain a definition for the event handler routine.

# INCOGNITO CONTROLS

You don't really need to give a control a name to give it an event handler. For example, the Button in the previous code doesn't need to be called btnApply or anything at all. The Click attribute tells the program what event handler to execute. If you're never going to refer to the Button in code (e.g., to enable or disable it), then you can omit the name.
Some development projects have standards for naming controls, however, and some may insist that any control with an event handler has a name.

# SEPARATE NO MORE

The fact that the program won't run without the event handler highlights a pretty serious breakdown in the separation between UI construction and the code-behind. It means the UI designer cannot test the interface until the event handlers exist, but the event handlers are not part of the interface so they should be none of the interface designer's business. You could argue that the programmer should make the event name attribute in the XAML code after writing the event handlers, but the programmer doesn't need to touch the interface.
In practice, this is probably not a huge problem — it just means that the interface designer and programmer need to speak to each other.
The techniques for attaching code-behind later in this chapter — adding event handlers at run time and using the Handles clause (in Visual Basic) — avoid this problem.

The following C# code handles the event declared in the previous XAML code:

```sharp
private void btnApply_Click(object sender, RoutedEventArgs e)
{
this.Background = borSample.Background;
}
```

This code catches the btnApply Button's Click event and sets the window's Background property by the value used by the borSample's Background property (more details on this).
Your code doesn't need to do anything to wire up the event handler to catch the event — Expression Blend and Visual Studio take care of that for you.

# Event Name Attributes | 183

The following XAML fragments show how the EventNameAttributes example program determines which event handles the key events raised by the program button, and the scrollbar and textbox that control the color's red component. The code for the other scrollbars and textboxes is similar.

```
<ScrollBar Orientation="Horizontal" Minimum="0" Maximum="255"
Grid.Row="0" Grid.Column="0" Name="scRed" ValueChanged="scRed_ValueChanged" />

<TextBox Margin="2" Grid.Row="0" Grid.Column="1" Text="255"
HorizontalAlignment="Right" VerticalAlignment="Center"
Name="txtRed" TextChanged="txtRed_TextChanged" />

<Button Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="3" Width="100"
Height="40"
Content="Apply" IsDefault="True"
Name="btnApply" Click="btnApply_Click"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_220_0.png)

The following C# fragments show how the EventNameAttributes program respond when you use the first scrollbar or textbox to change the red color component, and when you click on the Apply button. The handlers for the other scrollbars and textboxes are similar.

```csharp
// ScrollBar has changed. Update the corresponding TextBox.
private void scRed_ValueChanged(object sender,
    RoutedPropertyChanged<double> e)
{
    if (txtRed != null)
    {
        txtRed.Text = e.NewValue.ToString();
    }
}

// TextBox has changed. Update the corresponding ScrollBar.
private void txtRed_TextChanged(object sender, TextChangedEventArgs e)
{
    if (scRed != null)
    {
        scRed.Value = double.Parse(txtRed.Text);
    }
}
```
