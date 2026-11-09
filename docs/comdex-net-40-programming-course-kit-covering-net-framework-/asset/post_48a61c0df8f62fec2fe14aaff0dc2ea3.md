
![](img/9862a98a1a2d3bb14334137965a1ec60_771_0.png)

Fig.App-B.13

- 9. Add a TextBox, a textBlock, and a Button control from the Toolbox to the design view of the MainPage.xaml page, as shown in Fig.App-B.14:

![](img/9862a98a1a2d3bb14334137965a1ec60_771_1.png)

Fig.App-B.14

- 10. Remove the default text for textBox1 and textBlock1 control in the Properties window and change the Content property of the Button control to Click in the Properties window, as shown in Fig.App-B.15:

![](img/9862a98a1a2d3bb14334137965a1ec60_772_0.png)

Fig.App-B.15

- 11. *Double-click* the button1 control to generate the Click event of button1 and add the following code snippet to the button1_Click event in the MainPage.xaml.cs file:

```csharp
private void button1_Click(object sender, RoutedEventArgs e)
{
    textBlock1.Text=textBox1.Text;
}
```

In the preceding code snippet, the Text property of the textBlock1 control is set to the Text entered in the textBox1 control.

- 12. *Set* the deployment target of the application to Windows Phone 7 Emulator, from the standard toolbar, as shown in Fig.App-B.16:

![](img/9862a98a1a2d3bb14334137965a1ec60_772_1.png)

Fig.App-B.16

To debug your application on the phone device, you need to select the Windows Phone 7 Device option from the standard toolbar.

- 13. Press the F5 key on the keyboard to run the application. On debugging the application, first the phone operating system loads and then the output of the **WP7App** application appears (Fig.App-B.17).

![](img/9862a98a1a2d3bb14334137965a1ec60_773_0.png)

Fig.App-B.17

- 14. *Click* the TextBox control to display **Software Input Panel (SIP)** automatically, which allows you to enter text in a text box, as shown in Fig.App-B.18:

![](img/9862a98a1a2d3bb14334137965a1ec60_773_1.png)

Fig.App-B.18

- 15. *Enter* the text in the TextBox control using this panel and click the Click button (Fig.App-B.19).

![](img/9862a98a1a2d3bb14334137965a1ec60_774_0.png)

Fig.App-B.19

After clicking the Click button, the text entered in the text box gets displayed in the text block, as shown in Fig.App-B.20:

![](img/9862a98a1a2d3bb14334137965a1ec60_774_1.png)

Fig.App-B.20

You can also change the settings of the emulator by using the edit panel. Fig.App-B.21 shows the edit panel that gets displayed when you hover the cursor on the emulator:

![](img/9862a98a1a2d3bb14334137965a1ec60_775_0.png)

Fig.App-B.21

This edit panel allows you to change the settings for the emulator, such as changing the orientation of the emulator to landscape or portrait mode, changing the zoom level of the emulator, and minimizing or closing the emulator.
