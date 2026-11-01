
- 4. Double-click the Button to create its default event handler method `selectColourButton_Click()` as shown below:

```
private void selectColourButton_Click(object sender,
EventArgs e)
{
}
```

Code 6.5

- 5. When the user clicks the button, we want the ColorDialog to appear. We use the method `ShowDialog()` to fire the ColorDialog. We use this method in the following way:

```
DialogResult colourResult = selectColourDialog.ShowDialog();
```

Code 6.6

In this code line, the dialog box of selectColourDialog is opened with the `ShowDialog()` method. When the user selects a colour from the ColorDialog and clicks OK, the colourResult object is set to OK. We now need to apply the selected colour to the background colour as we did before:

```
this.BackColor = selectColourDialog.Color;
```

Code 6.7

With this code, the background colour is set to the colour existing in the Color property of the ColorDialog control. We need to insert these code lines into the Button's event handler:

```
private void selectColourButton_Click(object sender,
EventArgs e)
{
    DialogResult colourResult = selectColourDialog.ShowDialog();
    this.BackColor = selectColourDialog.Color;
}
```

Code 6.8

- 6. Build and run the project. The program window shown in Figure 6.25 will appear.

![](img/41d82527c4e41cdb7e56259564306ddc_152_0.png)

Figure 6.27. The background colour changed to white after selecting white on the ColorDialog

## 6.2.2. Font Dialog

FontDialog works with the same principles of the ColorDialog and is used for selecting Font properties from a dialog window. Its properties are similar to those of the ColorDialog.

Let's select the Font properties of a Button's Text using a FontDialog in an example:

- 1. Create a C# project in Visual Studio.
- 2. Add a FontDialog to the form. Set the Name property of the FontDialog as `selectFontDialog`.
- 3. Add a Button in the middle of the form. Set the Name and Text properties of the Button as `fontButton` and `Select font properties`.

The form should look as follows:

![](img/41d82527c4e41cdb7e56259564306ddc_152_1.png)

Figure 6.28. FontDialog example

- 4. We will now create the Click event handler method of the Button. For this, double-click the button and the following method will be created:

```
private void fontButton_Click(object sender, EventArgs e)
{
}
```

Code 6.9

- 5. As in the ColorDialog, we will use the `ShowDialog()` method to display the FontDialog as follows:

```
DialogResult fontResult = selectFontDialog.ShowDialog();
```

Code 6.10

When the user selects the Font properties from the FontDialog and clicks OK, the fontResult object will be set as OK. We'll now set the Button's Text's Font properties to the Font property of the selectFontDialog control:

```
fontButton.Font = selectFontDialog.Font;
```

Code 6.11

- 6. Let's insert these code lines into the button's event handler method:

```
private void fontButton_Click(object sender, EventArgs e)
{
    DialogResult fontResult = selectFontDialog.ShowDialog();
    fontButton.Font = selectFontDialog.Font;
}
```

Code 6.12

- 7. Build and run the project. The program will appear as in Figure 6.29. Click the Select font properties button and the FontDialog will be displayed as shown in Figure 6.30. I've selected bold and underlined in the FontDialog. When the OK button is clicked, this dialog will be closed and the Button's Text will be changed accordingly as in Figure 6.31.

![](img/41d82527c4e41cdb7e56259564306ddc_154_0.png)

Figure 6.29. The example program with a FontDialog

![](img/41d82527c4e41cdb7e56259564306ddc_154_1.png)

Figure 6.30. The FontDialog window

![](img/41d82527c4e41cdb7e56259564306ddc_154_2.png)

Figure 6.31. The Button's font properties set as selected in the FontDialog

![](img/41d82527c4e41cdb7e56259564306ddc_156_0.png)

Figure 6.33. The layout of the form

- 5. Double-click the button to create its Click event handler:

```
private void fbdButton_Click(object sender, EventArgs e)
{
}
```

Code 6.13

- 6. In order to show the FolderBrowserDialog, we will apply the `ShowDialog()` to it. The return value will be of the `DialogResult` type as in the previous dialog examples: `DialogResult fbdResult = selectFolderBrowserDialog.ShowDialog();`

- 7. We will update the Text of the Label with the selected folder with the following code: `selectedFolderLabel.Text = selectFolderBrowserDialog.SelectedPath;`. We take the `SelectedPath` property of the FolderBrowserDialog and assign it to the Text property of the Label. We will insert these code lines into the Click event handler method of the button as follows:

```
private void fbdButton_Click(object sender, EventArgs e)
{
    DialogResult fbdResult =
        selectFolderBrowserDialog.ShowDialog();
    selectedFolderLabel.Text =
        selectFolderBrowserDialog.SelectedPath;
}
```

Code 6.14

- 8. Build and run the project. The following program will appear:

![](img/41d82527c4e41cdb7e56259564306ddc_157_0.png)

Figure 6.34. The program window

Click the Select a folder button and the FolderBrowserDialog will be launched:

![](img/41d82527c4e41cdb7e56259564306ddc_157_1.png)

Figure 6.35. The FolderBrowserDialog waiting for a folder selection

When we select a folder from the dialog and click OK button, the full path to the selected folder will be shown in the Label as shown in Figure 6.36.

- 3. Add a Button on the form which will initiate the OpenFileDialog. Set the Name and Text properties of the Button as `openFileButton` and `Click to open a text file`, respectively.

- 4. Add a RichTextBox on the form below the Button. We will display the contents of the selected text file in this control. Set its Name as `fileRichTextBox`. The form will look as follows after these steps:

![](img/41d82527c4e41cdb7e56259564306ddc_159_0.png)

Figure 6.38. Layout of the form

- 5. We want to open text files only because, the contents of most of other file types (such as images, videos and formatted text files) cannot be displayed in a RichTextBox. We need to set a filter to the OpenFileDialog to open files with .txt extension only. For this, select the `textFileOpenFileDialog` and set its Filter property as `Text Files | *.txt` as shown in Figure 6.39.

- 6. When the Button is clicked, the OpenFileDialog window will appear. Therefore, double-click the Button on the form to generate its default event handler method as in Code 6.15.

![](img/41d82527c4e41cdb7e56259564306ddc_160_0.png)

Figure 6.39. Setting the Filter property of the OpenFileDialog

```
private void openFileButton_Click(object sender, EventArgs e)
{
}
```

Code 6.15

- 7. Firstly, we will add the code line `DialogResult openFileResult = textFileOpenFileDialog.ShowDialog();` which will launch the file opening dialog box.
- 8. When the user selects a text file and clicks OK in the file opening dialog, the FileName property of the OpenFileDialog will be assigned to the selected filename. We will take this FileName and assign it to a new string with the code line `string fileName = textFileOpenFileDialog.FileName;`. The variable fileName will then contain the selected file's name.
- 9. Then, we will use a special method `ReadAllText()` to read the contents of the text file. This method reads a text file and assigns the contents of the text file to a string variable. The code line `string text = File.ReadAllText(fileName);` will do this job. Note that the method `ReadAllText()` is not included in the default libraries existing in the Form1.cs file. Therefore we need to add the library containing this method to the top of our source code with the line: `using System.IO;`
- 10. Finally, we will set the Text of the RichTextBox to the text read from the file with the code line: `fileRichTextBox.Text = text;`. After these steps, the Form1.cs file will be as follows:

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.IO;

namespace OpenFileDialog
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void openFileButton_Click(object sender, EventArgs e)
        {
            DialogResult openFileResult = textFileOpenFileDialog.ShowDialog();
            string fileName = textFileOpenFileDialog.FileName;
            string text = File.ReadAllText(fileName);
            fileRichTextBox.Text = text;
        }
    }
}
```

Code 6.16

- 11. Build and run the project. The program window shown in Figure 6.40 will be launched. We need a text file to read from. For this aim, you can use a text file existing on your computer. I created a new text file, `test.txt`, in Notepad for this example. When `Click to open a text file...` button is clicked, it will display Text files as shown in Figure 6.41.
