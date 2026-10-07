# SQL Server Database Programming with C#

Each piece of information in the ComboBox control is associated with a form window and furthermore it is associated with a group of data stored in a data table in the database.
The operation steps for this form are summarized as follows:

+   1) When this form is opened, three pieces of information will be displayed in a ComboBox control to allow users to make a selection to browse the information related to that selection.
2) When the user clicks the OK button, the selected form should be displayed to enable the user to browse the related information.

Based on the operation step 1, the codes for displaying three pieces of information should be located in the constructor of the SelectionForm since this constructor should be called first as an instance of the SelectionForm is created.
Open the SelectionForm window and click the View Code button to open its window. Enter the codes, which are shown in Figure 5.50, into the constructor of the SelectionForm.
Let’s have a closer look at this piece of codes to see how it works.

+   A. Three instances are created, and each one is associated with a form class.
B. The Add() method of the ComboBox class is used to attach all three pieces of information to this ComboBox. The reference represents the current object, an instance of the SelectionForm class, and the property SelectedIndex is set to select the first information as the default one.

According to operation step 2 described above, when users click the OK button, the related form selected by the user should allow users to browse information from that form. The View Designer button to open the graphical interface of the SelectionForm object. Double click the OK button to open its cmdOK_Click method and enter the codes, which are shown in Figure 5.51.
Let’s take a closer look at this piece of codes to see how it works.

| SelectWizardProject | SelectionForm |
|---|---|
| namespace SelectWizard_Project | |
| public partial class SelectionForm : Form { | |
| { | |
| FacultyForm facultyForm = new FacultyForm(); | |
| CourseForm courseForm = new CourseForm(); | |
| StudentForm studentForm = new StudentForm(); | |
| public SelectionForm() | |
| { | |
| InitializeComponent(); | |
| this.ComboBox.Items.Add("Faculty Information"); | |
| this.ComboBox.Items.Add("Course Information"); | |
| this.ComboBox.Items.Add("Student Information"); | |
| this.ComboBox.SelectedIndex = 0; | |
| } | |
| } |

FIGURE 5.50 The detailed codes for the selection form.