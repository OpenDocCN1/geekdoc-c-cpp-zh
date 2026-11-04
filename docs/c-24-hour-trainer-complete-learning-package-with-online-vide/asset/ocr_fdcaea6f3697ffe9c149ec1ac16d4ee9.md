of responding to PrintPage events, a WPF program's code can directly print visual objects that it draws using WPF controls such as Label and TextBox. You create some sort of container; place Label, TextBox, and other controls on it; and then print the container.

In addition to being easier to understand, this approach has a couple of other benefits. For example, it lets the program use the same kind of code to display and print data. In Windows Forms, a program uses controls such as TextBox and Label to display text on the screen but it uses a Graphics object's DrawString method to draw text on a printout. WPF uses the same kinds of TextBox and Label objects for both display and printing.

WPF also allows you to zoom in as much as you like without creating a pixelated result. That means, for example, you can enlarge a window as much as you like for a printout and you'll still see a smooth result.

The following sections give more details explaining how to print in WPF applications.

# PRINTING VISUALS

In WPF, a PrintDialog object starts the printing process. This object can display a printer selection dialog and provides a PrintVisual method that prints visual objects.

Although your code can simply call PrintVisual to send output to the default printer immediately; most programs first display the dialog so the user can select a printer. To do that, the program creates a PrintDialog object and calls its ShowDialog method. If the user selects a printer and clicks Print, ShowDialog returns true and the program can then call the dialog's PrintVisual method, passing it the visual object to print.

For example, the Print Window program shown in Figure 30-3 uses the following code to print an image of its main window:

```
// Print the window.
private void printButton_Click(object
sender, RoutedEventArgs e)
{
    // Display the print dialog and
    // check the result.
    PrintDialog printDialog =
        new PrintDialog();
    if ((printDialog.ShowDialog() == true)
    {
        // Print.
        printDialog.PrintVisual(this, "Print Window Image");
    }
}
```

![](bbox=[0.6, 0.62, 0.9, 0.85])

FIGURE 30-3

The code creates a PrintDialog object and calls its ShowDialog method. If ShowDialog returns true (indicating that the user clicked the dialog's Print button), the code calls the dialog's PrintVisual method, passing it the parameter this (indicating that it should print the current window). It also passes PrintVisual a descriptive title for the printer to display in its user interface.