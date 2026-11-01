
![](img/41d82527c4e41cdb7e56259564306ddc_162_0.png)

Figure 6.40. The program window

![](img/41d82527c4e41cdb7e56259564306ddc_162_1.png)

Figure 6.41. OpenFileDialog showing text files only

When the file test.txt is shown in the OpenFileDialog and then OK is clicked, this file is read in our program and its contents are displayed inside the RichTextBox as shown in Figure 6.42.

![](img/41d82527c4e41cdb7e56259564306ddc_163_0.png)

Figure 6.42. The contents of test.txt file read and displayed in our program

It is worth noting that we can read all file types with OpenFileDialog using various file reading methods as we will see in the following chapters after learning more about C# programming.

## 6.2.5. SaveFileDialog

SaveFileDialog works similar to the OpenFileDialog but doing the opposite job: saving data to a file. Let’s use a SaveFileDialog in a project and save the text entered in a RichTextBox to a file:

- 1. Create a C# project in Visual Studio.
- 2. Add a SaveFileDialog on the form. It will appear in the pane below the form. Set the Name property of the SaveFileDialog as textSaveFileDialog as shown in Figure 6.43.
- 3. Add a Button and a RichTextBox to the project as in Figure 6.43.
- 4. Set the Name and Text of the Button as saveButton and Click to save to a file...
- 5. Set the Name of the RichTextBox as inputRichTextBox. After these settings, the form should look as shown in Figure 6.44.
- 6. When the Button’s clicked, the SaveFileDialog window will appear. Therefore, double-click the Button on the form to generate its default event handler method as in Code 6.16.

- 7. We'll use the ShowDialog() method to show the dialog. The code line:
DialogResult sfDialog = textSaveFileDialog.ShowDialog(); will show the dialog and let the user to select a filename and path to save entered text.

- 8. We have created and used a random number generator object before. Similarly, we will define a StreamWriter object that has the ability to save data to a file. We define this object with the code line:
StreamWriter save = new StreamWriter(textSaveFileDialog.FileName);. In this code, the expression in parentheses, textSaveFileDialog.FileName is the filename selected by the user in the file saving dialog box. Note that we have to include the System.IO library with the code line using System.IO; for being able to use the StreamWriter class as we did for the OpenFileDialog.

- 9. Actual file writing will be performed by the line:
save.Write(inputRichTextBox.Text); which has the Write() method applied on the StreamWriter type object save that was created in the previous code line. This code line writes the contents of the inputRichTextBox to the specified file.

- 10. Finally, we need to close the file after writing so that other applications will be able to access the saved file. We do this by the code line: save.Close();. The whole Form1.cs file will be as follows:

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

namespace SaveFileDialog
{
    public partial class Form1 : Form
    {
        public Form1()
        {
```

```
    InitializeComponent();
}
private void saveButton_Click(object sender, EventArgs e)
{
    DialogResult sfDialog = textSaveFileDialog.ShowDialog();
    StreamWriter save = new StreamWriter(textSaveFileDialog.FileName);
    save.Write(inputRichTextBox.Text);
    save.Close();
}
}
```

Code 6.17 (cont'd)

11. We are ready to build and run the project. The program will be as follows:

![](img/41d82527c4e41cdb7e56259564306ddc_166_0.png)

Figure 6.45. The file saving program

We may now input text to the RichTextBox. And then when we click the Click to save to a file button, the SaveFileDialog will appear as in Figure 6.46. I've set the file name as test2.txt and selected the Desktop as the folder. When the OK button is clicked in the file saving dialog, the text we entered will be saved to the specified file as shown in Figure 6.47. Note that the formatting of the text is lost when writing to the file using the Write() method.

## BEGINNER'S GUIDE TO C# PROGRAMMING

![](img/41d82527c4e41cdb7e56259564306ddc_167_0.png)

Figure 6.46. SaveFileDialog launched, the filename is chosen as test2.txt

![](img/41d82527c4e41cdb7e56259564306ddc_167_1.png)

Figure 6.47. Saved file opened in Notepad

## 6.3. Containers

Containers are used for grouping other controls and laying out the form in a robust and nicer way. It has six types as will be studied in this subsection.

### 6.3.1. Panel

Panel control is used for grouping and editing other controls. The controls included in a Panel can be moved to another location on the form together without changing their relative positions. Furthermore, common properties of these controls can be edited together. Panels are also used for grouping RadioButtons. Therefore we can use Panels to group RadioButtons on a form where we can select one RadioButton from each Panel.

Let's add three Panels on a form each of them containing three RadioButtons in our example:

- 1. Create a C# project.
- 2. Add three Panels on the form and divide the form among these Panels vertically as follows:

![](img/41d82527c4e41cdb7e56259564306ddc_168_0.png)

Figure 6.48. Adding three Panels on the form

Please note that Panel controls do not have borders by default. We can change this by setting their BorderStyle properties from None to FixedSingle or Fixed3D. I have changed the BorderStyle properties of the Panels of our example to FixedSingle and the appearance of the program window has changed as follows:

![](img/41d82527c4e41cdb7e56259564306ddc_170_0.png)

Figure 6.51. BorderStyle of Panels set as FixedSingle

Similarly, the Fixed3D option for the BorderStyle property also shows borders but with 3D effect as follows:

![](img/41d82527c4e41cdb7e56259564306ddc_170_1.png)

Figure 6.52. BorderStyle of Panels set as Fixed3D

### 6.3.2. GroupBox

GroupBox has the same functionality as the Panel control. Their difference is that GroupBox control has its name written at the left top.

We will use GroupBoxes to group Dessert and Drink selections in our example:

- 1. Create a C# project.
- 2. Add two GroupBoxes and add three CheckBoxes to each of these GroupBoxes. Set the Text properties of these GroupBoxes as Desserts and Drinks.
- 3. Set the Text properties of the CheckBoxes of the Desserts GroupBox as Ice cream, Cupcake and Cookies.
- 4. Similarly, set the Text properties of the CheckBoxes of the Drinks GroupBox as Soda water, Orange juice and Strawberry mojito.
- 5. Build and run the project. The program window will appear as follows:

![](img/41d82527c4e41cdb7e56259564306ddc_171_0.png)

Figure 6.53. A program utilizing GroupBoxes

Please note that we can use any control type inside the Panel and GroupBox controls as we need.

### 6.3.3. TabControl

TabControl provides a tabbed layout similar to the tabs we use in Internet browsers. The advantage of the TabControl is that we can use the form area effectively, the same area is used multiple times. Furthermore, the user may switch different tabs easier compared to opening and closing different forms in an application. Commonly used properties of the TabControl are as follows:

- **SizeMode**: Sets the sizing of tabs. It may take the following values: **Normal**, **FillToRight** and **Fixed**.
- **MultiLine**: Sets if more than one row of tabs are permitted or not.
- **TabPages**: Sets the Names of the tabs.

Let's use TabControl in a simple example. We'll enter text in a TextBox in the first tab and this text will be displayed in all capitals on a Label in the second tab.

- 1. Create a C# project.
- 2. Add a TabControl to the form. Click the ellipsis at the **TabPages** property of the TabControl to edit the tabs as indicated below:

![](img/41d82527c4e41cdb7e56259564306ddc_172_0.png)

Figure 6.54. Opening the TabPages dialog
