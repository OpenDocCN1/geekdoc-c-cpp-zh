In the next example, we are setting several properties including Text, BackColor, and StartPosition:

```
public Form1()
{
    InitializeComponent();
    FormBorderStyle = FormBorderStyle.FixedToolWindow;
    BackColor = Color.AliceBlue;
    Text = "Basic Form Demo";
    StartPosition = FormStartPosition.CenterScreen;
}
```

That concludes a basic look at Windows Forms applications. The System.Windows.Forms namespace classes can help us create some rich-client C# applications. The Form class is the base for most of the windows in one of these applications, and when you add new forms to the project, the class is created with the required methods predefined for you. The Form class also exposes several properties that can be changed through the code or through the Properties window for Form Designer.

The MessageBox class is used to show a user a message box and there are several options we can modify that control how the message box looks. With this class, you can control the icon display placement of buttons, and several other properties.

The Application class controls Windows Forms applications and is responsible to get the message loop started and show the top-level window. The Application class also has properties that help us to store application or per-user data. We don’t create instances of the Application class; instead, we call the static methods that the class exposes, like Application.Run and Application.Exit. And form properties can also be used to control form behavior, like border style and background properties.