# Data Selection Query with Visual C#.NET

| LINQSelect Project | cmdCancel_Click(object sender, EventArgs e) | |
| --- | --- | --- |
| private void cmdCancel_Click(object sender, EventArgs e) 
{
  cse_dept.Connection.Close();
  this.Close();
  Application.Exit();
} | |

**FIGURE 5.118** The codes for the cancel button method.

# 5.17.4 CODING FOR THE SECTION FORM

The coding for this form is basically identical with the same form we did for the previous project RTOSSelect Project and the only difference is that the database connection we used in this project is an instance of the derived class CSE_DEPTDataContext. Another point is that we do not need to add the namespace System.Linq to the namespace declaration section this Form since the LINQ to SQL will not be used for this form.

Open the SelectionForm and enter the codes that are shown in Figure 5.119 into the code window RTOSSelect Project, with the exception of the following codes:

+   A. When the Exit button is clicked, first all three Forms are closed by executing the Close() method.
B. Then the project is executed by executing the Application.Exit().

Now let's run the project to test the codes we did for two forms, LogInandForm. Click on the Start button to run the project and the LogIn Form is displayed first. Enter a valid username and password, such as jquery and test into the Username and Password boxes, hit the Login button. The login process is successful and next Form, Selection Form, is displayed. Click the Exit button on the SelectionForm to exit the project. Of course, by entering some incorrect username or password, you will see what happened.

Next's take a look at the code processing for the Faculty Form.

# 5.17.5 QUERY DATA USING THE LINQ TO SQL FOR THE FACULTY FORM

In this form, we want to use two methods to perform the data query using the LINQ to SQL for this Form. The first method is a general LINQ to SQL as we did for the LogInForm, but the second method is to query a single record from the Faculty table.

Open the window to add the System.Linq to the namespace section on this Form. Then enter the codes that are shown in Figure 5.120 into the constructor of this Form to perform the initialization jobs for this form.

Let's have a look at this piece of code to see how it works.

+   A. The namespace System.Linq is added to the namespace declaration section on this Form to allow us to use all LINQ related components in that namespace.
B. Eight faculty members are added into the Faculty Name combobox and the first one is selected as a default.
C. Two query methods are added into the ComboMethod combobox and the first method is selected at the default method.