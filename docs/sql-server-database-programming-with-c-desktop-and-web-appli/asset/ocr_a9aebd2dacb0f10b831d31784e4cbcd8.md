# LINQSelect Project

# SQL Server Database Programming with C#

```
private void cmdSelect_Click(object sender, EventArgs e)
{
    LogInForm logForm = new LogLoginForm();
    if (ComboMethod.Text == "LINQ to SQL Method")
    {
        var f_info = from fi logForm.cse_dept.Faculties
            where faculty.nameText = ComboName.Text;
            select fi;
        foreach (var fi in f_info)
        {
            txtFaculty.Text = fi.faculty_id;
            txtName.Text = fi.faculty_name;
            txtTitle.Text = fi.title;
            txtOffice.Text = fi.office;
            txtPhone.Text = fi.phone;
            txtCollege.Text = fi.college;
            txtEmail.Text = fi.email;
            byte[] img = (fi.image as System.Data.Linq.Binary).ToArray();
            PhotoBox.Image = Image.FromStream(new System.IO.MemoryStream(img));
        }
    }
    else
    {
        // LINQ - Single Record Method selected
        Faculty faculty = cse_dept.Faculties.Single(fi => fi.faculty_name == ComboName.Text);
        txtFacultyID.Text = faculty.faculty_id;
        txtName.Text = faculty.faculty_name;
        txtTitle.Text = faculty.title;
        txtOffice.Text = faculty.office;
        txtPhone.Text = faculty.phone;
        txtCollege.Text = faculty.college;
        txtEmail.Text = faculty.email;
        byte[] img = (faculty.image as System.Data.Linq.Binary).ToArray();
        PhotoBox.Image = Image.FromStream(new System.IO.MemoryStream(img));
    }
    logForm.Close();
```

FIGURE 5.121 The code for the constructor of the FacultyForm.

+   E. If the user selected the LINQ - Single Record Method, one single LINQ query is adopted and executed by calling the Single method. The implicit variable is an IQuery<Faculty> and the queried result is assigned to a typed Faculty object. Each column of the returned data is assigned to the associated TextBox in the FacultyForm to display each one by one.
G. Similar to dBox above, the type of the queried faculty image in the column faculty is converted to the System.Drawing.Image, and assigned to the image control PhotoBox in the Faculty Form window.
H. The newly created instance logForm is closed when we no longer need to use it.

This appears quite in this piece of codes. Yes, it is much simpler and shorter than those codes we did for the same method using the regular SQL Server databases. No any Connection string, Command object, Connection object, or even DataAdapter and DataReader used for this query.
The codes for the Back button's Click are very simple, and just putting the code, this.Hide(), into this method.
Now let's run the project to test the function of this Faculty Form class. Click on the Start button (or F5 key) to run the project. Enter a suitable username and password, such as jhenry and test, and