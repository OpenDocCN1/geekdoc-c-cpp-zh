
msg = msg + ListBox1.Items[5].Text + "<br />";
}
if (ListBox1.Items[6].Selected)
{
    msg = msg + ListBox1.Items[6].Text + "<br />";
}
if (ListBox1.Items[7].Selected)
{
    msg = msg + ListBox1.Items[7].Text + "<br />";
}
if (ListBox1.Items[8].Selected)
{
    msg = msg + ListBox1.Items[8].Text + "<br />";
}
if (ListBox1.Items[9].Selected)
{
    msg = msg + ListBox1.Items[9].Text + "<br />";
}
if (ListBox1.Items[10].Selected)
{
    msg = msg + ListBox1.Items[10].Text + "<br />";
}
if (ListBox1.Items[11].Selected)
{
    msg = msg + ListBox1.Items[11].Text + "<br />";
}
if (ListBox1.Items[12].Selected)
{
    msg = msg + ListBox1.Items[12].Text + "<br />";
}
if (ListBox1.Items[13].Selected)
{
    msg = msg + ListBox1.Items[13].Text + "<br />";
}
if (ListBox1.Items[14].Selected)
{
    msg = msg + ListBox1.Items[14].Text + "<br />";
}
if (ListBox1.Items[15].Selected)
{
    msg = msg + ListBox1.Items[15].Text + "<br />";
}
if (ListBox1.Items[16].Selected)
{
    msg = msg + ListBox1.Items[16].Text + "<br />";
}
Label5.Text = "Thank you for entering your details.<br />You have entered the following details:<br />Name " + TextBox1.Text + "<br />Address : " + TextBox2.Text + "<br />Telephone : " + telephone + "<br />Shopping items to deliver: <br />" + msg + "<br /><br />";
if (TextBox4.Text == "")

# 438 Programming in C#

20.9 Explain the significance of Application.Run method.

20.10 Explain any five default attributes of a form control through which its appearance can be modified.

20.11 What are design patterns? Briefly explain the three key design patterns supported in .NET

## Programming Exercises

20.1 Write a windows application in C#, having two textbox controls and a button control, validate that the textbox values are not blank. Clicking the button will interchange the textbox values and the button disappears.

20.2 Write an ASP.NET/C# application with two textbox controls (Name and Telephone) and a button control. After submitting the form, the application redirects to another page and displays the Name and Telephone in it in Blue Color.

20.3 Write an ASP.NET/C# application with a textbox username, textbox password and a button. Entering "admin" as username and password as "aspnetc#" will take you to another page with a welcome message written in blue-green. Entering the wrong password will take you to another page called error.aspx and show you the message wrong password.

20.4 Design a ‘Students Information’ form in Visual Studio with the help of standard controls such as text box, button, combo box, etc. The form should accept typical information pertaining to students, such as name, roll no, course, admission number, etc.

20.5 Write a Windows application in C# for emulating a very basic calculator that performs addition, subtraction, multiplication and division operations.

# Appendix

# A

# Minor Project 1: Project Planner

# Objective

The objective of the Project Planner application is to facilitate project and employee management in an organization. It is a form-based Windows application that uses the TabControl for segregating the project management and employee management activities.
The main form of the Project Planner application has two tabs: Employee and Project.

# Form1.cs [Design]

The following figures show the Employee and Project tabs in the Design view:

![](img/bae4ee2c7c29c052feb3b9a9c5659998_440_0.png)

The Employee Tab in Design View

![](img/bae4ee2c7c29c052feb3b9a9c5659998_441_0.png)

The project tab in design view

# Backend Database

As shown in the above figures, the Project Planner application uses a number of fields for recording employee and project related information. Thus, a backend database must be created for recording this information. The Project Planner application uses Microsoft Access as the backend database. The following figures show a snapshot of tables, Table 1 and Table 2, created in MS Access for storing Employee and Project related information:

# Linking Data Sources

As we can see in the Design view, both Employee and Project tabs use the DataGridView control for displaying the records submitted by the user. To populate the DataGridView from a backend data source, it must be linked with the corresponding data source. The following are the steps for linking DataGridView control with a data source:

- 1. Select the DataGridView control and open the DataGridView Tasks pane, as shown below:
- 2. Select the Add Project Data Source option from Choose Data Source list to initiate the Data Source Configuration Wizard, as shown below:
- 3. Select the Database option and click Next to display the Choose Your Data Connection screen, as shown below:
- 4. Click the New Connection button to display the Add Connection dialog box, as shown below:

![](img/bae4ee2c7c29c052feb3b9a9c5659998_442_0.png)

MS access tables

![](img/bae4ee2c7c29c052feb3b9a9c5659998_442_1.png)

DataGridView tasks pane

# Data Source Configuration Wizard

# Choose a Data Source Type

Where will the application get data from?

- Database
- Web Service
- Object

Lets you connect to a database and choose the database objects for your application. This option creates a dataset.

The Data source configuration wizard

# Data Source Configuration Wizard

# Choose Your Data Connection

Which data connection should your application use to connect to the database?

DBConnectionString (Settings)

New Connection...

Connection string

The choose Your Data connection screen

The add Connection Dialog Box

5. Select the Microsoft Access Database File (OLE DB) option in the Data Source field, enter the location of the backend MS Access file in the Database file name text box and click OK. A message box appears confirming the successful data source connection, as shown below:

Microsoft Visual Studio Message Box

6. Click Next to display the Save the Connection String to the Application Configuration file screen, as shown below:

# Data Source Configuration Wizard

# Save the Connection String to the Application Configuration File

Starting from this wizard, you will be guided through the process of creating a connection to a database. ...

Do you want to save the connection string to the application configuration file?

Yes, save the connection string to the application configuration file?

db1ConnectionString

The Save the Connection String to the Application Configuration file screen

7. Click Next to display the Choose Your Database Objects screen, as shown below:

# Choose Your Database Objects

Which database objects do you want in your dataset?

Dataset name: db1Dataset

The Choose Your Database Objects Screen

8. Select the table and the corresponding columns that you want to display in the DataGridView and click Finish to link the selected data source with the DataGridView control.

# Form1.cs Code File

The following is the source code contained in the Form1.cs file:

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Text;
using System.Windows.Forms;
using System.Data.OleDb;
namespace WindowsApplication7
{
public partial class Form1 : Form
{
public Form1()
{
InitializeComponent();
this.textBox1.Visible = false;
this.textBox2.Visible = false;
this.comboBox1.Visible = false;
this.comboBox2.Visible = false;
this.comboBox5.Visible = false;
this.label1.Visible = false;
this.label2.Visible = false;
this.label3.Visible = false;
this.label4.Visible = false;
this.label7.Visible = false;
this.button4.Visible = false;
this.dataGridView1.Visible = false;
this.button6.Visible = false;
this.label8.Visible = false;
this.label9.Visible = false;
this.label10.Visible = false;
this.label11.Visible = false;
this.label12.Visible = false;
this.textBox3.Visible = false;
this.textBox4.Visible = false;
this.textBox5.Visible = false;
this.dateTimePicker1.Visible = false;
this.dateTimePicker2.Visible = false;
this.dataGridView2.Visible = false;
}
private void listBox1_SelectedIndexChanged(object sender, EventArgs e)
{
}
private void tabPage1_Click(object sender, EventArgs e)
{
```
