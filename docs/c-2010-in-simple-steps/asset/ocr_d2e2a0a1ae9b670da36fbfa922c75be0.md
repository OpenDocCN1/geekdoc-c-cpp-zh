5 Double-click button1 in the Design view to open the code-behind file (MainWindow.xaml.cs) and add the Click event handler in the code-behind file.

6 Add the highlighted line of code in the MainWindow class, in the Click event handler of button1:

```
private void button1_Click(object sender, RoutedEventArgs e)
{
    textBox1.Text = "";
}
```

7 Press the F5 key to run the application. The output appears (Fig.C#7.20).

8 Enter some text in the TextBox control (Fig.C#7.20).

9 Click the Clear TextBox button, as shown in Fig.C#7.20:

![](bbox=[0.35, 0.32, 0.6, 0.44])

Fig.C#7.20

When you click the Clear TextBox button, the text in the TextBox control is cleared, as shown in Fig.C#7.21:

![](bbox=[0.38, 0.52, 0.6, 0.65])

Fig.C#7.21

Next, let's discuss about the PasswordBox control.

# Using the PasswordBox Control

Sometimes, you want the users of your application to enter confidential information, such as passwords. You can use a TextBox control for this purpose. However, while entering the password, another user may accidentally see the password, which is an undesirable situation. A better alternative would be to use the PasswordBox control to enter passwords. The PasswordBox control allows you to obscure or mask the password while you enter it in the control. The PasswordBox control is a special type of text box in which the individual characters of the input text are masked with a given character so that the text appears as a string of that character. By default, any text entered in the PasswordBox control appears as a string of solid circles (●).

> Note
> The PasswordBox control uses a System.Security.SecureString object, which ensures that the text entered as a password in the control remains confidential.

The PasswordBox control is represented by the PasswordBox class, which has various properties that allow you to work with the PasswordBox control. Table 7.5 lists the noteworthy properties of the PasswordBox class: