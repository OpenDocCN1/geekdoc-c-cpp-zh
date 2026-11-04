
use them, too?" (If you said this and are reading this book as part of a programming course, tell your instructor that you deserve 5 extra points on the next quiz.)

That's true—WPF programs can use the standard dialogs, but not in the same way a Windows Forms application does.

WPF normally doesn't display the common dialogs in the Toolbox, so you can't add them to a window and you can't set their properties in the Properties window at design time. Instead, you need to create, initialize, and display the dialogs with code.

Before you write any code, you need to tell Visual Studio about the part of the .NET Framework that contains the dialogs. To do that, open the Project menu and select Add Reference to open the Reference Manager shown in Figure 8-4.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_164_0.png)

FIGURE 8-4

On this dialog, check the boxes next to System.Windows.Forms and System.Drawing, and click OK. (The first reference tells where the dialogs are defined. The second lets the program understand Color and Font objects, so you need it if you're working with those two dialogs.)

Now you can use code similar to the following to make a WPF program display an OpenFileDialog:

```csharp
// Create the OpenFileDialog.
System.Windows.Forms.OpenFileDialog fileDialog =
    new System.Windows.Forms.OpenFileDialog();

// Set the Filter.
fileDialog.Filter = "Text Files|*.txt|RTF Files|*.rtf|All Files|*.*";

// Display the dialog and check the result.
if (fileDialog.ShowDialog() == System.Windows.Forms.DialogResult.OK)
{
    // Process the selected file.
    MessageBox.Show(fileDialog.FileName);
}
```

The first statement (which spans two lines because it's so long) creates a System.Windows.Forms.OpenFileDialog object. That statement really just creates an OpenFileDialog object. The rest of the declaration tells Visual Studio that this kind of object is located in the System.Windows.Forms part of the .NET Framework.

Next the code initializes the dialog. This example just sets the dialog's Filter property, but you could set other properties, too, such as FilterIndex, CheckFileExists, and ShowReadOnly.

The code then displays the dialog by calling its ShowDialog method as before and compares the returned result with System.Windows.Forms.DialogResult.OK. If the user clicked the OK button, the program processes the result. This example simply displays the selected file's name in a message box, but a real application would do something like open the file.

Unfortunately, the results returned by some of the dialogs aren't directly usable by a WPF program. For example, the ColorDialog lets the user select a Color but WPF programs use Brushes instead of Colors. Similarly, the FontDialog lets the user pick a Font but WPF programs don't use Font objects directly. Some of this lesson's exercises show how you can work around some of those issues.

## TRY IT

In this Try It, you get to try out all of the standard dialogs except the PageSetupDialog (which is hard to use until you're doing actual printing). You initialize, display, and process the results of the dialogs (if the user clicks the OK button).

## Lesson Requirements

In this lesson, you:
- Use Labels, TextBoxes, and Buttons to make a form similar to the one shown in Figure 8-5.
- Add ColorDialog, FontDialog, FolderBrowserDialog, OpenFileDialog, SaveFileDialog, PrintDialog, and PrintPreviewDialog components to the form.
- When the user clicks the BackColor button, display the ColorDialog but don't allow the user to define custom colors. If the user clicks OK, set the form's BackColor property to the dialog's Color value.
- When the user clicks the Font button, display the FontDialog, allowing the user to select the font's color. If the user clicks OK, set the form's Font property to the dialog's Font value and its ForeColor property to the dialog's Color property.
- When the user clicks the Folder button, display the FolderBrowserDialog. Make the dialog start browsing at MyComputer. If the user clicks OK, make the Folder TextBox display the dialog's SelectedPath property.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_165_0.png)

- When the user clicks the Open File button, display the OpenFileDialog. Use a filter that lets the user select text files, RTF files, or all files. If the user clicks Open, make the Open File TextBox display the dialog's FileName property and set the SaveFileDialog's FilterIndex equal to the OpenFileDialog's FilterIndex.
- When the user clicks the Save File button, display the SaveFileDialog. Use the same filter used by the OpenFileDialog. If the user clicks Save, make the Save File TextBox display the dialog's FileName property and set the OpenFileDialog's FilterIndex equal to the SaveFileDialog's FilterIndex.
- When the user clicks the Print button, display the PrintDialog and ignore the return result.
- When the user clicks the Print Preview button, display the PrintPreviewDialog and ignore the return result.

> > **NOTE** You can download the code and resources for this lesson from the web-site at www.wrox.com/go/csharpmoonhourtrainer2e.

## Hints

- Be sure to initialize each of the dialogs before displaying them.

## Step-by-Step

- Use Labels, TextBoxes, and Buttons to make a form similar to the one shown in Figure 8-5.
  1. Add and arrange the controls in whatever manner you find easiest.
  2. Set the Buttons' Anchor properties to Top, Right. Set the TextBoxes' Anchor properties to Top, Left, Right.
- Add ColorDialog, FontDialog, FolderBrowserDialog, OpenFileDialog, SaveFileDialog, PrintDialog, and PrintPreviewDialog components to the form.
  1. Add the dialogs. They appear in the Component Tray, not on the form.
  2. Give the dialogs good names.
- When the user clicks the BackColor button, display the ColorDialog but don't allow the user to define custom colors. If the user clicks OK, set the form's BackColor property to the dialog's color value.
  1. To prevent the user from defining custom colors, set the ColorDialog's AllowFullOpen property to False.
  2. Use code similar to the following:

```csharp
private void backColorButton_Click(object sender, EventArgs e)
{
    backgroundColorDialog.Color = BackColor;
    if (backgroundColorDialog.ShowDialog() == DialogResult.OK)
    {
        BackColor = backgroundColorDialog.Color;
    }
}
```

When the user clicks the Font button, display the FontDialog, allowing the user to select the font's color. If the user clicks OK, set the form's Font property to the dialog's Font value and its ForeColor property to the dialog's Color property.
  1. To allow the user to select the font's color, set the dialog's ShowColor property to True.
  2. Use code similar to the following:

```csharp
private void fontButton_Click(object sender, EventArgs e)
{
    formFontDialog.Font = Font;
    formFontDialog.Color = ForeColor;
    if (formFontDialog.ShowDialog() == DialogResult.OK)
    {
        Font = formFontDialog.Font;
        fontTextBox.Text = formFontDialog.Font.ToString();
        ForeColor = formFontDialog.Color;
    }
}
```

When the user clicks the Folder button, display the FolderBrowserDialog. Make the dialog start browsing at MyComputer. If the user clicks OK, make the Folder TextBox display the dialog's SelectedPath property.
  1. To start browsing at MyComputer, use the Properties window to set the dialog's RootFolder property to MyComputer.
  2. Use code similar to the following:

```csharp
private void folderButton_Click(object sender, EventArgs e)
{
    if (testFolderBrowserDialog.ShowDialog() == DialogResult.OK)
    {
        folderTextBox.Text = testFolderBrowserDialog.SelectedPath;
    }
}
```

When the user clicks the Open File button, display the OpenFileDialog. Use a filter that lets the user select text files, RTF files, or all files. If the user clicks Open, make the Open File TextBox display the dialog's FileName property and set the SaveFileDialog's FilterIndex equal to the OpenFileDialog's FilterIndex.
