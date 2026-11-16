# XML MAGIC AT WORK

The standard tags defined for XML comments help structure your documentation, which can be surprisingly helpful when you’re working in a team. And because Visual Studio knows about the tags, it will prompt you for the documentation you should include, and use that documentation itself. Let’s try it:

+   1. In the chapter Project, select the line containing the ToDo comment, and type three slashes. Visual Studio will add an XML comment stub:

```
/// <summary>
///
/// </summary>
/// <param name="sender"></param>
/// <param name="e"></param>
private void button1_Click(object sender, RoutedEventArgs e)
...
```

Visual Studio will add some basic documentation where it can.

+   2. Add a description of the code to the line between the <summary> and </summary> tags:

```
/// <summary>
/// This is the code that runs when the button is clicked
/// </summary>
/// <param name="sender"></param>
/// <param name="e"></param>
private void button1_Click(object sender, RoutedEventArgs e)
...
```

+   3. Now go to the MainWindow procedure, and on the line after InitializeComponent(); type “bu” to trigger Intellisense. Cursor down to button1_click. Like magic, your comment appears:

![](bbox=[0.35, 0.73, 0.9, 0.88])