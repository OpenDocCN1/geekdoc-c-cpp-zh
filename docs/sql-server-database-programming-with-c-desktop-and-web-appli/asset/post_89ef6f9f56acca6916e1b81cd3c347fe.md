
# SQL Server Database Programming with C#

| | | |
|---|---|---|
| CmdPW_Click(object sender, EventArgs e) | | |
| A private void cmdPW_Click(object sender, EventArgs e) | | |
| B { string passWord;
| C logTableAdapter.ClearBeforeFill = true; |
| | passWord = logTableAdapter.PasswordQuery(txtUserName.Text);
| D if (passWord != String.Empty)
| | MessageBox.Show("The password is: " + passWord);
| | else
| | | MessageBox.Show("No matched password found!");
| | } | | |

FIGURE 5.46 The codes for the cmdPW click button.

The SQL statement

```
SELECT pass_word From Login Where (user_name = @Param)
```

indicates that we want to select a password from the Login table based on the username that is a dynamic parameter, and this parameter will be entered by the user when the run starts. Click the OK button to go to the next wizard.

The next window is used to confirm your SQL statement. Click the Next button to go to continue.

The next wizard allows you to choose a name for this query. Click the default name as PasswordQuery, then click the Next button. A successful Result will be displayed if it is fine. Click the Finish button to complete this configuration.

Now let's do our coding process for the Login form. For the testing, we need to add a temporary button named cmdPW and the Text as Password to the Login form. Then select and open the Login form from the Solution Explorer window, double-click the Password button to open its method, and enter the codes in Figure 5.46 in this method. Let's have a closer look at this piece of code.

- A. A local variable password is created and it is used to hold the retrieved single value of the pass_word.
- B. The query method we will build in this section, PasswordQuery(), with a parameter username that is entered by the user to retrieve the matched pass_word.
- C. If this query find a valid password from the Login table based on the username entered by the user, the password will be returned and displayed in a MessageBox.
- D. If this query cannot find any matched pass_word, a blank string will be returned and assigned to the variable passWord. A MessageBox with a warning message will be displayed if this situation happened.

Now let's run the project to test this. Click the Start button to run the project and your running project match that is shown in Figure 5.47.

Enter a username as ybai for the User Name box and click the Password button. The returned password is displayed in a message box, which is shown in Figure 5.48.

Now you can remove the temporary button Password and its method from this Login form if you like since we do not need it anymore for this project.

# Data Selection Query with Visual C#.NET

# 215

![](img/d59a47501d0a20fc0460a49c469c6fb7_243_0.png)

FIGURE 5.47 The running status of the Login form.

![](img/d59a47501d0a20fc0460a49c469c6fb7_243_1.png)

FIGURE 5.48 The returned password.

In the following sections, we will show the readers how to develop a more professional data-driven project by using more controls and methods. We still use the SelectWizard Project example project and continue with the SelectionForm.

# 5.9 CODING FOR THE SELECTION FORM

As we discussed in Section 5.6, if the login process is successful, the SelectionForm window should be displayed to allow users to continue for the next step. Figure 5.49 shows an opened SelectionForm window.

![](img/d59a47501d0a20fc0460a49c469c6fb7_243_2.png)

FIGURE 5.49 The opened selection form.

# SQL Server Database Programming with C#

Each piece of information in the ComboBox control is associated with a form window and furthermore it is associated with a group of data stored in a data table in the database.
The operation steps for this form are summarized as follows:

- 1) When this form is opened, three pieces of information will be displayed in a ComboBox control to allow users to make a selection to browse the information related to that selection.
- 2) When the user clicks the OK button, the selected form should be displayed to enable the user to browse the related information.

Based on the operation step 1, the codes for displaying three pieces of information should be located in the constructor of the SelectionForm since this constructor should be called first as an instance of the SelectionForm is created.
Open the SelectionForm window and click the View Code button to open its window. Enter the codes, which are shown in Figure 5.50, into the constructor of the SelectionForm.
Let’s have a closer look at this piece of codes to see how it works.

- A. Three instances are created, and each one is associated with a form class.
- B. The Add() method of the ComboBox class is used to attach all three pieces of information to this ComboBox. The reference represents the current object, an instance of the SelectionForm class, and the property SelectedIndex is set to select the first information as the default one.

According to operation step 2 described above, when users click the OK button, the selected form should be displayed to enable the user to browse the related information. The GUI of SelectionForm, double-click the OK button to open its cmdOK_Click method and enter the codes, which are shown in Figure 5.51. Let’s take a closer look at this piece of codes to see how it works.

| SelectWizardProject | SelectionForm |
|---|---|
| namespace SelectWizard_Project | |
| public class SelectionForm : Form { |
| { | |
| FacultyForm facultyForm = new FacultyForm(); | |
| CourseForm courseForm = new CourseForm(); | |
| StudentForm studentForm = new StudentForm(); | |
| public SelectionForm() | |
| { | |
| InitializeComponent(); | |
| this.ComboBox.Add("Faculty Information"); | |
| this.ComboBox.Add("Course Information"); | |
| this.ComboBox.Add("Student Information"); | |
| this.ComboBox.SelectedIndex = 0; | |
| } | |
| } | |

FIGURE 5.50 The detailed codes for the selection form.

# Data Selection Query with Visual C#.NET

| SelectWizardProject | CmdOK_Click(object sender, EventArgs e) |
|---|---|
| A | private void CmdOK_Click(object sender, EventArgs e) |
| | { |
| | if (this.ComboSelection.Text == "Faculty Information") |
| | facultyForm.Show(); |
| B | else if (this.ComboSelection.Text == "Course Information") |
| | courseForm.Show(); |
| C | else if (this.ComboSelection.Text == "Student Information") |
| | studentForm.Show(); |
| D | else |
| | MessageBox.Show("Invalid Selection"); |
| | } |

FIGURE 5.51 The coding for the OK button.

| SelectWizardProject | cmdExit_Click(object sender, EventArgs e) |
|---|---|
| A | private void CmdExit_Click(object sender, EventArgs e) |
| | { |
| | courseForm.Close(); |
| | facultyForm.Close(); |
| | studentForm.Close(); |
| B | Application.Exit(); |
| | } |

FIGURE 5.52 The completed codes for the exit button.

The function for this piece of coding is straightforward and easily understood, and is outlined as:

- A. Open the FacultyForm window if the user selected the Faculty Information.
- B. Open the StudentForm window if the user selected the Student Information.
- C. Open the CourseForm window if the user selected the Course Information.
- D. An error message is displayed if no information is selected.

The last coding process for this form is the Exit button. The GUI of the SelectionForm, double-click the Exit button to open its cmdExit_Click() method. Enter the following codes into this method, which is shown in Figure 5.52.
This piece of codes looks a little complicated. Let's see how this piece of codes works.

Suppose the user selected the first information – Faculty Information. A faculty window will be displayed and this is supposed to be connected to a faculty data table in the DataSet. If the user selected a faculty name from the ComboBox control and clicked the Select button on that form, all information related to that faculty should be displayed on that form, exactly on seven TextBoxes and a picture.
