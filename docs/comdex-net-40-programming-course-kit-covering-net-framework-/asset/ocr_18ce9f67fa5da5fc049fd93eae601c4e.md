+   4. Select the **WPF Application** template in the middle pane to create a WPF standalone application.

+   5. Enter the name of the application as **MyButton** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.

+   6. Click the **OK** button to close the **New Project** dialog box and create the MyButton application.

+   7. Replace the default code in the XAML view of the **MainWindow.xaml** file with the code given in Listing 5.3:

**Listing 5.3:** Showing the Code of the **Button** Control

```
```xml
<Window x:Class="MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MyButton Application" Height="200" Width="300">
    <Grid>
        <Button Name="Button1" Height="25" Margin="0,0,0,100" Width="75"
                Content="One" Background="Black" Foreground="White"/>
        <Button Name="Button2" Height="25" Margin="0,0,0,50" Width="100"
                Content="Two" Background="Black" Foreground="White"/>
        <Button Name="Button3" Height="25" Width="125" Content="Three"
                Background="Black" Foreground="White"/>
    </Grid>
</Window>
```
```

In Listing 5.3, the **Title** property of the **Window** element is set to **MyButton Application**, which implies that the text **MyButton Application** appears on the title bar of the window. The **Window** element has a **Grid** control as its child element. Three **Button** controls are added as the child elements to the **Grid** control. The **Content** property of the three buttons (**Button1**, **Button2**, and **Button3**) are set to **One**, **Two**, and **Three**, respectively. You may also note that the **Background** and **Foreground** properties of all the three buttons are set to **Black** and **White**, respectively.

+   8. Double-click the **Button** in the Design view of the **MainWindow.xaml** file. The event handler for the **Click** event of the **One** button control is automatically added in the **MainWindow.xaml.vb** file.

+   9. Add the following highlighted code snippet in the event handler for the **Click** event of the One button:

```
```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.Windows.RoutedEventArgs) Handles Button1.Click
    MessageBox.Show("You clicked: " & Button1.Name)
End Sub
```
```

In the preceding code snippet, **Button1_Click** is the event handler for the **Click** event of **Button1** (or the **One** button). This event handler executes when you click the **One** button at runtime. The **Name** property of the button is used to display the name of the button in a message box, which appears when you click the **One** button.

+   10. Press the F7 key on the keyboard to switch to the **MainWindow.xaml** file.

+   11. Double-click the **Two** button in the Design view of the **MainWindow.xaml** file. The event handler for the **Click** event of the Two button is automatically added in the **MainWindow.xaml.vb** file.

+   12. Add the following highlighted code snippet in the event handler for the **Click** event of the Two button:

```
```vb
Private Sub Button2_Click(ByVal sender As System.Object, ByVal e As
    System.Windows.RoutedEventArgs) Handles Button2.Click
    MessageBox.Show("You clicked: " & Button2.Name)
End Sub
```
```

In the preceding code snippet, **Button2_Click** is the event handler for the **Click** event of **Button2** (or the **Two** button). This event handler executes when you click the **Two** button at runtime. The **Name** property of the button is used to display the name of the button in a message box, which appears when you click the **Two** button.

+   13. Press the F7 key on the keyboard to switch to the **MainWindow.xaml** file.